nmotools
========

3DVIA .nmo assets extractor

.nmo file format
----------------

1) 64-byte header, including "Nemo Fi" signature:

* 8 bytes, string "Nemo Fi"
* int32 date, crc, plugin1, plugin2, flags
* int32 compcsz, objcsz, objsz, addpath
* int32 componentsCount, objectsCount, zero, version, componentsSize

2) Components

if componentsSize!=compcsz, next compczs bytes are compressed (zlib)

* int32 id, componentType, offset, nameLength
* string name (nameLength bytes)

3) Objects

if objcsz!=objsz, next objcsz bytes are compressed (zlib)

To be continued.

See https://github.com/yesterday/Syberia for details.
