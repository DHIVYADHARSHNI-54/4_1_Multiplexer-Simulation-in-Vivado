# SIMULATION AND IMPLEMENTATION OF 4:1 MULTIPLEXER

## AIM
To design and simulate a 4:1 Multiplexer (MUX) using Verilog HDL in four different modeling styles—Gate-Level, Data Flow, Behavioral, and Structural—and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital logic circuit and analyze their performance.

## APPARATUS REQUIRED
- **Vivado 2023.1**

## Procedure

1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** and give a name (e.g., `Mux4_to_1`).  
3. Add/create your Verilog files and testbench.  
4. Select an FPGA part (e.g., `xc7a35ticsg324-1L`).  
5. Run **Synthesis** to check for errors.  
6. Run **Simulation** → **Run Behavioral Simulation**.  
7. Observe the waveforms of inputs and outputs.  
8. Adjust simulation time if needed (e.g., 1000ns).  
9. Save the project and take screenshots of results.  
10. Close simulation.  

---

## Logic Diagram
![image](https://github.com/user-attachments/assets/d4ab4bc3-12b0-44dc-8edb-9d586d8ba856)

---

## Truth Table
![image](https://github.com/user-attachments/assets/c850506c-3f6e-4d6b-8574-939a914b2a5f)

---

## Verilog Code

### 4:1 MUX Gate-Level Implementation
```verilog
// Gate Level Modelling - Skeleton
`timescale 1ns / 1ps
module mux4_1(i,s,y);
input [3:0]i;
input [1:0]s;
output y;
wire [3:0]w;
and g1(w[0],i[0],~s[1],~s[0]);
and g2(w[1],i[1],~s[1],s[0]);
and g3(w[2],i[2],s[1],~s[0]);
and g4(w[3],i[3],s[1],s[0]);
or g5(y,w[0],w[1],w[2],w[3]);
endmodule

```
### 4:1 MUX Gate-Level Implementation- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mux4_1_tb;
reg [3:0]i;
reg [1:0]s;
wire y;
mux4_1 uut(i,s,y);
initial
begin
i=4'b1100;
s=2'b00;
#10;
$display("selection is %b%b,output:%b",s[1],s[2],y);
s=2'b10;
#10;
$display("selection is %b%b,output:%b",s[1],s[2],y);
s=2'b01;
#10;
$display("selection is %b%b,output:%b",s[1],s[2],y);
s=2'b11;
#10;
$display("selection is %b%b,output:%b",s[1],s[2],y);
$finish;
end
endmodule
```
## Simulated Output Gate Level Modelling

<img width="1919" height="1073" alt="image" src="https://github.com/user-attachments/assets/9efe260e-5db3-48b4-9535-c5b35e795ab7" />


---
### 4:1 MUX Data flow Modelling
```verilog
// Dataflow Modelling - Skeleton
module mux41(I,S,Y);
input [3:0]I;
input [1:0]S;
output Y;
wire [4:1]w;
assign w[1]=I[0] & (~S[1]) & (~S[0]);
assign w[2]=I[1] & (~S[1]) & S[0];
assign w[3]=I[2] & S[1] & (~S[0]);
assign w[4]=I[3] & S[1] & S[0];
assign Y=w[1] | w[2] | w[3] | w[4];
endmodule

```
### 4:1 MUX Data flow Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
module mun_4_1_tb;
reg[3:0]I;
reg[1:0]S;
wire Y;
mux_4_1 uut(I,S,Y);
initial
begin 
I=4'b1001;
S=2'b00;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
S=2'b01;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
S=2'b10;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
S=2'b11;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
$finish;
end
endmodule

```
## Simulated Output Dataflow Modelling

<img width="1919" height="1076" alt="image" src="https://github.com/user-attachments/assets/e57d5f43-85b5-4d89-a21e-52763c122714" />


---
### 4:1 MUX Behavioral Implementation
```verilog
module mux_4_1(I,S,Y);
input[3:0]I;
input[1:0]S;
output reg Y;
always @(I,S)
    begin   
        case(S)
        2'b00:Y=I[0];
        2'b01:Y=I[1];
        2'b10:Y=I[2];
        2'b11:Y=I[3];
        endcase
     end
endmodule
```
### 4:1 MUX Behavioral Modelling- Testbench
```verilog
// Testbench Skeleton
`timescale 1ns/1ps
`timescale 1ns/1ps
module mun_4_1_tb;
reg[3:0]I;
reg[1:0]S;
wire Y;
mux_4_1 uut(I,S,Y);
initial
begin 
I=4'b1001;
S=2'b00;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
S=2'b01;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
S=2'b10;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
S=2'b11;
#10;
$display("selection is %b %b , output:%b",S[1],S[0],Y);
$finish;
end
endmodule

```
## Simulated Output Behavioral Modelling

<img width="1919" height="1074" alt="image" src="https://github.com/user-attachments/assets/a3a26331-d461-48f2-a4fc-940ab943bf64" />


### 4:1 MUX Structural Implementation

![image](https://github.com/user-attachments/assets/eea81c2c-7dfa-43aa-9cea-1ab4ed54db6c)


```verilog
// 2:1 Multiplexer Module
module mux2to1 (
input  wire d0, d1,   
input  wire sel,      
output wire y        
);
assign y = sel ? d1 : d0;
endmodule
module mux4to1 (
input  wire d0, d1, d2, d3,
input  wire [1:0] sel,
output wire y               
);
wire y0, y1; 
mux2to1 m1 (.d0(d0), .d1(d1), .sel(sel[0]), .y(y0));
mux2to1 m2 (.d0(d2), .d1(d3), .sel(sel[0]), .y(y1));
mux2to1 m3 (.d0(y0), .d1(y1), .sel(sel[1]), .y(y));

endmodule


```
### Testbench Implementation
```verilog
`timescale 1ns / 1ps

module tb_mux4to1;
reg d0, d1, d2, d3;
reg [1:0] sel;
 wire y;
mux4to1 uut (.d0(d0), .d1(d1), .d2(d2), .d3(d3),.sel(sel), .y(y));
initial begin
$monitor("Time=%0t | sel=%b | d0=%b d1=%b d2=%b d3=%b | y=%b", $time, sel, d0, d1, d2, d3, y);
d0 = 0; d1 = 1; d2 = 0; d3 = 1;
sel = 2'b00; #10;  
sel = 2'b01; #10; 
sel = 2'b10; #10;  
sel = 2'b11; #10; 
$finish;
end
endmodule
```
## Simulated Output Structural Modelling

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/f8e352a1-f4d5-4ffb-8861-4e5f76c32414" />


### CONCLUSION

In this experiment, a 4:1 Multiplexer was successfully designed and simulated using Verilog HDL across four different modeling styles: Gate-Level, Data Flow, Behavioral, and Structural.The simulation results verified the correct functionality of the MUX, with all implementations producing identical outputs for the given input conditions.

