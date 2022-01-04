# Quick-Setup-for-Unity3D-on-Ubuntu-20.04-LTS

## Intro
This guide assumes that you have just performed a fresh installation of `Ubuntu 20.04` and have now logged in.  From this point forward, we get you setup with an entire development environment using `Unity3D`.


## Update
Get basic patches and updates.

    sudo apt-get update
    sudo apt-get -y upgrade


## show os info

    cat /etc/os-release

#### Optional - Use a "Proprietary" Graphics Driver
Assuming you have the right hardware, you can use the proprietary driver from Nvidia.  Ubuntu already knows the versions available and presents them as an easy to click radio button.

- Step 1 - Navigate to "Show Applications > SOftware & Updates > Additional Drivers"
- Step 2 - Observe that "Nouveaux" is currently checked
- Step 3 - Check the radio button at the top such as the `nvidia-driver-470 (proprietary, tested)`


## Install gimp
The `gimp` application is like the `photoshop` of Linux and it will be needed to create artwork, save your screenshots, etc.

    #install the "snap" version of gimp
    sudo snap install gimp

*Note: Generally, you will avoid using `snap` packages when a real package is available; However, with `gimp` the community "snap" version is very good. Alternatively, you can install the official vendor version with `sudo apt install gimp` instead.*


## Optional - Install `powershell`
You do not need powershell, but why not.

    sudo apt-get install -y wget apt-transport-https software-properties-common
    cd Downloads/
    wget -q https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb
    sudo dpkg -i packages-microsoft-prod.deb
    sudo apt-get update
    sudo apt-get install -y powershell


## Install Visual Studio Code
This will be our code editor. Skip this if you have your own.

    #download gpg key
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    
    #add gpg key
    sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
    
    #Copy/Paste the following very long one-liner
    sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'

    #cleanup
    rm -f packages.microsoft.gpg

    #refresh package list
    sudo apt update

    #install visual studio code
    sudo apt install code


## Install .NET
This assumes you are running `20.04` which you can confirm by reviewing `cat /etc/os-release`.

    #get package list
    wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
    
    #add repo
    sudo dpkg -i packages-microsoft-prod.deb
        
    #install pre-reqs
    sudo apt-get install -y apt-transport-https
    
    #update package list
    sudo apt-get update
    
    #install .NET
    sudo apt-get install -y dotnet-sdk-6.0
    
    #confirm it works
    dotnet


## Install `mono`, by Microsoft
Before `.NET` was open sourced, `mono` existed to provide `.NET` functionality in Linux for those that wanted it.  While `.NET` is now available for Linux, there are still many things that use `mono`, such as `Unity3D`.  Here, we install `mono`.

    #install pre-reqs
    sudo apt install gnupg ca-certificates
    
    #add key
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
    
    #add repo
    echo "deb [arch=amd64] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
    
    #update package list
    sudo apt-get update

    #install mono
    sudo apt update -y

    #optional - show package
    sudo apt list --installed | grep mono


*Tip: When adding the above repo, we enhanced the vendor documentation by adding `[arch=amd64]` to prevent `apt` errors (about missing `i386` bits).*


## Required - Install `mono-devel` 
This is required; Do not skip this step.

    sudo apt install mono-devel -y


## Optional - Hello World for `mono`
Once you have `mono` and `mono-devel` installed, feel free to follow the hello world examples at the official `mono` site:

    https://www.mono-project.com/docs/getting-started/mono-basics/


*Tip: To prepare for the hello world examples, you might install the following first:*


    sudo apt install mono-xsp4
    sudo apt-get install libgtk-3-dev
    sudo apt-get install gcc


## Install `Unity3D`
- Download the `Unity Hub`for Linux which comes as a ready made image, like a snap.
- Extract the contents by right-clicking `UnityHub.tar.gz` (or similar) and selecting "Extract Here"
- Locate the `INSTALL.sh` file and navigate to "Right-click > Properties > Permissions" and check the box to make it executable.
- Finally, from a terminal run the following:

    ./INSTALL.sh


## Optional - Install VS Code `Extensions`
 - Open `code` and click the `Extensions` button in the left pane or navigate to "File > Preferences > Extensions"
 - Search for `Powershell` and install the `powershell` extension from Microsoft.
 - Search for `C#` and install the desired extension, such as the `Micrsoft` C# extension, powered by `OmniSharp`.


## Optional - Modify VS Code `Settings`
Navigate to `File > Preferences > Settings` and look for the C# section for anything of interest to you.  Then, search for `mono` and where you see `OmniSharp:Mono Path`, click the the link titled `Edit in Settings.Json`.

Here is an example setup, which includes turning off `telemetry` and disabling `dragAndDrop` functionality.


*Tip: Some of these settings were created from the gui at `File > Preferences > Settings` but you can also type them manually.*

```
{
    "telemetry.telemetryLevel": "off",
    "editor.dragAndDrop": false,
    "window.zoomLevel": 4,
    "omnisharp.useGlobalMono": "always",
    "omnisharp.monoPath": "/usr/bin/mono"
}
```

*Important: By default, you can drag and drop your words in `Visual Studio Code` (i.e. within the same script), which can easily break your scripts if you did not realize this was possible.*


## Summary
In this write-up (written Q1 2022), we installed a game development environment from scratch on `Ubuntu 20.04 LTS`.  Remember the importance of staying on `Ubuntu 20.04 LTS` as `Unity3D` may crash on project startup for any later releases (for now).  As a developer it is wise to stay on `LTS` and do not be swayed to upgrade.  Of course you should do your part and run some other devices with the latest `21.10` (or even try experimental installs of the next LTS `jammy`. For now though, keep your development  / creator / important machine running Ubuntu `20.04` for a flawless experience with `Unity3D`.


## Next Steps
Go watch some youtube game design videos for Unity3D. There are many great creators that walk you through the entire process.  Try to watch a blend of some design that is just out of your reach, but also some that you can actually do like a flappy bird example.  Finally, keep in mind that the the user interface for `Unity3D` on youtube videos may be slightly different than yours, but nothing too major.

 -end-
