nmotools
========

3DVIA .nmo assets extractor

.nmo binary file format specification
-------------------------------------

The first 64 (HeaderSize) bytes contain the header

* Bytes 0..7: "Nemo Fi" signature, including trailing zero
* Bytes 8..63: 14 int32 fields - date, crc, plugin1, plugin2, flags, int32 compcsz, objcsz, objsz, addpath, int32 componentsCount, objectsCount, zero, version, componentsSize

Directly after this data there is compcsz bytes of component records (componentsCount records). If componentsSize != compcsz, those compczs bytes are zlib-compressed.

Component record format
-----------------------

* Bytes 0..16: 4 int32 fields - id, componentType, offset, nameLength
* Bytes 16..16+nameLength - string name (including trailing zero)

Known component types are:

OBJECT(1), PARAMETERIN(2), PARAMETEROPERATION(4), STATE(5),
BEHAVIORLINK(6), BEHAVIOR(8), BEHAVIORIO(9), RENDERCONTEXT(12),
KINEMATICCHAIN(13), SCENEOBJECT(11), OBJECTANIMATION(15), ANIMATION(16),
KEYEDANIMATION(18), BEOBJECT(19), DATAARRAY(52), SCENE(10), LEVEL(21),
PLACE(22), GROUP(23), SOUND(24), WAVESOUND(25), MIDISOUND(26),
MATERIAL(30), TEXTURE(31), MESH(32), PATCHMESH(53), RENDEROBJECT(47),
ENTITY_2D(27), SPRITE(28), SPRITETEXT(29), ENTITY_3D(33), GRID(50),
CURVEPOINT(36), SPRITE3D(37), CURVE(43), CAMERA(34), TARGETCAMERA(35),
LIGHT(38), TARGETLIGHT(39), CHARACTER(40), OBJECT_3D(41), BODYPART(42),
PARAMETER(46), PARAMETERLOCAL(45), PARAMETERVARIABLE(55), PARAMETEROUT(3),
INTERFACEOBJECTMANAGER(48), CRITICALSECTION(49), LAYER(51), PROGRESSIVEMESH(54),
SYNCHRO(20), POINTCLOUD_3D(56), VIDEO(57), MAXCLASSID(58),
OBJECTARRAY(80), SCENEOBJECTDESC(81), ATTRIBUTEMANAGER(82), MESSAGEMANAGER(83),
COLLISIONMANAGER(84), OBJECTMANAGER(85), FLOORMANAGER(86), RENDERMANAGER(87),
BEHAVIORMANAGER(88), INPUTMANAGER(89), PARAMETERMANAGER(90), GRIDMANAGER(91),
SOUNDMANAGER(92), TIMEMANAGER(93), VIDEOMANAGER(94), CUIKBEHDATA(-1)

Directly after this there is binary data containing objects. If objcsz != objsz, next objcsz bytes are zlib-compressed.

Object binary data format
-------------------------
Object names and offsets are in the components record. Objects start from offset 0.
Object sizes are relative, excluding the first and the last records.
The first object size is offset-componentsSize-HeaderSize.
The last object size is objsz - offset + componentsSize + HeaderSize.
The first object name is always "PARAMETEROPERATION", other names are shifted by one.

Texture object format
---------------------



See https://github.com/yesterday/Syberia for textures and other object formats.
