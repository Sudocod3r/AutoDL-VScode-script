# AutoDL-VScode-script
# Automates downloading and installing VScode on Debian based Linux systems.
import time
import subprocess

# Function to print the message with delay
def delayed_print(message, delay):
    print(message)
    time.sleep(delay)

# Print the delayed message
delayed_print("Hello World! Sit back, relax, and enjoy the show! -Kyle Martin.", 5)

# Install wget if not already installed
subprocess.run(['sudo', 'apt', 'install', 'wget', '-y'], check=True)

# Check if dpkg is available
try:
    subprocess.run(['dpkg', '--version'], check=True)
except FileNotFoundError:
    print('dpkg is not available on your system. Please make sure you are running this script on a Debian-based system.')
    exit(1)

# Update system packages
print('Updating system packages...')
subprocess.run(['sudo', 'apt', 'update'], check=True)
subprocess.run(['sudo', 'apt', 'upgrade', '-y'], check=True)

# Download VSCode .deb package
print('Downloading Visual Studio Code...')
subprocess.run(['wget', 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64', '-O', 'vscode.deb'], check=True)

# Install VSCode
print('Installing Visual Studio Code...')
subprocess.run(['sudo', 'dpkg', '-i', 'vscode.deb'], check=True)
subprocess.run(['sudo', 'apt', 'install', '-f'], check=True)

# Clean up downloaded .deb file
subprocess.run(['rm', 'vscode.deb'], check=True)

# Open VSCode
print('Opening Visual Studio Code...')
subprocess.run(['code'], check=True)
