# Debian apt repository

Packages built from ronny-rentner's forks for Debian `forky`, served by GitHub Pages at
`https://ronny-rentner.github.io/debian`. The indices are signed with the key in `key.asc`.

## Packages

- `ghostty`: Ghostty 1.4.0 with Debian packaging, from [ronny-rentner/ghostty](https://github.com/ronny-rentner/ghostty), branch `debian`
- `zig0.16`, `zig0.16-dev`: Zig 0.16.0, from [ronny-rentner/zig](https://github.com/ronny-rentner/zig), branch `debian`

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
