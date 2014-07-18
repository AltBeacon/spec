
# AltBeacon Spec

## AltBeacon Advertisement Proposal

The following protocol describes an advertisement by a proximity beacon using a non-connectable, undirected Advertising PDU, `ADV_NONCONN_IND`.

| Bytes  | Name                                 | Value           | Notes
| ------:| ------------------------------------ | --------------- | -------------------------------------------------------
| 0      | AD Length                            | `0x02`          | Length of Flags AD structure in bytes
| 1      | AD Type - Flags                      | `0x01`          | Type of AD structure as Flags type
| 2      | AD Data - Flags                      | `0x1a`          | Flags data LE General Discoverable
| 3      | AD Length                            | `0x1b`          | Length of manufacturer specific data AD structure in bytes
| 4      | AD Type - Manufacturer Specific Data | `0xff`          | Type of AD structure as Manufacturere Specific Data
| 5-6    | AD Data - Company Identifier         | `0x1801`        | Radius Networks company identifier
| 7-8    | AD Data - Proximity Type             | `0xbeac`        | Proximity Beacon Advertisement Type 00
| 9 - 24 | AD Data - Identifier1                | `0xMMNNOOPP...` | Organizational identifier as 16 byte UUID value
| 25-28  | AD Data - Identifier2                | `0xMMNN`        | Beacon Group as 2 byte value
| 27-38  | AD Data - Identifier3                | `0xOOPP`        | Beacon Unit as  2 byte value
| 29     | AD Data - Reference Power            | `0xMM`          | A power measurement as signed byte for beacon device at 1m with a reference device
| 30     | AD Data - Manufacturer Reserved      | `0x00-0x64`     | Reserved for use by manufacturer as specified by company identifier in bytes 5-6
