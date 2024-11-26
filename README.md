# EXP1: 4 Bit Adder functionality verification

**Aim:**

To write a verilog code for 4bit adder and verify the functionality using Test bench.<br>

&emsp;&emsp;Write Verilog Code<br>

&emsp;&emsp;Verify the Functionality using Test-bench.<br>

**Tool Required:**

&emsp;&emsp;Functional Simulation: nclaunch Simulator (nclaunch) <br>

**4-bit Adder Design:**

&emsp;&emsp;To construct a 4-bit adder, need to chain together four 1-bit full adders. Each full adder computes the sum and carry for one bit of the two numbers. The carry-out from one adder feeds into the carry-in of the next adder in the sequence. This process adds the two 4-bit numbers bit by bit, with the carry propagating through each stage, resulting in a final sum and carry-out at the end.<br>

&emsp;&emsp;To design a 1-bit full adder, the first step is to create a truth table that represents all possible combinations of the inputs (A, B, and CIN) and the corresponding outputs (Sum(S) and COUT).<br>

![image](https://github.com/user-attachments/assets/716a26b6-a449-42e0-9e2d-cdbaa4b291b9)

Here’s the truth table for a 1-bit full adder:

![tt](https://github.com/user-attachments/assets/0b3ab24f-1d7e-4a01-80ce-5e7406f4082b)

**Fig 1 : Diagram and truth table of full adder**

**Logic Expressions:**

1.	Sum (S):
   
&emsp;&emsp;S=A⊕B⊕CIN

&emsp;&emsp;Where ⊕ represents XOR.

3.	Carry out (COUT):
   
&emsp;&emsp;COUT=(A&B) | (CIN&(A^B))

![image](https://github.com/user-attachments/assets/7d6fa554-2614-4f19-aa68-65c9e6153caa)

**Fig 2:Diagram of 4 Bit Adder**

**Creating Source Codes**

&emsp;&emsp;In the Terminal, type gedit <filename>.v (ex: gedit 4bitadder.v). <br>

&emsp;&emsp;A Blank Document opens up into which the following source code can be typed down. <br>

&emsp;&emsp;Note : File name should be with HDL Extension<br>

**Verilog code for 1 Bit Full adder**

```
module full_adder(A,B,CIN,S,COUT);
input A,B,CIN;
output S,COUT;
assign S=A^B^CIN;
assign COUT=(A&B) | (CIN&(A^B));
endmodule
```

**Verilog Code for 4 Bit Full Adder**

```module fulladd_4bit(A,B,C0,S,C4);
input [3:0] A,B;
input C0;
output [3:0] S;
output C4;
wire C1,C2,C3;
full_adder fa0 (A[0],B[0],C0,S[0],C1);
full_adder fa1 (A[1],B[1],C1,S[1],C2);
full_adder fa2 (A[2],B[2],C2,S[2],C3);
full_adder fa3 (A[3],B[3],C3,S[3],C4);
endmodule
```

**a) Verify the Functionality**

&emsp;&emsp;Three Codes shall be written for implementation of 4-bit Adder as follows, <br>

&emsp;&emsp;&emsp;&emsp;fa.v → Single Bit 3-Input Full Adder [Sub-Module / Function] <br>

&emsp;&emsp;&emsp;&emsp;fa_4bit.v → Top Module for Adding 4-bit Inputs. <br>

&emsp;&emsp;&emsp;&emsp;fa_4bit_test.v → Test bench <br>

**Testbench Code for 4 bit Full Adder**

```
module test_4bit;
reg [3:0] A;
reg [3:0] B; reg C0;
wire [3:0] S; wire C4;
fulladd_4bit dut (A,B,C0,S,C4);
initial 
begin
A=4'b0011;B=4'b0011;C0=1'b0;
#10;  A=4'b1011;B=4'b0111;C0=1'b1;
#10; A=4'b1111;B=4'b1111;C0=1'b1;
#10;
end initial
#50 $finish;
endmodule
```

**Functional Simulation:**

&emsp;&emsp;Invoke the cadence environment by type the below commands <br>

&emsp;&emsp;tcsh (Invokes C-Shell) <br>

&emsp;&emsp;source /cadence/install/cshrc (mention the path of the tools) <br>

&emsp;&emsp;```(The path of cshrc could vary depending on the installation destination)<br>```
      
&emsp;&emsp;After this you can see the window like below <br>

![Screenshot (32)](https://github.com/user-attachments/assets/e50442db-24cc-4e6d-af42-5a776efb203d)


**Fig 3:Invoke the Cadence Environment**

&emsp;&emsp;To Launch Simulation tool <br>

&emsp;&emsp;&emsp;&emsp;linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design <br>

&emsp;&emsp;&emsp;&emsp;or<br>

&emsp;&emsp;&emsp;&emsp;linux:/> nclaunch& // On subsequent calls to NCVERILOG <br>

&emsp;&emsp;It will invoke the nclaunch window for functional simulation we can compile,elaborate and simulate it using Multiple Step .<br>

![Screenshot (32)](https://github.com/user-attachments/assets/ca4eaea5-adc8-4191-bb3a-52db4aacd5d8)

**Fig 4:Setting Multi-step simulation**

&emsp;&emsp;Select Multiple Step and then select “Create cds.lib File” .<br>

&emsp;&emsp;Click the cds.lib file and save the file by clicking on Save option <br>

![Screenshot (33)](https://github.com/user-attachments/assets/92391592-0652-4da7-86de-b4dc4e77fed2)

**Fig 5:cds.lib file Creation**

&emsp;&emsp;Save cds.lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used. <br>

&emsp;&emsp;Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in below figure .<br>

&emsp;&emsp;&emsp;&emsp;We are simulating verilog design without using any libraries <br>

&emsp;&emsp;&emsp;&emsp;A Click “OK” in the “nclaunch: Open Design Directory” window as shown in below figure <br>

![Screenshot (27)](https://github.com/user-attachments/assets/8e6dec98-4285-4f39-bbaa-00edb13e7063)

**Fig 6: Selection of Don’t include any libraries**

&emsp;&emsp;A ‘NCLaunch window’ appears as shown in figure below <br>

&emsp;&emsp;Left side you can see the HDL files. Right side of the window has worklib and snapshots directories listed. <br>

&emsp;&emsp;Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation .<br>

&emsp;&emsp;To perform the function simulation, the following three steps are involved Compilation, Elaboration and Simulation. <br>

![Screenshot (28)](https://github.com/user-attachments/assets/1e341815-8122-49db-a384-ab75260e1643)

**Fig 7: Nclaunch Window**

**Step 1: Compilation:– Process to check the correct Verilog language syntax and usage**

&emsp;&emsp;Inputs: Supplied are Verilog design and test bench codes <br>

&emsp;&emsp;Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file <br>

**Steps for compilation:**

&emsp;&emsp;1. Create work/library directory (most of the latest simulation tools creates automatically) <br>
&emsp;&emsp;2. Map the work to library created (most of the latest simulation tools creates automatically) <br>
&emsp;&emsp;3. Run the compile command with compile options <br>
&emsp;&emsp;i.e Cadence IES command for compile: ncverilog +access+rwc -compile fa.v<br>

&emsp;&emsp;Left side select the file and in Tools : launch verilog compiler with current selection will get enable. Click it to compile the code <br>

&emsp;&emsp;Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation<br>

![Screenshot (34)](https://github.com/user-attachments/assets/998c025d-1ffe-422c-a68a-2d8495b585a9)

**Fig 8: Compiled database in worklib**

&emsp;&emsp;After compilation it will come under worklib you can see in right side window<br>

&emsp;&emsp;Select the test bench and compile it. It will come under worklib. Under Worklib you can see the module and test-bench. <br>

&emsp;&emsp;The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”<br>

**Step 2: Elaboration:– To check the port connections in hierarchical design**

&emsp;&emsp;Inputs: Top level design / test bench Verilog codes <br>

&emsp;&emsp;Outputs: Elaborate database updated in mapped library if successful, generates report else error reported in log file <br>

&emsp;&emsp;Steps for elaboration – Run the elaboration command with elaborate options <br>

&emsp;&emsp;&emsp;&emsp;1.	It builds the module hierarchy <br>
&emsp;&emsp;&emsp;&emsp;2.	Binds modules to module instances <br>
&emsp;&emsp;&emsp;&emsp;3.	Computes parameter values <br>
&emsp;&emsp;&emsp;&emsp;4.	Checks for hierarchical names conflicts <br>
&emsp;&emsp;&emsp;&emsp;5.	It also establishes net connectivity and prepares all of this for simulation<br>
   
&emsp;&emsp;After elaboration the file will come under snapshot. Select the test bench and elaborate it.<br>

![Screenshot (34)](https://github.com/user-attachments/assets/9f5f6d93-05db-4aad-8ba5-a5d3d9ed9d92)

**Fig 9: Elaboration Launch Option**

**Step 3: Simulation: – Simulate with the given test vectors over a period of time to observe the output behaviour.**

&emsp;&emsp;Inputs: Compiled and Elaborated top level module name <br>

&emsp;&emsp;Outputs: Simulation log file, waveforms for debugging <br>

&emsp;&emsp;Simulation allow to dump design and test bench signals into a waveform <br>

&emsp;&emsp;Steps for simulation – Run the simulation command with simulator options<br>

![Screenshot (35)](https://github.com/user-attachments/assets/9c9cf45d-49e6-4731-94ea-5bdeb48043be)

**Fig 10: Design Browser window for simulation**

![Screenshot (36)](https://github.com/user-attachments/assets/733742cc-54c8-4355-bed2-93b8fd396fc6)

**Fig 11: Launching Simulation Waveform WindowSimulation Waveform Window**

![Screenshot (37)](https://github.com/user-attachments/assets/9bb6ff50-875e-4914-8429-1f144fd0e62c)

**Fig 12: Simulation Waveform Window**

![Screenshot (37)](https://github.com/user-attachments/assets/fad7f8c0-75ea-4bf0-802f-ab94a7c54c6c)
















