# Shai-Hulud NPM Supply Chain Attack Detector

**⚠️ This is a purpose-built fork of [shai-hulud-detect](https://github.com/Cobenian/shai-hulud-detect). It is designed to be deployed via MDM instead of executed by the local user. It is very much a work in progress.**

## About

[shai-hulud-detect](https://github.com/Cobenian/shai-hulud-detect) is a Bash tool that helps you spot known traces of the September 2025 and November 2025 npm supply-chain attacks—including the Shai-Hulud self-replicating worm, the chalk/debug crypto-theft incident, and the "Shai-Hulud: The Second Coming" fake Bun runtime attack.

## Key Differences from Original

This fork's primary modifications:

- **Zsh Implementation**: Converted from Bash to Zsh for better compatibility with macOS deployments via MDM. Zsh is the default shell on macOS and the included bash version is too out of date to comply with the requirements of the original script.

- **CSV-Based Package List**: Requires a CSV URL to be provided in Jamf Parameter 5 (e.g., DataDog's [indicators-of-compromise](https://github.com/DataDog/indicators-of-compromise) repository). The script fetches and parses the CSV to build the compromised packages database. No local files are required, and new vulnerabilities are automatically accounted for as they are discovered.

- **Jamf Pro Parameters** (required):
  - **Parameter 4**: Project directory path to scan (or just use "default")
  - **Parameter 5**: CSV URL for compromised packages (must be a raw GitHub URL, e.g., `https://raw.githubusercontent.com/...`) 

## Deployment

This script is designed for deployment via Jamf Pro (or other MDM). 

1. Upload `shai-hulud-detector.sh` to your Jamf Pro script library
2. Create a policy that runs the script
3. Configure the policy parameters:
   - **Parameter 4**: Set to either "default" or specify the directory path you want to scan (e.g., `/Users/Shared/jamf-assets`). Note that you cannot use `~` to expand your user home directory 
   - **Parameter 5**: Set to the CSV URL for compromised packages (e.g., `https://raw.githubusercontent.com/DataDog/indicators-of-compromise/main/shai-hulud-2.0/consolidated_iocs.csv`)

**Important**: The CSV URL must be a raw GitHub URL (using `raw.githubusercontent.com`), not a blob URL (using `github.com/.../blob/...`).

### Testing Locally
Since Jamf uses $1-3, values passed in use `$4` and `$5`. If you want to test locally, you'll have to a) run the script with `sudo` and b) provide 3 "junk" arguments before passing the dir path and .csv file url

## Disclaimers

This was built using:
- a limited amount of scripting experience 
- a healthy (🫠) amount of assistance from Cursor
- an almost impossibly short imposed dealine

Use at your own risk.

In theory any MDM should work, but this was only tested and used with Jamf Pro.

## Requirements

- macOS, probably
- **Zsh** (standard on macOS, no additional installation needed)
- Standard Unix tools: `find`, `grep`, `shasum`
- Network access (required to fetch compromised packages CSV from Parameter 5)

## Exit Codes

- **Exit Code 0**: Clean system - no significant security findings
- **Exit Code 1**: High-risk findings detected - immediate action required
- **Exit Code 2**: Medium-risk findings detected - manual investigation needed

## Original Repository

For the original, fully-featured version with comprehensive documentation, please refer to the [original project](https://github.com/Cobenian/shai-hulud-detect)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
