# gcslib/gcc

C with GCC: compiling, archiving and linking, each a hermetic step,
with Bootlin's pinned toolchains or the host's own compiler.

A GCSL library for pekit, Peios's build tool. Import it as
`github.com/gcslib/gcc`.

## Usage

In `workspace.gcsl`, register its toolchains:

```text
import Toolchain::* from "github.com/gcslib/gcc"
import Toolchain from toolchain

pekitconf = {toolchains = [Toolchain::C gcc_x86_64]}
```

In a build file:

```text
import "github.com/gcslib/gcc"

def build hello() {
    = gcc.link([gcc.compile(file("hello.c"))], output = "hello")
}
```

Without the `pekitconf` line, the rules use the host's own `cc`.

## What it provides

- `compile(src, headers, output, flags)`: the object of one C source.
- `archive(objs, output)`: a static library, made deterministically, so
  that the same objects always give the same bytes.
- `link(objs, libraries, output, flags)`: a program.
- `gcc_x86_64` and `gcc_x86_64_to_aarch64`: Bootlin's GCC for x86-64 and
  for aarch64, both running on x86-64 Linux, each pinned by its SHA-256.
- `musl_x86_64()`: Bootlin's GCC for x86-64 with musl, for static
  programs.

The comments at the top of `rules.gcsl` and `toolchains.gcsl` document each in
full.

## Status

gcslib is new, and its libraries' APIs can still change. Pin the commit you
build with: `pekit lock` does so in `pekit.lock`.

## Licence

MIT. See [LICENSE](LICENSE).
