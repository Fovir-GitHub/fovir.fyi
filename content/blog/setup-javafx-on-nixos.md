---
# prettier-ignore
date: 2025-12-11
title: Setup JavaFX on NixOS
description: Introduce how to setup Javafx on NixOS in dev shell, jdtls, and nixvim.
tags:
  - Java
  - Neovim
  - nixvim
---

## Dev Shell

Refer to [NixOS Wiki](https://wiki.nixos.org/wiki/Java#JavaFX_and_Webkit_support), to enable JavaFX support, an override is required:

```nix
jdkWithFX = pkgs.openjdk.override {
  enableJavaFX = true;
};
```

The minimal `flake.nix` looks like:

```nix
{
  description = "Devshell for JavaFX.";
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
  outputs = {
    self,
    nixpkgs,
  }: let
    system = "x86_64-linux";
    pkgs = import nixpkgs {inherit system;};
    jdkWithFX = pkgs.openjdk.override {
      enableJavaFX = true;
    };
  in {
    devShells.${system}.default = pkgs.mkShell {
      buildInputs = [ jdkWithFX ];
    };
  };
}
```

After creating this file, run `nix develop` to enter the dev shell.

## Setup LSP in `nixvim`

Firstly, we need to enable [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig/) in `nixvim` as a framework for LSP.

```nix
plugins.lsp.enable = true;
```

Then, I choose to use [jdtls](https://github.com/eclipse-jdtls/eclipse.jdt.ls) as LSP of Java. Add the following code to enable it in nixvim:

```nix
plugins.lsp.servers.jdtls.enable = true;
```

Now, try to edit a Java file in the dev shell environment, but `jdtls` can not find `JavaFX`. To solve this issue, I use [Gradle](https://github.com/openjfx/samples/tree/master/IDE/Eclipse/Non-Modular/Gradle).

In the same level directory of `flake.nix`, create a file named `build.gradle`, then add the following content:

```groovy
plugins {
  id 'application'
  id 'org.openjfx.javafxplugin' version '0.1.0'
}

repositories {
    mavenCentral()
}

javafx {
    version = "21"
    modules = [ 'javafx.controls', 'javafx.fxml' ]
}
```

> Please ensure the `version` of `javafx` is compatible with the JDK.

Finally, restart the LSP, `jdtls` will find `JavaFX` and provide code completions.

## References

> [NixOS Wiki](https://wiki.nixos.org)
>
> [openjfx/samples](https://github.com/openjfx/samples)
