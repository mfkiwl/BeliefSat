# BeliefSat
BeliefSat is a 2p-PocketQube standard student nano-satellite being developed by the undergraduate students of [***K.J.Somaiya Institute of Engineering and Information Technology, Sion, Mumbai*** .](https://kjsieit.somaiya.edu/en) The satellite itself is a sub-part of team's proposal under [PS4-Orbital platform program](https://www.isro.gov.in/update/15-jun-2019/announcement-of-opportunity-ao-orbital-platform) of ISRO, wherein, team aims to demonstrate indegenously developed technologies for PocketQube standard nano-satellites. As a part of this demonstration, **BeliefSat** will be launched out of **SomaiyaPod** which is a Pocketqube standard deployer being indegenously developed at the institute. The unique construction technique, combination of COTS components for communication, on-board computer and power sub-systems , together constitute of **SomaiyaPQBus**, around which the satellite is being made, is also one of the technologies that the team wants to demonstrate and open-source to enable use by future missions.

## So what will BeliefSat do in space and what results it will give?
1. If it is successfully deployed out of the SomaiyaPod and completes startup procedure (it will be dead inside the Pod and will only get power after it is out of pod)and then sends a beacon; it reliability of both deployer and the design of the satellite will be confirmed.
2. Every 30 seconds or 1 minute (depending on which mode it is in currently), it will send a telemetry packet, which will have values from different COTS sensors. The team aims to project the activity of telemetry reception as a way of involving more students in to Software Defined Radio and RF in general.
3. It will have a functionality as of a amateur-radio digipeater. Which means if you hold a proper Amateur radio license then you can send a 42 character message (including the spaces) to the satellite and the satellite will repeat it (after delay of upto 10 seconds depending on other important processes running on-board). Making it a utility for Amateur radio community.
4. There is a COTS 2MP colour Camera onboards, which can be activated either for single snapshot by a command or multiple snapshots once evey 10 min. These captured snaps will be sent in SSDV i.e. Slow Scan Digital Video format, which is a famous format used by amateur radio community for transmitting images. Thus will also contribute as a service to amateur radio community. However, anyone with COTS radio receiver modules and software, can recieve the images and thus they will also help attracting more young students towards Amateur radio by giving a hint of exiting world of amateur radio.
5. If the satellite is able to operate for more than 3 months while responding to the commands and sending the health data at proper intervals, it will prove the reliablity of the unique design and set of COTS hardware used. Thus future mission could use flight proven hardwares for communication and power generation. 
6. As the satellite doesn't have attitutde stabilization system (apart from a magnet parallel to antennas to orient them in N-S direction), all the sensor readings taken and images captured will be the ones in random orientation. For some this may look like useless thing, but it may actually serve a very useful puspose. The captured images could be analysed and a rough estimation of orientation of the satellite can be determined, then this estimation could be feed along with sensor readings at the instant of capturing the images to a machine learning algo to develop a model of orientation w.r.t. the sensor readings. Once a large no. of data points are avaialble, the generated model will be able to be used in future missions along with COTS sensors to reduce complexity and cost involved in ***Attitude Determination and Control*** subsystem.   

## Dimenssions, drawings and mass

## How is it powered?
The satellite is powered by AltaDevices Single Juntion cells ([which unfortunately are out of buisness as of date of writing](https://pv-magazine-usa.com/2019/12/31/shutdown-continues-at-hanergy-owned-alta-devices-high-efficiency-pv-pioneer/)). Each of these cell produce 0.25W power when illumniated at intensity of 1000W/m^2. There are 4 such cells on long sides and 2 on shorter sides. So when illuminated, satellite may produce 0.5W watt/1watt/>1W depending on the orientation. The power remaining after being used is then stored in 2 parallely connected [2600mah Samsung 18650 batteries](https://robokits.co.in/batteries-chargers/samsung-premium-li-ion-battery/3.7v-samsung-li-ion-batteries/samsung-icr-18650-26j-2600mah-li-ion-cell-original?gclid=CjwKCAjwltH3BRB6EiwAhj0IUHaLyAB-D4SHw_PhNjM4cJyQy68a7cGyKCsCMS-I6JLJSGFChlp92BoC6-4QAvD_BwE). [SPV1040](https://www.st.com/en/power-management/spv1040.html) is used on every panel for maximum power point tracking and giving regulated voltage from the solar cells. The choice of SPV1040 was made based on flight history in [FossaSat-1](https://github.com/FOSSASystems/FOSSASAT-1). Now that AltaDevices cells won't be available in market, team will also be making one prototype with [SM141K06L by IXYS](https://www.digikey.com/product-detail/en/ixys/SM141K06L/SM141K06L-ND/9990462) and will be publishing test results for it too. Along with other things, Every solar panel has a [INA219](https://www.ti.com/product/INA219) current sensor and [OPT3001](https://www.ti.com/lit/ds/symlink/opt3001.pdf?ts=1593144788653&ref_url=https%253A%252F%252Fwww.google.com%252F). Making a solar panel a complete module.

## How does it communicate?

***Transciever Specs***

 * **Name :** [LORA1268F30](https://www.nicerf.com/product_193_312.html)
 * **Frequency :** Yet to be coordinated by [IARU](https://www.iaru.org/) but will be in UHF HAM Band
 * **Modulation :** MSK (FSK with Fdev= 0.25*data_rate)
 * **Output Power :** 1W in Normal mode and 0.5W while in Safe mode to save power
 * **Reciever Sensitivity :** -123 dbm @1.2kbps and bw=20khz (As per datasheet, observed sensititvity yet to be calculated)

***Antenna***

Dipole made from measuring tape, which is in folded state during launch. Once in orbit, fishing cord which holds the antenna in folded position, is burnt by heating a resistor around which it is tied.

***Link Budget***

* **Orbit Height :** 500 Km (proposed, may vary as per allocation by launch provider)
* **Slant Range at 15 degree elevation :** 1408 Km (approximately)
* **Free Space Path Loss at this distance :** 148.2 dbm 
* **Received power neglecting mismatch,connector,atmospheric, pointing and polarization losses and receiving and transmitting antenna gains :** -118.2/121.2 (op= 30/27dbm)
* **Note :** A good directional antenna at receving groundstation (e.g. a 6 element yagi, plans for which will be released soon) can ensure the above mentioned losses are made up for and the signals can be received at even lower angles. However, to ensure best performance, circular polarized antennas copuled with a good LNA (e.g. [LNA4ALL](http://lna4all.blogspot.com/)) mounted over a Azimuth-Elevation antenna rotator (e.g. [Satnogs rotator](https://wiki.satnogs.org/SatNOGS_Rotator_v3)/[Sarcnet Rotator](https://www.sarcnet.org/rotator-mk2.html#RotatorMk2a)/[Yaesu G5500](https://www.yaesu.com/indexVS.cfm?cmd=DisplayProducts&ProdCatID=104&encProdID=79A89CEC477AA3B819EE02831F3FD5B8)/[WRAPS portable antenna rotator](https://ukamsat.files.wordpress.com/2013/12/wraps-mark-spencer-wa8sme-qst-jan-2014-copyright-arrl.pdf)) is recommended.
