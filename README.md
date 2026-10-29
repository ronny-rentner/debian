# Debian apt repository

Packages for Debian `forky`, served by GitHub Pages at
`https://ronny-rentner.github.io/debian`. The indices are signed with the key in `key.asc`.

## Packages

- `ghostty`: [Ghostty](https://github.com/ghostty-org/ghostty) 1.4.0, with [Debian packaging](https://github.com/ronny-rentner/ghostty/tree/bf478abcd6af02ef5b593e7602db5e5f185fc171/debian)
- `zig0.16`, `zig0.16-dev`: [Zig](https://codeberg.org/ziglang/zig) 0.16.0, with [Debian packaging](https://github.com/ronny-rentner/zig/tree/114d0b992b31468d48197d34a7c138f99184a247/debian)
- `zig0.17`, `zig0.17-dev`: [Zig](https://codeberg.org/ziglang/zig) 0.17.0, with [Debian packaging](https://github.com/ronny-rentner/zig/tree/9a61034f0fcb51ebda6791c3701184090a5f3922/debian)

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
