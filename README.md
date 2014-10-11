nmotools
========

3DVIA .nmo assets extractor

.nmo binary file format specification
-------------------------------------

The first 64 bytes contain the header

* Bytes 0..7: "Nemo Fi" signature, including trailing zero
* Bytes 8..63: 14 int32 fields - date, crc, plugin1, plugin2, flags, int32 compcsz, objcsz, objsz, addpath, int32 componentsCount, objectsCount, zero, version, componentsSize

Directly after this data there is compcsz bytes of component records (componentsCount records). If componentsSize!=compcsz, those compczs bytes are zlib-compressed.

Component record format
-----------------------

* Bytes 0..16: 4 int32 fields - id, componentType, offset, nameLength
* Bytes 16..16+nameLength - string name (including trailing zero)

Directly after this there is binary data containing objects. If objcsz!=objsz, next objcsz bytes are zlib-compressed.

See https://github.com/yesterday/Syberia for details (the oldsource directory).
