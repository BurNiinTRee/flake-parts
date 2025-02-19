
# Flake Parts

_Core of a distributed framework for writing Nix Flakes._

`flake-parts` provides the options that represent standard flake attributes 
and establishes a way of working with `system`.
Opinionated features are provided by an ecosystem of modules that you can import.

`flake-parts` _itself_ has the goal to be a minimal mirror of the Nix flake schema.
Used by itself, it is very lightweight. 

# Why Modules?

Flakes are configuration. The module system lets you refactor configuration
into modules that can be shared.

It reduces the proliferation of custom Nix glue code, similar to what the
module system has done for NixOS configurations.

Unlike NixOS, but following Flakes' spirit, `flake-parts` is not a
monorepo with the implied goal of absorbing all of open source, but rather
a single module that other repositories can build upon, while ensuring a
baseline level of compatibility: the core attributes that constitute a flake.

# Features

 - Split your `flake.nix` into focused units, each in their own file.

 - Take care of [system](https://flake.parts/system.html).

 - Allow users of your library flake to easily integrate your generated flake outputs
   into their flake.

 - Reuse project logic written by others

<!-- end_of_intro -->
<!-- ^^^^^^^^^^^^ used by https://github.com/hercules-ci/flake.parts-website -->

# Getting Started

If your project does not have a flake yet:

```console
nix flake init -t github:hercules-ci/flake-parts
```

# Migrate

Otherwise, add the input,

```
    flake-parts.url = "github:hercules-ci/flake-parts";
```

then slide `mkFlake` between your outputs function head and body,

```
  outputs = inputs@{ flake-parts, ... }:
    flake-parts.lib.mkFlake { inherit inputs; } {
      flake = {
        # Put your original flake attributes here.
      };
      systems = [
        # systems for which you want to build the `perSystem` attributes
        "x86_64-linux"
        # ...
      ];
    };
```

Now you can add the remaining module attributes like in the [the template](./template/default/flake.nix).

# Example

See [the template](./template/default/flake.nix).

# Options Reference

See [flake.parts options](https://flake.parts/options/flake-parts.html)

# Documentation

See [flake.parts](https://flake.parts)
