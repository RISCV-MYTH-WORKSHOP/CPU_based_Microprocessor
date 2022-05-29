# Digital Logic with TL-Verilog and Makerchip
Makerchip is a free online environment for developing high-quality integrated circuits. You can code, compile, simulate, and debug Verilog designs, all from your browser. Your code, block diagrams, and waveforms are tightly integrated.
The Application Binary Interface is the sum total of what the application programmer needs to understand in order to write programs; the programmer does not have to understand or know what is going on within the Application Execution Environment.

An Application Binary Interface would combine the processor ISA along with the OS system-call interface. The below snippet gives the list of registers, thier short description and ABI name of every register in RISC-V ISA.


# Combinational Logic
Starting with basic example in combinational logic is an inverter. To write the logic of inverter using TL-verilog is 
```
$out = ! $in;
```

* There is no need to declare
```
$out and $in unlike Verilog
```

There is also no need to assign ``` $in``` Random stimulus is provided, and a warning is produced.

![IMG_20220527_194822](https://user-images.githubusercontent.com/88897605/170717943-aff0f3e1-6ed0-4be8-8fed-c348f405edc1.jpg)


# Sequential logic
Starting with basic example in sequential logic is Fibonacci Series with reset. To write the logic of Series using TL-Verilog is ``` $num[31:0] = $reset ? 1 : (>>1$num + >>2$num).``` This operator >>? is ahead of operator which will provide the value of that signal 1 cycle before and 2 cycle before respectively.

 Sequential Calculator Shown Below
 ![srq](https://user-images.githubusercontent.com/88897605/170718723-5e6c51c9-63d7-40fd-920f-279f2ea6ff9c.jpg)

# Pipelined Logic 
Timing abstract powerful feature of TL-Verilog which converts a code into pipeline stages easily
* This is a place where TLV Shines bright. All us Verilog users have faced the endless pains of pipelining and fails. In both the calculator and the cpu core we have used pipelines
* Defined with a '|' symbol
* Within the Pipeline, multiple stages can be defined using '@'
* This concept is called Time Abstraction

* 2-cycle calculator which clears the output alternatively and output of given inputs are observed at the next cycle.
![21](https://user-images.githubusercontent.com/88897605/170719820-9a484354-db42-45c2-ad08-e09d9b767275.jpg)

## Validity

* NOTE: This functionality is not a part of other circuit design languages and is exclusive to TLV
* This will make no difference on the nature of the code to be honest. In usual processes, these would all be not care
* It basically decides when a signal has significance, so it is only executed then.
* This keeps the Waveform clean and easy to debug
* You will see this operator being used '?' throughout the CPU Code.

![21_v](https://user-images.githubusercontent.com/88897605/170719922-4f8432ad-6024-48d3-a45b-2359a305acc2.jpg)
