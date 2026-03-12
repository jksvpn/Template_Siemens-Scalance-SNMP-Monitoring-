## ZabbixTemplate_Siemens-Scalance-SNMP-Monitoring

# Overview
I have taken an existing Cisco SNMP template and added Siemens Scalance OIDs. I started this project due to the need I had for monitoring Siemens Scalance devices, and this is my first project on GitHub, so please excuse any mistakes I may have made

# Discovery Rules
There are no discovery rules in this template for scalance.

# Items collected
Since I created this template from an existing Cisco SNMP template, you should already have items such as 
* Uptime 
* system name 
* system location
* ICMP info 

 | Name | Description | Type |  Keys |
| ---         |   ---      |    --- |  --- |
| Scalance Temperature   | (will work only for scalance switches, FW doesn’t support temperature monitoring)    | SNMP agent (Number unsigned)  | snMspsTemperatureValue |
| Ports Status  | Here you can check the status of the port such as up or down   | SNMP agent (Number unsigned)  | snMspsPort1LinkState (port number change based on the monitoring ports) |
| Port Blocked Reason | Here you monitor when the port is down and reason why it is down  | SNMP agent (Number unsigned)  | snMspsport1blockstate(port number change based on the monitoring ports) |
| Power supply status | Here I am checking only PSU1 status  | SNMP agent (Number unsigned)  | snMspsTrapPowerLine1State |
| Scalance Fault State | To check if scalance in fault state or not  | SNMP agent (Number unsigned)  |snMspsFaultState |


# Triggers

 | Name | Description | Expressions |  
| ---         |   ---      |    --- | 
| Port Status  | Triggers are active when the port status value is other than 9 (Admin disabled port) or 0, (port monitoring not supported) & linkstate = 2 is scalance in fault state)| (last(/Siemens by SNMP/snMspsPort1LinkState)=2 and last(/Siemens by SNMP/snMspsport1blockstate)<>9 and last(/Siemens by SNMP/snMspsport1blockstate)<>0)  | 





			
			
			





