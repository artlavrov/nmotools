nmotools
========

3DVIA .nmo assets extractor

.nmo file format
----------------

1) 64-byte header, including "Nemo Fi" signature:

* string "Nemo Fi"\0 (8 bytes)
* int date, crc, plugin1, plugin2, flags;
* int compcsz, objcsz, objsz, addpath;
* int componentsCount, objectsCount, zero, version, componentsSize
* if componentsSize!=compcsz, next compczs bytes are compressed (zlib)
* if objcsz!=objsz, next objcsz bytes are compressed (zlib)

2) Components (may be compressed)

* object header:
* int id, componentType, offset, nameLength
* string name (nameLength bytes)

3) Objects

To be continued.

See https://github.com/yesterday/Syberia for details.
