# mach-zstd

<p>
  <a href="https://github.com/briar-systems/mach-zstd/actions/workflows/ci.yml"><img src="https://github.com/briar-systems/mach-zstd/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/briar-systems/mach-zstd?color=FF00FF&labelColor=000000" alt="License"></a>
</p>

**A Mach library for Zstandard (RFC 8878) decompression.**

## Usage

Add the dependency to `mach.toml`:

```toml
[dep.zstd]
git = "https://github.com/briar-systems/mach-zstd"
ref = "branch/dev"
```

Then bind the library in a source file:

```mach
use zstd;
```

The decoder is a streaming state machine in the shape of `std.compress.inflate`. Input comes in chunks of any size and output drains in pieces of any size. A frame whose window exceeds `Limits.max_window` is refused, never truncated, and every buffer comes from the allocator you pass.

```mach
use D: zstd.decode;

val r: res[D.Decoder, D.ZstdError] = D.init(a, D.limits_default());
var d: D.Decoder = r.ok;

# for each chunk of compressed input, drain until it is consumed
val p: res[D.Progress, D.ZstdError] = D.decompress(?d, src, src_len, dst, dst_len);
# p.ok.status is NEED_INPUT, OUTPUT_FULL or DONE, with consumed and written counts

D.dnit(?d);
```

`decompress_into` decodes a whole stream into a buffer of known size, and `decompress_alloc` into a growing vector. Concatenated frames and skippable frames are handled. Dictionaries are not supported.


## Modules

- `zstd.bits` backward and forward bit readers and little-endian helpers
- `zstd.fse` FSE table descriptions, decode tables and the predefined distributions
- `zstd.huffman` literal tree descriptions and the one and four stream decoders
- `zstd.xxhash` XXH64 for the content checksum
- `zstd.decode` frames, blocks, sequences and the streaming API


## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for building, testing and the contribution rules.


## License

[MIT](LICENSE)
