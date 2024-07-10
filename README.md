# ruskel

[![Crates.io](https://img.shields.io/crates/v/libruskel.svg)](https://crates.io/crates/libruskel)
[![Documentation](https://docs.rs/libruskel/badge.svg)](https://docs.rs/libruskel)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Ruskel generates skeletonized outlines of Rust crates. It produces a
single-page representation of a crate's public API with all implementation
omitted, while still rendering syntactically correct Rust. 

Ruskel has two main uses:

- To provide quick access to Rust documentation from the command line.
- To export the full public API of a crate as a single file to pass to LLMs and
  other tools.


## Features

- Generate a skeletonized view of any Rust crate
- Support for local crates and remote crates from crates.io
- Syntax highlighting for terminal output 
- Option to output raw JSON data for further processing
- Configurable to include private items and auto-implemented traits
- Support for custom feature flags


## ruskel command line tool

`ruskel` is the command-line interface for easy use of the Ruskel functionality.

```sh
cargo install ruskel
```

Because Ruskel uses nightly-only features on `cargo doc`, you need to have the
nightly toolchain installed.


### Usage

Basic usage:

```sh
ruskel [TARGET]
```

Where `TARGET` can be a directory, file path, or a module name. If omitted, it defaults to the current directory.

#### Sample Options

- `--raw`: Output raw JSON instead of rendered Rust code
- `--auto-impls`: Render auto-implemented traits
- `--private`: Render private items
- `--no-default-features`: Disable default features
- `--all-features`: Enable all features
- `--features <FEATURES>`: Specify features to enable (comma-separated)
- `--highlight`: Force enable syntax highlighting
- `--no-highlight`: Disable syntax highlighting

For full details, run:

```sh
ruskel --help
```

### Examples

Generate a skeleton for the current project:

```sh
ruskel
```

Generate a skeleton for a specific crate, or a specific path within a crate
from crates.io:

```sh
ruskel serde
ruskel serde::de::Deserialize 
```

Generate a skeleton for at the given path:

```sh
ruskel /my/path
```

Generate a skeleton for the module `foo` under the given path:

```sh
ruskel /my/path::foo
```

Include private items and auto-implemented traits:

```sh
ruskel --private --auto-impls
```


## libruskel library

`libruskel` is a library that can be integrated into other Rust projects to provide Ruskel functionality.

```sh
cargo add libruskel
```

### Usage

Here's a basic example of using `libruskel` in your Rust code:

```rust
use libruskel::Ruskel;

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let rs = Ruskel::new(".")?;
    let rendered = rs.render(false, false)?;
    println!("{}", rendered);
    Ok(())
}
```

Check the [API documentation](https://docs.rs/libruskel) for more details on using the library.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.



