# SXD-Document

An XML library in Rust, modified to add a `no-unsafe` feature flag that avoids use of `unsafe` in the library implementation.

[![crates.io][Crate Logo]][Crate]
[![Documentation][Doc Logo]][Doc]
[![Build Status][CI Logo]][CI]

[Crate]: https://crates.io/crates/sxd-document-no-unsafe
[Crate Logo]: https://img.shields.io/crates/v/sxd-document-no-unsafe.svg

[Doc]: https://docs.rs/sxd-document-no-unsafe
[Doc Logo]: https://docs.rs/sxd-document-no-unsafe/badge.svg

[CI]: https://github.com/nsoiffer/sxd-document-no-unsafe/actions?query=branch%3Amaster
[CI Logo]: https://github.com/nsoiffer/sxd-document-no-unsafe/workflows/Continuous%20integration/badge.svg

## Overview

The project is currently broken into two crates:

1. `document` - Basic DOM manipulation and reading/writing XML from strings.
2. [`xpath`][sxd-xpath] - Implementation of XPath 1.0 expressions.

There are also scattered utilities for playing around at the command line.

[sxd-xpath]: https://github.com/nsoiffer/sxd-xpath-no-unsafe/

## Goals

This project aims to offer a version of the [sxd-document](https://crates.io/crates/sxd-document) library
that does not contain calls to `unsafe`, for users who are constrained to avoid code containing `unsafe`.
Enabling the `no-unsafe` feature results in roughly 15% slower execution in informal benchmarks.
I did _not_ measure any change in the memory usage.
With default features enabled, the compiled code should match Jake Goulding's [original project](https://github.com/shepmaster/sxd-document).

Unfortunately, it was not possible to completely hide the difference between the default build and the `no-unsafe` build.
Both expose `InternedString`, but the `no-unsafe` version requires considering lifetimes.
Most differences are papered over by using the `as_str!`, `as_opt_str!`, and `as_qname!` macros.

I have _not_ updated the documentation.

## Contributing

1. Fork it (<https://github.com/nsoiffer/sxd-document-no-unsafe/fork>)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Add a failing test.
4. Add code to pass the test.
5. Commit your changes (`git commit -am 'Add some feature'`)
6. Ensure tests pass.
7. Push to the branch (`git push origin my-new-feature`)
8. Create a new Pull Request
