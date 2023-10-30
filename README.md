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
const ronin = @import("ronin");

pub fn build(b: *std.Build) !void {
    ...

    const ronin_build = ronin.build("rule_name");

    // or

    const ronin_step = ronin.step("rule_name", "A description");

    ...
}
```

[ninja]: https://github.com/ninja-build/ninja
[samurai]: https://github.com/michaelforney/samurai
