# EasyDRM
DRM scheme for consumer products (water purifiers, food preparation equipment, drinks maker)

# Abstract
This is a low-cost DRM scheme that can be easily applied to consumer products which uses consumable, non-reusable items such as cartridges or filters.
![IMG1631021397](https://user-images.githubusercontent.com/11834016/132353232-47248ba6-55f9-406c-a56b-10205f1e643e.png)
Using a 24C01 EEPROM or other data storage medium (such as 25-seires Serial EEPROM, eMMC, Micro SD card or NFC tag), the chip stores this data:
```
00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F
-----------------------------------------------
AA AA BB BB CC CC CC CC DD DD DD DD EE EE FF FF 

AA: Product code (0x00~0xFF), 2 Bytes
BB: Consumable code (0x00~0xFF), 2 Bytes
CC: Consumable batch or serial number (0x00~0xFF), 4 Bytes
DD: Vendor ID (0x00~0xFF), 4 Bytes
EE: Use counter (0x00~0xFF), 2 Bytes
FF: Checksum of 0x00~0x0D (Checksum-16/CRC-16), 2 Bytes
```

This facilitates both Consumable Batch ID and Vendor ID to enable effective inventory control and product recall if needed. The reader can reject cartridge or consumable if it's in the recall list or blacklist.

Should longer ID or data needs to be stored in the Consumable ID and/or Vendor ID, the data should start with `7F FF` followed by the offset to the data, and the data shall end with a pattern of `FF 00`. For example:
```
00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F
-----------------------------------------------
43 FC 01 AF 7F FF 00 10 7F FF 00 1E 00 01 05 1A 
57 61 74 65 72 20 46 69 6C 74 65 72 FF 00 43 68 
69 6E 61 FF 00 00 00 00 00 00 00 00 00 00 00 00

```
In this example, "Water Filter" is the consumable ID, and "China" is the vendor ID.

# Acceptable Uses
This DRM scheme can be used freely as long as the code that uses this scheme obeys GNU Public License 3.

This DRM scheme may not be used on products such as life-saving equipment (such as insulin pumps).

# License
All parts of this repository is licensed under GPL3 (GNU Public License 3). Any violations to this license will not be tolerated.
