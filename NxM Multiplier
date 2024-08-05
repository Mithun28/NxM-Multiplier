module fa(
  output sum,
  output cout,
  input a, 
  input b, 
  input cin
);
  assign sum = a ^ b ^ cin;
  assign cout = (a & b) | (a & cin) | (b & cin);
endmodule

module multiplier_4_x_4(product, inp1, inp2);
  output [7:0] product;
  input [3:0] inp1;
  input [3:0] inp2;

  assign product[0] = (inp1[0] & inp2[0]);

  wire x1, x2, x3, x4, x5, x6, x7, x8, x9, x10, x11, x12, x13, x14, x15, x16, x17;

  fa HA1(product[1], x1, (inp1[1] & inp2[0]), (inp1[0] & inp2[1]), 1'b0);
  fa FA1(x2, x3, (inp1[1] & inp2[1]), (inp1[0] & inp2[2]), x1);
  fa FA2(x4, x5, (inp1[1] & inp2[2]), (inp1[0] & inp2[3]), x3);
  fa HA2(x6, x7, (inp1[1] & inp2[3]), x5, 1'b0);

  fa HA3(product[2], x15, x2, (inp1[2] & inp2[0]), 1'b0);
  fa FA5(x14, x16, x4, (inp1[2] & inp2[1]), x15);
  fa FA4(x13, x17, x6, (inp1[2] & inp2[2]), x16);
  fa FA3(x9, x8, x7, (inp1[2] & inp2[3]), x17);

  fa HA4(product[3], x12, x14, (inp1[3] & inp2[0]), 1'b0);
  fa FA8(product[4], x11, x13, (inp1[3] & inp2[1]), x12);
  fa FA7(product[5], x10, x9, (inp1[3] & inp2[2]), x11);
  fa FA6(product[6], product[7], x8, (inp1[3] & inp2[3]), x10);
endmodule

module main_project(
  input [3:0] n,
  output [3:0]m,
  output [7:0] p
);
	wire e;
	wire [3:0]mc;
	wire [3:0]m1,n1;
	assign e=(n[3]^n[2])|(((~n[3])&n[1])&n[0])|(n[3]&(~n[0]))|(n[2]&(~n[1]));
    	fa FA7(m[0],mc[0],n[0],1'b1, 1'b0);
	fa FA8(m[1],mc[1],n[1],1'b0, mc[0]);
	fa FA9(m[2],mc[2],n[2],1'b0, mc[1]);
	fa FA10(m[3],mc[3],n[3],1'b0, mc[2]);
	assign m1[0]=m[0]&e;
	assign m1[1]=m[1]&e;
	assign m1[2]=m[2]&e;
	assign m1[3]=m[3]&e;

	assign n1[0]=n[0]&e;
	assign n1[1]=n[1]&e;
	assign n1[2]=n[2]&e;
	assign n1[3]=n[3]&e;
        multiplier_4_x_4 uttt(
        .inp1(n1),
        .inp2(m1),
        .product(p));
endmodule

module maintb;
  	reg [3:0] n;
  	// Outputs
	wire [3:0]m;
  	wire [7:0]p;

  // Instantiate the Unit Under Test (UUT)
  main_project uut(.p(p),.m(m),.n(n));

  initial begin
    // Initialize Inputs
    n = 4'b0001;
    // Add stimulus here
    #100;
    n = 4'b1100;
    #100;
    n = 4'b1111;
    #100;
    n = 4'b1111;
  end
endmodule