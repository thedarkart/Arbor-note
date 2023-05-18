# Unit 3: Layer 3, 4 Protection

## Table of contents

- [Unit 3: Layer 3, 4 Protection](#unit-3-layer-3-4-protection)
  - [Table of contents](#table-of-contents)
  - [Invalid packets category](#invalid-packets-category)
    - [Reasons](#reasons)
      - [IPv4](#ipv4)
      - [IPv6](#ipv6)
  - [Rate-based blocking](#rate-based-blocking)
  - [Payload regular expression](#payload-regular-expression)
    - [Payload regular expression](#payload-regular-expression-1)

## Invalid packets category

- Non-configurable, always-on
- Precedence
- Not blocking protection

### Reasons

#### IPv4

- Invalid header (malformed, checksum, short packet)
- Invalid fragmemtation (incomplete, duplicate, too long)
- Invalid protocol (short packet, flag, number)

#### IPv6

- Invalid Extension Header (duplicate, out-of-order, route type 0)
- Maximum transmission unit (MTU) violation
- Bad Options (hop-by-hop, inconsistent)
- Invalid Payload (length)

## Rate-based blocking

- Examining the bit rate and packet rate of traffic per source
- Use profile capture to identify thresholds

## Payload regular expression

### Payload regular expression

- Flexible alternative attack handling to find unique signature 