# COMMUNICATION PROTOCOLS – UART, I2C, SPI

Communication Protocols are set of rules and syntax that allow two or more communication systems to transmit and receive data from one another.

***
## 1] UART
- Full Form: Universal Asynchronous Receiver Transmitter.
- UART is a communication protocol which will allow data to transmit and receive data serially.
- As the name suggest (Asynchronous), we do not use any clock cycle for data transmission and reception.
- Figure 1 shows basic block diagram of communication through UART.
   ![Figure 1](https://user-images.githubusercontent.com/70748543/154222580-74090567-730c-4ebe-8377-dbc025a5686e.jpeg)

- We use only two wires for communication.
- As we don’t use any clock cycle, we need a package format for communication.
- Figure 2 shows Basic Block Diagram of Package Format.
   ![Figure 2](https://user-images.githubusercontent.com/70748543/154222750-da2c1baf-716b-4ae3-a30b-430554d3784d.jpeg)

### - Working:

1] Consider data sequence “10010101”

2] Initially the data bus is at High voltage, so to indicate start and stop of data we increase or decrease the voltage level  
    START and STOP bit.
    ![Figure 3](https://user-images.githubusercontent.com/70748543/154222920-bf4190c7-2e31-43dd-a39e-94cb215dc201.jpeg)

3] UART will receive the 8 bit data in parallel way.

4] Start bit will be at 0 to indicate that transmission of data has started. Similarly stop bit will be 1 to indicate transmission has ended.

5] LSB bit will be added in the data frame first.

6] Parity bit will be 
             0 – even no. of 1s
             1 – odd no, of 1s
    Here, we have even no. of 1s in data. Hence, we add 0+ in the bit. 
    
7] UART will add 0+ (start bit), 0+ (parity bit) and 1+(stop bit) to the original data sequence at UART-1 (transmitting system) and similarly add 0- (start bit), 0- (parity bit) and 1- (stop bit) at UART-2 (receiving system).

8] As soon as UART-2 will receive 0+ from UART-1 it will be indicate that the next 8 bits will be the data bits and it will start reading those bits and stop at the parity bit 0+ and will verify the parity bit. If parity it is same it will stop receiving at 1+ stop bit.

   ![Figure 4](https://user-images.githubusercontent.com/70748543/154223023-be094fac-55a3-410a-a851-055e04e20d64.jpeg)

- In UART, data format and transmission speeds are configurable. 

- BAUD RATE: It is the rate of data transfer in serial communication. Expressed in bits per second (bps).

- Depending on Application, UART can be configured in 3-ways:

  1] Simplex: One way communication
  
  2] Half Duplex: Communication can happen in both direction but not at same time.
  
  3] Full Duplex: Communication can happen in both directions at same time.
  ![Figure 5](https://user-images.githubusercontent.com/70748543/154223122-1ef7c799-2ff9-4354-a254-4ab26f4c3f9b.jpeg)

- Since, Full duplex operations require characters to be send and receive at same time UART uses two different shift registers for transmitted and received characters.

- Transmitting and receiving UARTs must be set for the same bit speed, character length, parity and stop bit for proper operation.

### - TYPES OF ERRORS:

**1] OVERRUN ERROR:** Occurs when the receiver cannot process the characters that just came in before the next one arrives.

**2] UNDERRUN:** Occurs when the UART transmitter has completed sending a character and transmitter buffer is empty.

**3] FRAMING ERROR:** UART will detect framing error when it does not see a stop bit at the expected stop bit time.

**4] PARITY BIT:** Occurs when the parity of the number of one-bits disagrees with that specified by the parity bit. 

### - ADVANTAGES: 

1] Only uses two wires.

2] No clock signal is necessary.

3] Provide error detection by parity bit check.

4] Cost and size will be much lesser compared to the parallel communication

### - DISADVANTAGES:

1] The size of data frame is limited to 9 bits,

2] Doesn’t support multi-master and multi-slave systems.

3] We get less speed as compared to parallel communication.

***

## 2] I2C













 

