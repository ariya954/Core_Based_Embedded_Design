module Slave(input CS, SCLK, SDI, output SDO, output reg [6 : 0]Red_Leds, output reg [6 : 0]Blue_Leds);

reg [7 : 0] Register [1 : 0];
reg input_sample, address;
reg number_of_got_samples;

always @(negedge SCLK) begin
	if(~CS) begin
		input_sample = SDI;
		address = (number_of_got_samples == 0) ? input_sample : address;
		number_of_got_samples = 1;
	end
end

always @(posedge SCLK) begin
	if(~CS) begin
		Register[address] = {input_sample, Register[address][7 : 1]};
	end
end

always @(negedge CS) begin
	Register[0] = 8'b0;
	Register[1] = 8'b0;
	number_of_got_samples = 0;
end

always @(posedge CS) begin
	Red_Leds = Register[0][7 : 1];
	Blue_Leds = Register[1][7 : 1];
end

endmodule