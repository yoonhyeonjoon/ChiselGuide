module RRArbiter(
  input         clock,
  output        io_in_0_ready,
  input         io_in_0_valid,
  input  [2:0]  io_in_0_bits_addr,
  input  [11:0] io_in_0_bits_data,
  output        io_in_1_ready,
  input         io_in_1_valid,
  input  [2:0]  io_in_1_bits_addr,
  input  [11:0] io_in_1_bits_data,
  output        io_in_2_ready,
  input         io_in_2_valid,
  input  [2:0]  io_in_2_bits_addr,
  input  [11:0] io_in_2_bits_data,
  input         io_out_ready,
  output        io_out_valid,
  output [2:0]  io_out_bits_addr,
  output [11:0] io_out_bits_data,
  output [1:0]  io_chosen
);
`ifdef RANDOMIZE_REG_INIT
  reg [31:0] _RAND_0;
`endif // RANDOMIZE_REG_INIT
  wire  _GEN_1 = 2'h1 == io_chosen ? io_in_1_valid : io_in_0_valid; // @[Arbiter.scala 56:{16,16}]
  wire [2:0] _GEN_4 = 2'h1 == io_chosen ? io_in_1_bits_addr : io_in_0_bits_addr; // @[Arbiter.scala 57:{15,15}]
  wire [11:0] _GEN_7 = 2'h1 == io_chosen ? io_in_1_bits_data : io_in_0_bits_data; // @[Arbiter.scala 57:{15,15}]
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
  wire [1:0] _GEN_10 = io_in_1_valid ? 2'h1 : 2'h2; // @[Arbiter.scala 92:{26,35}]
  wire [1:0] _GEN_11 = io_in_0_valid ? 2'h0 : _GEN_10; // @[Arbiter.scala 92:{26,35}]
  wire [1:0] _GEN_12 = validMask_2 ? 2'h2 : _GEN_11; // @[Arbiter.scala 94:{24,33}]
  assign io_in_0_ready = ctrl_3 & io_out_ready; // @[Arbiter.scala 75:21]
  assign io_in_1_ready = _T_3 & io_out_ready; // @[Arbiter.scala 75:21]
  assign io_in_2_ready = _T_5 & io_out_ready; // @[Arbiter.scala 75:21]
  assign io_out_valid = 2'h2 == io_chosen ? io_in_2_valid : _GEN_1; // @[Arbiter.scala 56:{16,16}]
  assign io_out_bits_addr = 2'h2 == io_chosen ? io_in_2_bits_addr : _GEN_4; // @[Arbiter.scala 57:{15,15}]
  assign io_out_bits_data = 2'h2 == io_chosen ? io_in_2_bits_data : _GEN_7; // @[Arbiter.scala 57:{15,15}]
  assign io_chosen = validMask_1 ? 2'h1 : _GEN_12; // @[Arbiter.scala 94:{24,33}]
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
module XBarV1(
  input         clock,
  input         reset,
  output        io_in_0_ready,
  input         io_in_0_valid,
  input  [2:0]  io_in_0_bits_addr,
  input  [11:0] io_in_0_bits_data,
  output        io_in_1_ready,
  input         io_in_1_valid,
  input  [2:0]  io_in_1_bits_addr,
  input  [11:0] io_in_1_bits_data,
  output        io_in_2_ready,
  input         io_in_2_valid,
  input  [2:0]  io_in_2_bits_addr,
  input  [11:0] io_in_2_bits_data,
  input         io_out_0_ready,
  output        io_out_0_valid,
  output [2:0]  io_out_0_bits_addr,
  output [11:0] io_out_0_bits_data,
  input         io_out_1_ready,
  output        io_out_1_valid,
  output [2:0]  io_out_1_bits_addr,
  output [11:0] io_out_1_bits_data,
  input         io_out_2_ready,
  output        io_out_2_valid,
  output [2:0]  io_out_2_bits_addr,
  output [11:0] io_out_2_bits_data,
  input         io_out_3_ready,
  output        io_out_3_valid,
  output [2:0]  io_out_3_bits_addr,
  output [11:0] io_out_3_bits_data
);
  wire  arbs_0_clock; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_in_0_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_in_0_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_0_io_in_0_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_0_io_in_0_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_in_1_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_in_1_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_0_io_in_1_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_0_io_in_1_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_in_2_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_in_2_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_0_io_in_2_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_0_io_in_2_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_out_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_0_io_out_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_0_io_out_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_0_io_out_bits_data; // @[CrossBarV1.scala 22:65]
  wire [1:0] arbs_0_io_chosen; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_clock; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_in_0_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_in_0_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_1_io_in_0_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_1_io_in_0_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_in_1_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_in_1_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_1_io_in_1_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_1_io_in_1_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_in_2_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_in_2_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_1_io_in_2_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_1_io_in_2_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_out_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_1_io_out_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_1_io_out_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_1_io_out_bits_data; // @[CrossBarV1.scala 22:65]
  wire [1:0] arbs_1_io_chosen; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_clock; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_in_0_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_in_0_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_2_io_in_0_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_2_io_in_0_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_in_1_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_in_1_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_2_io_in_1_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_2_io_in_1_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_in_2_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_in_2_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_2_io_in_2_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_2_io_in_2_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_out_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_2_io_out_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_2_io_out_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_2_io_out_bits_data; // @[CrossBarV1.scala 22:65]
  wire [1:0] arbs_2_io_chosen; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_clock; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_in_0_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_in_0_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_3_io_in_0_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_3_io_in_0_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_in_1_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_in_1_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_3_io_in_1_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_3_io_in_1_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_in_2_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_in_2_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_3_io_in_2_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_3_io_in_2_bits_data; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_out_ready; // @[CrossBarV1.scala 22:65]
  wire  arbs_3_io_out_valid; // @[CrossBarV1.scala 22:65]
  wire [2:0] arbs_3_io_out_bits_addr; // @[CrossBarV1.scala 22:65]
  wire [11:0] arbs_3_io_out_bits_data; // @[CrossBarV1.scala 22:65]
  wire [1:0] arbs_3_io_chosen; // @[CrossBarV1.scala 22:65]
  RRArbiter arbs_0 ( // @[CrossBarV1.scala 22:65]
    .clock(arbs_0_clock),
    .io_in_0_ready(arbs_0_io_in_0_ready),
    .io_in_0_valid(arbs_0_io_in_0_valid),
    .io_in_0_bits_addr(arbs_0_io_in_0_bits_addr),
    .io_in_0_bits_data(arbs_0_io_in_0_bits_data),
    .io_in_1_ready(arbs_0_io_in_1_ready),
    .io_in_1_valid(arbs_0_io_in_1_valid),
    .io_in_1_bits_addr(arbs_0_io_in_1_bits_addr),
    .io_in_1_bits_data(arbs_0_io_in_1_bits_data),
    .io_in_2_ready(arbs_0_io_in_2_ready),
    .io_in_2_valid(arbs_0_io_in_2_valid),
    .io_in_2_bits_addr(arbs_0_io_in_2_bits_addr),
    .io_in_2_bits_data(arbs_0_io_in_2_bits_data),
    .io_out_ready(arbs_0_io_out_ready),
    .io_out_valid(arbs_0_io_out_valid),
    .io_out_bits_addr(arbs_0_io_out_bits_addr),
    .io_out_bits_data(arbs_0_io_out_bits_data),
    .io_chosen(arbs_0_io_chosen)
  );
  RRArbiter arbs_1 ( // @[CrossBarV1.scala 22:65]
    .clock(arbs_1_clock),
    .io_in_0_ready(arbs_1_io_in_0_ready),
    .io_in_0_valid(arbs_1_io_in_0_valid),
    .io_in_0_bits_addr(arbs_1_io_in_0_bits_addr),
    .io_in_0_bits_data(arbs_1_io_in_0_bits_data),
    .io_in_1_ready(arbs_1_io_in_1_ready),
    .io_in_1_valid(arbs_1_io_in_1_valid),
    .io_in_1_bits_addr(arbs_1_io_in_1_bits_addr),
    .io_in_1_bits_data(arbs_1_io_in_1_bits_data),
    .io_in_2_ready(arbs_1_io_in_2_ready),
    .io_in_2_valid(arbs_1_io_in_2_valid),
    .io_in_2_bits_addr(arbs_1_io_in_2_bits_addr),
    .io_in_2_bits_data(arbs_1_io_in_2_bits_data),
    .io_out_ready(arbs_1_io_out_ready),
    .io_out_valid(arbs_1_io_out_valid),
    .io_out_bits_addr(arbs_1_io_out_bits_addr),
    .io_out_bits_data(arbs_1_io_out_bits_data),
    .io_chosen(arbs_1_io_chosen)
  );
  RRArbiter arbs_2 ( // @[CrossBarV1.scala 22:65]
    .clock(arbs_2_clock),
    .io_in_0_ready(arbs_2_io_in_0_ready),
    .io_in_0_valid(arbs_2_io_in_0_valid),
    .io_in_0_bits_addr(arbs_2_io_in_0_bits_addr),
    .io_in_0_bits_data(arbs_2_io_in_0_bits_data),
    .io_in_1_ready(arbs_2_io_in_1_ready),
    .io_in_1_valid(arbs_2_io_in_1_valid),
    .io_in_1_bits_addr(arbs_2_io_in_1_bits_addr),
    .io_in_1_bits_data(arbs_2_io_in_1_bits_data),
    .io_in_2_ready(arbs_2_io_in_2_ready),
    .io_in_2_valid(arbs_2_io_in_2_valid),
    .io_in_2_bits_addr(arbs_2_io_in_2_bits_addr),
    .io_in_2_bits_data(arbs_2_io_in_2_bits_data),
    .io_out_ready(arbs_2_io_out_ready),
    .io_out_valid(arbs_2_io_out_valid),
    .io_out_bits_addr(arbs_2_io_out_bits_addr),
    .io_out_bits_data(arbs_2_io_out_bits_data),
    .io_chosen(arbs_2_io_chosen)
  );
  RRArbiter arbs_3 ( // @[CrossBarV1.scala 22:65]
    .clock(arbs_3_clock),
    .io_in_0_ready(arbs_3_io_in_0_ready),
    .io_in_0_valid(arbs_3_io_in_0_valid),
    .io_in_0_bits_addr(arbs_3_io_in_0_bits_addr),
    .io_in_0_bits_data(arbs_3_io_in_0_bits_data),
    .io_in_1_ready(arbs_3_io_in_1_ready),
    .io_in_1_valid(arbs_3_io_in_1_valid),
    .io_in_1_bits_addr(arbs_3_io_in_1_bits_addr),
    .io_in_1_bits_data(arbs_3_io_in_1_bits_data),
    .io_in_2_ready(arbs_3_io_in_2_ready),
    .io_in_2_valid(arbs_3_io_in_2_valid),
    .io_in_2_bits_addr(arbs_3_io_in_2_bits_addr),
    .io_in_2_bits_data(arbs_3_io_in_2_bits_data),
    .io_out_ready(arbs_3_io_out_ready),
    .io_out_valid(arbs_3_io_out_valid),
    .io_out_bits_addr(arbs_3_io_out_bits_addr),
    .io_out_bits_data(arbs_3_io_out_bits_data),
    .io_chosen(arbs_3_io_chosen)
  );
  assign io_in_0_ready = arbs_0_io_in_0_ready | arbs_1_io_in_0_ready | arbs_2_io_in_0_ready | arbs_3_io_in_0_ready; // @[CrossBarV1.scala 24:64]
  assign io_in_1_ready = arbs_0_io_in_1_ready | arbs_1_io_in_1_ready | arbs_2_io_in_1_ready | arbs_3_io_in_1_ready; // @[CrossBarV1.scala 24:64]
  assign io_in_2_ready = arbs_0_io_in_2_ready | arbs_1_io_in_2_ready | arbs_2_io_in_2_ready | arbs_3_io_in_2_ready; // @[CrossBarV1.scala 24:64]
  assign io_out_0_valid = arbs_0_io_out_valid; // @[CrossBarV1.scala 31:16]
  assign io_out_0_bits_addr = arbs_0_io_out_bits_addr; // @[CrossBarV1.scala 31:16]
  assign io_out_0_bits_data = arbs_0_io_out_bits_data; // @[CrossBarV1.scala 31:16]
  assign io_out_1_valid = arbs_1_io_out_valid; // @[CrossBarV1.scala 31:16]
  assign io_out_1_bits_addr = arbs_1_io_out_bits_addr; // @[CrossBarV1.scala 31:16]
  assign io_out_1_bits_data = arbs_1_io_out_bits_data; // @[CrossBarV1.scala 31:16]
  assign io_out_2_valid = arbs_2_io_out_valid; // @[CrossBarV1.scala 31:16]
  assign io_out_2_bits_addr = arbs_2_io_out_bits_addr; // @[CrossBarV1.scala 31:16]
  assign io_out_2_bits_data = arbs_2_io_out_bits_data; // @[CrossBarV1.scala 31:16]
  assign io_out_3_valid = arbs_3_io_out_valid; // @[CrossBarV1.scala 31:16]
  assign io_out_3_bits_addr = arbs_3_io_out_bits_addr; // @[CrossBarV1.scala 31:16]
  assign io_out_3_bits_data = arbs_3_io_out_bits_data; // @[CrossBarV1.scala 31:16]
  assign arbs_0_clock = clock;
  assign arbs_0_io_in_0_valid = io_in_0_valid & io_in_0_bits_addr == 3'h0; // @[CrossBarV1.scala 29:33]
  assign arbs_0_io_in_0_bits_addr = io_in_0_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_0_io_in_0_bits_data = io_in_0_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_0_io_in_1_valid = io_in_1_valid & io_in_1_bits_addr == 3'h0; // @[CrossBarV1.scala 29:33]
  assign arbs_0_io_in_1_bits_addr = io_in_1_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_0_io_in_1_bits_data = io_in_1_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_0_io_in_2_valid = io_in_2_valid & io_in_2_bits_addr == 3'h0; // @[CrossBarV1.scala 29:33]
  assign arbs_0_io_in_2_bits_addr = io_in_2_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_0_io_in_2_bits_data = io_in_2_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_0_io_out_ready = io_out_0_ready; // @[CrossBarV1.scala 31:16]
  assign arbs_1_clock = clock;
  assign arbs_1_io_in_0_valid = io_in_0_valid & io_in_0_bits_addr == 3'h1; // @[CrossBarV1.scala 29:33]
  assign arbs_1_io_in_0_bits_addr = io_in_0_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_1_io_in_0_bits_data = io_in_0_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_1_io_in_1_valid = io_in_1_valid & io_in_1_bits_addr == 3'h1; // @[CrossBarV1.scala 29:33]
  assign arbs_1_io_in_1_bits_addr = io_in_1_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_1_io_in_1_bits_data = io_in_1_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_1_io_in_2_valid = io_in_2_valid & io_in_2_bits_addr == 3'h1; // @[CrossBarV1.scala 29:33]
  assign arbs_1_io_in_2_bits_addr = io_in_2_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_1_io_in_2_bits_data = io_in_2_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_1_io_out_ready = io_out_1_ready; // @[CrossBarV1.scala 31:16]
  assign arbs_2_clock = clock;
  assign arbs_2_io_in_0_valid = io_in_0_valid & io_in_0_bits_addr == 3'h2; // @[CrossBarV1.scala 29:33]
  assign arbs_2_io_in_0_bits_addr = io_in_0_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_2_io_in_0_bits_data = io_in_0_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_2_io_in_1_valid = io_in_1_valid & io_in_1_bits_addr == 3'h2; // @[CrossBarV1.scala 29:33]
  assign arbs_2_io_in_1_bits_addr = io_in_1_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_2_io_in_1_bits_data = io_in_1_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_2_io_in_2_valid = io_in_2_valid & io_in_2_bits_addr == 3'h2; // @[CrossBarV1.scala 29:33]
  assign arbs_2_io_in_2_bits_addr = io_in_2_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_2_io_in_2_bits_data = io_in_2_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_2_io_out_ready = io_out_2_ready; // @[CrossBarV1.scala 31:16]
  assign arbs_3_clock = clock;
  assign arbs_3_io_in_0_valid = io_in_0_valid & io_in_0_bits_addr == 3'h3; // @[CrossBarV1.scala 29:33]
  assign arbs_3_io_in_0_bits_addr = io_in_0_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_3_io_in_0_bits_data = io_in_0_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_3_io_in_1_valid = io_in_1_valid & io_in_1_bits_addr == 3'h3; // @[CrossBarV1.scala 29:33]
  assign arbs_3_io_in_1_bits_addr = io_in_1_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_3_io_in_1_bits_data = io_in_1_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_3_io_in_2_valid = io_in_2_valid & io_in_2_bits_addr == 3'h3; // @[CrossBarV1.scala 29:33]
  assign arbs_3_io_in_2_bits_addr = io_in_2_bits_addr; // @[CrossBarV1.scala 28:18]
  assign arbs_3_io_in_2_bits_data = io_in_2_bits_data; // @[CrossBarV1.scala 28:18]
  assign arbs_3_io_out_ready = io_out_3_ready; // @[CrossBarV1.scala 31:16]
endmodule
