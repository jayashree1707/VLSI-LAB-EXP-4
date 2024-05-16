## SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS                                                                                     
## AIM: 
To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using vivado 2023.2.
## APPARATUS REQUIRED:
vivado 2023.2
## PROCEDURE:
STEP:1  Start  the vivado software, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.  
## LOGIC DIAGRAM:
## SR FLIPFLOP
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)
## VERILOG CODE:
```
module srff(s,r,clk,reset,q);
input s,r,clk,reset;
output reg q;
always@(posedge clk)
begin
if(reset==1)
q =1'b0;
else 
begin
case({s,r})
 2'b00: q = q;
 2'b01: q = 1'b0;
 2'b10: q = 1'b1;
 2'b11: q = 1'bx;
 default:q = ~q;
endcase
end 
end
endmodule
```
## OUTPUT:
![WhatsApp Image 2024-04-12 at 20 43 43_11b64f07](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/76dd3b2b-2552-4558-9989-02a238ad5a52)

## JK FLIPFLOP
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)
## VERILOG CODE:
```
module jk_ff(j,k,clk,reset,q);
input j,k,clk,reset;
output reg q;
always@(posedge clk)
begin
if(reset==1)
q =1'b0;
else 
begin
case({j,k})
 2'b00: q = q;
 2'b01: q = 1'b0;
 2'b10: q = 1'b1;
 2'b11: q = ~q;
 default:q =1'b0;
endcase
end 
end
endmodule
```
## OUTPUT:
![WhatsApp Image 2024-04-12 at 20 46 33_bb26db50](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/da8fdddd-f458-4d50-b041-cdec899e433e)

## T FLIPFLOP:
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)
## VERILOG CODE:
```
module tff(clk,rst,j,q);
input clk,rst,j;
output reg q;
always@(posedge clk)
begin
case(t)
1'b0:q=q;
1'b1:q=~q;
default=q=1'b0;
endcase
end
endmodule
```
## OUTPUT:
![WhatsApp Image 2024-04-12 at 20 47 36_fd48d610](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/39821533-3ed5-40d8-baff-361365b2a097)

## D FLIPFLOP
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)
## VERILOG CODE:
```
module dff(clk,rst,d,q);
input clk,rst,d;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
## OUTPUT:
![WhatsApp Image 2024-04-12 at 20 41 41_6aff88f5](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/c9ddaf50-4871-434f-95f3-4d07d4237a7b)

## COUNTER
![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)
## UPDOWN COUNTER:
## VERILOG CODE:
```
module updowncounter(clk,e,rst,count);
input e,rst,clk;
output reg[3:0]count;
always@(posedge clk)
begin
if(rst)
count=4'b0;
else
begin
if(e==1)
count=count+4'b1;
 else 
 count=count-4'b1;
 end 
 end
endmodule
```
### OUTPUT:
![WhatsApp Image 2024-04-12 at 20 49 39_e042057c](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/615a391b-7ad9-419e-9ff0-8b6e99fa9014)
### MOD 10 COUNTER:
## VERILOG CODE:
```
module counter10(clk,rst,count);
input clk,rst;
output reg [3:0]count;
always@(posedge clk)
begin
if (rst==1 | count == 4'b1001)
count=4'b0;
else
count=count+4'b1;
end
endmodule
```
## OUTPUT:
![WhatsApp Image 2024-04-12 at 20 47 33_b3f532d5](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/244933f1-c0f1-45f4-a18a-51d580e3ac80)
### RIPPLE CARRY COUNTER:
### VERILOG CODE:
```
module ripplecounter(q,clk,reset);
input clk,reset;
output[3:0]q;
T_FF tff0(q[0],clk,reset);
T_FF tff1(q[1],q[0],reset);
T_FF tff2(q[2],q[1],reset);
T_FF tff3(q[3],q[2],reset);
endmodule
module D_FF(q,d,clk,reset);
input d,clk,reset;
output reg q;
always@(negedge clk or posedge reset)
begin
if(reset)
q<=1'b0;
else
q<=d;
end
endmodule
module T_FF(q,clk,reset);
input clk,reset;
output q;
wire d;
D_FF dff0(q,d,clk,reset);
not n1(d,q);
endmodule
```
## OUTPUT:
![WhatsApp Image 2024-04-12 at 20 48 37_eb479c8a](https://github.com/jayashree1707/VLSI-LAB-EXP-4/assets/160314881/dead3e75-ef9f-400f-adac-91d90504f279)




  





## RESULT:
   Hence thus given To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using vivado.


