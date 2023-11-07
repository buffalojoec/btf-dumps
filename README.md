# BTF Dumps

Inspecting ELF files from Cargo builds.

On MacOS, Cargo won't build ELF files by default when running `cargo build`.
Instead, the file will be of type `Mach-O`, which is an `arm64` Mac-specific
executable.

ELF files are produced by `cargo build` by default on Linux operating systems,
so I've opted to use Docker for now.

I will record the steps to link MacOS architecture with a target Linux
architecture for Cargo builds and ELF file inspections, just not now.

## Sampling ELF Files

Use Docker to spin up a Linux Rust container.

```
docker run -it -v $(pwd)/elf-project:/elf-project rust
cd elf-project
cargo build --release
```

The ELF file will be located at `target/release/elf_project`.

| Command | Description |
| :------ | :---------- |
| `readelf -h <elf>` | ELF file header |
| `readelf -l <elf>` | Program headers |
| `readelf -S <elf>` | Section headers |
| `readelf -g <elf>` | Section groups |
| `readelf -t <elf>` | Section details |
| `readelf -e <elf>` | Headers |
| `readelf -s <elf>` | Syms |