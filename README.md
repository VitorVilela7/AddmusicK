# AddmusicK

![Travis CI](https://travis-ci.org/HertzDevil/AddmusicK.svg?branch=master)

You saw this coming!

This repository is based on AddmusicK version 1.0.5. (The new 1.1.0 beta will not be considered at this moment, but some of the changes planned / implemented here might be ported over there.) Changes to existing code are marked with `// // //`.

#### Namespaces
- `AMKd`: The top-level namespace for all new classes. "AMKd" is not the name of this fork; there is no name yet.
  - `MML`: Classes related to parsing text files.
    - `Lexer`: Classes that extract tokens.
  - `Music`: Classes that deal with compile-time music data representation.
  - `Binary`: Classes related to outputting music data, and things exclusive to SMW.
    - `ChunkNSPC`: Binary command representations from the original N-SPC sound engine.
    - `ChunkAMK`: Binary command representations added in Addmusic.
  - `Utility`: Other things.

#### Programming stuffs

- [x] Replace `boost::filesystem` with `std::experimental::filesystem`
- [ ] Remove VS-exclusive bloat
- [ ] Decompose pretty much everything in `Music.cpp`
- [ ] `AMKd::Music::Action` and `AMKd::Binary::Command` classes
- [ ] Bring in the `Chunk` classes I wrote a while ago (originally for 0CC-FT) (maybe)
- [x] Makefiles
- [ ] Better makefiles (maybe)

#### Compiler stuffs

- [ ] Run AMK from anywhere as long as it is available in `$PATH`
- [ ] Conditional compilation for both sound driver and music data
- [ ] Makefile / Ruby script for inserting music into SMW
- [x] Make AddmusicK's core compiler cross-platform
- [ ] Single separate program to remove any old music data
- [ ] Merge duplicate label loops and remote code definitions

#### MML stuffs

- [x] Separate `o`/`l`/`h`/`q` states for each track
- [ ] Key signature and full accidental support
- [ ] Legible names for all commands
- [ ] Track multiplexing (e.g. `#0123`)
- [ ] N-SPC block support
- [ ] Globally defined patterns
- [ ] `#include` directive, this allows for example core instruments to be defined solely using MML
- [ ] Using label loops and remote code before they are defined

#### Things that should die (and might irreversibly break some MMLs)

- Hex validation, there is no reason to once all commands have names
- Whitespace requirements, missing post-conditions, case-insensitivity etc.
- Drop support for everything below `#amk 2`

#### Things that have actually been added

- There can be spaces between `#` and the preprocessor directive identifier
- full nesting of `#ifdef` and friends for both music and sound effects
- `#if` produces false instead of failing if the preprocessor constant is not defined
- `#else`, `#elseif`
- `#error` (mentioned in the doc but never really worked)
- `#dumper` field

#### Things that already died

- `|` command used for bypassing hex validation, it is now a no-op (since there is no guarantee bytes already placed with `$` will be inserted verbatim)
- `#define` and friends no longer accept arguments on a different line
- Replacement macros are still allowed but each result must form complete tokens (tokens cannot cross macro boundaries)
- Hex commands will become exactly identical to plain-text equivalents
- `$DD` no longer accepts a note as its last parameter, it never worked properly and I have never seen anyone using it
