```verilog
module RRArbiter(
  input        clock,
  output       io_in_0_ready,
  input        io_in_0_valid,
  input  [3:0] io_in_0_bits_data_addr,
  input  [4:0] io_in_0_bits_data_data,
  output       io_in_1_ready,
  input        io_in_1_valid,
  input  [3:0] io_in_1_bits_data_addr,
  input  [4:0] io_in_1_bits_data_data,
  output       io_in_2_ready,
  input        io_in_2_valid,
  input  [3:0] io_in_2_bits_data_addr,
  input  [4:0] io_in_2_bits_data_data,
  input        io_out_ready,
  output       io_out_valid,
  output [3:0] io_out_bits_data_addr,
  output [4:0] io_out_bits_data_data,
  output [1:0] io_chosen
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
`endif // RANDOMIZE_REG_INIT
  wire  _GEN_1 = 2'h1 == io_chosen ? io_in_1_valid : io_in_0_valid; // @[Arbiter.scala 56:{16,16}]
  wire [3:0] _GEN_7 = 2'h1 == io_chosen ? io_in_1_bits_data_addr : io_in_0_bits_data_addr; // @[Arbiter.scala 57:{15,15}]
  wire [4:0] _GEN_10 = 2'h1 == io_chosen ? io_in_1_bits_data_data : io_in_0_bits_data_data; // @[Arbiter.scala 57:{15,15}]
  wire  _ctrl_validMask_grantMask_lastGrant_T = io_out_ready & io_out_valid; // @[Decoupled.scala 50:35]
  reg [1:0] lastGrant; // @[Reg.scala 16:16]
  wire  grantMask_1 = 2'h1 > lastGrant; // @[Arbiter.scala 82:49]
  wire  grantMask_2 = 2'h2 > lastGrant; // @[Arbiter.scala 82:49]
  wire  validMask_1 = io_in_1_valid & grantMask_1; // @[Arbiter.scala 83:76]
  wire  validMask_2 = io_in_2_valid & grantMask_2; // @[Arbiter.scala 83:76]
  wire  ctrl_2 = ~validMask_1; // @[Arbiter.scala 46:78]
  wire  ctrl_3 = ~(validMask_1 | validMask_2); // @[Arbiter.scala 46:78]
  wire  ctrl_4 = ~(validMask_1 | validMask_2 | io_in_0_valid); // @[Arbiter.scala 46:78]
  wire  ctrl_5 = ~(validMask_1 | validMask_2 | io_in_0_valid | io_in_1_valid); // @[Arbiter.scala 46:78]
  wire  _T_3 = grantMask_1 | ctrl_4; // @[Arbiter.scala 87:50]
  wire  _T_5 = ctrl_2 & grantMask_2 | ctrl_5; // @[Arbiter.scala 87:50]
  wire [1:0] _GEN_13 = io_in_1_valid ? 2'h1 : 2'h2; // @[Arbiter.scala 92:{26,35}]
  wire [1:0] _GEN_14 = io_in_0_valid ? 2'h0 : _GEN_13; // @[Arbiter.scala 92:{26,35}]
  wire [1:0] _GEN_15 = validMask_2 ? 2'h2 : _GEN_14; // @[Arbiter.scala 94:{24,33}]
  assign io_in_0_ready = ctrl_3 & io_out_ready; // @[Arbiter.scala 75:21]
  assign io_in_1_ready = _T_3 & io_out_ready; // @[Arbiter.scala 75:21]
  assign io_in_2_ready = _T_5 & io_out_ready; // @[Arbiter.scala 75:21]
  assign io_out_valid = 2'h2 == io_chosen ? io_in_2_valid : _GEN_1; // @[Arbiter.scala 56:{16,16}]
  assign io_out_bits_data_addr = 2'h2 == io_chosen ? io_in_2_bits_data_addr : _GEN_7; // @[Arbiter.scala 57:{15,15}]
  assign io_out_bits_data_data = 2'h2 == io_chosen ? io_in_2_bits_data_data : _GEN_10; // @[Arbiter.scala 57:{15,15}]
  assign io_chosen = validMask_1 ? 2'h1 : _GEN_15; // @[Arbiter.scala 94:{24,33}]
  always @(posedge clock) begin
    if (_ctrl_validMask_grantMask_lastGrant_T) begin // @[Reg.scala 17:18]
      lastGrant <= io_chosen; // @[Reg.scala 17:22]
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
  lastGrant = _RAND_0[1:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
module CrossBarV3(
  input        clock,
  output       io_ports_0_in_ready,
  input  [1:0] io_ports_0_in_bits_addr,
  input  [3:0] io_ports_0_in_bits_data_addr,
  input  [4:0] io_ports_0_in_bits_data_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_data_addr,
  output [4:0] io_ports_0_out_bits_data_data,
  output       io_ports_1_in_ready,
  input  [1:0] io_ports_1_in_bits_addr,
  input  [3:0] io_ports_1_in_bits_data_addr,
  input  [4:0] io_ports_1_in_bits_data_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_data_addr,
  output [4:0] io_ports_1_out_bits_data_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [1:0] io_ports_2_in_bits_addr,
  input  [3:0] io_ports_2_in_bits_data_addr,
  input  [4:0] io_ports_2_in_bits_data_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_data_addr,
  output [4:0] io_ports_2_out_bits_data_data
);
  wire  arbs_0_clock; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_in_0_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_in_0_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_0_io_in_0_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_0_io_in_0_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_in_1_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_in_1_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_0_io_in_1_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_0_io_in_1_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_in_2_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_in_2_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_0_io_in_2_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_0_io_in_2_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_out_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_0_io_out_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_0_io_out_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_0_io_out_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire [1:0] arbs_0_io_chosen; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_clock; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_in_0_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_in_0_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_1_io_in_0_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_1_io_in_0_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_in_1_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_in_1_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_1_io_in_1_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_1_io_in_1_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_in_2_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_in_2_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_1_io_in_2_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_1_io_in_2_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_out_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_1_io_out_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_1_io_out_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_1_io_out_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire [1:0] arbs_1_io_chosen; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_clock; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_in_0_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_in_0_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_2_io_in_0_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_2_io_in_0_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_in_1_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_in_1_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_2_io_in_1_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_2_io_in_1_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_in_2_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_in_2_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_2_io_in_2_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_2_io_in_2_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_out_ready; // @[RingNetworkV3.scala 9:73]
  wire  arbs_2_io_out_valid; // @[RingNetworkV3.scala 9:73]
  wire [3:0] arbs_2_io_out_bits_data_addr; // @[RingNetworkV3.scala 9:73]
  wire [4:0] arbs_2_io_out_bits_data_data; // @[RingNetworkV3.scala 9:73]
  wire [1:0] arbs_2_io_chosen; // @[RingNetworkV3.scala 9:73]
  RRArbiter arbs_0 ( // @[RingNetworkV3.scala 9:73]
    .clock(arbs_0_clock),
    .io_in_0_ready(arbs_0_io_in_0_ready),
    .io_in_0_valid(arbs_0_io_in_0_valid),
    .io_in_0_bits_data_addr(arbs_0_io_in_0_bits_data_addr),
    .io_in_0_bits_data_data(arbs_0_io_in_0_bits_data_data),
    .io_in_1_ready(arbs_0_io_in_1_ready),
    .io_in_1_valid(arbs_0_io_in_1_valid),
    .io_in_1_bits_data_addr(arbs_0_io_in_1_bits_data_addr),
    .io_in_1_bits_data_data(arbs_0_io_in_1_bits_data_data),
    .io_in_2_ready(arbs_0_io_in_2_ready),
    .io_in_2_valid(arbs_0_io_in_2_valid),
    .io_in_2_bits_data_addr(arbs_0_io_in_2_bits_data_addr),
    .io_in_2_bits_data_data(arbs_0_io_in_2_bits_data_data),
    .io_out_ready(arbs_0_io_out_ready),
    .io_out_valid(arbs_0_io_out_valid),
    .io_out_bits_data_addr(arbs_0_io_out_bits_data_addr),
    .io_out_bits_data_data(arbs_0_io_out_bits_data_data),
    .io_chosen(arbs_0_io_chosen)
  );
  RRArbiter arbs_1 ( // @[RingNetworkV3.scala 9:73]
    .clock(arbs_1_clock),
    .io_in_0_ready(arbs_1_io_in_0_ready),
    .io_in_0_valid(arbs_1_io_in_0_valid),
    .io_in_0_bits_data_addr(arbs_1_io_in_0_bits_data_addr),
    .io_in_0_bits_data_data(arbs_1_io_in_0_bits_data_data),
    .io_in_1_ready(arbs_1_io_in_1_ready),
    .io_in_1_valid(arbs_1_io_in_1_valid),
    .io_in_1_bits_data_addr(arbs_1_io_in_1_bits_data_addr),
    .io_in_1_bits_data_data(arbs_1_io_in_1_bits_data_data),
    .io_in_2_ready(arbs_1_io_in_2_ready),
    .io_in_2_valid(arbs_1_io_in_2_valid),
    .io_in_2_bits_data_addr(arbs_1_io_in_2_bits_data_addr),
    .io_in_2_bits_data_data(arbs_1_io_in_2_bits_data_data),
    .io_out_ready(arbs_1_io_out_ready),
    .io_out_valid(arbs_1_io_out_valid),
    .io_out_bits_data_addr(arbs_1_io_out_bits_data_addr),
    .io_out_bits_data_data(arbs_1_io_out_bits_data_data),
    .io_chosen(arbs_1_io_chosen)
  );
  RRArbiter arbs_2 ( // @[RingNetworkV3.scala 9:73]
    .clock(arbs_2_clock),
    .io_in_0_ready(arbs_2_io_in_0_ready),
    .io_in_0_valid(arbs_2_io_in_0_valid),
    .io_in_0_bits_data_addr(arbs_2_io_in_0_bits_data_addr),
    .io_in_0_bits_data_data(arbs_2_io_in_0_bits_data_data),
    .io_in_1_ready(arbs_2_io_in_1_ready),
    .io_in_1_valid(arbs_2_io_in_1_valid),
    .io_in_1_bits_data_addr(arbs_2_io_in_1_bits_data_addr),
    .io_in_1_bits_data_data(arbs_2_io_in_1_bits_data_data),
    .io_in_2_ready(arbs_2_io_in_2_ready),
    .io_in_2_valid(arbs_2_io_in_2_valid),
    .io_in_2_bits_data_addr(arbs_2_io_in_2_bits_data_addr),
    .io_in_2_bits_data_data(arbs_2_io_in_2_bits_data_data),
    .io_out_ready(arbs_2_io_out_ready),
    .io_out_valid(arbs_2_io_out_valid),
    .io_out_bits_data_addr(arbs_2_io_out_bits_data_addr),
    .io_out_bits_data_data(arbs_2_io_out_bits_data_data),
    .io_chosen(arbs_2_io_chosen)
  );
  assign io_ports_0_in_ready = arbs_0_io_in_0_ready | arbs_1_io_in_0_ready | arbs_2_io_in_0_ready; // @[RingNetworkV3.scala 11:70]
  assign io_ports_0_out_bits_data_addr = arbs_0_io_out_bits_data_addr; // @[RingNetworkV3.scala 18:22]
  assign io_ports_0_out_bits_data_data = arbs_0_io_out_bits_data_data; // @[RingNetworkV3.scala 18:22]
  assign io_ports_1_in_ready = arbs_0_io_in_1_ready | arbs_1_io_in_1_ready | arbs_2_io_in_1_ready; // @[RingNetworkV3.scala 11:70]
  assign io_ports_1_out_bits_data_addr = arbs_1_io_out_bits_data_addr; // @[RingNetworkV3.scala 18:22]
  assign io_ports_1_out_bits_data_data = arbs_1_io_out_bits_data_data; // @[RingNetworkV3.scala 18:22]
  assign io_ports_2_in_ready = arbs_0_io_in_2_ready | arbs_1_io_in_2_ready | arbs_2_io_in_2_ready; // @[RingNetworkV3.scala 11:70]
  assign io_ports_2_out_bits_data_addr = arbs_2_io_out_bits_data_addr; // @[RingNetworkV3.scala 18:22]
  assign io_ports_2_out_bits_data_data = arbs_2_io_out_bits_data_data; // @[RingNetworkV3.scala 18:22]
  assign arbs_0_clock = clock;
  assign arbs_0_io_in_0_valid = io_ports_0_in_bits_addr == 2'h0; // @[RingNetworkV3.scala 16:58]
  assign arbs_0_io_in_0_bits_data_addr = io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_0_io_in_0_bits_data_data = io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_0_io_in_1_valid = io_ports_1_in_bits_addr == 2'h0; // @[RingNetworkV3.scala 16:58]
  assign arbs_0_io_in_1_bits_data_addr = io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_0_io_in_1_bits_data_data = io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_0_io_in_2_valid = io_ports_2_in_valid & io_ports_2_in_bits_addr == 2'h0; // @[RingNetworkV3.scala 16:36]
  assign arbs_0_io_in_2_bits_data_addr = io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_0_io_in_2_bits_data_data = io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_0_io_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 18:22]
  assign arbs_1_clock = clock;
  assign arbs_1_io_in_0_valid = io_ports_0_in_bits_addr == 2'h1; // @[RingNetworkV3.scala 16:58]
  assign arbs_1_io_in_0_bits_data_addr = io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_1_io_in_0_bits_data_data = io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_1_io_in_1_valid = io_ports_1_in_bits_addr == 2'h1; // @[RingNetworkV3.scala 16:58]
  assign arbs_1_io_in_1_bits_data_addr = io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_1_io_in_1_bits_data_data = io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_1_io_in_2_valid = io_ports_2_in_valid & io_ports_2_in_bits_addr == 2'h1; // @[RingNetworkV3.scala 16:36]
  assign arbs_1_io_in_2_bits_data_addr = io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_1_io_in_2_bits_data_data = io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_1_io_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 18:22]
  assign arbs_2_clock = clock;
  assign arbs_2_io_in_0_valid = io_ports_0_in_bits_addr == 2'h2; // @[RingNetworkV3.scala 16:58]
  assign arbs_2_io_in_0_bits_data_addr = io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_2_io_in_0_bits_data_data = io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_2_io_in_1_valid = io_ports_1_in_bits_addr == 2'h2; // @[RingNetworkV3.scala 16:58]
  assign arbs_2_io_in_1_bits_data_addr = io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_2_io_in_1_bits_data_data = io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_2_io_in_2_valid = io_ports_2_in_valid & io_ports_2_in_bits_addr == 2'h2; // @[RingNetworkV3.scala 16:36]
  assign arbs_2_io_in_2_bits_data_addr = io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 15:18]
  assign arbs_2_io_in_2_bits_data_data = io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 15:18]
  assign arbs_2_io_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 18:22]
