```verilog
module RingRouterV1(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h0 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_1(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h1 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_2(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h2 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_3(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h3 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_4(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h4 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_5(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h5 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_6(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h6 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_7(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h7 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_8(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h8 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_9(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h9 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_10(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'ha & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_11(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'hb & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_12(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'hc & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_13(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'hd & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_14(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'he & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_15(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'hf & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_16(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h10 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_17(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h11 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_18(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h12 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingRouterV1_19(
  input        clock,
  output       io_in_ready,
  input        io_in_valid,
  input  [4:0] io_in_bits_addr,
  input  [4:0] io_in_bits_data,
  input        io_out_ready,
  output       io_out_valid,
  output [4:0] io_out_bits_addr,
  output [4:0] io_out_bits_data,
  output       io_host_in_ready,
  input        io_host_in_valid,
  input  [4:0] io_host_in_bits_addr,
  input  [4:0] io_host_in_bits_data,
  input        io_host_out_ready
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
`endif // RANDOMIZE_REG_INIT
  wire  forMe = io_in_bits_addr == 5'h13 & io_in_valid; // @[RingNetworkV1.scala 18:48]
  reg  validReg; // @[RingNetworkV1.scala 25:27]
  wire  _validReg_T = io_in_ready & io_in_valid; // @[Decoupled.scala 50:35]
  wire  _validReg_T_3 = io_host_in_ready & io_host_in_valid; // @[Decoupled.scala 50:35]
  reg [4:0] validBits_addr; // @[RingNetworkV1.scala 29:38]
  reg [4:0] validBits_data; // @[RingNetworkV1.scala 29:38]
  assign io_in_ready = io_host_out_ready & io_out_ready; // @[RingNetworkV1.scala 23:36]
  assign io_out_valid = validReg; // @[RingNetworkV1.scala 27:16]
  assign io_out_bits_addr = validBits_addr; // @[RingNetworkV1.scala 31:15]
  assign io_out_bits_data = validBits_data; // @[RingNetworkV1.scala 31:15]
  assign io_host_in_ready = io_out_ready; // @[RingNetworkV1.scala 19:20]
  always @(posedge clock) begin
    validReg <= _validReg_T & ~forMe | _validReg_T_3; // @[RingNetworkV1.scala 26:38]
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_addr <= io_host_in_bits_addr;
    end else begin
      validBits_addr <= io_in_bits_addr;
    end
    if (_validReg_T_3) begin // @[RingNetworkV1.scala 30:19]
      validBits_data <= io_host_in_bits_data;
    end else begin
      validBits_data <= io_in_bits_data;
    end
  end
// Register and memory initialization
`ifdef RANDOMIZE_GARBAGE_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_INVALID_ASSIGN
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_REG_INIT
`define RANDOMIZE
`endif
`ifdef RANDOMIZE_MEM_INIT
`define RANDOMIZE
`endif
`ifndef RANDOM
`define RANDOM $random
`endif
`ifdef RANDOMIZE_MEM_INIT
  integer initvar;
