# 5G-PHY-LAYER
- physical layer of 5G responsible for transmission and reception of data over the wireless network . It sits at the bottom of NR protocol stack , interacting with MAC layer via Transport channel .
- The physical layer is based on multiple features like , an OFDM  (orthogonal frequency division multiplexing) , numerology , Frame strucure , RBs , PRBs  Channel coding , MCS , HARQ etc.

## MCS (modulation and coding scheme) 
- **CODE RATE**
  - can be defined as the ratio between useful bit and total transmitted bit (useful + redundant Bits) , always ranges between 0 and 1 cause the useful number of bits can never be more than the total number of transmited bits for a successful transmission . In other words we can it is the ratio between the number of information bits at the top of the Physical layer and the number of bits which are mapped to PDSCH at the bottom of the Physical layer. We can also say, it  a measure of the redundancy which is added by the Physical layer. A low coding rate corresponds to increased redundancy( extra binary bits added externally into the original data bit to prevent damage to the transmitted data and are also needed to recover the original data ) .Decreasing code rate can increase the robustness of the transmission

![Screenshot from 2023-11-29 17-51-34](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/3f157929-3725-4884-8fab-030cd9cbe6eb)
![Screenshot from 2023-11-29 17-52-01](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/973e3335-a268-49f1-9ab7-31696c9a2032)






















