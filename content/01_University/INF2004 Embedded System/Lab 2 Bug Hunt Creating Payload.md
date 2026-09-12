---
title: Lab 2 Bug Hunt Creating Payload
---
# Background
- The following information is about how the frame is created and what information is contained in each byte.
```C
/* Frame layout on the wire (9 bytes of payload):
 *
 *   +------+------+------------------------+----------+
 *   | 0xAA | LEN  | LEN bytes of payload   | CHECKSUM |
 *   +------+------+------------------------+----------+
 *
 *   LEN       number of payload bytes that follow (must be 9)
 *   payload   the reading_t fields, BIG-ENDIAN, tightly packed:
 *
 *               offset 0..1   sensor_id     (uint16, big-endian -> MSB first)
 *               offset 2      status        (uint8)
 *               offset 3..4   temp_c_x10    (int16, big-endian)
 *               offset 5..8   timestamp_ms  (uint32, big-endian)
 *
 *   CHECKSUM  8-bit sum of every payload byte, truncated to 8 bits.
 *             It does NOT cover the 0xAA or the LEN byte.
 *
 * This layout is the specification. It is correct. The code is not.
 */
```

> [!Note]
> 1. Must start with 0xAA (1 Byte)
> 2. Length of payload bytes (1 Byte)
> 3. Payload (9 Bytes)
> 4. Checksum (1 Byte)
> 
> Payload Breakdown
> - Byte 1 - 2: `sensor_id`
> - Byte 3: `status`
> - Byte 4 - 5: `temp_c_x10`
> - Byte 6 - 9: `timestamp_ms`
> 
> Another note it is stated that we are to use [Big-Endian](https://en.wikipedia.org/wiki/Endianness) Which means the MSB goes first

## Encoding Frame
- Given 4 hex data from the sensor return the full payload
```C
// Given {0x1234, 0x01, 253, 0x0A0B0C0D}
// Return {0xAA, 0x09, 0x12, 0x34, 0x01, 0x00, 0xFD, 0x0A, 0x0B, 0x0C, 0x0D, 0x72}
```

```C
uint8_t frame_encode(const reading_t *r, uint8_t *out)
{
	uint8_t len = FRAME_PAYLOAD; // 9u
	uint8_t sum = 0;
	uint8_t n = 0;
	uint8_t b = 0;
	
	out[n++] = FRAME_SOF; // 0xAA 1st byte
	out[n++] = len;       // 09 2nd byte
	// take note that n++ is post-increment so it takes `n` old value BEFORE incrementing
	// Increment happens AFTER the value is used.
	
	// Getting payload data
	uint16_t id = r->sensor_id;
	uint8_t status = r->status;
	uint16_t temp = r->temp_c_x10;
	uint32_t ts = r->timestamp_ms;
	
	// Creating frame
	b = (id >> 8) & 0xFF;    // Shift right 8, AND 0xFF to get MSB
	out[n++] = b, sum += b;
	b = id & 0xFF;           // LSB
	
	b = status & 0xFF;
	out[n++] = b, sum += b;
	
	b = (temp >> 8) & 0xFF;
	out[n++] = b, sum += b;
	b = temp & 0xFF;
	out[n++] = b, sum += b;
	
	b = (ts >> 24) & 0xFF;   // Since ts is 32bits, we move 24 to find the MSB
	out[n++] = b, sum += b;
	b = (ts >> 16) & 0xFF;
	out[n++] = b, sum += b;
	b = (ts >> 8) & 0xFF;
	out[n++] = b, sum += b;
	b = ts & 0xFF;
	out[n++] = b, sum += b;
	
	out[n++] = sum;
	return n;
}
```

> [!Note]
> Throughout this function we take in a pointer to a buffer called `out` and we are changing it throughout the function, HOWEVER we return `n` to tell the caller how many bytes of the buffer is meaningful.

