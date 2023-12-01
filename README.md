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

- [good video on MSC TABLE](https://www.youtube.com/watch?v=QBiBPbME5tY)
- [2nd](https://www.youtube.com/watch?v=6WiX_ASCaec&t=340s)

- example illustrated that MSC table section can be controlled using only Physical layer signalling once the initial RRC signalling has been completed 
  - consider a UE has been configured with parameter PSCH-config with MSC-TABLE : **QAM256** and allocated an MSC-C-RNTI along with traditional C-RNTI
  - if the UE receives a PDSCH resource allocation using DCI format 1_1( is used for the scheduling of PDSCH in one cell.) with the C-RNTI then the UE will select 256QAM MSC TABLE
  - if the UE receives a PDSCH resorce allocation using DCI format 1_0( is used for the scheduling of PDSCH in one DL cell.) with C-RNTI then the UE will select the 64QAM MSC TABLE
  - if the same UE receives a PDSCH resorce allocation using DCI format 1_1 or 1_0 but with MSC-C-RNTI then the UE will select the LSE MSC table 

![Screenshot from 2023-11-30 10-25-07](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/a625271e-00a7-4bad-98e8-c26226255e01)

## Channel coding 
- It is a technique used to add redudancy to the transmitted data to make it more resilient to errors caused by the communication channel
- Its essential in wireless comm systems as the transmitted signal may experience noise , fading and other channel impairments . 
- 5G traffic channels are encoded using LDPC(low density parity chechk) coding and Control Channels are encoded with polar codes

### LDPC (low density parity check)
- Used in channel coding on traffic channel in 5G
- lDPC corrects errors by maintaining parity bits for a selection of the data bits
- [more on LDPC](https://www.youtube.com/watch?time_continue=738&v=RWUxtGh-guY&embeds_widget_referrer=https%3A%2F%2Fmedium.com%2F5g-nr%2Fldpc-low-density-parity-check-code-8a4444153934&embeds_referring_euri=https%3A%2F%2Fcdn.embedly.com%2F&embeds_referring_origin=https%3A%2F%2Fcdn.embedly.com&source_ve_path=MTM5MTE3LDEzOTExNywxMzkxMTcsMTM5MTE3LDIzODUx&feature=emb_title)
- [for better understanding](https://medium.com/5g-nr/ldpc-low-density-parity-check-code-8a4444153934#:~:text=5G%20NR%20uses%20LDPC%20for,the%20data%20and%20parity%20bits.)

## Polar coding 
- Used on control channel in 5G
- The polar encoding uses an SNR-independent method where the reliability of each subchannel is computed offline and the ordered sequence stored for a maximum code length
- for example
   1. polar code in PDCCH
   2. LDPC code in PDSCH 
- Control information is typically transmitted with a smaller amount of information bits and with a shorter codeword length. Control information is also typically transmitted with a lower code rate while good performance in a lower BLER regime is required.

## CSI (channel state information) 
- It refers to the information about the wireless channel between the transmitter and the receiver .
- It is used to optimize the transmission and reception of data
- Following are the components of CSI in NR
  - **CQI(channel Quality Information)** : scroll up
  - **PMI(Precoding Matrix indicator)** : The Precoding Matrix Indicator (PMI) report is the device's recommendation (a 2-bit or 4-bit value depending on the number of antenna ports) regarding what precoding matrix to use in PDSCH
    
  - **CRI(CSI-RS RESORCE INDICATOR)**
    - It is a reference signal (RS) that is used in the Downlink (DL) direction in 5G NR, for the purpose of Channel Sounding and used to measure the characteristics of a radio channel so that it can use correct modulation, code rate, beam forming etc. `UEs will use these reference signals to measure the quality of the DL channel and report this in the UL through the` **CQI Reports** [reference](https://info-nrlte.com/tag/cri/)
    
   ![Screenshot from 2023-11-30 20-46-36](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/fe2dc20c-0dca-4368-a8ec-481d5137afd2)

  - **SSBRI(SS/PBCH RESORCE BLOCK INDICATOR** : can be used to identify best downlink beam(s)
  
  - **LI(LAYER INDICATOR)**
  - **RI(RANK INDICATOR)**
    - RI is an indicator showing how well multiple antenna work (no interferene to each other)
    - max RI is related to number of antenna , Maximum RI is same as number of antenna on each side if the number of Tx antenna and Rx antenna is same. If the number of Tx and Rx are different, the one with less antenna is the same as Max achievable RI.
    - Max RI means "No Correlation between the antenna", "No interference to each other", "Best Performance". For example, in case of 2x2 MIMO, the RI value can be 1 or 2. When the value 2 in this case means "No Correlation between the antenna", "No interference to each other", "Best Performance". If the value is 1, it implies that the signal from the two Tx antenna is percieved by UE to be like single signal from single Antenna, which means the worst performance. [reference](https://www.sharetechnote.com/html/Handbook_LTE_RI.html)

## FRAME STRUCTURE 
- Data(UL/DL) is transmitted in the form of radio frames in the air.
-  the 5G frame structure is based on a slot and symbol-based design. This means the 5G network can dynamically adjust the duration of each time slot based on the service's needs. A data-heavy service might get longer slots, while services needing quick response times, like remote surgery or smart factories, might be allocated shorter slots. This flexibility improves the efficiency and responsiveness of the 5G network.
-  Each radio frame of a duration of 10ms is split into 10 subfarmes each of duration 1 ms
-  Each 1ms sub frame is then spit into slots , the number of slots depend upon the numerology (1 subframe = 2^u slots)
-  Now each slot contains symobls , number of symbols depend on the type of CP used (extended = 12 , normal = 14)

![Screenshot from 2023-12-01 07-45-34](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/24d86347-2109-4397-a84d-55cd126a2d06)

## NUMEROLOGY - SUBCARRIER SPACING 
- Numerology refers to the set of parameters that define the physical layer structure , specifically , the subcarrier spacing , symbol duration , and cyclic prefix

![NR_Numerology_SubCarrierSpacing_38_211_v17_6_0_01](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/a76636d0-bbc0-4e5c-be2d-a20337927a6b)

- Slot length gets different depending on numerology , i.e slot length gets shorter as SCS get swider

![NR_Numerology_SlotLength_38_211_01](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/289d535b-e046-46e7-b0be-a8b2000f5908)
![Screenshot from 2023-12-01 08-02-41](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/682e6a57-e6c3-4db4-9ce7-056f69c935d9)
![NR_Numerology_FrameStructure_u_4__NormalCP_38_211_01](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/073fe071-a486-4b64-8c4c-76e2fef16b43)

## RESOUCE GRID 
- 5G has more flexibility in the duration of different transmissions. The time domain can be altered based on the need. E.g. if a particular activity needs high throughput, it can be scheduled for multiple symbols and if it requires low latency, only fewer symbols will be allocated. 
- The number of Resource Blocks varies with numerology. Resource Block is defined as 12 consecutive subcarriers in the frequency domain. 

![NR_Resource_Grid_01](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/472fd472-fb86-4478-9837-1fbb3f926b11)
![Screenshot from 2023-12-01 08-20-29](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/bf887506-a1b4-4e3c-bbf4-7a5fa5c75fcd)

- The maximum number of Resource blocks for DL and UL are defined below

![Screenshot from 2023-12-01 08-28-27](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/a0aa5a4f-940a-4a2f-ae35-736c7ce9a121)
![Screenshot from 2023-12-01 08-28-27](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/b0aeeb1a-2acc-461b-a3f0-7e4efe16593e)

### RF SPECTRUM
- Channel Bandwidth(CBW) is about [ N_RB x NumOfSubcarrier x SCS + GuardBand x 2 ]
[for estimating RF bandwidth](https://www.sharetechnote.com/html/5G/5G_FR_Bandwidth.html#Spectrum_and_Bandwidth)
- [For calculating RBs](https://www.techplayon.com/nr-resource-block-definition-and-rbs-calculation/)

### MINI SLOTS


## PHYSICAL LAYER PROCESSING

- DCI provides device with nesseccary info and decoding of DL data
- UCI provides scheduler and the HARQ protocol about information at the device
- PBCH carries part of the system info that the devices use to access the network
- PDSCH is the main channel for data transmission to the devices
- PDCCH used for DL control info like scheduling decisions
- PUSCH main channel for data transmission from the device side
- PUCCH used by device for HARQ acknowledment indicating whether the transport block successfully or unsuccessfully
- PRACH used for RACH procedure
  [more on this](https://docs.google.com/document/d/1o37edJ7BEuTi3WOFEtKhZxpHpT97edf81LeTHu4BejE/edit#heading=h.ue6b1lthokz2)
  
![Screenshot from 2023-12-01 14-44-48](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/d0bda608-1402-41be-a8de-1947f71e0b38)

![Screenshot from 2023-12-01 15-15-06](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/cc6f695e-efa1-4c5b-aef6-0d30e86039e7)

## CRC (cyclic redundancy check)
- first we need a mechanism to detect errors on level of transport block
- for this purpose a CRC (cyclic redundancy check) is calculated and added to the [transport block](https://www.techplayon.com/5g-nr-transport-block-size-tbs-calculation/#google_vignette) (a block of data, referred to as a Transport Block (TB))
- In the receiver side this **CRC** can be used to detect any error in the TB level and request retransmission if TB is fully corrupt
- The size of CSC varies
  1. A 24 bit **CRC** is used for payloads larger than 3824 bits
  2. For a smaller payload 16 bit **CRC** is used
  
![Screenshot from 2023-12-01 15-31-52](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/b8f70d35-0877-4370-a16d-04d3a2405558)

## LDPC graph selection 
- Now that we have an error detection mechanism in the TB level lets look into **error correction**
- when it comes to channel coding which is used for **error correction** NR uses **LDPC**(low density parity check)
- The **LDPC** is mainly used for data channels/traffic channels and **polar coding** is used for control channels
- since this is an example of **PDSCH** we will look at **LDPC**
- The **LDPC** uses a parameter called base graph that governs the coding process
- the **LDPC** base graph type is determined by 2 parameters
  1. Size of TB
  2. Coding rate

- NR supports 2 **LDPC** base graph
  1. when the size of TB and coding rate is above a certain threshhold then base graph 1 is used . Base graph 1 has matrix size of 46x68 entries and it is used for large transport blocks or high coding rates
  2. 2nd Base graph with 42x52 is used for small TB or lower coding rates 

![Screenshot from 2023-12-01 15-45-17](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/7a185ee2-8714-4bf5-85c7-968bd329c002)

## CODE BLOCK SEGMENTATION 
- Next the TB can get quite big but the **LDPC** has a maximum code block size to limit the computational complexity
- So the TB greter than that limit has to be segmented into smaller blocks called **code blocks** before the **LDPC coding** can be performed
- So along with selecting **base graph** the TB is segmented into size of **code block** and a **CRC** is added to each **code block**
- This segmentation is nesseccary before **LDPC coding** can be applied cause the TB itself can be too big to perform **LDPC** on it 
-  The **CRC** on code block might seem redundant compared **CRC** that we added in TB level but NR supports retransmiting just the erroneous (incorrect) code block instead of retransmitting the whole TB
-  For this purpose we need to detect errors not only on the whole TB but if it is a small error we can say exactly which code block the error is in so we need an error detection mechanism that is granular to the extent of code block level for this purpose we add CRC to each code block 

![Screenshot from 2023-12-01 16-02-54](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/c9385637-755d-447c-993e-a49c025537ec)

## LDPC coding 
- While the **CRC** helps in error detection , **LDPC** coding helps in error correction
- **Channel Coding** is the process of adding additional bits that makes the information bits ressislient to noise
- Some of the errors can be corrceted without retransmission using channel coding process channel coding uses LDPC coding
- In this step we take each code block and apply LDPC coding to it to improve resiliency and to be able to correct some of the smaller errors

![Screenshot from 2023-12-01 16-13-30](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/a85f8271-36a4-429d-af32-6b9337c15a26)

## RATE MATCHING 
- Not all of the output bits of the LDPC coding step can be transmited in a given transmission interval , so after LDPC coding proccess rate matching takes the coded bits extracts the exact set of bits that can be transmitted in a given transmission interval
-  Rate matching is performed seperataly for each code block

## SCRAMBLING 
- A UE might be hearing multiple gNBs simultaneously
- So how can the UE differentiate the incoming signals into seperate gNBs at very low layer of protocol stack(PHY layer)
- In scarmbling , the block of code is multiplied by a scrambling sequence
- Now the device that knows this sequence can see the info corresponding to the correct gNB as a signal but all the interfaring gNBs will use a different scrambling code so info from them will look like pure noise to the UE

![Screenshot from 2023-12-01 16-24-54](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/5ef638c1-f4fd-4ea1-9807-afd20f73562f)

## MODULATION 
- QPSK , 16QAM , 64QAM and 256QAM in both UL and DL (scroll up)

![Screenshot from 2023-12-01 16-27-25](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/4ed9c4e2-24e6-4a2a-8230-b00dd194c49b)

## LAYER MAPPING 
- NR supports spacial multiplexing meaning it can transmit more than 1 layer of data simulatneously using multiple antenna technologies
- The complex valued modulation symbols that needs to be transmited or mapped on one ore more layers
- For ex 
![Screenshot from 2023-12-01 16-54-14](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/3f12c7c7-b97d-4c8a-81ee-5cd3e305cf7b)

- The incoming symbols are mapped to the corresponding layers so every 4th symbol goes to layer 1 and every 4th symbol goes to layer 2 so on

## ANTENNA MAPPING AND PRECODING
- After mapping data to different layers the next step is to map to corresponding **virtual antenna ports**
- In order for the different data layers to be decoded as if they are different layers on the receivers side they need to be precoded
- the precoding process maps the different numbers of layers into corresponding number of virtual ports using **Precoded matrix**
- The **Precoded matrix** is selected based on what is the current channel condition
- Precoding is the process which helps use the multiple antenna system and the understanding of the channel knowledge to make multiple layers possible

![Screenshot from 2023-12-01 17-02-19](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/9fecceb3-2f87-4432-a481-a3c23d99c8d0)

## RESOURCE AND PHYSICAL ANTENNA MAPPING 
- From the previous step we have the symbols for each virtual antenna port
- The resouce block mapping takes modulation symbols to be transmitted on each antenna port and maps to the set of available **RESOUCRE ELEMENTS** in the set of **RESOURCE BLOCKS** assigned by the map scheduler for current transmission
- The RBs are shared together with **control signals and reference signals**
- The other RBs are used for TBs for actual data transmission
- So the Number of physical antennas is usually larger than Number of vitual antenna blocks
- virtual ports mapping to phyical antenna port is also done in this
- we take the data which mapped to different vitual antenna ports and put them into the right time and frequency RBs corresponse to the decisions made by the schedular and we also put control signals here and map it to physical antenna ports 

![Screenshot from 2023-12-01 17-29-48](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/05928d74-a28f-4eb6-9209-47fff167cfb4)

## OFDM 
- after mapping symbols on physical antenna the symbols are mapped into the OFDM waveform together with corresponding CP 

## SSB (SYNCHRONIZATION SIGNAL BLOCK) 
- SSB contains
  1. Synchronization signal : PSS , SSS
  2. PBCH : PBCH DMRS and PBCH(DATA)
- SSB is transmitted in 4 OFDM symbols in time domain and 240(20RBs) sub carriers in frequency domain
- 1 symbol PSS , 1 symbol SSS and a 2 symbol PBCH
- PSS occupies 1st OFDM symbol and span over 127 sub carriers
- SSS is located in 3rd OFDM symbol and span over 127 sub carriers
- PBCH occupies 2 full OFDM symbols(2nd and 4th) spanning 240 subcarriers and in third OFDM symbol spaning 48 subcarriers below and above SSS totaling to (240 + 48 + 48 + 240) = 576 sub carriers 
- In that PBCH DM-RS occupies 144 REs
- PBCH DATA ( 576-144 = 432 REs)

![64](https://github.com/KRIISHSHARMA/5G-PHY-LAYER/assets/86760658/84fd14cc-8f8f-4414-a03a-58ac5fc1eb11)








