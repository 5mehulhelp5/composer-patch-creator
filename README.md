# PHP Composer Patch Creator

## 🛠 Overview

A robust and lightning-fast Bash utility script designed to simplify and accelerate the process of creating and managing vendor package patches for Composer-based PHP projects (such as Magento, Laravel, Symfony, etc.).

This is likely the quickest and most efficient way to generate Composer-compatible patches for vendor packages, saving developers significant time and effort.

## 🚀 Why Use This Script?

### Traditional Patch Creation Workflow
```bash
# Manually stage specific files
git add -f ./vendor/{vendor}/{package}/file1.php ./vendor/{vendor}/{package}/file2.php ...

# Perform required changes on files
# ... (manual editing)

# Create patch manually
git diff ./vendor/{vendor}/{package}/file1.php ./vendor/{vendor}/{package}/file2.php ... > patches/{patch-name}.patch

# Cleanup steps
git restore ./vendor/{vendor}/{package}/file1.php ./vendor/{vendor}/{package}/file2.php ...
git reset HEAD ./vendor/{vendor}/{package}/file1.php ./vendor/{vendor}/{package}/file2.php ...

# Manually update composer.json
# "extra": {
#     "patches": {
#         "{vendor}/{package}": {
#             "{patch-message}": "patches/{patch-name}.patch",
#         },
#     }
# }
```

### With Composer Patch Creation Utility
```bash
# Single command to start patch creation
cpc {vendor}/{package} -n {patch-name}.patch -m {patch-message}

# Perform required changes in vendor repo files
# Press 'y' when done

# Automatic patch generation and composer.json update ✨
```

### 🌟 Key Benefits
- **Simplified Workflow**: Reduce multiple manual steps to a single command
- **Automatic File Management**:
    - Automatically stages files
    - Generates patch
    - Restores original files
    - Cleans up git staging
- **Composer.json Integration**:
    - Automatically updates patch configuration
    - Creates backup before modification
- **Interactive Process**:
    - Guides you through patch creation
    - Provides clear prompts and feedback
- **Error Handling**:
    - Checks dependencies
    - Validates input
    - Provides detailed error messages

## 📦 Prerequisites

### Required Tools
- `git`
- `composer`
- `jq`
- Standard Unix tools (`cp`, `mkdir`, `sed`, `date`)
- Composer Patches Plugin: `cweagans/composer-patches`

### Supported Environments
- Linux
- macOS

## 🚀 Installation

1. Clone the script to your project:
```bash
curl -0 https://raw.githubusercontent.com/MagePsycho/composer-patch-creator/main/src/composer-patch-creator.sh -o cpc.sh
chmod +x cpc.sh
```

To make it system-wide command
```bash
sudo mv cpc.sh /usr/local/bin/cpc
```

2. Ensure all dependencies are installed

## 💡 Usage

### Basic Usage
```bash
./cpc.sh <vendor/package>
```

### Advanced Options
```bash
# Custom patch name
./cpc.sh magento/module-url-rewrite -n TICKET-custom-patch.patch

# Patch with description
./cpc.sh magento/module-url-rewrite -m "Fixed critical URL rewrite bug"

# Full example
./cpc.sh magento/module-url-rewrite -n TICKET-123.patch -m "Resolved routing issue"
```

### Options
- `-h, --help`: Show help message
- `-n, --name`: Specify custom patch filename
- `-m, --message`: Add patch description

Once the script execution is complete, run the `composer install` command to apply the patches.  
For more details, refer to the `Composer Configuration` section.

## 🔍 How It Works

1. Checks system dependencies
2. Validates vendor package existence
3. Stages vendor package files
4. Prompts for file modifications
5. Creates patch file
6. Updates `composer.json` with patch information

## 📝 Composer Configuration

Ensure your `composer.json` has patch plugin configuration:

```json
{
    "require": {
        "cweagans/composer-patches": "^1.7"
    },
    "extra": {
        "patches": {}
    }
}
```

## ⚠️ Best Practices

- Always review patches before applying
- Use descriptive patch names
- Keep patch files version-controlled
- Minimize patch scope and complexity

## 🐛 Troubleshooting

- Ensure you're in a git repository
- Verify all dependencies are installed
- Check file permissions
- Confirm `composer.json` is present

## 📄 License
MIT License

## 👥 Contributing
Contributions welcome! Please open issues or submit pull requests.

## 🙌 Credit
Developed with ❤️ by Raj KB <magepsycho@gmail.com>
