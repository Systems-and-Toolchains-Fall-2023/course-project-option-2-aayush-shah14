# Course Project - MQTT - Aayush Shah

This read me file contains description about the MQTT dataset and its features. This GitHub repository contains all the relevant code and dataset for '18-763 Systems and ToolChains for AI Engineers' course project.
The goal of the course project is to analyze the MQTTset database on Kaggle: https://www.kaggle.com/datasets/cnrieiit/mqttset.

## MQTT Protocol:

MQTT is a protocol for communication between IoT devices. It was invented in 1999 for use in the oil and gas industry. Engineers needed a protocol for minimal bandwidth and minimal battery loss to monitor oil pipelines via satellite.
The MQTT protocol works on the principles of the publish/subscribe model. 

## This dataset:

The scenario for this dataset is related to a smart home environment where 8 sensors retrieve information about temperature, light, humidity, CO-Gas, motion, smoke, door and fan. The sensors send the data to a MQTT broker which is instantiated by using Eclipse Mosquitto, an open-source MQTT broker.
The data pertaining to message transmission between these is collated in CSV files for the training and testing. I have used the reduced version in this project - train70_reduced.csv and test30_reduced.csv. This indicates a 70-30 train-test split. 

## Columns:

There are 34 columns in the dataset. Following is a brief description of each along with some constraints. 

### Columns 1-3 define the TCP features upon which MQTT acts. 

1.	tcp.flags: Flags associated with the TCP (Transmission Control Protocol) packet. Frequent two values: 0x00000018 and 0x00000010. 0x00000018 indicates that both the PSH and ACK flags are set in the TCP header whereas 0x00000010 depicts only ACK. Categorical value hence String type. 

2.	tcp.time_delta: Time delta or time difference between TCP packets. Constraint: Non-negative real values.

3.	tcp.len: Length of the TCP packet. Maximum in the dataset is 32768, which is half of the maximum TCP size of 65535. Constraint: Should always be less than 65535.

### Columns 4-7 specify Connect Acknowledgement part of the package. The connection between Client and Broker is set up through a connect-acknowledgement handshake. ate the connection by sending a CONNECT message to the MQTT broker. The broker confirms that a connection has been established by responding with a CONNACK message. Both the MQTT client and the broker require a TCP/IP stack to communicate. 

4.	mqtt.conack.flags: MQTT Connect Acknowledgment flags. This is full of zeros indicating a succesful connection. 

5.	mqtt.conack.flags.reserved: Reserved flags in MQTT Connect Acknowledgment. The value of this is always set to 0. 

6.	mqtt.conack.flags.sp: MQTT Connect Acknowledgment flags for Session Present. The value of this is also always set to 0.

7.	mqtt.conack.val: MQTT Connect Acknowledgment value. Constraint: should be between 0 to 5. Following is what each value depicts. 

0x00: Connection Accepted
0x01: Connection Refused, unacceptable protocol version
0x02: Connection Refused, identifier rejected
0x03: Connection Refused, server unavailable
0x04: Connection Refused, bad username or password
0x05: Connection Refused, not authorized

### Columns 8-15 contain various flags for different connection scenarios. They are binary variables (either 0 or 1) except mqtt.conflags, which is combined connect flags. 

8.	mqtt.conflag.cleansess: MQTT Connect flags for Clean Session. Constraint: 0 or 1. 

9.	mqtt.conflag.passwd: MQTT Connect flags for Password. Constraint: 0 or 1. 

10.	mqtt.conflag.qos: MQTT Connect flags for Quality of Service (QoS). Constraint: 0 or 1. 

11.	mqtt.conflag.reserved: Reserved flags in MQTT Connect. Constraint: 0 or 1. 

12.	mqtt.conflag.retain: MQTT Connect flags for Retain. Constraint: 0 or 1. 

13.	mqtt.conflag.uname: MQTT Connect flags for Username. Constraint: 0 or 1. 

14.	mqtt.conflag.willflag: MQTT Connect flags for Will Flag. Constraint: 0 or 1. 

15.	mqtt.conflags: Combined MQTT Connect flags of the above values.

16.	mqtt.dupflag: MQTT Duplicate Publish flag. Constraint 0 or 1. 

17.	mqtt.hdrflags: MQTT Header Flags.

18.	mqtt.kalive: MQTT Keep Alive value. Keep Alive in MQTT is a flag that defines a time interval in seconds during which a client shall notify an MQTT broker that the connection is alive.

19.	mqtt.len: Length of MQTT packets. Max value in the dataset is 692 but theoretical maximum length of MQTT packet is 256 MB. 

20.	mqtt.msg: MQTT message content.

21.	mqtt.msgid: MQTT Message ID.

22.	mqtt.msgtype: MQTT Message Type. Integer values representing MQTT Message Types (e.g., 1 for CONNECT, 2 for CONNACK). 

23.	mqtt.proto_len: Length of the MQTT Protocol Name. Basically it is 4 when protocol name is MQTT, since it has 4 letters. Most of the values are 0.

24.	mqtt.protoname: MQTT Protocol Name. It is either 0 or string 'MQTT'. This seems redundant hence can be dropped. 

25.	mqtt.qos: Quality of Service (QoS) for MQTT messages. Integer values representing MQTT Message Types (e.g., 1 for CONNECT, 2 for CONNACK). In this dataset it is either 0 or 1.

26.	mqtt.retain: MQTT Retain flag. Constraint: 0 or 1. 

27.	mqtt.sub.qos: MQTT Subscribe Quality of Service. All values are 0, can be dropped.

28.	mqtt.suback.qos: MQTT Subscribe Acknowledgment Quality of Service. All values are 0, can be dropped. 

29.	mqtt.ver: MQTT Protocol Version. Goes from 0 to 4. 

### Columns 30-33 specify the Will messages. This pertains to "Last Will and Testament" mechanism that allows an MQTT client to specify a message that the broker will publish on behalf of the client in the event of an unexpected or unclean client disconnection. It is a feature designed to handle scenarios where a client may disconnect abruptly or unexpectedly without sending a proper "DISCONNECT" message to the broker.
This scenario seems rare, hence all the values in these columns are 0. These columns can be dropped. 

30.	mqtt.willmsg: MQTT Will Message.

31.	mqtt.willmsg_len: Length of the MQTT Will Message.

32.	mqtt.willtopic: MQTT Will Topic.

33.	mqtt.willtopic_len: Length of the MQTT Will Topic.

34.	target: The target, which is the type of attack in this case. The types of attack in the dataset are: legitimate, dos, bruteforce, malformed, slowite.

50% of the values are legitimate, which means the network is not undergoing an attack and is legitimate. 
39% of the values are dos, indicating denial of service type of attack. 
11% are the rest. 


## References: 
The un-abbreviated name of each column was generated from ChatGPT after which further research was done from variety of sources to write the description and constraints:

1) https://aws.amazon.com/what-is/mqtt/
2) http://www.steves-internet-guide.com/mqttv5-connect-and-connack-messages-overview/
3) http://www.steves-internet-guide.com/mqtt-protocol-messages-overview/
4) https://www.emqx.com/en/blog/mqtt-5-0-control-packets-01-connect-connack

