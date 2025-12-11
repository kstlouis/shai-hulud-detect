# Shai-Hulud NPM Supply Chain Attack Detector

**⚠️ This is a purpose-built fork of [shai-hulud-detect](https://github.com/Cobenian/shai-hulud-detect). It is designed to be deployed via MDM instead of executed by the local user. It is very much a work in progress.**

## About

[shai-hulud-detect](https://github.com/Cobenian/shai-hulud-detect) is a Bash tool that helps you spot known traces of the September 2025 and November 2025 npm supply-chain attacks—including the Shai-Hulud self-replicating worm, the chalk/debug crypto-theft incident, and the "Shai-Hulud: The Second Coming" fake Bun runtime attack.

## Key Differences from Original

This fork includes a few modifications:

- **Online CSV Source**: Loads compromised packages from DataDog's [indicators-of-compromise](https://github.com/DataDog/indicators-of-compromise) repository instead of a local file; one-click redeployment if more infected packages are discovered

- **Parameter Substitution**: When deployed via MDM, use Parameter (`$4`) to specify the project directory. 

## Testing

```bash
# Clone the repository
cd shai-hulud-detect

# Make the script executable
chmod +x shai-hulud-detector.sh

# Scan your project for Shai-Hulud indicators
./shai-hulud-detector.sh /path/to/your/project
```
Not that if nothign is passed to `$4`, the script will fall back to original behaviour so you can still pass a directory path as a command argument.

When you're ready, upload `shai-hulud-detector.sh` to your MDM to deploy remotely.

## Disclaimers

This was built using:
- a limited amount of scripting experience 
- a healthy (..) amount of assistance from Cursor
- an almost impossibly short imposed dealine
Use at your own risk.

In theory any MDM should work, but this was only tested and used with Jamf Pro.

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

For the original, fully-featured version with comprehensive documentation, please refer to:
- **Original Repository**: https://github.com/Cobenian/shai-hulud-detect

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