endmodule
module RingRouterV3(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [4:0] _portsRouted_routed_in_bits_addr_distTowards0_T_5 = {{1'd0},
    _portsRouted_routed_in_bits_addr_distTowards0_T_4}; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = _portsRouted_routed_in_bits_addr_distTowards0_T_5[3:0]; // @[RingNetworkV3.scala 32:67]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h0; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h0; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h0 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [4:0] _portsRouted_routed_in_bits_addr_distTowards0_T_12 = {{1'd0},
    _portsRouted_routed_in_bits_addr_distTowards0_T_11}; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = _portsRouted_routed_in_bits_addr_distTowards0_T_12[3:0]; // @[RingNetworkV3.scala 32:67]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h0; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h0 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [4:0] _portsRouted_routed_in_bits_addr_distTowards0_T_19 = {{1'd0},
    _portsRouted_routed_in_bits_addr_distTowards0_T_18}; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = _portsRouted_routed_in_bits_addr_distTowards0_T_19[3:0]; // @[RingNetworkV3.scala 32:67]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h0; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h0 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h0 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h0 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h0 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_1(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h1 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h1 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h1 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h1; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h1; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h1 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h1 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h1 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h1 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h1; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h1 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h1 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h1 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h1 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h1; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h1 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h1 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h1 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h1 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_2(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h2 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h2 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h2 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h2; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h2; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h2 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h2 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h2 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h2 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h2; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h2 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h2 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h2 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h2 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h2; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h2 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h2 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h2 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h2 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_3(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h3 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h3 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h3 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h3; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h3; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h3 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h3 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h3 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h3 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h3; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h3 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h3 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h3 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h3 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h3; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h3 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h3 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h3 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h3 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_4(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h4 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h4 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h4 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h4; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h4; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h4 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h4 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h4 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h4 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h4; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h4 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h4 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h4 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h4 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h4; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h4 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h4 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h4 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h4 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_5(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h5 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h5 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h5 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h5; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h5; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h5 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h5 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h5 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h5 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h5; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h5 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h5 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h5 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h5 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h5; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h5 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h5 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h5 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h5 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_6(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h6 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h6 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h6 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h6; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h6; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h6 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h6 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h6 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h6 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h6; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h6 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h6 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h6 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h6 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h6; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h6 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h6 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h6 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h6 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_7(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h7 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h7 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h7 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h7; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h7; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h7 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h7 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h7 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h7 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h7; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h7 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h7 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h7 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h7 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h7; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h7 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h7 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h7 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h7 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_8(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h8 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h8 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h8 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h8; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h8; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h8 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h8 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h8 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h8 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h8; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h8 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h8 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h8 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h8 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h8; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h8 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h8 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h8 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h8 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingRouterV3_9(
  input        clock,
  output       io_ports_0_in_ready,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data
);
  wire  xbar_clock; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_0_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_1_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_in_valid; // @[RingNetworkV3.scala 38:48]
  wire [1:0] xbar_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_in_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_in_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire  xbar_io_ports_2_out_ready; // @[RingNetworkV3.scala 38:48]
  wire [3:0] xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 38:48]
  wire [4:0] xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 38:48]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_2 = 4'h9 - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_4 = 4'ha - io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_6 = 4'h9 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_4; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0 = io_ports_0_in_bits_addr < 4'h9 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_2 : _portsRouted_routed_in_bits_addr_distTowards0_T_6; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_2 = io_ports_0_in_bits_addr - 4'h9; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_4 = 4'ha - 4'h9; // @[RingNetworkV3.scala 33:76]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_6 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1 = io_ports_0_in_bits_addr > 4'h9 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_2 : _portsRouted_routed_in_bits_addr_distTowards1_T_6; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_2 = portsRouted_routed_in_bits_addr_distTowards0 <
    portsRouted_routed_in_bits_addr_distTowards1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_9 = 4'h9 - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_11 = 4'ha - io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_13 = 4'h9 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_11; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_1 = io_ports_1_in_bits_addr < 4'h9 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_9 : _portsRouted_routed_in_bits_addr_distTowards0_T_13; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_9 = io_ports_1_in_bits_addr - 4'h9; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_13 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_1 = io_ports_1_in_bits_addr > 4'h9 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_9 : _portsRouted_routed_in_bits_addr_distTowards1_T_13; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_6 = portsRouted_routed_in_bits_addr_distTowards0_1 <
    portsRouted_routed_in_bits_addr_distTowards1_1 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_16 = 4'h9 - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:50]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_18 = 4'ha - io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 32:83]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards0_T_20 = 4'h9 +
    _portsRouted_routed_in_bits_addr_distTowards0_T_18; // @[RingNetworkV3.scala 32:67]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards0_2 = io_ports_2_in_bits_addr < 4'h9 ?
    _portsRouted_routed_in_bits_addr_distTowards0_T_16 : _portsRouted_routed_in_bits_addr_distTowards0_T_20; // @[RingNetworkV3.scala 32:27]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_16 = io_ports_2_in_bits_addr - 4'h9; // @[RingNetworkV3.scala 33:54]
  wire [3:0] _portsRouted_routed_in_bits_addr_distTowards1_T_20 = _portsRouted_routed_in_bits_addr_distTowards1_T_4 +
    io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 33:84]
  wire [3:0] portsRouted_routed_in_bits_addr_distTowards1_2 = io_ports_2_in_bits_addr > 4'h9 ?
    _portsRouted_routed_in_bits_addr_distTowards1_T_16 : _portsRouted_routed_in_bits_addr_distTowards1_T_20; // @[RingNetworkV3.scala 33:27]
  wire  _portsRouted_routed_in_bits_addr_T_10 = portsRouted_routed_in_bits_addr_distTowards0_2 <
    portsRouted_routed_in_bits_addr_distTowards1_2 ? 1'h0 : 1'h1; // @[RingNetworkV3.scala 34:36]
  CrossBarV3 xbar ( // @[RingNetworkV3.scala 38:48]
    .clock(xbar_clock),
    .io_ports_0_in_ready(xbar_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(xbar_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data_addr(xbar_io_ports_0_in_bits_data_addr),
    .io_ports_0_in_bits_data_data(xbar_io_ports_0_in_bits_data_data),
    .io_ports_0_out_ready(xbar_io_ports_0_out_ready),
    .io_ports_0_out_bits_data_addr(xbar_io_ports_0_out_bits_data_addr),
    .io_ports_0_out_bits_data_data(xbar_io_ports_0_out_bits_data_data),
    .io_ports_1_in_ready(xbar_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(xbar_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data_addr(xbar_io_ports_1_in_bits_data_addr),
    .io_ports_1_in_bits_data_data(xbar_io_ports_1_in_bits_data_data),
    .io_ports_1_out_ready(xbar_io_ports_1_out_ready),
    .io_ports_1_out_bits_data_addr(xbar_io_ports_1_out_bits_data_addr),
    .io_ports_1_out_bits_data_data(xbar_io_ports_1_out_bits_data_data),
    .io_ports_2_in_ready(xbar_io_ports_2_in_ready),
    .io_ports_2_in_valid(xbar_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(xbar_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data_addr(xbar_io_ports_2_in_bits_data_addr),
    .io_ports_2_in_bits_data_data(xbar_io_ports_2_in_bits_data_data),
    .io_ports_2_out_ready(xbar_io_ports_2_out_ready),
    .io_ports_2_out_bits_data_addr(xbar_io_ports_2_out_bits_data_addr),
    .io_ports_2_out_bits_data_data(xbar_io_ports_2_out_bits_data_data)
  );
  assign io_ports_0_in_ready = xbar_io_ports_0_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_addr = xbar_io_ports_0_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_0_out_bits_data = xbar_io_ports_0_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_in_ready = xbar_io_ports_1_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_addr = xbar_io_ports_1_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_1_out_bits_data = xbar_io_ports_1_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_in_ready = xbar_io_ports_2_in_ready; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_addr = xbar_io_ports_2_out_bits_data_addr; // @[RingNetworkV3.scala 41:22 59:41]
  assign io_ports_2_out_bits_data = xbar_io_ports_2_out_bits_data_data; // @[RingNetworkV3.scala 41:22 59:41]
  assign xbar_clock = clock;
  assign xbar_io_ports_0_in_bits_addr = io_ports_0_in_bits_addr == 4'h9 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_2}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_0_in_bits_data_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_in_bits_data_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_0_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_1_in_bits_addr = io_ports_1_in_bits_addr == 4'h9 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_6}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_1_in_bits_data_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_in_bits_data_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_1_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
  assign xbar_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 41:22 44:21]
  assign xbar_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr == 4'h9 ? 2'h2 : {{1'd0},
    _portsRouted_routed_in_bits_addr_T_10}; // @[RingNetworkV3.scala 34:8]
  assign xbar_io_ports_2_in_bits_data_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_in_bits_data_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 41:22 43:25]
  assign xbar_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 41:22 49:22]
endmodule
module RingNetworkV3(
  input        clock,
  input        reset,
  output       io_ports_0_in_ready,
  input        io_ports_0_in_valid,
  input  [3:0] io_ports_0_in_bits_addr,
  input  [4:0] io_ports_0_in_bits_data,
  input        io_ports_0_out_ready,
  output       io_ports_0_out_valid,
  output [3:0] io_ports_0_out_bits_addr,
  output [4:0] io_ports_0_out_bits_data,
  output       io_ports_1_in_ready,
  input        io_ports_1_in_valid,
  input  [3:0] io_ports_1_in_bits_addr,
  input  [4:0] io_ports_1_in_bits_data,
  input        io_ports_1_out_ready,
  output       io_ports_1_out_valid,
  output [3:0] io_ports_1_out_bits_addr,
  output [4:0] io_ports_1_out_bits_data,
  output       io_ports_2_in_ready,
  input        io_ports_2_in_valid,
  input  [3:0] io_ports_2_in_bits_addr,
  input  [4:0] io_ports_2_in_bits_data,
  input        io_ports_2_out_ready,
  output       io_ports_2_out_valid,
  output [3:0] io_ports_2_out_bits_addr,
  output [4:0] io_ports_2_out_bits_data,
  output       io_ports_3_in_ready,
  input        io_ports_3_in_valid,
  input  [3:0] io_ports_3_in_bits_addr,
  input  [4:0] io_ports_3_in_bits_data,
  input        io_ports_3_out_ready,
  output       io_ports_3_out_valid,
  output [3:0] io_ports_3_out_bits_addr,
  output [4:0] io_ports_3_out_bits_data,
  output       io_ports_4_in_ready,
  input        io_ports_4_in_valid,
  input  [3:0] io_ports_4_in_bits_addr,
  input  [4:0] io_ports_4_in_bits_data,
  input        io_ports_4_out_ready,
  output       io_ports_4_out_valid,
  output [3:0] io_ports_4_out_bits_addr,
  output [4:0] io_ports_4_out_bits_data,
  output       io_ports_5_in_ready,
  input        io_ports_5_in_valid,
  input  [3:0] io_ports_5_in_bits_addr,
  input  [4:0] io_ports_5_in_bits_data,
  input        io_ports_5_out_ready,
  output       io_ports_5_out_valid,
  output [3:0] io_ports_5_out_bits_addr,
  output [4:0] io_ports_5_out_bits_data,
  output       io_ports_6_in_ready,
  input        io_ports_6_in_valid,
  input  [3:0] io_ports_6_in_bits_addr,
  input  [4:0] io_ports_6_in_bits_data,
  input        io_ports_6_out_ready,
  output       io_ports_6_out_valid,
  output [3:0] io_ports_6_out_bits_addr,
  output [4:0] io_ports_6_out_bits_data,
  output       io_ports_7_in_ready,
  input        io_ports_7_in_valid,
  input  [3:0] io_ports_7_in_bits_addr,
  input  [4:0] io_ports_7_in_bits_data,
  input        io_ports_7_out_ready,
  output       io_ports_7_out_valid,
  output [3:0] io_ports_7_out_bits_addr,
  output [4:0] io_ports_7_out_bits_data,
  output       io_ports_8_in_ready,
  input        io_ports_8_in_valid,
  input  [3:0] io_ports_8_in_bits_addr,
  input  [4:0] io_ports_8_in_bits_data,
  input        io_ports_8_out_ready,
  output       io_ports_8_out_valid,
  output [3:0] io_ports_8_out_bits_addr,
  output [4:0] io_ports_8_out_bits_data,
  output       io_ports_9_in_ready,
  input        io_ports_9_in_valid,
  input  [3:0] io_ports_9_in_bits_addr,
  input  [4:0] io_ports_9_in_bits_data,
  input        io_ports_9_out_ready,
  output       io_ports_9_out_valid,
  output [3:0] io_ports_9_out_bits_addr,
  output [4:0] io_ports_9_out_bits_data
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
  reg [31:0] _RAND_1;
  reg [31:0] _RAND_2;
  reg [31:0] _RAND_3;
  reg [31:0] _RAND_4;
  reg [31:0] _RAND_5;
  reg [31:0] _RAND_6;
  reg [31:0] _RAND_7;
  reg [31:0] _RAND_8;
  reg [31:0] _RAND_9;
  reg [31:0] _RAND_10;
  reg [31:0] _RAND_11;
  reg [31:0] _RAND_12;
  reg [31:0] _RAND_13;
  reg [31:0] _RAND_14;
  reg [31:0] _RAND_15;
  reg [31:0] _RAND_16;
  reg [31:0] _RAND_17;
  reg [31:0] _RAND_18;
  reg [31:0] _RAND_19;
  reg [31:0] _RAND_20;
  reg [31:0] _RAND_21;
  reg [31:0] _RAND_22;
  reg [31:0] _RAND_23;
  reg [31:0] _RAND_24;
  reg [31:0] _RAND_25;
  reg [31:0] _RAND_26;
  reg [31:0] _RAND_27;
  reg [31:0] _RAND_28;
  reg [31:0] _RAND_29;
  reg [31:0] _RAND_30;
  reg [31:0] _RAND_31;
  reg [31:0] _RAND_32;
  reg [31:0] _RAND_33;
  reg [31:0] _RAND_34;
  reg [31:0] _RAND_35;
  reg [31:0] _RAND_36;
  reg [31:0] _RAND_37;
  reg [31:0] _RAND_38;
  reg [31:0] _RAND_39;
  reg [31:0] _RAND_40;
  reg [31:0] _RAND_41;
  reg [31:0] _RAND_42;
  reg [31:0] _RAND_43;
  reg [31:0] _RAND_44;
  reg [31:0] _RAND_45;
  reg [31:0] _RAND_46;
  reg [31:0] _RAND_47;
  reg [31:0] _RAND_48;
  reg [31:0] _RAND_49;
  reg [31:0] _RAND_50;
  reg [31:0] _RAND_51;
  reg [31:0] _RAND_52;
  reg [31:0] _RAND_53;
  reg [31:0] _RAND_54;
  reg [31:0] _RAND_55;
  reg [31:0] _RAND_56;
  reg [31:0] _RAND_57;
  reg [31:0] _RAND_58;
  reg [31:0] _RAND_59;
`endif // RANDOMIZE_REG_INIT
  wire  routers_0_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_0_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_0_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_0_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_0_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_0_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_0_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_0_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_0_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_0_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_0_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_0_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_0_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_0_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_1_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_1_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_1_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_1_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_1_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_1_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_1_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_1_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_1_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_1_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_1_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_1_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_1_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_2_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_2_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_2_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_2_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_2_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_2_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_2_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_2_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_2_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_2_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_2_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_2_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_2_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_3_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_3_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_3_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_3_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_3_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_3_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_3_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_3_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_3_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_3_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_3_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_3_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_3_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_4_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_4_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_4_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_4_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_4_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_4_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_4_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_4_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_4_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_4_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_4_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_4_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_4_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_5_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_5_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_5_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_5_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_5_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_5_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_5_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_5_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_5_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_5_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_5_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_5_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_5_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_6_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_6_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_6_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_6_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_6_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_6_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_6_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_6_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_6_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_6_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_6_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_6_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_6_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_7_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_7_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_7_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_7_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_7_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_7_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_7_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_7_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_7_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_7_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_7_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_7_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_7_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_8_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_8_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_8_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_8_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_8_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_8_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_8_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_8_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_8_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_8_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_8_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_8_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_8_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_clock; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_0_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_9_io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_9_io_ports_0_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_0_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_9_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_9_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_1_in_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_9_io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_9_io_ports_1_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_1_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_9_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_9_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_2_in_ready; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_2_in_valid; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_9_io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_9_io_ports_2_in_bits_data; // @[RingNetworkV3.scala 66:77]
  wire  routers_9_io_ports_2_out_ready; // @[RingNetworkV3.scala 66:77]
  wire [3:0] routers_9_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 66:77]
  wire [4:0] routers_9_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 66:77]
  reg [3:0] outBitsAddr0; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0; // @[RingNetworkV3.scala 73:34]
  reg  inReady0; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1; // @[RingNetworkV3.scala 93:34]
  reg  inReady1; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_1; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_1; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_1; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_1; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_1; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_1; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_2; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_2; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_2; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_2; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_2; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_2; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_3; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_3; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_3; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_3; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_3; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_3; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_4; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_4; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_4; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_4; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_4; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_4; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_5; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_5; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_5; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_5; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_5; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_5; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_6; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_6; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_6; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_6; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_6; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_6; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_7; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_7; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_7; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_7; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_7; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_7; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_8; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_8; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_8; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_8; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_8; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_8; // @[RingNetworkV3.scala 95:34]
  reg [3:0] outBitsAddr0_9; // @[RingNetworkV3.scala 72:34]
  reg [4:0] outBitsData0_9; // @[RingNetworkV3.scala 73:34]
  reg  inReady0_9; // @[RingNetworkV3.scala 75:34]
  reg [3:0] outBitsAddr1_9; // @[RingNetworkV3.scala 92:34]
  reg [4:0] outBitsData1_9; // @[RingNetworkV3.scala 93:34]
  reg  inReady1_9; // @[RingNetworkV3.scala 95:34]
  RingRouterV3 routers_0 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_0_clock),
    .io_ports_0_in_ready(routers_0_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_0_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_0_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_0_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_0_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_0_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_0_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_0_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_0_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_0_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_0_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_0_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_0_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_0_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_0_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_0_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_0_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_0_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_0_io_ports_2_out_bits_data)
  );
  RingRouterV3_1 routers_1 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_1_clock),
    .io_ports_0_in_ready(routers_1_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_1_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_1_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_1_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_1_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_1_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_1_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_1_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_1_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_1_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_1_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_1_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_1_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_1_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_1_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_1_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_1_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_1_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_1_io_ports_2_out_bits_data)
  );
  RingRouterV3_2 routers_2 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_2_clock),
    .io_ports_0_in_ready(routers_2_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_2_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_2_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_2_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_2_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_2_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_2_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_2_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_2_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_2_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_2_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_2_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_2_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_2_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_2_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_2_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_2_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_2_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_2_io_ports_2_out_bits_data)
  );
  RingRouterV3_3 routers_3 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_3_clock),
    .io_ports_0_in_ready(routers_3_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_3_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_3_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_3_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_3_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_3_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_3_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_3_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_3_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_3_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_3_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_3_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_3_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_3_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_3_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_3_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_3_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_3_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_3_io_ports_2_out_bits_data)
  );
  RingRouterV3_4 routers_4 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_4_clock),
    .io_ports_0_in_ready(routers_4_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_4_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_4_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_4_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_4_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_4_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_4_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_4_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_4_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_4_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_4_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_4_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_4_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_4_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_4_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_4_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_4_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_4_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_4_io_ports_2_out_bits_data)
  );
  RingRouterV3_5 routers_5 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_5_clock),
    .io_ports_0_in_ready(routers_5_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_5_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_5_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_5_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_5_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_5_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_5_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_5_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_5_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_5_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_5_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_5_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_5_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_5_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_5_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_5_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_5_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_5_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_5_io_ports_2_out_bits_data)
  );
  RingRouterV3_6 routers_6 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_6_clock),
    .io_ports_0_in_ready(routers_6_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_6_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_6_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_6_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_6_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_6_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_6_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_6_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_6_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_6_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_6_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_6_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_6_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_6_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_6_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_6_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_6_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_6_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_6_io_ports_2_out_bits_data)
  );
  RingRouterV3_7 routers_7 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_7_clock),
    .io_ports_0_in_ready(routers_7_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_7_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_7_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_7_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_7_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_7_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_7_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_7_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_7_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_7_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_7_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_7_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_7_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_7_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_7_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_7_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_7_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_7_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_7_io_ports_2_out_bits_data)
  );
  RingRouterV3_8 routers_8 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_8_clock),
    .io_ports_0_in_ready(routers_8_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_8_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_8_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_8_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_8_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_8_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_8_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_8_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_8_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_8_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_8_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_8_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_8_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_8_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_8_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_8_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_8_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_8_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_8_io_ports_2_out_bits_data)
  );
  RingRouterV3_9 routers_9 ( // @[RingNetworkV3.scala 66:77]
    .clock(routers_9_clock),
    .io_ports_0_in_ready(routers_9_io_ports_0_in_ready),
    .io_ports_0_in_bits_addr(routers_9_io_ports_0_in_bits_addr),
    .io_ports_0_in_bits_data(routers_9_io_ports_0_in_bits_data),
    .io_ports_0_out_ready(routers_9_io_ports_0_out_ready),
    .io_ports_0_out_bits_addr(routers_9_io_ports_0_out_bits_addr),
    .io_ports_0_out_bits_data(routers_9_io_ports_0_out_bits_data),
    .io_ports_1_in_ready(routers_9_io_ports_1_in_ready),
    .io_ports_1_in_bits_addr(routers_9_io_ports_1_in_bits_addr),
    .io_ports_1_in_bits_data(routers_9_io_ports_1_in_bits_data),
    .io_ports_1_out_ready(routers_9_io_ports_1_out_ready),
    .io_ports_1_out_bits_addr(routers_9_io_ports_1_out_bits_addr),
    .io_ports_1_out_bits_data(routers_9_io_ports_1_out_bits_data),
    .io_ports_2_in_ready(routers_9_io_ports_2_in_ready),
    .io_ports_2_in_valid(routers_9_io_ports_2_in_valid),
    .io_ports_2_in_bits_addr(routers_9_io_ports_2_in_bits_addr),
    .io_ports_2_in_bits_data(routers_9_io_ports_2_in_bits_data),
    .io_ports_2_out_ready(routers_9_io_ports_2_out_ready),
    .io_ports_2_out_bits_addr(routers_9_io_ports_2_out_bits_addr),
    .io_ports_2_out_bits_data(routers_9_io_ports_2_out_bits_data)
  );
  assign io_ports_0_in_ready = routers_0_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_0_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_0_out_bits_addr = routers_0_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_0_out_bits_data = routers_0_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_1_in_ready = routers_1_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_1_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_1_out_bits_addr = routers_1_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_1_out_bits_data = routers_1_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_2_in_ready = routers_2_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_2_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_2_out_bits_addr = routers_2_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_2_out_bits_data = routers_2_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_3_in_ready = routers_3_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_3_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_3_out_bits_addr = routers_3_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_3_out_bits_data = routers_3_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_4_in_ready = routers_4_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_4_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_4_out_bits_addr = routers_4_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_4_out_bits_data = routers_4_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_5_in_ready = routers_5_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_5_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_5_out_bits_addr = routers_5_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_5_out_bits_data = routers_5_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_6_in_ready = routers_6_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_6_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_6_out_bits_addr = routers_6_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_6_out_bits_data = routers_6_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_7_in_ready = routers_7_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_7_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_7_out_bits_addr = routers_7_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_7_out_bits_data = routers_7_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_8_in_ready = routers_8_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_8_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_8_out_bits_addr = routers_8_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_8_out_bits_data = routers_8_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign io_ports_9_in_ready = routers_9_io_ports_2_in_ready; // @[RingNetworkV3.scala 114:47]
  assign io_ports_9_out_valid = 1'h1; // @[RingNetworkV3.scala 114:47]
  assign io_ports_9_out_bits_addr = routers_9_io_ports_2_out_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign io_ports_9_out_bits_data = routers_9_io_ports_2_out_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_0_clock = clock;
  assign routers_0_io_ports_0_in_bits_addr = outBitsAddr1_1; // @[RingNetworkV3.scala 106:37]
  assign routers_0_io_ports_0_in_bits_data = outBitsData1_1; // @[RingNetworkV3.scala 107:37]
  assign routers_0_io_ports_0_out_ready = inReady1_1; // @[RingNetworkV3.scala 103:34]
  assign routers_0_io_ports_1_in_bits_addr = outBitsAddr0_1; // @[RingNetworkV3.scala 86:37]
  assign routers_0_io_ports_1_in_bits_data = outBitsData0_1; // @[RingNetworkV3.scala 87:37]
  assign routers_0_io_ports_1_out_ready = inReady0_1; // @[RingNetworkV3.scala 83:34]
  assign routers_0_io_ports_2_in_valid = io_ports_0_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_0_io_ports_2_in_bits_addr = io_ports_0_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_0_io_ports_2_in_bits_data = io_ports_0_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_0_io_ports_2_out_ready = io_ports_0_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_1_clock = clock;
  assign routers_1_io_ports_0_in_bits_addr = outBitsAddr1_2; // @[RingNetworkV3.scala 106:37]
  assign routers_1_io_ports_0_in_bits_data = outBitsData1_2; // @[RingNetworkV3.scala 107:37]
  assign routers_1_io_ports_0_out_ready = inReady1_2; // @[RingNetworkV3.scala 103:34]
  assign routers_1_io_ports_1_in_bits_addr = outBitsAddr0_2; // @[RingNetworkV3.scala 86:37]
  assign routers_1_io_ports_1_in_bits_data = outBitsData0_2; // @[RingNetworkV3.scala 87:37]
  assign routers_1_io_ports_1_out_ready = inReady0_2; // @[RingNetworkV3.scala 83:34]
  assign routers_1_io_ports_2_in_valid = io_ports_1_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_1_io_ports_2_in_bits_addr = io_ports_1_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_1_io_ports_2_in_bits_data = io_ports_1_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_1_io_ports_2_out_ready = io_ports_1_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_2_clock = clock;
  assign routers_2_io_ports_0_in_bits_addr = outBitsAddr1_3; // @[RingNetworkV3.scala 106:37]
  assign routers_2_io_ports_0_in_bits_data = outBitsData1_3; // @[RingNetworkV3.scala 107:37]
  assign routers_2_io_ports_0_out_ready = inReady1_3; // @[RingNetworkV3.scala 103:34]
  assign routers_2_io_ports_1_in_bits_addr = outBitsAddr0_3; // @[RingNetworkV3.scala 86:37]
  assign routers_2_io_ports_1_in_bits_data = outBitsData0_3; // @[RingNetworkV3.scala 87:37]
  assign routers_2_io_ports_1_out_ready = inReady0_3; // @[RingNetworkV3.scala 83:34]
  assign routers_2_io_ports_2_in_valid = io_ports_2_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_2_io_ports_2_in_bits_addr = io_ports_2_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_2_io_ports_2_in_bits_data = io_ports_2_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_2_io_ports_2_out_ready = io_ports_2_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_3_clock = clock;
  assign routers_3_io_ports_0_in_bits_addr = outBitsAddr1_4; // @[RingNetworkV3.scala 106:37]
  assign routers_3_io_ports_0_in_bits_data = outBitsData1_4; // @[RingNetworkV3.scala 107:37]
  assign routers_3_io_ports_0_out_ready = inReady1_4; // @[RingNetworkV3.scala 103:34]
  assign routers_3_io_ports_1_in_bits_addr = outBitsAddr0_4; // @[RingNetworkV3.scala 86:37]
  assign routers_3_io_ports_1_in_bits_data = outBitsData0_4; // @[RingNetworkV3.scala 87:37]
  assign routers_3_io_ports_1_out_ready = inReady0_4; // @[RingNetworkV3.scala 83:34]
  assign routers_3_io_ports_2_in_valid = io_ports_3_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_3_io_ports_2_in_bits_addr = io_ports_3_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_3_io_ports_2_in_bits_data = io_ports_3_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_3_io_ports_2_out_ready = io_ports_3_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_4_clock = clock;
  assign routers_4_io_ports_0_in_bits_addr = outBitsAddr1_5; // @[RingNetworkV3.scala 106:37]
  assign routers_4_io_ports_0_in_bits_data = outBitsData1_5; // @[RingNetworkV3.scala 107:37]
  assign routers_4_io_ports_0_out_ready = inReady1_5; // @[RingNetworkV3.scala 103:34]
  assign routers_4_io_ports_1_in_bits_addr = outBitsAddr0_5; // @[RingNetworkV3.scala 86:37]
  assign routers_4_io_ports_1_in_bits_data = outBitsData0_5; // @[RingNetworkV3.scala 87:37]
  assign routers_4_io_ports_1_out_ready = inReady0_5; // @[RingNetworkV3.scala 83:34]
  assign routers_4_io_ports_2_in_valid = io_ports_4_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_4_io_ports_2_in_bits_addr = io_ports_4_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_4_io_ports_2_in_bits_data = io_ports_4_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_4_io_ports_2_out_ready = io_ports_4_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_5_clock = clock;
  assign routers_5_io_ports_0_in_bits_addr = outBitsAddr1_6; // @[RingNetworkV3.scala 106:37]
  assign routers_5_io_ports_0_in_bits_data = outBitsData1_6; // @[RingNetworkV3.scala 107:37]
  assign routers_5_io_ports_0_out_ready = inReady1_6; // @[RingNetworkV3.scala 103:34]
  assign routers_5_io_ports_1_in_bits_addr = outBitsAddr0_6; // @[RingNetworkV3.scala 86:37]
  assign routers_5_io_ports_1_in_bits_data = outBitsData0_6; // @[RingNetworkV3.scala 87:37]
  assign routers_5_io_ports_1_out_ready = inReady0_6; // @[RingNetworkV3.scala 83:34]
  assign routers_5_io_ports_2_in_valid = io_ports_5_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_5_io_ports_2_in_bits_addr = io_ports_5_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_5_io_ports_2_in_bits_data = io_ports_5_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_5_io_ports_2_out_ready = io_ports_5_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_6_clock = clock;
  assign routers_6_io_ports_0_in_bits_addr = outBitsAddr1_7; // @[RingNetworkV3.scala 106:37]
  assign routers_6_io_ports_0_in_bits_data = outBitsData1_7; // @[RingNetworkV3.scala 107:37]
  assign routers_6_io_ports_0_out_ready = inReady1_7; // @[RingNetworkV3.scala 103:34]
  assign routers_6_io_ports_1_in_bits_addr = outBitsAddr0_7; // @[RingNetworkV3.scala 86:37]
  assign routers_6_io_ports_1_in_bits_data = outBitsData0_7; // @[RingNetworkV3.scala 87:37]
  assign routers_6_io_ports_1_out_ready = inReady0_7; // @[RingNetworkV3.scala 83:34]
  assign routers_6_io_ports_2_in_valid = io_ports_6_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_6_io_ports_2_in_bits_addr = io_ports_6_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_6_io_ports_2_in_bits_data = io_ports_6_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_6_io_ports_2_out_ready = io_ports_6_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_7_clock = clock;
  assign routers_7_io_ports_0_in_bits_addr = outBitsAddr1_8; // @[RingNetworkV3.scala 106:37]
  assign routers_7_io_ports_0_in_bits_data = outBitsData1_8; // @[RingNetworkV3.scala 107:37]
  assign routers_7_io_ports_0_out_ready = inReady1_8; // @[RingNetworkV3.scala 103:34]
  assign routers_7_io_ports_1_in_bits_addr = outBitsAddr0_8; // @[RingNetworkV3.scala 86:37]
  assign routers_7_io_ports_1_in_bits_data = outBitsData0_8; // @[RingNetworkV3.scala 87:37]
  assign routers_7_io_ports_1_out_ready = inReady0_8; // @[RingNetworkV3.scala 83:34]
  assign routers_7_io_ports_2_in_valid = io_ports_7_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_7_io_ports_2_in_bits_addr = io_ports_7_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_7_io_ports_2_in_bits_data = io_ports_7_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_7_io_ports_2_out_ready = io_ports_7_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_8_clock = clock;
  assign routers_8_io_ports_0_in_bits_addr = outBitsAddr1_9; // @[RingNetworkV3.scala 106:37]
  assign routers_8_io_ports_0_in_bits_data = outBitsData1_9; // @[RingNetworkV3.scala 107:37]
  assign routers_8_io_ports_0_out_ready = inReady1_9; // @[RingNetworkV3.scala 103:34]
  assign routers_8_io_ports_1_in_bits_addr = outBitsAddr0_9; // @[RingNetworkV3.scala 86:37]
  assign routers_8_io_ports_1_in_bits_data = outBitsData0_9; // @[RingNetworkV3.scala 87:37]
  assign routers_8_io_ports_1_out_ready = inReady0_9; // @[RingNetworkV3.scala 83:34]
  assign routers_8_io_ports_2_in_valid = io_ports_8_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_8_io_ports_2_in_bits_addr = io_ports_8_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_8_io_ports_2_in_bits_data = io_ports_8_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_8_io_ports_2_out_ready = io_ports_8_out_ready; // @[RingNetworkV3.scala 114:47]
  assign routers_9_clock = clock;
  assign routers_9_io_ports_0_in_bits_addr = outBitsAddr1; // @[RingNetworkV3.scala 106:37]
  assign routers_9_io_ports_0_in_bits_data = outBitsData1; // @[RingNetworkV3.scala 107:37]
  assign routers_9_io_ports_0_out_ready = inReady1; // @[RingNetworkV3.scala 103:34]
  assign routers_9_io_ports_1_in_bits_addr = outBitsAddr0; // @[RingNetworkV3.scala 86:37]
  assign routers_9_io_ports_1_in_bits_data = outBitsData0; // @[RingNetworkV3.scala 87:37]
  assign routers_9_io_ports_1_out_ready = inReady0; // @[RingNetworkV3.scala 83:34]
  assign routers_9_io_ports_2_in_valid = io_ports_9_in_valid; // @[RingNetworkV3.scala 114:47]
  assign routers_9_io_ports_2_in_bits_addr = io_ports_9_in_bits_addr; // @[RingNetworkV3.scala 114:47]
  assign routers_9_io_ports_2_in_bits_data = io_ports_9_in_bits_data; // @[RingNetworkV3.scala 114:47]
  assign routers_9_io_ports_2_out_ready = io_ports_9_out_ready; // @[RingNetworkV3.scala 114:47]
  always @(posedge clock) begin
    outBitsAddr0 <= routers_0_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0 <= routers_0_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0 <= routers_0_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1 <= routers_0_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1 <= routers_0_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1 <= routers_0_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_1 <= routers_1_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_1 <= routers_1_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_1 <= routers_1_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_1 <= routers_1_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_1 <= routers_1_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_1 <= routers_1_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_2 <= routers_2_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_2 <= routers_2_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_2 <= routers_2_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_2 <= routers_2_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_2 <= routers_2_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_2 <= routers_2_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_3 <= routers_3_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_3 <= routers_3_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_3 <= routers_3_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_3 <= routers_3_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_3 <= routers_3_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_3 <= routers_3_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_4 <= routers_4_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_4 <= routers_4_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_4 <= routers_4_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_4 <= routers_4_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_4 <= routers_4_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_4 <= routers_4_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_5 <= routers_5_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_5 <= routers_5_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_5 <= routers_5_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_5 <= routers_5_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_5 <= routers_5_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_5 <= routers_5_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_6 <= routers_6_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_6 <= routers_6_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_6 <= routers_6_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_6 <= routers_6_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_6 <= routers_6_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_6 <= routers_6_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_7 <= routers_7_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_7 <= routers_7_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_7 <= routers_7_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_7 <= routers_7_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_7 <= routers_7_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_7 <= routers_7_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_8 <= routers_8_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_8 <= routers_8_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_8 <= routers_8_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_8 <= routers_8_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_8 <= routers_8_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_8 <= routers_8_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
    outBitsAddr0_9 <= routers_9_io_ports_0_out_bits_addr; // @[RingNetworkV3.scala 72:34]
    outBitsData0_9 <= routers_9_io_ports_0_out_bits_data; // @[RingNetworkV3.scala 73:34]
    inReady0_9 <= routers_9_io_ports_0_in_ready; // @[RingNetworkV3.scala 75:34]
    outBitsAddr1_9 <= routers_9_io_ports_1_out_bits_addr; // @[RingNetworkV3.scala 92:34]
    outBitsData1_9 <= routers_9_io_ports_1_out_bits_data; // @[RingNetworkV3.scala 93:34]
    inReady1_9 <= routers_9_io_ports_1_in_ready; // @[RingNetworkV3.scala 95:34]
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
  outBitsAddr0 = _RAND_0[3:0];
  _RAND_1 = {1{`RANDOM}};
  outBitsData0 = _RAND_1[4:0];
  _RAND_2 = {1{`RANDOM}};
  inReady0 = _RAND_2[0:0];
  _RAND_3 = {1{`RANDOM}};
  outBitsAddr1 = _RAND_3[3:0];
  _RAND_4 = {1{`RANDOM}};
  outBitsData1 = _RAND_4[4:0];
  _RAND_5 = {1{`RANDOM}};
  inReady1 = _RAND_5[0:0];
  _RAND_6 = {1{`RANDOM}};
  outBitsAddr0_1 = _RAND_6[3:0];
  _RAND_7 = {1{`RANDOM}};
  outBitsData0_1 = _RAND_7[4:0];
  _RAND_8 = {1{`RANDOM}};
  inReady0_1 = _RAND_8[0:0];
  _RAND_9 = {1{`RANDOM}};
  outBitsAddr1_1 = _RAND_9[3:0];
  _RAND_10 = {1{`RANDOM}};
  outBitsData1_1 = _RAND_10[4:0];
  _RAND_11 = {1{`RANDOM}};
  inReady1_1 = _RAND_11[0:0];
  _RAND_12 = {1{`RANDOM}};
  outBitsAddr0_2 = _RAND_12[3:0];
  _RAND_13 = {1{`RANDOM}};
  outBitsData0_2 = _RAND_13[4:0];
  _RAND_14 = {1{`RANDOM}};
  inReady0_2 = _RAND_14[0:0];
  _RAND_15 = {1{`RANDOM}};
  outBitsAddr1_2 = _RAND_15[3:0];
  _RAND_16 = {1{`RANDOM}};
  outBitsData1_2 = _RAND_16[4:0];
  _RAND_17 = {1{`RANDOM}};
  inReady1_2 = _RAND_17[0:0];
  _RAND_18 = {1{`RANDOM}};
  outBitsAddr0_3 = _RAND_18[3:0];
  _RAND_19 = {1{`RANDOM}};
  outBitsData0_3 = _RAND_19[4:0];
  _RAND_20 = {1{`RANDOM}};
  inReady0_3 = _RAND_20[0:0];
  _RAND_21 = {1{`RANDOM}};
  outBitsAddr1_3 = _RAND_21[3:0];
  _RAND_22 = {1{`RANDOM}};
  outBitsData1_3 = _RAND_22[4:0];
  _RAND_23 = {1{`RANDOM}};
  inReady1_3 = _RAND_23[0:0];
  _RAND_24 = {1{`RANDOM}};
  outBitsAddr0_4 = _RAND_24[3:0];
  _RAND_25 = {1{`RANDOM}};
  outBitsData0_4 = _RAND_25[4:0];
  _RAND_26 = {1{`RANDOM}};
  inReady0_4 = _RAND_26[0:0];
  _RAND_27 = {1{`RANDOM}};
  outBitsAddr1_4 = _RAND_27[3:0];
  _RAND_28 = {1{`RANDOM}};
  outBitsData1_4 = _RAND_28[4:0];
  _RAND_29 = {1{`RANDOM}};
  inReady1_4 = _RAND_29[0:0];
  _RAND_30 = {1{`RANDOM}};
  outBitsAddr0_5 = _RAND_30[3:0];
  _RAND_31 = {1{`RANDOM}};
  outBitsData0_5 = _RAND_31[4:0];
  _RAND_32 = {1{`RANDOM}};
  inReady0_5 = _RAND_32[0:0];
  _RAND_33 = {1{`RANDOM}};
  outBitsAddr1_5 = _RAND_33[3:0];
  _RAND_34 = {1{`RANDOM}};
  outBitsData1_5 = _RAND_34[4:0];
  _RAND_35 = {1{`RANDOM}};
  inReady1_5 = _RAND_35[0:0];
  _RAND_36 = {1{`RANDOM}};
  outBitsAddr0_6 = _RAND_36[3:0];
  _RAND_37 = {1{`RANDOM}};
  outBitsData0_6 = _RAND_37[4:0];
  _RAND_38 = {1{`RANDOM}};
  inReady0_6 = _RAND_38[0:0];
  _RAND_39 = {1{`RANDOM}};
  outBitsAddr1_6 = _RAND_39[3:0];
  _RAND_40 = {1{`RANDOM}};
  outBitsData1_6 = _RAND_40[4:0];
  _RAND_41 = {1{`RANDOM}};
  inReady1_6 = _RAND_41[0:0];
  _RAND_42 = {1{`RANDOM}};
  outBitsAddr0_7 = _RAND_42[3:0];
  _RAND_43 = {1{`RANDOM}};
  outBitsData0_7 = _RAND_43[4:0];
  _RAND_44 = {1{`RANDOM}};
  inReady0_7 = _RAND_44[0:0];
  _RAND_45 = {1{`RANDOM}};
  outBitsAddr1_7 = _RAND_45[3:0];
  _RAND_46 = {1{`RANDOM}};
  outBitsData1_7 = _RAND_46[4:0];
  _RAND_47 = {1{`RANDOM}};
  inReady1_7 = _RAND_47[0:0];
  _RAND_48 = {1{`RANDOM}};
  outBitsAddr0_8 = _RAND_48[3:0];
  _RAND_49 = {1{`RANDOM}};
  outBitsData0_8 = _RAND_49[4:0];
  _RAND_50 = {1{`RANDOM}};
  inReady0_8 = _RAND_50[0:0];
  _RAND_51 = {1{`RANDOM}};
  outBitsAddr1_8 = _RAND_51[3:0];
  _RAND_52 = {1{`RANDOM}};
  outBitsData1_8 = _RAND_52[4:0];
  _RAND_53 = {1{`RANDOM}};
  inReady1_8 = _RAND_53[0:0];
  _RAND_54 = {1{`RANDOM}};
  outBitsAddr0_9 = _RAND_54[3:0];
  _RAND_55 = {1{`RANDOM}};
  outBitsData0_9 = _RAND_55[4:0];
  _RAND_56 = {1{`RANDOM}};
  inReady0_9 = _RAND_56[0:0];
  _RAND_57 = {1{`RANDOM}};
  outBitsAddr1_9 = _RAND_57[3:0];
  _RAND_58 = {1{`RANDOM}};
  outBitsData1_9 = _RAND_58[4:0];
  _RAND_59 = {1{`RANDOM}};
  inReady1_9 = _RAND_59[0:0];
`endif // RANDOMIZE_REG_INIT
  `endif // RANDOMIZE
end // initial
`ifdef FIRRTL_AFTER_INITIAL
`FIRRTL_AFTER_INITIAL
`endif
`endif // SYNTHESIS
endmodule
```
