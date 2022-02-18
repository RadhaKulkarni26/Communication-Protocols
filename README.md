# COMMUNICATION PROTOCOLS – UART, I2C, SPI

Communication Protocols are a set of rules and syntax that allow two or more communication systems to transmit and receive data from one another.

## 1] UART
- Full Form: Universal Asynchronous Receiver Transmitter.
- UART is a communication protocol that will allow data to transmit and receive data serially.
- As the name suggests (Asynchronous), we do not use any clock cycle for data transmission and reception.
- Below shows the basic block diagram of communication through UART.
   ![Figure 1](https://user-images.githubusercontent.com/70748543/154222580-74090567-730c-4ebe-8377-dbc025a5686e.jpeg)

- We use only two wires for communication.
- As we don’t use any clock cycle, we need a package format for communication.
- Below shows the Basic Block Diagram of Package Format.
   ![Figure 2](https://user-images.githubusercontent.com/70748543/154222750-da2c1baf-716b-4ae3-a30b-430554d3784d.jpeg)

### - Working:

1] Consider data sequence “10010101”

2] Initially the data bus is at High voltage, so to indicate the start and stop of data we increase or decrease the voltage level  
    START and STOP bit.
    ![Figure 3](https://user-images.githubusercontent.com/70748543/154222920-bf4190c7-2e31-43dd-a39e-94cb215dc201.jpeg)

3] UART will receive the 8-bit data in a parallel way.

4] Start bit will be at 0 to indicate that the transmission of data has started. Similarly, the stop bit will be 1 to indicate transmission has ended.

5] LSB bit will be added in the data frame first.

6] Parity bit will be 
             0 – even no. of 1s
             1 – odd no, of 1s
    Here, we have even no. of 1s in data. Hence, we add 0+ in the bit. 
    
7] UART will add 0+ (start bit), 0+ (parity bit) and 1+(stop bit) to the original data sequence at UART-1 (transmitting system) and similarly add 0- (start bit), 0- (parity bit) and 1- (stop bit) at UART-2 (receiving system).

8] As soon as UART-2 will receive 0+ from UART-1 it will be indicated that the next 8 bits will be the data bits and it will start reading those bits and stop at the parity bit 0+ and will verify the parity bit. If parity is the same it will stop receiving at 1+ stop bit.

   ![Figure 4](https://user-images.githubusercontent.com/70748543/154223023-be094fac-55a3-410a-a851-055e04e20d64.jpeg)

- In UART, data format and transmission speeds are configurable. 

- BAUD RATE: It is the rate of data transfer in serial communication. Expressed in bits per second (bps).

- Depending on the Application, UART can be configured in 3-ways:

  1] Simplex: One way communication
  
  2] Half Duplex: Communication can happen in both directions but not at the same time.
  
  3] Full Duplex: Communication can happen in both directions at the same time.
  ![Figure 5](https://user-images.githubusercontent.com/70748543/154223122-1ef7c799-2ff9-4354-a254-4ab26f4c3f9b.jpeg)

- Since Full duplex operations require characters to be sent and received at the same time UART uses two different shift registers for transmitted and received characters.

- Transmitting and receiving UARTs must be set for the same bit speed, character length, parity ,and stop bit for proper operation.

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

1] The size of the data frame is limited to 9 bits,

2] Doesn’t support multi-master and multi-slave systems.

3] We get less speed as compared to parallel communication.

***

## 2] I2C

- Full Form: Inter Integrated Circuit

- I2C is a Serial Communication protocol in which data is transferred bit by bit using a single wire (SDA).

- I2C is a synchronous communication protocol that uses a clock cycle for data transmission and reception.

- Below diagram shows a basic block diagram of I2C.
    ![Figure 6](https://user-images.githubusercontent.com/70748543/154634888-c50c4eb1-eec4-4427-b201-2ea08702e3c5.jpeg)

- I2C uses only two wire (SDA and SCL) for communication.

  1] SDA – Serial Data Line is used to read/write data between two or more communication systems namely Master and Slave.
  
  2] SCL – Serial Clock Line is used to control clock cycle from Master to Slave.   

- We can have multiple Master and Slave in I2C Communication Protocol.

- Acknowledge Bit will be sent by the receiver to the transmitter to confirm that data frame or characters have been delivered successfully.

- Working

  Consider we have a single Master and 3 slaves as shown in the figure below
  ![Figure 7](https://user-images.githubusercontent.com/70748543/154634956-11ec17e2-a0db-4eeb-8f33-ac2e3ce55dff.jpeg)

  
   1] Start Condition: Initially, to write data from master to slave we need to make SDA voltage HIGH to LOW and then SCL voltage HIGH to LOW.
  
   2] Slave Address + R/W bit: Consider, each slave will have its unique slave address.
   
        - Slave 1: 0000001
        
        - Slave 2: 0000010
        
        - Slave 3: 0000011
      
    Each slave will then be connected to the same clock pulse through the SCL pin.
      
    Then, the Master will send W/R bit + required Slave address to all 3 slaves through the SDA line.
      
    Consider we need to write data to slave 3 so Master will send W+0000011 to all 3 slaves.
   
   3] Acknowledge Bit: Each slave will then compare address 0000011 with its unique slave address, if they are the same it will send Acknowledge Bit back to Master.
                       Acknowledge bit will be sent by lowering the SDA voltage by 1 bit.

   4] Master Send/Receiver: Master will then send data to respective slave in form of a Data frame.
   
   5] For every data frame received acknowledge bit will be sent by the receiver.
   
   6] Stop Condition: After receiving complete data we will make SCL voltage LOW to HIGH and then SDA HIGH to LOW.

- I2C is a Half Duplex Communication Protocol

- Typical Voltage used are +5V or +3.3V.

 ***

## 3] SPI

- Full Form: Serial Peripheral Interface

- SPI is nothing but Synchronous Serial Communication Interface,

- It uses a clock cycle for interfacing

- It will transmit and receive data using 4 wires.
   
   1] MOSI: Master out slave in
   
   2] MISO: Master in slave out
   
   3] SCLK: Serial clock
   
   4] SS bar: Slave select

- It can have a single Master and multiple slaves.

- Slave select or chip select will decide which slave will receive the data.

- Below diagram shows a Basic block diagram of SPI.
  ![Figure 8](https://user-images.githubusercontent.com/70748543/154646040-c0dada30-304d-4e2c-beb2-cc1b0492a27c.jpeg)

- The two most commonly used configurations are:
   
  1] Independent slave configuration: It will have individual slave select pins for each slave.
     Below diagram shows the Block Diagram of Independent Slave Configuration.
     ![Figure 9](https://user-images.githubusercontent.com/70748543/154646111-e60898ab-856f-4a22-b6b1-046f6a047860.jpeg)

  2] Daisy Chain Configuration:
    ![Figure 10](https://user-images.githubusercontent.com/70748543/154646206-dbdbd8d7-f121-422f-8986-afaa3d029ae5.jpeg)

    Here, we have the same slave select for all slaves but the MISO of 1st slave will be connected to the MOSI to 2nd till the last slave and then MISO of last slave will be given as MISO of the master. 

- Advantages:
 
 1] It can perform Full Duplex operation as we have separate MISO and MOSI lines.
 
 2] No use of start and stop bit, hence data can be interfaced continuously.

- Disadvantages:

 1] Use of 4 wires ,unlike I2C and SPI.
 
 2] Can have only a single Master.
 
 3] No acknowledgment bit to check whether the data has been received or not.












 

