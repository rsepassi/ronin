# ronin

*Status*: Just starting out...

[Ninja][ninja]-compatible build system written in (and for) Zig, inspired by
[samurai][samurai].

Standalone usage:

```
// processes build.ninja
# ronin
```

Zig-compatible usage:

`build.zig.zon`:

```
.deps = .{
    .ronin = {
        ...
    },
},
```

`build.zig`:

```
// Can run steps defined in build.ninja
const ronin = @import("ronin");

pub fn build(b: *std.Build) !void {
    ...

    const ronin_build = ronin.build("stepname");
    const ronin_step = b.step("stepname", "A description");
    ronin_step.dependOn(&ronin_build.step);

    // or, as a shorthand:

    const ronin_step = ronin.step("stepname", "A description");

    ...
}
```

```
# zig build stepname
```

## Notes

Some thoughts:
* I want to be able to depend on Ronin and then have an *easy* and flexible
  build system. Writing Zig for things that are trivial shell is really painful.
* Use Zig to generate build.ninja? Or embed Wren/Lua to generate it.
* Possibly compromise on full Ninja compatibility and assume that Zig is used
  for the C/C++ bits?

Some things I'd like to eventually have:
* [Bubblewrapped][bwrap] steps
* Packaged shell and utilities (a la BusyBox) written in Zig, to make things
  zig-contained (i.e. only assume a Zig compiler).

[ninja]: https://github.com/ninja-build/ninja
[samurai]: https://github.com/michaelforney/samurai
[bwrap]: https://github.com/containers/bubblewrap
