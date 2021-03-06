# atom

[![Build Status](https://travis-ci.org/rust-syndication/atom.svg?branch=master)](https://travis-ci.org/rust-syndication/atom)
[![Crates.io Status](http://meritbadge.herokuapp.com/atom_syndication)](https://crates.io/crates/atom_syndication)

Library for serializing the Atom web content syndication format.

[Documentation](https://docs.rs/atom_syndication/)

## Usage

Add the dependency to your `Cargo.toml`.

```toml
[dependencies]
atom_syndication = "0.5"
```

The package includes a single crate named `atom_syndication`.

```rust
extern crate atom_syndication;
```

## Reading

A feed can be read from any object that implements the `BufRead` trait or using the `FromStr` trait.

```rust
use std::fs::File;
use std::io::BufReader;
use atom_syndication::Feed;

let file = File::open("example.xml").unwrap();
let feed = Feed::read_from(BufReader::new(reader)).unwrap();

let string = "<feed></feed>";
let feed = string.parse::<Feed>().unwrap();
```

## Writing

A feed can be written to any object that implements the `Write` trait or converted to an XML string using the `ToString` trait.

**Note**: Writing a feed does not perform any escaping of XML entities.

### Example

```rust
use std::fs::File;
use std::io::{BufReader, sink};
use atom_syndication::Feed;

let file = File::open("example.xml").unwrap();
let feed = Feed::read_from(BufReader::new(file)).unwrap();

// write to the feed to a writer
feed.write_to(sink()).unwrap();

// convert the feed to a string
let string = feed.to_string();
```

## Invalid Feeds

As a best effort to parse invalid feeds `atom_syndication` will default elements declared as "required" by the Atom specification to an empty string.

## License

Licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.
