# AltBeacon Protocol Specification v1.0

AltBeacon is a protocol specification that defines a message format for proximity beacon advertisements. AltBeacon proximity beacon advertisements are transmitted by devices for the purpose of signaling their proximity to nearby receivers. The contents of the emitted message contains information that the receiving device can use to identify the beacon and to compute its relative distance to the beacon. The receiving device may uses this information as a contextual trigger to execute procedures and implement behaviors that are relevant to being in proximity to the transmitting beacon.

Example use cases for proximity beacons include but are not limited to:

* Notifying users of special offers as they visit areas within a department store
* Presenting opportunities to explore additional information about an exhibit to a museum visitor
* Automatically checking a customer in a customer with a restaurants reservation system as the customer arrives at the restaurant

## Design Goals

The development of the AltBeacon specification has been driven by several objectives:

1. Provide a concise proximity advertising message for interchange of proximity information between advertisers and scanners.
1. Maintain compliance with Bluetooth Specification Version 4.0 by utilizing defined advertising PDU and and advertising types.
1. Encourage adoption by all interested parties by avoiding any obvious implementation limitations.
1. Enable the implementation for vendor-specific features if possible.


## Implementation Requirements
Proximity beacon functionality is not limited to single function devices, but can be incorporated as a feature of any device that is Bluetooth Low Energy compliant and which conforms to the requirements defined in _Bluetooth Specification Version 4.0, Volume 0, Part B, Section 4.4 Low Energy Core Configuration or Section 4.5 Basic Rate and Low Energy Combined Core Configuration_.

AltBeacon advertisements may be encapsulated as the payload of a connectable undirected advertising `PDU` (`ADV_IND`) or a non connectable undirected advertising `PDU` (`ADV_NONCONN_IND`) as defined in _Bluetooth Specification Version 4.0, Volume 6, Part B, Section 2.3 Advertising Channel PDU_.

Devices that transmit proximity beacon advertisement packets are referred to as advertisers.  Devices that receive proximity beacon advertisements are referred to as scanners. These roles follow the conventions defined in _Bluetooth Specification Version 4.0, Volume 1, Section 1.2 Overview of Bluetooth Low Energy Operation_.


## AltBeacon Protocol Format

The AltBeacon advertisement makes use of the Manufacturer Specific Advertising Data structure as defined in _Bluetooth Specification Version 4.0, Volume 3, Part C, Section 2.3 Advertising Channel PDU_.

The AltBeacon advertisement is made up of a 1-byte length field, 1-byte type field and two-byte company identifier, as prescribed by the Manufacturer Specific Advertising Data structure format, followed by 24 additional bytes containing the beacon advertisement data.

See the AltBeacon Protocol Data and AltBeacon Protocol Fields as described below for information on the specific fields, their descriptions and accepted values.

## AltBeacon Protocol Diagram


<table>
  <caption>AltBeacon Protocol Format</caption>
  <tbody><tr>
    <th style="border-bottom:none; border-right:none;"><i>Offsets</i></th>
    <th style="border-left:none;">Octet</th>
    <th colspan="8">0</th>
    <th colspan="8">1</th>
    <th colspan="8">2</th>
    <th colspan="8">3</th>
  </tr>
  <tr>
    <th style="border-top: none">Octet</th>
    <th>Bit</th>
    <th style="width:2.6%;">0</th>
    <th style="width:2.6%;">1</th>
    <th style="width:2.6%;">2</th>
    <th style="width:2.6%;">3</th>
    <th style="width:2.6%;">4</th>
    <th style="width:2.6%;">5</th>
    <th style="width:2.6%;">6</th>
    <th style="width:2.6%;">7</th>
    <th style="width:2.6%;">8</th>
    <th style="width:2.6%;">9</th>
    <th style="width:2.6%;">10</th>
    <th style="width:2.6%;">11</th>
    <th style="width:2.6%;">12</th>
    <th style="width:2.6%;">13</th>
    <th style="width:2.6%;">14</th>
    <th style="width:2.6%;">15</th>
    <th style="width:2.6%;">16</th>
    <th style="width:2.6%;">17</th>
    <th style="width:2.6%;">18</th>
    <th style="width:2.6%;">19</th>
    <th style="width:2.6%;">20</th>
    <th style="width:2.6%;">21</th>
    <th style="width:2.6%;">22</th>
    <th style="width:2.6%;">23</th>
    <th style="width:2.6%;">24</th>
    <th style="width:2.6%;">25</th>
    <th style="width:2.6%;">26</th>
    <th style="width:2.6%;">27</th>
    <th style="width:2.6%;">28</th>
    <th style="width:2.6%;">29</th>
    <th style="width:2.6%;">30</th>
    <th style="width:2.6%;">31</th>
  </tr>
  <tr>
    <th>0</th>
    <th>0</th>
    <td colspan="8">AD LENGTH</td>
    <td colspan="8">AD TYPE</td>
    <td colspan="16">MFG ID</td>
  </tr>
  <tr>
    <th>4</th>
    <th>32</th>
    <td colspan="16">BEACON CODE</td>
    <td colspan="16">BEACON ID</td>
  </tr>
  <tr>
    <th>12</th>
    <th>96</th>
    <td colspan="32">BEACON ID (CONTINUED)</td>
  </tr>
  <tr>
    <th>16</th>
    <th>128</th>
    <td colspan="32">BEACON ID (CONTINUED)</td>
  </tr>
  <tr>
    <th>20</th>
    <th>160</th>
    <td colspan="32">BEACON ID (CONTINUED)</td>
  </tr>
  <tr>
    <th>24</th>
    <th>192</th>
    <td colspan="16">BEACON ID (CONTINUED)</td>
    <td colspan="8">REFERENCE POWER</td>
    <td colspan="8">MFG RESERVED</td>
  </tr>
  </tbody>
</table>




## AltBeacon Protocol Fields

Field Name               |  Description                                                                                 | Accepted Values
------------------------ | -------------------------------------------------------------------------------------------- | ---------------
AD LENGTH [MFG SPECIFIC] | Length of the type and data portion of the Manufacturer Specific advertising data structure. | 0x1B
AD TYPE [MFG SPECIFIC]   | Type representing the Flags advertising data structure.                                      | 0xFF
MFG ID                   | The beacon device manufacturer’s company identifier code.                                    | The little endian representation of the beacon device manufacturer’s company code as maintained by the Bluetooth SIG assigned numbers database.
BEACON ADV CODE          | The AltBeacon advertisement code.                                                            | 0xBEAC
BEACON ID                | A 20-byte value uniquely identifying the beacon.                                             | The big endian representation of the beacon identifier
REFERENCE RSSI           | A 1-byte value representing the average received signal strength at 1m from the advertiser.  | A signed 1-byte value from 0 to -127
MFG RESERVED             | Reserved for use by the manufacturer to implement special features.                          | A 1-byte value from 0x00 to 0xFF. Interpretation of this value is to be defined by the manufacturer and is to be evaluated based on the MFG IDENTIFIER value.
