# 1x3-Router
Routing is the process of moving a packet of data from source to destination and enables messages to pass from one computer to another and eventually reach the target machine. A router is a networking device that forwards data packets between computer networks. It is connected to two or more data lines from different networks (as opposed to a network switch, which connects data lines from one single network).<br>This project, mainly emphasizes upon the study of router device, its top level architecture, and how various sub-modules of router i.e. Register, FIFO, FSM and Synchronizer are synthesized, and simulated and finally connected to its top module.
### 1x3-Router Block diagram: <p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/Router%20block.png)</p>
The router follows packet based protocol. It receives input packet as data_in from source network on a byte by byte basis on posedge of clock. resetn is synchronous active low reset. The starting of a packet is indicated by asserting pkt_valid and end of the packet is indicated by deasserting pkt_valid. The design stores the packet inside a FIFO as per the address of the packet. There are 3 different FIFOs for 3 different networks. During read operation, the destination monitors vld_out_x(x=0,1,2) and then asserts read_enb_x. The packet is then read by the destination using data_out_x. The router may enter into busy state indicated by the busy signal. The busy signal is sent back to the source LAN so that source has to wait to send the next byte of the packet. To confirm the correctness of the received, a parity checking mechanism has been implemented. If there is a mismatch in the parity byte sent and the internal parity calculated by the router , an error signal is generated which is sent to the source and the source can then resend the packet. The design can only receive 1 packet at a time, but 3 packets can be read simultaneouly.
<br>Packet format: The packet consists of 3 parts: header, payload data and parity such that each is of 8 bits. Payload can of 1 to 63 length.


The router consists of the following blocks:
- It contains 3 FIFOs to store packet based on the address.
- It contains a Synchroniser block that resets the FIFO if read_enb_x is not received within 30 clock cycles of assertion of vld_out_x.
- It contains a Register block that temporarily stores header byte, internal parity while calculating parity, packet parity and full state byte. It also generates error signal in case of mismatch in generated and received parity.
- It contains an FSM controller that generates and sends the control signals.


### Synthesised Schematic:<p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/Schematic.png)</p>


<br>The block diagram of following blocks are as shown:
- FIFO:<p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/FIFO.png)</p>
- Register:<p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/Register.png)</p>
- Synchroniser:<p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/Synchroniser.png)</p>
- FSM Controller:<p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/FSM.png)</p>



### Output waveform for an input applied to the router is as shown below:<p align="center">![alt text](https://github.com/Praranya/1x3-Router/blob/main/1x3-Router_pics/Wave_output.png)</p>
