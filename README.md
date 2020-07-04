BinaryReader and BinaryWriter from .NET for NodeJS
==============================================================

These utilities provide you with a BufferReader and BufferWriter class with functions similar to the BinaryReader and BinaryWriter .NET classes.\
They also allow you to define a specific endianness!

Basic installation and usage
----------------------------

You can install this package either by using npm or by downloading the source from GitHub and requiring it directly.

To install using npm open your terminal (or command line), make sure you're in your application directory and execute the following command:

    npm install bufferutils

You can then start using the package by requiring it from your application as such:

    var BufferUtils = require('bufferutils');

BinaryReader Class
------------------

### BinaryReader(inputBuffer, isBigEndian, position)

* Initializes a BinaryReader with the specified settings
* inputBuffer can be a `Buffer`, a `string` (text or file path) or a `fd` (file descriptor)
* isBigEndian is a boolean (default: false)
* position set the default position of the reader (default: 0)

* for `fd`, recommanded flags is `r`

### Read(length[, position])

* Reads a specific region of the buffer and advances the current position by the length if a position is not specified

### ReadUInt8()

* Reads a 8 bit unsigned integer from the buffer and advances the current position by 1 byte

### ReadUInt16()

* Reads a 16 bit unsigned integer from the buffer and advances the current position by 2 bytes

### ReadUInt32()

* Reads a 32 bit unsigned integer from the buffer and advances the current position by 4 bytes

### ReadUInt64()

* Reads a 64 bit unsigned integer from the buffer and advances the current position by 8 bytes

### ReadInt8()

* Reads a 8 bit signed integer from the buffer and advances the current position by 1 byte

### ReadInt16()

* Reads a 16 bit signed integer from the buffer and advances the current position by 2 bytes

### ReadInt32()

* Reads a 32 bit signed integer from the buffer and advances the current position by 4 bytes

### ReadInt64()

* Reads a 64 bit signed integer from the buffer and advances the current position by 8 bytes

### Read7BitEncodedInt()

* Reads a 7 bit encoded integer from the buffer

### ReadFloat() or ReadSingle()

* Reads a float from the buffer and advances the current position by 4 bytes

### ReadDouble()

* Reads a double from the buffer and advances the current position by 8 bytes

### ReadByte()

* Reads the next byte into a integer and advances the current position by 1 byte

### ReadBytes(count)

* Reads the specified number of bytes into a new buffer and advances the current position by that number of bytes

### ReadBoolean()

* Reads a boolean from the buffer and advances the current position by 1 byte

### ReadChar()

* Reads the next byte into a string and advances the current position by 1 byte

### ReadChars(count)

* Reads the specified number of bytes into a char array and advances the current position by that number of bytes

### ReadString(count)

* Reads the specified number of bytes into a string and advances the current position by that number of bytes

### ReadInt(count)

* Reads the specified number of bytes into an signed integer and advances the current position by that number of bytes

### ReadUInt(count)

* Reads the specified number of bytes into an unsigned integer and advances the current position by that number of bytes

### Close()

* Close the reader

### Length [Number]

* The length of the initially provided data

### Position [Number]

* The current position (index) of the reader

### IsBigEndian [Boolean]

* The boolean tell if the reader use LittleEndian (false) or BigEndian (true)

### Buffer [Buffer]

* A buffer containing the remaining data from the original buffer

### String [String]

* A string containing the remaining data from the original buffer

BinaryWriter Class
------------------

### BinaryWriter(inputBuffer, isBigEndian, position)

* Initializes a BinaryWriter with the specified settings
* inputBuffer can be undefined, a `Buffer`, a `string` or a `fd` (file descriptor)
* isBigEndian is a boolean (default: false)
* position set the default position of the writer (default: 0)

* for `fd`, recommanded flags is `rs+`

### WriteUInt8(value)

* Writes a 8 bit unsigned integer to the buffer and advances the current position by 1 byte

### WriteUInt16(value)

* Writes a 16 bit unsigned integer to the buffer and advances the current position by 2 bytes

### WriteUInt32(value)

* Writes a 32 bit unsigned integer to the buffer and advances the current position by 4 bytes

### WriteUInt64(value)

* Writes a 64 bit unsigned integer to the buffer and advances the current position by 8 bytes

### WriteInt8(value)

* Writes a 8 bit signed integer to the buffer and advances the current position by 1 byte

### WriteInt16(value)

* Writes a 16 bit signed integer to the buffer and advances the current position by 2 bytes

### WriteInt32(value)

* Writes a 32 bit signed integer to the buffer and advances the current position by 4 bytes

### WriteInt64(value)

* Writes a 64 bit signed integer to the buffer and advances the current position by 8 bytes
* value can be a `number` or a `BigInt`

### Write7BitEncodedInt(value)

* Writes a 7 bit encoded integer to the buffer

### WriteFloat(value) or WriteSingle(value)

* Writes a float to the buffer and advances the current position by 4 bytes

### WriteDouble(value)

* Writes a double to the buffer and advances the current position by 8 bytes

### WriteByte(value)

* Writes a byte to the buffer and advances the current position by 1 byte

### WriteBytes(value)

* Writes the specified bytes to the buffer and advances the current position by the number of bytes
* value can be a `Buffer` or an `array`

### WriteBoolean(value)

* Writes a boolean to the buffer and advances the current position by 1 bytes

### WriteChar(value)

* Writes a char to the buffer and advances the current position by 1 bytes

### WriteChars(value)

* Writes the specified chars to the buffer and advances the current position by the number of chars

### WriteString(value)

* Writes a string to the buffer and advances the position by the length of the string

### WriteInt(value, length)

* Writes a signed integer to the buffer and advances the position by the length

### WriteUInt(value, length)

* Writes a unsigned integer to the buffer and advances the position by the length

### Close()

* Close the writer

### Length [Number]

* The length of the current data buffer

### Position [Number]

* The current position (index) of the writer

### IsBigEndian [Boolean]

* The boolean tell if the reader use LittleEndian (false) or BigEndian (true)

### buffer [Buffer]

* A buffer containing the data written using the class functions

### String [String]

* A string containing the remaining data from the original buffer

Example
-------

```javascript
var {BufferReader, BufferWriter} = require('bufferutils');

var reader = new BufferReader([0x1, 0x2, 0x0, 0x3, 0x0, 0x0, 0x0, 0x4, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x1, 0x2, 0x3, 0x4, 0x5, 0x6]);

console.log(reader.ReadUInt8()); // Will print '1'
console.log(reader.ReadUInt16()); // Will print '2'
console.log(reader.ReadUInt32()); // Will print '3'
console.log(reader.ReadUInt64()); // Will print '4n'
reader.Position = 7;
reader.IsBigEndian = true;
console.log(reader.ReadUInt64()); // Will print '288230376151711744n'
console.log(reader.ReadBytes(6)); // Will print '<Buffer 01 02 03 04 05 06>'
console.log(reader.Position); // Will print '21'
console.log(reader.Length); // Will print '21'

//

var writer = new BufferWriter();

writer.WriteUInt16(65535);
writer.WriteUInt32(0);
writer.WriteInt32(-1);
writer.WriteBytes([5, 4, 3, 2, 1]);

console.log(writer.Buffer); // Will print '<Buffer ff ff 00 00 00 00 ff ff ff ff 05 04 03 02 01>'
console.log(writer.Length); // Will print '15'
```
