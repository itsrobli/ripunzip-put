# ripunzip-put

A tool to unzip files in parallel.

Forked from https://crates.io/crates/ripunzip

This is a Rust library (and command-line tool) which utilises the power of Rust's `rayon`
library to unzip a zip file in parallel. If you're fetching the zip file from a URI, it
may also be able to start unzipping in parallel with the download.

#### Why fork?

Features I need:

- [x] Add support for password unzip. [Diff](https://github.com/google/ripunzip/compare/main...itsrobli:ripunzip-put:feature/password-protected-zip) 
and [issue](https://github.com/google/ripunzip/issues/62)

- [ ] Unzip directly to cloud storage (for very large zip files)

#### Development

`cargo criterion` is used for performance testing, though the
benchmark suite doesn't do a great job of simulating real conditions. In particular please
be aware that this tool is often used on devices with spinny hard disks and very limited
disk write bandwidth, so in different circumstances that may be the limiting circumstance,
or network bandwidth, or CPU time. Please consider the impact of your changes on all these
permutations.

Release procedure:
1. Revise the version number
2. `cargo publish`
3. Retrieve the latest `.deb` file from the latest CI job
4. Declare a new release and tag on GitHub
5. As you make that release, include the `.deb` file as an artifact.

There's also `cargo fuzz` support for comparitive fuzzing against non-parallel unzipping
to try to spot any unforeseen circumstances where we do anything differently. If you
change the core unzipping logic please use this.

#### License and usage notes

<sup>
License

This software is distributed under the terms of both the MIT license and the
Apache License (Version 2.0).

See LICENSE for details.
</sup>

