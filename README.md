# 5G-PHY-LAYER
- physical layer of 5G responsible for transmission and reception of data over the wireless network . It sits at the bottom of NR protocol stack , interacting with MAC layer via Transport channel .
- The physical layer is based on multiple features like , an OFDM  (orthogonal frequency division multiplexing) , numerology , Frame strucure , RBs , PRBs  Channel coding , MCS , HARQ etc.

## MCS (modulation and coding scheme) 
- **CODE RATE**
  - can be defined as the ratio between useful bit and total transmitted bit (useful + redundant Bits) , always ranges between 0 and 1 cause the useful number of bits can never be more than the total number of transmited bits for a successful transmission . In other words we can it is the ratio between the number of information bits at the top of the Physical layer and the number of bits which are mapped to PDSCH at the bottom of the Physical layer. We can also say, it  a measure of the redundancy which is added by the Physical layer. A low coding rate corresponds to increased redundancy( extra binary bits added externally into the original data bit to prevent damage to the transmitted data and are also needed to recover the original data ) .Decreasing code rate can increase the robustness of the transmission

![Screenshot from 2023-11-29 17-51-34](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/3f157929-3725-4884-8fab-030cd9cbe6eb)
![Screenshot from 2023-11-29 17-52-01](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/973e3335-a268-49f1-9ab7-31696c9a2032)

- **Modulation**
  - how many bits can be carried by a single RE irrespective of whether its useful bit or parity bits (simple form of error detection used in digital communications, computing, and data storage. It is an extra bit added to a binary code to ensure the accuracy of data transmission or storage)
  - Higher order modulation schemes have
more points allocated in the constellation diagram, leading to each signal
representing a greater number of information bits. However, this means that
the Euclidian distance between each point will be decreased since there are
more points, and therefore will lead to increased number of errors for a fixed SINR value

![Screenshot from 2023-11-29 18-06-51](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/effaad72-b7f3-4e5e-998d-5a0a4bcb703d)
![Screenshot from 2023-11-29 18-07-16](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/21329dc8-58ac-435e-8e56-9ca4b752c47b)

 - with 16QAM  it can be 4 bits, with 64QAM it can be 6 bits and with 256QAM it can 8 bits. These 16, 64 and 256 are know as modulation order of QAM Modulation and The no. of bits for each modulation order can be calculated using following formula.

![Screenshot from 2023-11-29 18-14-49](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/03072a33-8ec9-470e-a685-ffa78e85067c)

### CQI (channel quality indicator)
- gNB determines the MCS index based on CQI index that gNB got from UE to define the possible modulation orders and coding schemes to use for data transmission. Getting a higher CQI index indicates a better signal quality, and the gNB can transmit a larger transport block size.
  
- However, since CQI is a 4-bit integer ranging between 0 to 15 and MCS is a 5-bit integer ranging between 0 to 31, there will be more than one MCS value that corresponds to a certain CQI value in many cases. Therefore, the scheduler must determine which MCS value corresponds to the received CQI value

- The chosen modulation order and code rate will be used for transmission
on the Physical Downlink Shared Channel (PDSCH). Then the MCS value
will be sent among the Downlink Control Information (DCI), to enable the
UE for correct demodulation

![Screenshot from 2023-11-29 19-03-38](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/5825f699-ad54-4d0c-8bed-c01a3afadc0e)

### MCS 5G characteristics 
- Modulation and Coding Scheme (MCS) defines the numbers of useful bits per symbols
- MCS is change by gNB based on **link adaptation algorithm**
- MCS information is provided to UE using DCI
- 5G NR supports QPSK,16 QAM, 64 QAM and 256 QAM modulation for PDSCH
There are about 32 **MCS Indexes** (gNB determines the MCS index based on **CQI index** that gNB got from UE to define the possible modulation orders and coding schemes to use for data transmission. Getting a higher CQI index indicates a better signal quality, and the gNB can transmit a larger transport block size.)  (0-31) are defined and MCS Index 29,30 and 31 are reserved and used for re-transmission

### MCS tables
- There are 28 possible values, and 3 reserved values, By increasing the MCS value, the Transfer Block Size (TBS) of the transmitted subframe is increased, which represent the useful bits in a subframe. As a consequence, higher data rates can be achieved on the expense of signal robustness against noise and interference. 

- 64 QAM table may be used when gNB or UE is not supporting 256 QAM or in poor radio connection where 256 QAM table decoding is not successful and gNB needs to allocate QPSK order modulation

![Screenshot from 2023-11-29 19-35-17](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/6bcfd5ef-4aad-470d-99cf-662743d065f7)

- 256 QAM table may be used whenever 256QAM is to allocated in very good radio condtions

![Screenshot from 2023-11-29 19-36-24](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/b0a09aa4-7cba-405a-9146-164011ca3efc)

- Low spectral efficiency (Low SE) 64 QAM table is suitable for applications which need reliable data transfer, e.g. applications belonging to the URLLC category. This table includes MCS which have low Spectral Efficiency  i.e. a reduced coding rate which increase channel coding redundancy

![Screenshot from 2023-11-29 19-36-55](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/ef140bfc-bdd8-4e03-bb07-33426f91cdcd)

![Screenshot from 2023-11-30 09-57-22](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/2ce58b5d-5acd-4c58-94c4-ef2bf1ed1be3)

- [good video on MSC TABLE](https://www.youtube.com/watch?v=QBiBPbME5tY)












