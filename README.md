# Debian apt repository

Packages for Debian `forky`, served by GitHub Pages at
`https://ronny-rentner.github.io/debian`. The indices are signed with the key in `key.asc`.

## Packages

- `ghostty`: [Ghostty](https://github.com/ghostty-org/ghostty), with [Debian packaging](https://github.com/ronny-rentner/ghostty/tree/debian/debian)
- `zig0.17`, `zig0.17-dev`: [Zig](https://codeberg.org/ziglang/zig), with [Debian packaging](https://github.com/ronny-rentner/zig/tree/debian/debian)
- `parakeet-cli`, `parakeet-server`: [parakeet.cpp](https://github.com/mudler/parakeet.cpp) from the [ronny-rentner fork](https://github.com/ronny-rentner/parakeet.cpp) with phrase boosting and model handling, with [Debian packaging](https://github.com/ronny-rentner/parakeet.cpp/tree/debian/debian)

## Installing

```sh
sudo curl -fsSL -o /usr/share/keyrings/ronny-rentner.asc https://ronny-rentner.github.io/debian/key.asc
sudo tee /etc/apt/sources.list.d/ronny-rentner.sources <<'EOF'
Types: deb
URIs: https://ronny-rentner.github.io/debian
Suites: forky
Components: main
Signed-By: /usr/share/keyrings/ronny-rentner.asc
EOF
sudo apt update
sudo apt install ghostty
```

## Adding a package

The repository is managed with `reprepro` from the checkout's root. `db/` is reprepro's database and not
committed; a fresh checkout rebuilds it by including the packages again.

```sh
reprepro includedeb forky path/to/package.deb
git add -A && git commit -m "Add package 1.2.3-4" && git push
```

reprepro keeps one version per package: including a newer version removes the older one from `pool/`.
