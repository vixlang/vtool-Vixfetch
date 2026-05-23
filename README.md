# vixfetch

A simple system information fetch tool written in the **Vix programming language**, inspired by [neofetch](https://github.com/dylanaraps/neofetch) and [vfetch](https://github.com/0xA672/vfetch).

![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)

## Features

- **System Information Display**: Shows OS, kernel, memory usage, disk usage, and Vix compiler version
- **Cross-platform Support**: Works on Linux, macOS, and Windows (primarily designed for Unix-like systems)
- **Simple & Lightweight**: Minimal dependencies, uses only C standard library interop
- **Clean Output**: Plain text display with ASCII art logo

## Installation

### Prerequisites

- **Vix Compiler** (`vixc`) installed
- **Unix-like environment** (Linux, macOS, or WSL on Windows)

### Build from Source

```bash
# Clone the repository
git clone https://github.com/vixlang/vixfetch.git
cd vixfetch

# Compile vixfetch
vixc vixfetch.vix -o vixfetch

# Run the program
./vixfetch
```

## Usage

Simply run the compiled binary:

```bash
./vixfetch
```

### Example Output

```
 __      __  _        
 \ \    / / (_)       
  \ \  / /   _  __  __
   \ \/ /   | | \ \/ /
    \  /    | |  >  < 
     \/     |_| /_/\_\
                      
                      

vixfetch - Vix Language System Info
  ───────────────────────────────
Language: Vix
Compiler: vixc
Architecture: x86_64

System Commands Output:
  ───────────────────────────────

[OS Information]
Linux hostname 6.6.114.1-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux

[Memory Usage]
               total        used        free      shared  buff/cache   available
Mem:           7.6Gi       1.4Gi       4.0Gi        52Mi       2.5Gi       6.3Gi
Swap:          2.0Gi       3.0Mi       2.0Gi

[Disk Usage]
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdd       1007G  130G  827G  14% /

[Vix Environment]
  ───────────────────────────────
Version: Vix Compiler 0.1.0_rc1_2 (Beta_26.01.01) by:Mincx1203 Copyright(c) 2025-2026

██████
```

## How It Works

`vixfetch` demonstrates key features of the Vix language:

### 1. C Standard Library Interoperability

Vix's standard library is minimal, so it uses `extern "C"` to call C functions:

```vix
extern "C"
{
    fn printf(format: ptr, ...) -> i32
    fn system(cmd: ptr) -> i32
}
```

### 2. System Command Execution

Instead of built-in APIs, it executes shell commands to gather system information:

- **OS Info**: `uname -a`
- **Memory Usage**: `free -h`
- **Disk Usage**: `df -h /`
- **Compiler Version**: `vixc --version`

### 3. Fallback Handling

Commands include fallback logic for compatibility:

```vix
system("free -h 2>/dev/null || echo 'Not available'")
```

This ensures the program continues even if a command isn't available.

## Technical Details

### Why No Colors?

Vix's lexer currently only supports basic escape sequences (`\n`, `\t`, `\\`, etc.). ANSI color codes using hexadecimal (`\x1b`) or octal (`\033`) escapes are **not supported**. Therefore, `vixfetch` uses plain text output.

### Supported Platforms

| Platform | Status | Notes |
|----------|--------|-------|
| Linux    | Tested | Works on most distributions |
| macOS    | Untested | Should work with minor adjustments |
| Windows  | Limited | Requires WSL or MSYS2 for best results |
| WSL2     | Tested | Fully functional |

## Source Code

The complete source code is located in [`vixfetch.vix`](file://d:\Download\Vix-lang\examples\vixfetch.vix). Key sections:

```vix
// External C functions
extern "C" {
    fn printf(format: ptr, ...) -> i32
    fn system(cmd: ptr) -> i32
}

// Main function
fn main(argc: i32, argv: ptr) -> i32 {
    // Print logo
    printf(" __      __  _        \n")
    // ... (more ASCII art)
    
    // Gather system info
    system("uname -a")
    system("free -h 2>/dev/null || echo 'Not available'")
    system("df -h / 2>/dev/null || echo 'Not available'")
    
    return 0
}
```

## Contributing

Contributions are welcome! If you'd like to improve `vixfetch`:

1. **Add more system information** (CPU model, uptime, etc.)
2. **Improve cross-platform compatibility**
3. **Add color support** (once Vix lexer supports advanced escape sequences)
4. **Optimize output formatting**

Please follow the [Apache License 2.0](LICENSE) terms.

## License

This project is licensed under the **Apache License 2.0**.  
See the [LICENSE](LICENSE) file for details.

**Copyright 2025 Mulang_zty** (Vix Language)  
**Copyright 2026 0xA672** (vfetch inspiration)

## Acknowledgments

- **[neofetch](https://github.com/dylanaraps/neofetch)** - The original inspiration for system fetch tools
- **[vfetch](https://github.com/0xA672/vfetch)** - Direct inspiration for this tool, created by 0xA672
- **[Vix Language](https://github.com/vixlang/Vix-lang)** - The programming language used to build vixfetch
- **Vix Community Contributors** - For building the compiler and standard library

## Contact

For questions or issues, please open an issue on the [Vix-lang repository](https://github.com/vixlang/Vix-lang/issues).

---

**Made with love using Vix**
