# HEllo

There are two tables, IVI2VEH and VEH2IVI, specifiying rules for
traffic going from the IVI to the vehicle and from vehicle to IVI.


Each one of the two tables has a number of rules.

Each rule has a numberic ID. Rules are executed in order of ascending IDs.

Each rule has an Frame ID mask and a Frame ID filter, applied
according to the standard CAN bus filter principl:e
http://www.cse.dmu.ac.uk/~eg/tele/CanbusIDandMask.html


ID | IdMask     |   IdFilter | Action          | IdOperand  | DataOperand        |
---|------------|------------|-----------------|------------|--------------------|
1  | 0x00000000 | 0x00000000 | ID_AND-DATA_AND | 0xFFFFFFFF | 0xFFFFFF0000000000 |
2  | 0x000000FF | 0x00000012 | ID_AND-DATA_OR  | 0x00FFFFFF | 0x000000FFFFFFFFFF |
3  | 0x00000FF0 | 0x00000120 | ID_SET-DATA_SET | 0x01234567 | 0x0123456780ABCDEF |
99 | 0x00000000 | 0x00000000 | BLOCK           | 0x00000000 | 0x0000000000000000 |







mask   = 0x00F0;
filter = 0x0070;
input  = 0x002E;


masked_input = (input & mask); // 0x002E & 0x00F0 == 0x0020

if (!masked_input)
	forward(input);

if (masked_input & filter) // 0x0020 & 0x0070 == 0x0020
	forward(input);

drop();
