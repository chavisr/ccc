---
name: nixit
description: Generate flake.nix for project dependency management using Nix
disable-model-invocation: false
---

# Purpose
Analyze the codebase and create a `flake.nix` file to manage all project dependencies using Nix flakes. Always use the unstable nixpkgs repository for the latest packages.

# Core Requirements
1. **Codebase Analysis**: Thoroughly examine the project to detect:
   - Programming languages used
   - Package managers and dependency files
   - Build tools and frameworks
   - Development tools needed
   - Runtime dependencies

2. **Nixpkgs Repository**: ALWAYS use `nixpkgs-unstable`
   ```nix
   inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixpkgs-unstable";
   ```

3. **Shell Hook**: ALWAYS include this shellHook in the devShells:
   ```nix
   shellHook = ''
     export PS1="(nix) $PS1"
   '';
   ```

# Detection Strategy

## Language/Framework Detection
Look for these indicator files:
- **Python**: `requirements.txt`, `pyproject.toml`, `setup.py`, `Pipfile`, `*.py`
- **Node.js**: `package.json`, `package-lock.json`, `yarn.lock`, `*.js`, `*.ts`
- **Rust**: `Cargo.toml`, `Cargo.lock`, `*.rs`
- **Go**: `go.mod`, `go.sum`, `*.go`
- **Ruby**: `Gemfile`, `Gemfile.lock`, `*.rb`
- **Java**: `pom.xml`, `build.gradle`, `*.java`
- **C/C++**: `Makefile`, `CMakeLists.txt`, `*.c`, `*.cpp`, `*.h`
- **Shell**: `*.sh`, `*.bash`

## Dependency Analysis
- Parse package manager files to identify required packages
- Map dependencies to Nix package names (common mappings below)
- Include language-specific package managers (pip, npm, cargo, etc.)
- Add development tools (linters, formatters, LSPs)

# Flake.nix Template Structure

```nix
{
  description = "Development environment for [PROJECT_NAME]";

  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixpkgs-unstable";
    flake-utils.url = "github:numtide/flake-utils";
  };

  outputs = { self, nixpkgs, flake-utils }:
    flake-utils.lib.eachDefaultSystem (system:
      let
        pkgs = nixpkgs.legacyPackages.${system};
      in
      {
        devShells.default = pkgs.mkShell {
          buildInputs = with pkgs; [
            # Add detected packages here
          ];

          shellHook = ''
            export PS1="(nix) $PS1"
          '';
        };
      }
    );
}
```

# Common Package Mappings

## Python Projects
```nix
buildInputs = with pkgs; [
  python311          # or python310, python312
  python311Packages.pip
  python311Packages.virtualenv
  # Add based on detected tools:
  python311Packages.pytest
  python311Packages.black
  python311Packages.flake8
  python311Packages.mypy
];
```

## Node.js Projects
```nix
buildInputs = with pkgs; [
  nodejs_20         # or nodejs_18, nodejs_22
  nodePackages.npm  # or yarn, pnpm
  nodePackages.typescript
  nodePackages.eslint
  nodePackages.prettier
];
```

## Rust Projects
```nix
buildInputs = with pkgs; [
  rustc
  cargo
  rustfmt
  rust-analyzer
  clippy
];
```

## Go Projects
```nix
buildInputs = with pkgs; [
  go
  gopls
  gotools
  golangci-lint
];
```

## Shell Script Projects
```nix
buildInputs = with pkgs; [
  bash
  shellcheck
  shfmt
];
```

## C/C++ Projects
```nix
buildInputs = with pkgs; [
  gcc
  cmake
  gnumake
  clang-tools
  gdb
];
```

# Multi-Language Projects
For projects using multiple languages, combine packages:
```nix
buildInputs = with pkgs; [
  # Language runtimes
  python311
  nodejs_20

  # Build tools
  gnumake
  cmake

  # Version control
  git

  # Utilities
  jq
  curl
];
```

# Additional Considerations

## System Libraries
Include system libraries if needed:
```nix
buildInputs = with pkgs; [
  # ... other packages
  openssl
  zlib
  libffi
  postgresql
  sqlite
];
```

## Environment Variables
Add environment variables in shellHook if needed:
```nix
shellHook = ''
  export PS1="(nix) $PS1"
  export LD_LIBRARY_PATH="${pkgs.lib.makeLibraryPath [ pkgs.openssl ]}"
  export PKG_CONFIG_PATH="${pkgs.openssl.dev}/lib/pkgconfig"
'';
```

## Common Development Tools
Consider including:
```nix
buildInputs = with pkgs; [
  git
  vim
  curl
  wget
  jq
  ripgrep
  fd
  tree
];
```

# Workflow
1. **Analyze**: Use Glob and Read tools to scan the project
2. **Detect**: Identify languages, frameworks, and dependencies
3. **Map**: Convert dependencies to Nix packages
4. **Generate**: Create flake.nix with appropriate packages
5. **Verify**: Ensure shellHook and nixpkgs-unstable are included
6. **Explain**: Describe what was detected and included

# Output Format
After creating flake.nix:
1. List detected languages and frameworks
2. List key dependencies identified
3. List Nix packages included
4. Provide commands to use:
   ```bash
   nix develop    # Enter the development shell
   nix flake show # Show flake outputs
   ```

# Important Notes
- ALWAYS use `nixpkgs-unstable` for the latest packages
- ALWAYS include the shellHook: `export PS1="(nix) $PS1"`
- Be comprehensive in package detection
- Include both runtime and development dependencies
- Add language-specific tools (LSPs, linters, formatters)
- Consider system libraries the project might need