`endif
`ifndef SYNTHESIS
`ifdef FIRRTL_BEFORE_INITIAL
`FIRRTL_BEFORE_INITIAL
`endif
initial begin
  `ifdef RANDOMIZE
    `ifdef INIT_RANDOM
      `INIT_RANDOM
    `endif
    `ifndef VERILATOR
      `ifdef RANDOMIZE_DELAY
        #`RANDOMIZE_DELAY begin end
      `else
        #0.002 begin end
      `endif
    `endif
`ifdef RANDOMIZE_REG_INIT
  _RAND_0 = {1{`RANDOM}};
  validReg = _RAND_0[0:0];
  _RAND_1 = {1{`RANDOM}};
  validBits_addr = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  validBits_data = _RAND_2[4:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module RingNetworkV1(
  input        clock,
  input        reset,
  output       io_ports_0_in_ready,
  input        io_ports_0_in_valid,
  input  [4:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output       io_ports_0_out_valid,
  output [4:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input        io_ports_1_in_valid,
  input  [4:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output       io_ports_1_out_valid,
  output [4:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [4:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output       io_ports_2_out_valid,
  output [4:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data,
  output       io_ports_3_in_ready,
  input        io_ports_3_in_valid,
  input  [4:0] io_ports_3_in_bits_addr,
  input  [4:0] io_ports_3_in_bits_data,
  input        io_ports_3_out_ready,
  output       io_ports_3_out_valid,
  output [4:0] io_ports_3_out_bits_addr,
  output [4:0] io_ports_3_out_bits_data,
  output       io_ports_4_in_ready,
  input        io_ports_4_in_valid,
  input  [4:0] io_ports_4_in_bits_addr,
  input  [4:0] io_ports_4_in_bits_data,
  input        io_ports_4_out_ready,
  output       io_ports_4_out_valid,
  output [4:0] io_ports_4_out_bits_addr,
  output [4:0] io_ports_4_out_bits_data,
  output       io_ports_5_in_ready,
  input        io_ports_5_in_valid,
  input  [4:0] io_ports_5_in_bits_addr,
  input  [4:0] io_ports_5_in_bits_data,
  input        io_ports_5_out_ready,
  output       io_ports_5_out_valid,
  output [4:0] io_ports_5_out_bits_addr,
  output [4:0] io_ports_5_out_bits_data,
  output       io_ports_6_in_ready,
  input        io_ports_6_in_valid,
  input  [4:0] io_ports_6_in_bits_addr,
  input  [4:0] io_ports_6_in_bits_data,
  input        io_ports_6_out_ready,
  output       io_ports_6_out_valid,
  output [4:0] io_ports_6_out_bits_addr,
  output [4:0] io_ports_6_out_bits_data,
  output       io_ports_7_in_ready,
  input        io_ports_7_in_valid,
  input  [4:0] io_ports_7_in_bits_addr,
  input  [4:0] io_ports_7_in_bits_data,
  input        io_ports_7_out_ready,
  output       io_ports_7_out_valid,
  output [4:0] io_ports_7_out_bits_addr,
  output [4:0] io_ports_7_out_bits_data,
  output       io_ports_8_in_ready,
  input        io_ports_8_in_valid,
  input  [4:0] io_ports_8_in_bits_addr,
  input  [4:0] io_ports_8_in_bits_data,
  input        io_ports_8_out_ready,
  output       io_ports_8_out_valid,
  output [4:0] io_ports_8_out_bits_addr,
  output [4:0] io_ports_8_out_bits_data,
  output       io_ports_9_in_ready,
  input        io_ports_9_in_valid,
  input  [4:0] io_ports_9_in_bits_addr,
  input  [4:0] io_ports_9_in_bits_data,
  input        io_ports_9_out_ready,
  output       io_ports_9_out_valid,
  output [4:0] io_ports_9_out_bits_addr,
  output [4:0] io_ports_9_out_bits_data,
  output       io_ports_10_in_ready,
  input        io_ports_10_in_valid,
  input  [4:0] io_ports_10_in_bits_addr,
  input  [4:0] io_ports_10_in_bits_data,
  input        io_ports_10_out_ready,
  output       io_ports_10_out_valid,
  output [4:0] io_ports_10_out_bits_addr,
  output [4:0] io_ports_10_out_bits_data,
  output       io_ports_11_in_ready,
  input        io_ports_11_in_valid,
  input  [4:0] io_ports_11_in_bits_addr,
  input  [4:0] io_ports_11_in_bits_data,
  input        io_ports_11_out_ready,
  output       io_ports_11_out_valid,
  output [4:0] io_ports_11_out_bits_addr,
  output [4:0] io_ports_11_out_bits_data,
  output       io_ports_12_in_ready,
  input        io_ports_12_in_valid,
  input  [4:0] io_ports_12_in_bits_addr,
  input  [4:0] io_ports_12_in_bits_data,
  input        io_ports_12_out_ready,
  output       io_ports_12_out_valid,
  output [4:0] io_ports_12_out_bits_addr,
  output [4:0] io_ports_12_out_bits_data,
  output       io_ports_13_in_ready,
  input        io_ports_13_in_valid,
  input  [4:0] io_ports_13_in_bits_addr,
  input  [4:0] io_ports_13_in_bits_data,
  input        io_ports_13_out_ready,
  output       io_ports_13_out_valid,
  output [4:0] io_ports_13_out_bits_addr,
  output [4:0] io_ports_13_out_bits_data,
  output       io_ports_14_in_ready,
  input        io_ports_14_in_valid,
  input  [4:0] io_ports_14_in_bits_addr,
  input  [4:0] io_ports_14_in_bits_data,
  input        io_ports_14_out_ready,
  output       io_ports_14_out_valid,
  output [4:0] io_ports_14_out_bits_addr,
  output [4:0] io_ports_14_out_bits_data,
  output       io_ports_15_in_ready,
  input        io_ports_15_in_valid,
  input  [4:0] io_ports_15_in_bits_addr,
  input  [4:0] io_ports_15_in_bits_data,
  input        io_ports_15_out_ready,
  output       io_ports_15_out_valid,
  output [4:0] io_ports_15_out_bits_addr,
  output [4:0] io_ports_15_out_bits_data,
  output       io_ports_16_in_ready,
  input        io_ports_16_in_valid,
  input  [4:0] io_ports_16_in_bits_addr,
  input  [4:0] io_ports_16_in_bits_data,
  input        io_ports_16_out_ready,
  output       io_ports_16_out_valid,
  output [4:0] io_ports_16_out_bits_addr,
  output [4:0] io_ports_16_out_bits_data,
  output       io_ports_17_in_ready,
  input        io_ports_17_in_valid,
  input  [4:0] io_ports_17_in_bits_addr,
  input  [4:0] io_ports_17_in_bits_data,
  input        io_ports_17_out_ready,
  output       io_ports_17_out_valid,
  output [4:0] io_ports_17_out_bits_addr,
  output [4:0] io_ports_17_out_bits_data,
  output       io_ports_18_in_ready,
  input        io_ports_18_in_valid,
  input  [4:0] io_ports_18_in_bits_addr,
  input  [4:0] io_ports_18_in_bits_data,
  input        io_ports_18_out_ready,
  output       io_ports_18_out_valid,
  output [4:0] io_ports_18_out_bits_addr,
  output [4:0] io_ports_18_out_bits_data,
  output       io_ports_19_in_ready,
  input        io_ports_19_in_valid,
  input  [4:0] io_ports_19_in_bits_addr,
  input  [4:0] io_ports_19_in_bits_data,
  input        io_ports_19_out_ready,
  output       io_ports_19_out_valid,
  output [4:0] io_ports_19_out_bits_addr,
  output [4:0] io_ports_19_out_bits_data
);
  wire  routers_0_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_0_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_0_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_0_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_0_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_0_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_0_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_0_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_1_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_1_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_1_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_1_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_1_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_1_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_1_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_2_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_2_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_2_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_2_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_2_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_2_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_2_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_3_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_3_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_3_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_3_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_3_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_3_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_3_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_4_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_4_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_4_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_4_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_4_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_4_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_4_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_5_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_5_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_5_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_5_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_5_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_5_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_5_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_6_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_6_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_6_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_6_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_6_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_6_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_6_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_7_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_7_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_7_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_7_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_7_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_7_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_7_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_8_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_8_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_8_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_8_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_8_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_8_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_8_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_9_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_9_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_9_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_9_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_9_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_9_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_9_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_10_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_10_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_10_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_10_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_10_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_10_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_10_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_11_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_11_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_11_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_11_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_11_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_11_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_11_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_12_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_12_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_12_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_12_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_12_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_12_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_12_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_13_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_13_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_13_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_13_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_13_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_13_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_13_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_14_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_14_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_14_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_14_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_14_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_14_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_14_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_15_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_15_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_15_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_15_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_15_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_15_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_15_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_16_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_16_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_16_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_16_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_16_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_16_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_16_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_17_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_17_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_17_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_17_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_17_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_17_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_17_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_18_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_18_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_18_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_18_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_18_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_18_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_18_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_clock; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_19_io_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_19_io_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_out_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_out_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_19_io_out_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_19_io_out_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_host_in_ready; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_host_in_valid; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_19_io_host_in_bits_addr; // @[RingNetworkV1.scala 39:77]
  wire [4:0] routers_19_io_host_in_bits_data; // @[RingNetworkV1.scala 39:77]
  wire  routers_19_io_host_out_ready; // @[RingNetworkV1.scala 39:77]
  RingRouterV1 routers_0 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_0_clock),
    .io_in_ready(routers_0_io_in_ready),
    .io_in_valid(routers_0_io_in_valid),
    .io_in_bits_addr(routers_0_io_in_bits_addr),
    .io_in_bits_data(routers_0_io_in_bits_data),
    .io_out_ready(routers_0_io_out_ready),
    .io_out_valid(routers_0_io_out_valid),
    .io_out_bits_addr(routers_0_io_out_bits_addr),
    .io_out_bits_data(routers_0_io_out_bits_data),
    .io_host_in_ready(routers_0_io_host_in_ready),
    .io_host_in_valid(routers_0_io_host_in_valid),
    .io_host_in_bits_addr(routers_0_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_0_io_host_in_bits_data),
    .io_host_out_ready(routers_0_io_host_out_ready)
  );
  RingRouterV1_1 routers_1 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_1_clock),
    .io_in_ready(routers_1_io_in_ready),
    .io_in_valid(routers_1_io_in_valid),
    .io_in_bits_addr(routers_1_io_in_bits_addr),
    .io_in_bits_data(routers_1_io_in_bits_data),
    .io_out_ready(routers_1_io_out_ready),
    .io_out_valid(routers_1_io_out_valid),
    .io_out_bits_addr(routers_1_io_out_bits_addr),
    .io_out_bits_data(routers_1_io_out_bits_data),
    .io_host_in_ready(routers_1_io_host_in_ready),
    .io_host_in_valid(routers_1_io_host_in_valid),
    .io_host_in_bits_addr(routers_1_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_1_io_host_in_bits_data),
    .io_host_out_ready(routers_1_io_host_out_ready)
  );
  RingRouterV1_2 routers_2 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_2_clock),
    .io_in_ready(routers_2_io_in_ready),
    .io_in_valid(routers_2_io_in_valid),
    .io_in_bits_addr(routers_2_io_in_bits_addr),
    .io_in_bits_data(routers_2_io_in_bits_data),
    .io_out_ready(routers_2_io_out_ready),
    .io_out_valid(routers_2_io_out_valid),
    .io_out_bits_addr(routers_2_io_out_bits_addr),
    .io_out_bits_data(routers_2_io_out_bits_data),
    .io_host_in_ready(routers_2_io_host_in_ready),
    .io_host_in_valid(routers_2_io_host_in_valid),
    .io_host_in_bits_addr(routers_2_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_2_io_host_in_bits_data),
    .io_host_out_ready(routers_2_io_host_out_ready)
  );
  RingRouterV1_3 routers_3 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_3_clock),
    .io_in_ready(routers_3_io_in_ready),
    .io_in_valid(routers_3_io_in_valid),
    .io_in_bits_addr(routers_3_io_in_bits_addr),
    .io_in_bits_data(routers_3_io_in_bits_data),
    .io_out_ready(routers_3_io_out_ready),
    .io_out_valid(routers_3_io_out_valid),
    .io_out_bits_addr(routers_3_io_out_bits_addr),
    .io_out_bits_data(routers_3_io_out_bits_data),
    .io_host_in_ready(routers_3_io_host_in_ready),
    .io_host_in_valid(routers_3_io_host_in_valid),
    .io_host_in_bits_addr(routers_3_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_3_io_host_in_bits_data),
    .io_host_out_ready(routers_3_io_host_out_ready)
  );
  RingRouterV1_4 routers_4 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_4_clock),
    .io_in_ready(routers_4_io_in_ready),
    .io_in_valid(routers_4_io_in_valid),
    .io_in_bits_addr(routers_4_io_in_bits_addr),
    .io_in_bits_data(routers_4_io_in_bits_data),
    .io_out_ready(routers_4_io_out_ready),
    .io_out_valid(routers_4_io_out_valid),
    .io_out_bits_addr(routers_4_io_out_bits_addr),
    .io_out_bits_data(routers_4_io_out_bits_data),
    .io_host_in_ready(routers_4_io_host_in_ready),
    .io_host_in_valid(routers_4_io_host_in_valid),
    .io_host_in_bits_addr(routers_4_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_4_io_host_in_bits_data),
    .io_host_out_ready(routers_4_io_host_out_ready)
  );
  RingRouterV1_5 routers_5 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_5_clock),
    .io_in_ready(routers_5_io_in_ready),
    .io_in_valid(routers_5_io_in_valid),
    .io_in_bits_addr(routers_5_io_in_bits_addr),
    .io_in_bits_data(routers_5_io_in_bits_data),
    .io_out_ready(routers_5_io_out_ready),
    .io_out_valid(routers_5_io_out_valid),
    .io_out_bits_addr(routers_5_io_out_bits_addr),
    .io_out_bits_data(routers_5_io_out_bits_data),
    .io_host_in_ready(routers_5_io_host_in_ready),
    .io_host_in_valid(routers_5_io_host_in_valid),
    .io_host_in_bits_addr(routers_5_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_5_io_host_in_bits_data),
    .io_host_out_ready(routers_5_io_host_out_ready)
  );
  RingRouterV1_6 routers_6 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_6_clock),
    .io_in_ready(routers_6_io_in_ready),
    .io_in_valid(routers_6_io_in_valid),
    .io_in_bits_addr(routers_6_io_in_bits_addr),
    .io_in_bits_data(routers_6_io_in_bits_data),
    .io_out_ready(routers_6_io_out_ready),
    .io_out_valid(routers_6_io_out_valid),
    .io_out_bits_addr(routers_6_io_out_bits_addr),
    .io_out_bits_data(routers_6_io_out_bits_data),
    .io_host_in_ready(routers_6_io_host_in_ready),
    .io_host_in_valid(routers_6_io_host_in_valid),
    .io_host_in_bits_addr(routers_6_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_6_io_host_in_bits_data),
    .io_host_out_ready(routers_6_io_host_out_ready)
  );
  RingRouterV1_7 routers_7 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_7_clock),
    .io_in_ready(routers_7_io_in_ready),
    .io_in_valid(routers_7_io_in_valid),
    .io_in_bits_addr(routers_7_io_in_bits_addr),
    .io_in_bits_data(routers_7_io_in_bits_data),
    .io_out_ready(routers_7_io_out_ready),
    .io_out_valid(routers_7_io_out_valid),
    .io_out_bits_addr(routers_7_io_out_bits_addr),
    .io_out_bits_data(routers_7_io_out_bits_data),
    .io_host_in_ready(routers_7_io_host_in_ready),
    .io_host_in_valid(routers_7_io_host_in_valid),
    .io_host_in_bits_addr(routers_7_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_7_io_host_in_bits_data),
    .io_host_out_ready(routers_7_io_host_out_ready)
  );
  RingRouterV1_8 routers_8 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_8_clock),
    .io_in_ready(routers_8_io_in_ready),
    .io_in_valid(routers_8_io_in_valid),
    .io_in_bits_addr(routers_8_io_in_bits_addr),
    .io_in_bits_data(routers_8_io_in_bits_data),
    .io_out_ready(routers_8_io_out_ready),
    .io_out_valid(routers_8_io_out_valid),
    .io_out_bits_addr(routers_8_io_out_bits_addr),
    .io_out_bits_data(routers_8_io_out_bits_data),
    .io_host_in_ready(routers_8_io_host_in_ready),
    .io_host_in_valid(routers_8_io_host_in_valid),
    .io_host_in_bits_addr(routers_8_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_8_io_host_in_bits_data),
    .io_host_out_ready(routers_8_io_host_out_ready)
  );
  RingRouterV1_9 routers_9 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_9_clock),
    .io_in_ready(routers_9_io_in_ready),
    .io_in_valid(routers_9_io_in_valid),
    .io_in_bits_addr(routers_9_io_in_bits_addr),
    .io_in_bits_data(routers_9_io_in_bits_data),
    .io_out_ready(routers_9_io_out_ready),
    .io_out_valid(routers_9_io_out_valid),
    .io_out_bits_addr(routers_9_io_out_bits_addr),
    .io_out_bits_data(routers_9_io_out_bits_data),
    .io_host_in_ready(routers_9_io_host_in_ready),
    .io_host_in_valid(routers_9_io_host_in_valid),
    .io_host_in_bits_addr(routers_9_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_9_io_host_in_bits_data),
    .io_host_out_ready(routers_9_io_host_out_ready)
  );
  RingRouterV1_10 routers_10 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_10_clock),
    .io_in_ready(routers_10_io_in_ready),
    .io_in_valid(routers_10_io_in_valid),
    .io_in_bits_addr(routers_10_io_in_bits_addr),
    .io_in_bits_data(routers_10_io_in_bits_data),
    .io_out_ready(routers_10_io_out_ready),
    .io_out_valid(routers_10_io_out_valid),
    .io_out_bits_addr(routers_10_io_out_bits_addr),
    .io_out_bits_data(routers_10_io_out_bits_data),
    .io_host_in_ready(routers_10_io_host_in_ready),
    .io_host_in_valid(routers_10_io_host_in_valid),
    .io_host_in_bits_addr(routers_10_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_10_io_host_in_bits_data),
    .io_host_out_ready(routers_10_io_host_out_ready)
  );
  RingRouterV1_11 routers_11 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_11_clock),
    .io_in_ready(routers_11_io_in_ready),
    .io_in_valid(routers_11_io_in_valid),
    .io_in_bits_addr(routers_11_io_in_bits_addr),
    .io_in_bits_data(routers_11_io_in_bits_data),
    .io_out_ready(routers_11_io_out_ready),
    .io_out_valid(routers_11_io_out_valid),
    .io_out_bits_addr(routers_11_io_out_bits_addr),
    .io_out_bits_data(routers_11_io_out_bits_data),
    .io_host_in_ready(routers_11_io_host_in_ready),
    .io_host_in_valid(routers_11_io_host_in_valid),
    .io_host_in_bits_addr(routers_11_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_11_io_host_in_bits_data),
    .io_host_out_ready(routers_11_io_host_out_ready)
  );
  RingRouterV1_12 routers_12 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_12_clock),
    .io_in_ready(routers_12_io_in_ready),
    .io_in_valid(routers_12_io_in_valid),
    .io_in_bits_addr(routers_12_io_in_bits_addr),
    .io_in_bits_data(routers_12_io_in_bits_data),
    .io_out_ready(routers_12_io_out_ready),
    .io_out_valid(routers_12_io_out_valid),
    .io_out_bits_addr(routers_12_io_out_bits_addr),
    .io_out_bits_data(routers_12_io_out_bits_data),
    .io_host_in_ready(routers_12_io_host_in_ready),
    .io_host_in_valid(routers_12_io_host_in_valid),
    .io_host_in_bits_addr(routers_12_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_12_io_host_in_bits_data),
    .io_host_out_ready(routers_12_io_host_out_ready)
  );
  RingRouterV1_13 routers_13 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_13_clock),
    .io_in_ready(routers_13_io_in_ready),
    .io_in_valid(routers_13_io_in_valid),
    .io_in_bits_addr(routers_13_io_in_bits_addr),
    .io_in_bits_data(routers_13_io_in_bits_data),
    .io_out_ready(routers_13_io_out_ready),
    .io_out_valid(routers_13_io_out_valid),
    .io_out_bits_addr(routers_13_io_out_bits_addr),
    .io_out_bits_data(routers_13_io_out_bits_data),
    .io_host_in_ready(routers_13_io_host_in_ready),
    .io_host_in_valid(routers_13_io_host_in_valid),
    .io_host_in_bits_addr(routers_13_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_13_io_host_in_bits_data),
    .io_host_out_ready(routers_13_io_host_out_ready)
  );
  RingRouterV1_14 routers_14 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_14_clock),
    .io_in_ready(routers_14_io_in_ready),
    .io_in_valid(routers_14_io_in_valid),
    .io_in_bits_addr(routers_14_io_in_bits_addr),
    .io_in_bits_data(routers_14_io_in_bits_data),
    .io_out_ready(routers_14_io_out_ready),
    .io_out_valid(routers_14_io_out_valid),
    .io_out_bits_addr(routers_14_io_out_bits_addr),
    .io_out_bits_data(routers_14_io_out_bits_data),
    .io_host_in_ready(routers_14_io_host_in_ready),
    .io_host_in_valid(routers_14_io_host_in_valid),
    .io_host_in_bits_addr(routers_14_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_14_io_host_in_bits_data),
    .io_host_out_ready(routers_14_io_host_out_ready)
  );
  RingRouterV1_15 routers_15 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_15_clock),
    .io_in_ready(routers_15_io_in_ready),
    .io_in_valid(routers_15_io_in_valid),
    .io_in_bits_addr(routers_15_io_in_bits_addr),
    .io_in_bits_data(routers_15_io_in_bits_data),
    .io_out_ready(routers_15_io_out_ready),
    .io_out_valid(routers_15_io_out_valid),
    .io_out_bits_addr(routers_15_io_out_bits_addr),
    .io_out_bits_data(routers_15_io_out_bits_data),
    .io_host_in_ready(routers_15_io_host_in_ready),
    .io_host_in_valid(routers_15_io_host_in_valid),
    .io_host_in_bits_addr(routers_15_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_15_io_host_in_bits_data),
    .io_host_out_ready(routers_15_io_host_out_ready)
  );
  RingRouterV1_16 routers_16 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_16_clock),
    .io_in_ready(routers_16_io_in_ready),
    .io_in_valid(routers_16_io_in_valid),
    .io_in_bits_addr(routers_16_io_in_bits_addr),
    .io_in_bits_data(routers_16_io_in_bits_data),
    .io_out_ready(routers_16_io_out_ready),
    .io_out_valid(routers_16_io_out_valid),
    .io_out_bits_addr(routers_16_io_out_bits_addr),
    .io_out_bits_data(routers_16_io_out_bits_data),
    .io_host_in_ready(routers_16_io_host_in_ready),
    .io_host_in_valid(routers_16_io_host_in_valid),
    .io_host_in_bits_addr(routers_16_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_16_io_host_in_bits_data),
    .io_host_out_ready(routers_16_io_host_out_ready)
  );
  RingRouterV1_17 routers_17 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_17_clock),
    .io_in_ready(routers_17_io_in_ready),
    .io_in_valid(routers_17_io_in_valid),
    .io_in_bits_addr(routers_17_io_in_bits_addr),
    .io_in_bits_data(routers_17_io_in_bits_data),
    .io_out_ready(routers_17_io_out_ready),
    .io_out_valid(routers_17_io_out_valid),
    .io_out_bits_addr(routers_17_io_out_bits_addr),
    .io_out_bits_data(routers_17_io_out_bits_data),
    .io_host_in_ready(routers_17_io_host_in_ready),
    .io_host_in_valid(routers_17_io_host_in_valid),
    .io_host_in_bits_addr(routers_17_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_17_io_host_in_bits_data),
    .io_host_out_ready(routers_17_io_host_out_ready)
  );
  RingRouterV1_18 routers_18 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_18_clock),
    .io_in_ready(routers_18_io_in_ready),
    .io_in_valid(routers_18_io_in_valid),
    .io_in_bits_addr(routers_18_io_in_bits_addr),
    .io_in_bits_data(routers_18_io_in_bits_data),
    .io_out_ready(routers_18_io_out_ready),
    .io_out_valid(routers_18_io_out_valid),
    .io_out_bits_addr(routers_18_io_out_bits_addr),
    .io_out_bits_data(routers_18_io_out_bits_data),
    .io_host_in_ready(routers_18_io_host_in_ready),
    .io_host_in_valid(routers_18_io_host_in_valid),
    .io_host_in_bits_addr(routers_18_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_18_io_host_in_bits_data),
    .io_host_out_ready(routers_18_io_host_out_ready)
  );
  RingRouterV1_19 routers_19 ( // @[RingNetworkV1.scala 39:77]
    .clock(routers_19_clock),
    .io_in_ready(routers_19_io_in_ready),
    .io_in_valid(routers_19_io_in_valid),
    .io_in_bits_addr(routers_19_io_in_bits_addr),
    .io_in_bits_data(routers_19_io_in_bits_data),
    .io_out_ready(routers_19_io_out_ready),
    .io_out_valid(routers_19_io_out_valid),
    .io_out_bits_addr(routers_19_io_out_bits_addr),
    .io_out_bits_data(routers_19_io_out_bits_data),
    .io_host_in_ready(routers_19_io_host_in_ready),
    .io_host_in_valid(routers_19_io_host_in_valid),
    .io_host_in_bits_addr(routers_19_io_host_in_bits_addr),
    .io_host_in_bits_data(routers_19_io_host_in_bits_data),
    .io_host_out_ready(routers_19_io_host_out_ready)
  );
  assign io_ports_0_in_ready = routers_0_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_0_out_valid = routers_0_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_0_out_bits_addr = routers_0_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_0_out_bits_data = routers_0_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_1_in_ready = routers_1_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_1_out_valid = routers_1_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_1_out_bits_addr = routers_1_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_1_out_bits_data = routers_1_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_2_in_ready = routers_2_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_2_out_valid = routers_2_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_2_out_bits_addr = routers_2_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_2_out_bits_data = routers_2_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_3_in_ready = routers_3_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_3_out_valid = routers_3_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_3_out_bits_addr = routers_3_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_3_out_bits_data = routers_3_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_4_in_ready = routers_4_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_4_out_valid = routers_4_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_4_out_bits_addr = routers_4_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_4_out_bits_data = routers_4_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_5_in_ready = routers_5_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_5_out_valid = routers_5_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_5_out_bits_addr = routers_5_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_5_out_bits_data = routers_5_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_6_in_ready = routers_6_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_6_out_valid = routers_6_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_6_out_bits_addr = routers_6_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_6_out_bits_data = routers_6_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_7_in_ready = routers_7_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_7_out_valid = routers_7_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_7_out_bits_addr = routers_7_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_7_out_bits_data = routers_7_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_8_in_ready = routers_8_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_8_out_valid = routers_8_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_8_out_bits_addr = routers_8_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_8_out_bits_data = routers_8_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_9_in_ready = routers_9_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_9_out_valid = routers_9_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_9_out_bits_addr = routers_9_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_9_out_bits_data = routers_9_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_10_in_ready = routers_10_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_10_out_valid = routers_10_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_10_out_bits_addr = routers_10_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_10_out_bits_data = routers_10_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_11_in_ready = routers_11_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_11_out_valid = routers_11_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_11_out_bits_addr = routers_11_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_11_out_bits_data = routers_11_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_12_in_ready = routers_12_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_12_out_valid = routers_12_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_12_out_bits_addr = routers_12_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_12_out_bits_data = routers_12_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_13_in_ready = routers_13_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_13_out_valid = routers_13_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_13_out_bits_addr = routers_13_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_13_out_bits_data = routers_13_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_14_in_ready = routers_14_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_14_out_valid = routers_14_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_14_out_bits_addr = routers_14_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_14_out_bits_data = routers_14_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_15_in_ready = routers_15_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_15_out_valid = routers_15_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_15_out_bits_addr = routers_15_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_15_out_bits_data = routers_15_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_16_in_ready = routers_16_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_16_out_valid = routers_16_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_16_out_bits_addr = routers_16_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_16_out_bits_data = routers_16_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_17_in_ready = routers_17_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_17_out_valid = routers_17_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_17_out_bits_addr = routers_17_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_17_out_bits_data = routers_17_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_18_in_ready = routers_18_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_18_out_valid = routers_18_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_18_out_bits_addr = routers_18_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_18_out_bits_data = routers_18_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign io_ports_19_in_ready = routers_19_io_host_in_ready; // @[RingNetworkV1.scala 48:22]
  assign io_ports_19_out_valid = routers_19_io_out_valid; // @[RingNetworkV1.scala 49:21]
  assign io_ports_19_out_bits_addr = routers_19_io_out_bits_addr; // @[RingNetworkV1.scala 49:21]
  assign io_ports_19_out_bits_data = routers_19_io_out_bits_data; // @[RingNetworkV1.scala 49:21]
  assign routers_0_clock = clock;
  assign routers_0_io_in_valid = routers_19_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_0_io_in_bits_addr = routers_19_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_0_io_in_bits_data = routers_19_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_0_io_out_ready = io_ports_0_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_0_io_host_in_valid = io_ports_0_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_0_io_host_in_bits_addr = io_ports_0_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_0_io_host_in_bits_data = io_ports_0_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_0_io_host_out_ready = io_ports_0_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_1_clock = clock;
  assign routers_1_io_in_valid = routers_0_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_1_io_in_bits_addr = routers_0_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_1_io_in_bits_data = routers_0_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_1_io_out_ready = io_ports_1_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_1_io_host_in_valid = io_ports_1_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_1_io_host_in_bits_addr = io_ports_1_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_1_io_host_in_bits_data = io_ports_1_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_1_io_host_out_ready = io_ports_1_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_2_clock = clock;
  assign routers_2_io_in_valid = routers_1_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_2_io_in_bits_addr = routers_1_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_2_io_in_bits_data = routers_1_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_2_io_out_ready = io_ports_2_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_2_io_host_in_valid = io_ports_2_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_2_io_host_in_bits_addr = io_ports_2_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_2_io_host_in_bits_data = io_ports_2_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_2_io_host_out_ready = io_ports_2_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_3_clock = clock;
  assign routers_3_io_in_valid = routers_2_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_3_io_in_bits_addr = routers_2_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_3_io_in_bits_data = routers_2_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_3_io_out_ready = io_ports_3_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_3_io_host_in_valid = io_ports_3_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_3_io_host_in_bits_addr = io_ports_3_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_3_io_host_in_bits_data = io_ports_3_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_3_io_host_out_ready = io_ports_3_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_4_clock = clock;
  assign routers_4_io_in_valid = routers_3_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_4_io_in_bits_addr = routers_3_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_4_io_in_bits_data = routers_3_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_4_io_out_ready = io_ports_4_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_4_io_host_in_valid = io_ports_4_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_4_io_host_in_bits_addr = io_ports_4_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_4_io_host_in_bits_data = io_ports_4_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_4_io_host_out_ready = io_ports_4_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_5_clock = clock;
  assign routers_5_io_in_valid = routers_4_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_5_io_in_bits_addr = routers_4_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_5_io_in_bits_data = routers_4_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_5_io_out_ready = io_ports_5_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_5_io_host_in_valid = io_ports_5_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_5_io_host_in_bits_addr = io_ports_5_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_5_io_host_in_bits_data = io_ports_5_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_5_io_host_out_ready = io_ports_5_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_6_clock = clock;
  assign routers_6_io_in_valid = routers_5_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_6_io_in_bits_addr = routers_5_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_6_io_in_bits_data = routers_5_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_6_io_out_ready = io_ports_6_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_6_io_host_in_valid = io_ports_6_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_6_io_host_in_bits_addr = io_ports_6_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_6_io_host_in_bits_data = io_ports_6_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_6_io_host_out_ready = io_ports_6_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_7_clock = clock;
  assign routers_7_io_in_valid = routers_6_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_7_io_in_bits_addr = routers_6_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_7_io_in_bits_data = routers_6_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_7_io_out_ready = io_ports_7_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_7_io_host_in_valid = io_ports_7_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_7_io_host_in_bits_addr = io_ports_7_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_7_io_host_in_bits_data = io_ports_7_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_7_io_host_out_ready = io_ports_7_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_8_clock = clock;
  assign routers_8_io_in_valid = routers_7_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_8_io_in_bits_addr = routers_7_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_8_io_in_bits_data = routers_7_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_8_io_out_ready = io_ports_8_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_8_io_host_in_valid = io_ports_8_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_8_io_host_in_bits_addr = io_ports_8_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_8_io_host_in_bits_data = io_ports_8_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_8_io_host_out_ready = io_ports_8_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_9_clock = clock;
  assign routers_9_io_in_valid = routers_8_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_9_io_in_bits_addr = routers_8_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_9_io_in_bits_data = routers_8_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_9_io_out_ready = io_ports_9_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_9_io_host_in_valid = io_ports_9_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_9_io_host_in_bits_addr = io_ports_9_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_9_io_host_in_bits_data = io_ports_9_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_9_io_host_out_ready = io_ports_9_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_10_clock = clock;
  assign routers_10_io_in_valid = routers_9_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_10_io_in_bits_addr = routers_9_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_10_io_in_bits_data = routers_9_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_10_io_out_ready = io_ports_10_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_10_io_host_in_valid = io_ports_10_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_10_io_host_in_bits_addr = io_ports_10_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_10_io_host_in_bits_data = io_ports_10_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_10_io_host_out_ready = io_ports_10_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_11_clock = clock;
  assign routers_11_io_in_valid = routers_10_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_11_io_in_bits_addr = routers_10_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_11_io_in_bits_data = routers_10_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_11_io_out_ready = io_ports_11_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_11_io_host_in_valid = io_ports_11_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_11_io_host_in_bits_addr = io_ports_11_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_11_io_host_in_bits_data = io_ports_11_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_11_io_host_out_ready = io_ports_11_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_12_clock = clock;
  assign routers_12_io_in_valid = routers_11_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_12_io_in_bits_addr = routers_11_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_12_io_in_bits_data = routers_11_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_12_io_out_ready = io_ports_12_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_12_io_host_in_valid = io_ports_12_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_12_io_host_in_bits_addr = io_ports_12_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_12_io_host_in_bits_data = io_ports_12_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_12_io_host_out_ready = io_ports_12_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_13_clock = clock;
  assign routers_13_io_in_valid = routers_12_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_13_io_in_bits_addr = routers_12_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_13_io_in_bits_data = routers_12_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_13_io_out_ready = io_ports_13_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_13_io_host_in_valid = io_ports_13_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_13_io_host_in_bits_addr = io_ports_13_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_13_io_host_in_bits_data = io_ports_13_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_13_io_host_out_ready = io_ports_13_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_14_clock = clock;
  assign routers_14_io_in_valid = routers_13_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_14_io_in_bits_addr = routers_13_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_14_io_in_bits_data = routers_13_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_14_io_out_ready = io_ports_14_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_14_io_host_in_valid = io_ports_14_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_14_io_host_in_bits_addr = io_ports_14_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_14_io_host_in_bits_data = io_ports_14_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_14_io_host_out_ready = io_ports_14_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_15_clock = clock;
  assign routers_15_io_in_valid = routers_14_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_15_io_in_bits_addr = routers_14_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_15_io_in_bits_data = routers_14_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_15_io_out_ready = io_ports_15_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_15_io_host_in_valid = io_ports_15_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_15_io_host_in_bits_addr = io_ports_15_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_15_io_host_in_bits_data = io_ports_15_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_15_io_host_out_ready = io_ports_15_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_16_clock = clock;
  assign routers_16_io_in_valid = routers_15_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_16_io_in_bits_addr = routers_15_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_16_io_in_bits_data = routers_15_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_16_io_out_ready = io_ports_16_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_16_io_host_in_valid = io_ports_16_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_16_io_host_in_bits_addr = io_ports_16_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_16_io_host_in_bits_data = io_ports_16_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_16_io_host_out_ready = io_ports_16_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_17_clock = clock;
  assign routers_17_io_in_valid = routers_16_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_17_io_in_bits_addr = routers_16_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_17_io_in_bits_data = routers_16_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_17_io_out_ready = io_ports_17_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_17_io_host_in_valid = io_ports_17_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_17_io_host_in_bits_addr = io_ports_17_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_17_io_host_in_bits_data = io_ports_17_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_17_io_host_out_ready = io_ports_17_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_18_clock = clock;
  assign routers_18_io_in_valid = routers_17_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_18_io_in_bits_addr = routers_17_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_18_io_in_bits_data = routers_17_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_18_io_out_ready = io_ports_18_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_18_io_host_in_valid = io_ports_18_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_18_io_host_in_bits_addr = io_ports_18_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_18_io_host_in_bits_data = io_ports_18_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_18_io_host_out_ready = io_ports_18_out_ready; // @[RingNetworkV1.scala 48:22]
  assign routers_19_clock = clock;
  assign routers_19_io_in_valid = routers_18_io_out_valid; // @[RingNetworkV1.scala 42:33]
  assign routers_19_io_in_bits_addr = routers_18_io_out_bits_addr; // @[RingNetworkV1.scala 42:33]
  assign routers_19_io_in_bits_data = routers_18_io_out_bits_data; // @[RingNetworkV1.scala 42:33]
  assign routers_19_io_out_ready = io_ports_19_out_ready; // @[RingNetworkV1.scala 49:21]
  assign routers_19_io_host_in_valid = io_ports_19_in_valid; // @[RingNetworkV1.scala 48:22]
  assign routers_19_io_host_in_bits_addr = io_ports_19_in_bits_addr; // @[RingNetworkV1.scala 48:22]
  assign routers_19_io_host_in_bits_data = io_ports_19_in_bits_data; // @[RingNetworkV1.scala 48:22]
  assign routers_19_io_host_out_ready = io_ports_19_out_ready; // @[RingNetworkV1.scala 48:22]
endmodule
```
