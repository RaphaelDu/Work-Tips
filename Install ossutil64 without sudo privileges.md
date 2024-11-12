# How to install ossutil64 without sudo privileges

## Background
When working in environments where sudo privileges are not available (like some Docker containers or restricted systems), the standard installation method for ossutil64 might fail. This guide provides a workaround for installing ossutil64 without sudo.

## Problem
The standard installation command that requires sudo:
```bash
sudo -v ; curl https://gosspublic.alicdn.com/ossutil/install.sh | sudo bash
```
This will fail with an error message like:
```
-bash: sudo: command not found
```

## Solution
You can install ossutil64 without sudo privileges using these steps:

1. Download the installation script:
```bash
curl https://gosspublic.alicdn.com/ossutil/install.sh -o install.sh
```

2. Make the script executable:
```bash
chmod +x install.sh
```

3. Run the installation script:
```bash
./install.sh
```

## Verification
After installation, verify that ossutil64 is installed correctly:
```bash
ossutil64 version
```

## Alternative Method
If the above method doesn't work, you can try installing manually:

1. Download the binary directly:
```bash
curl -o ossutil64 http://gosspublic.alicdn.com/ossutil/1.7.7/ossutil64
```

2. Make it executable:
```bash
chmod 755 ossutil64
```

3. Move to a user-accessible binary location:
```bash
mkdir -p ~/bin
mv ossutil64 ~/bin/
```

4. Add to PATH (add to ~/.bashrc):
```bash
export PATH=$PATH:~/bin
```

5. Reload shell configuration:
```bash
source ~/.bashrc
```

## Notes
- This installation method is particularly useful in Docker containers or environments where sudo access is restricted
- The installation path will be user-specific rather than system-wide
- Make sure you have write permissions in the installation directory

## Related Documentation
- [Official ossutil Documentation](https://www.alibabacloud.com/help/en/object-storage-service/latest/ossutil-overview)
- [Alibaba Cloud OSS](https://www.alibabacloud.com/product/oss)

## Contributing
Feel free to open issues or submit pull requests if you have other useful tips for working with ossutil64 in restricted environments.

## License
This documentation is available under the MIT License.
