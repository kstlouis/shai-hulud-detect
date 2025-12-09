# Shai-Hulud NPM Supply Chain Attack Detector

**⚠️ This is a purpose-built fork of the [original repository](https://github.com/Cobenian/shai-hulud-detect). This fork is very much still a work in progress.**

A Bash tool that helps you spot known traces of the September 2025 and November 2025 npm supply-chain attacks—including the Shai-Hulud self-replicating worm, the chalk/debug crypto-theft incident, and the "Shai-Hulud: The Second Coming" fake Bun runtime attack.

## Key Differences from Original

This fork includes modifications for specific use cases:

- **Online CSV Source**: Loads compromised packages from DataDog's [indicators-of-compromise](https://github.com/DataDog/indicators-of-compromise) repository instead of a local file
- **Configurable CSV URL**: The CSV URL can be overridden via the `COMPROMISED_PACKAGES_CSV_URL` environment variable
- **Work in Progress**: Additional modifications and improvements are ongoing

## Quick Start

```bash
# Clone the repository
git clone https://github.com/kstlouis/shai-hulud-detect
cd shai-hulud-detect

# Make the script executable
chmod +x shai-hulud-detector.sh

# Scan your project for Shai-Hulud indicators
./shai-hulud-detector.sh /path/to/your/project

# Override CSV URL (optional)
COMPROMISED_PACKAGES_CSV_URL="https://example.com/my-csv.csv" ./shai-hulud-detector.sh /path/to/your/project
```

## Requirements

- macOS or Unix-like system
- **Bash 5.0 or newer** (required for associative arrays and performance features)
- Standard Unix tools: `find`, `grep`, `shasum`
- Network access (to fetch compromised packages CSV)

## Exit Codes

- **Exit Code 0**: Clean system - no significant security findings
- **Exit Code 1**: High-risk findings detected - immediate action required
- **Exit Code 2**: Medium-risk findings detected - manual investigation needed

## Original Repository

For the original, fully-featured version with comprehensive documentation, see:
- **Original Repository**: https://github.com/Cobenian/shai-hulud-detect

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
