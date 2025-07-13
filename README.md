# SRAM-Memory-Architecture-and-In-Memory-Computing-Logic
## Introduction
* In-memory computing (IMC) processes data directly within memory arrays, reducing the need to 
transfer data between memory and separate processing units like CPUs or GPUs.
* This approach minimizes latency and energy consumption by cutting down on data movement, 
enhancing performance efficiency.
![Screenshot 2025-06-29 112622](https://github.com/user-attachments/assets/3d39cd83-364a-46f2-a27f-88c2915c23cc)

*  In Von-Neumann Architecture, the CPU and memory are separate, causing data to move between them for processing and creating a bottleneck due to limited bandwidth
  <p align="center">
  <img src="https://github.com/user-attachments/assets/699dc3ff-e4b4-4966-8268-cd474e374c8e" 
       alt="Screenshot 2025-06-28 154723" 
       width="300"/>  
  
#### Digital In Memory Computing Architecture:
* Digital IMC is a computing approach where logic operations like AND, OR, XOR,addition etc are performed directly inside memory, rather than transferring data to a separate processor. Since all operations use binary values (0s and 1s), it's called digital IMC—offering high reliability, speed, and energy efficiency.
* To enable this, we use SRAM as a key component because it can store weights and input data in binary form, and also allows performing bitwise operations within the memory array itself. SRAM is fast, CMOS-compatible, and ideal for repeated read/write cycles—making it perfect for implementing digital logic directly in hardware.

## SRAM 4x4 Array Peripharals and Architecture Using CMOS Technology

### 1. 6T Sram Bitcell
* Consists of 6 transistors: 4 for storage (cross-coupled inverters) + 2 access transistors for read/write.
* Stores 1 bit of data in a stable latch without needing refresh (unlike DRAM).
* Fast Read/Write: Very low access time, ideal for high-speed memory like caches.
* CMOS Compatible: Easily integrates with logic circuits in digital systems.
  <p align="center">
  <img src="https://github.com/user-attachments/assets/8d8f5cfc-af53-468a-851b-f5fed2c05c62" 
       alt="Screenshot 2025-06-28 154723" 
       width="300"/>  
    
### 2. Precharge Circuit 
* One of the cruicial periphary, all the read-write operations are performed after BL and BLB are initially precharged and for this purpose we use the precharge circuit .
* In my design , I have used common precharge for both read and write operation , hence the control 'PRE' becomes high in case of any read or write operation , hence saving the hardware .

 <p align="center">
  <img src="https://github.com/user-attachments/assets/1a75390b-7240-4d17-85a6-c183bb365d29" 
       alt="Screenshot 2025-06-28 154723" 
       width="300"/>  
   
  ### 3. Cross Coupled Sense Amplifier
**Read Operation:**
* When a wordline is activated, the bitcell slightly pulls down either BL or BLB, depending on whether it stores 0 or 1
* This creates a tiny imbalance between BL and BLB.
* The sense amplifier, which is connected to both lines, is then enabled (using SAE).
* The sense amplifier detects the data stored based on changes observed in BL and BLB value , if BL changes from 1->0 then it means data stored in bitcell is logic 0 and if BLB changes from 1->o depicts data stored was logic 1 
* Note - These BL and BlB were precharged initially before read operation and thus changes in these values are fed to sense amplifier .
  
**Why Cross Coupled Design**
* Works well even when the cell doesn’t strongly pull the bitlines (important for low-voltage or fast-access SRAM), hence **High Sensitivity.**
* It only turns on when SAE (Sense Amplifier Enable) is high.
* With SAE low;  Data and Data# are pre-charge high
![WhatsApp Image 2025-07-13 at 20 24 09_4dc793d9](https://github.com/user-attachments/assets/8b176603-20e6-41e9-a762-38afdfc248a9)

  

### 4. 2x4 Decoder 
* Address Selection:The word decoder translates the binary address input into a single active wordline, ensuring that only one row of the SRAM array is accessed at a time for read or write operations , it enables WL Control of all the bitcells of that particular row .
* Area and Wiring Efficiency:
Instead of requiring a separate control line for each wordline, the decoder allows us to use a compact address bus, reducing complexity and saving routing area on chip.
![Screenshot 2025-06-29 125116](https://github.com/user-attachments/assets/18480b47-409c-4759-91bd-a218152a723d)

### 5. Write Driver 
* A circuit which basically forces the data into the bitcell by enabling wr_enable control.
* It also uses BL and BLB and based on their value the 1 bit data is written into the bitcell .
* The circuitry works as , if BL changes from 1->0 the logic 0 will be written into the bitcell and if BLB is changed form 1->0 then logic 1 will be written.
 <p align="center">
  <img src="https://github.com/user-attachments/assets/37981e50-8298-4db2-841c-55ea504b1397" 
       alt="Screenshot 2025-06-28 154723" 
       width="300"/>  
   
* This Write Driver circuit is also attached to precharge circuit hence making the single unit and the outputs from this overall unit are BL and BLB which can act both as precharge circuit initially for both read and  write and also can be useful in writing the values to the bitcell directly on the basis of values BL and BLB.
   
![wr drv final](https://github.com/user-attachments/assets/7796beac-e920-46f5-b591-24182b994076)

### Overall Circuit For 1 Bitcell Read and Write:
![WhatsApp Image 2025-06-29 at 13 49 24_97b9c413](https://github.com/user-attachments/assets/078095d0-04a8-4c71-9dd3-5b266cf9be7b)

## Final Circuit 4X4 Sram Array:
![Screenshot 2025-06-29 140201](https://github.com/user-attachments/assets/9ccae914-c127-4931-8250-91c4d1e64216)

## 🛠️ Project Status & Next Steps:
* I will be designing Digital In-Memory Computing (IMC) logic desgin, modified to perform bitwise multiplication operations directly within the memory array to improve computational efficiency.
* The project will also include the development of a MAC (Multiply-Accumulate) unit and supporting digital logic design to enable basic arithmetic inside memory.
* Second approach instead of MAC unit ,Planning to incorporate a logarithmic computing approach to enable efficient multiplication using addition of exponents.
