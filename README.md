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
version = "^0.1"
```

Then bind the library in a source file:

```mach
use zstd;
```


## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for building, testing and the contribution rules.


## License

[MIT](LICENSE)
