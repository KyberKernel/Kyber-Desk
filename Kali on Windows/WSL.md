# Kali Linux on Windows with WSL

<img width="1000" height="600" alt="download (1)" src="https://github.com/user-attachments/assets/fa43e48c-5824-4229-b724-a18f5f211422" />

### WSL lets you run a Linux CLI inside Windows.
You can use Linux commands on Windows and Windows commands on Linux.

It's crazy!

It’s like Linux and Windows fused into one powerful OS

But is it too powerful?

This guide shows you how to
- Install WSL and Kali Linux
- Add a different Linux distribution ( Debian )
- Remove Debian or uninstall WSL completely

To start you need ```Windows 11 ```or``` Windows 10 version 2004 ```or newer

### 1 - Check your Windows version

Press

```bash
Windows key + R
```
Type 
```bash
winver
```
And press Enter

### 2 - Check virtualization

WSL runs Linux in a lightweight virtual machine, so your computer’s hardware virtualization feature needs to be enabled.

It may already be on.


To check press 

```bash
Ctrl + Shift + Esc 
```

To open Task Manager. Select ```Performance```, then ```CPU```, and look for ```Virtualization```. 

If it says ```Enabled```, you’re ready to continue.

If it says ```Disabled```, restart your computer and open its ```BIOS/UEFI``` settings.

Find the virtualization setting often called ```Intel Virtualization Technology```

```VT-x```, ```AMD-V```, or ```SVM Mode``` 

Enable it, then save your changes and restart. The key for opening BIOS/UEFI varies by computer

But if you dont know the key then open ```Powershell``` as administrator and type this command

```bash
shutdown /r /fw /ts 0
```
And press Enter 

This command will reboot the computer and enter the ```BIOS/UEFI``` settings automatically.

#  1 - Open PowerShell as administrator
- Open the Start menu ( click the Windows logo, usually at the bottom of the screen ).
- Type ```PowerShell```.
- In the results, right-click the ```Windows PowerShell``` or ```PowerShell``` and select ```Run as administrator```.
- If Windows asks,  ```“Do you want to allow this app to make changes?” ```, click  ```Yes ```.


 <img width="450" height="350" alt="screenshot-run-powershell-as-administrator-en-bizplay-2325497325" src="https://github.com/user-attachments/assets/b483c54b-bb49-43a9-ac2b-728c8bc3cd57" />

A window with a text prompt will open.

 <img width="450" height="250" alt="powershell-from-cmd-1499411875" src="https://github.com/user-attachments/assets/e6f91bdc-4e9c-44ab-b860-49fa9ed11a39" />

# 2 - Install WSL with Kali

Click inside the PowerShell window and type 

```bash
wsl --install kali-linux
```
and press``` Enter```.

This installs Kali with WSL. Windows may ask you to restart your computer and if so, save your work and restart.

After restarting, open PowerShell as administrator and type

```bash
wsl
```

The first time Kali opens, it may take a few minutes to set itself up.

It will ask you to choose a Linux``` username``` and``` password```

- Create a Linux username and press Enter. ```This is separate from your Windows username```.
- Create a password and press Enter. ```You won’t see the characters as you type and that’s normal in Kali and other security focused Linux distributions.```.
- Type the password again to confirm it, then press ```Enter```.

# 3 - Update Kali

When you see the Kali prompt, type this command and press Enter

```bash
sudo apt update && sudo apt full-upgrade -y
```
If Kali asks for your password, type the password you just created and press Enter. Again, nothing will appear while you type.

To open Kali another time, find Kali Linux in the Start menu and open it.

# Install another Linux distribution

You can keep Kali and add another distribution, such as ```Debian```. Open PowerShell and run
```bash
wsl -l -o
```
OR 
```bash
wsl --list --online
```

<img width="450" height="350" alt="Screenshot 2026-10-07 141910" src="https://github.com/user-attachments/assets/9c5fce5c-4c8b-4924-bfbd-8694b47b665e" />

This lists the distributions available to install. To add Debian, run

```bash
wsl --install debian
```
After its done downloading, create a separate Linux username and password for it

Installing ```Debian``` this way does not remove``` Kali```

To close Debian or any other distro you have open, type ```exit``` in the command prompt.

This will take you back to the PowerShell command prompt.

# Checking the default distro

“Default distro” means that when you open``` PowerShell ```and type``` wsl```, the default distro will open.

If you have multiple distros installed, you can also check them with this same command

```bash
wsl -l -v
```
OR 

```bash
wsl --list --verbose
```

<img width="396" height="61" alt="Screenshot 2026-10-07 142841" src="https://github.com/user-attachments/assets/19f87e86-df30-41fc-8d98-550655a97e96" />

Now, if you notice that Kali here has an asterisk beside its name, that means Kali is the default distro on my system.

If you want to make Debian the default distro, you need to type this command.

```bash
wsl --set-default debian
```

<img width="413" height="117" alt="Screenshot 2026-10-07 143926" src="https://github.com/user-attachments/assets/8d5e6231-1a8d-429b-8e22-de229a3effd9" />


If you want to open Debian while keeping Kali as the default, you need to type this command.

```bash
wsl -d debian
```

OR

```bash
wsl --distribution debian
```
You can also use this command to open multiple Linux terminals at the same time by launching a new PowerShell window, typing that command, and specifying the distro name and enter.

```wsl -d <distro-name>```


# Remove Debian or any distro you want but keep WSL

This permanently deletes Debian and the files stored inside it.

First in PowerShell list your distributions.

```bash
wsl -l -v
```
OR 

```bash
wsl --list --verbose
```

Find Debian’s exact name in the list. It is usually ```Debian```. Then remove it with the following command.

```bash
wsl --unregister debian
```

# Remove WSL completely

This removes all your WSL distributions and their Linux files.

First, run 

```bash
wsl --list --verbose
```

And unregister each distribution you see, using its exact name. For example
```bash
wsl --unregister kali-linux
wsl --unregister Debian
```
Then, in PowerShell, run

```bash
wsl --uninstall
```
Restart Windows if prompted

# Run Windows command in Linux
You can launch many Windows programs directly from Kali by typing the program name with``` .exe ```at the end.
For example, to open Notepad, type:

```bash
notepad.exe
```
To open the current folder in File Explorer, type:

```bash
explorer.exe
```
To check and display your network settings in windows we use ```ipconfig``` we can use that in Linux WSL by adding ```.exe```

```bash
ipconfig.exe
```

Let’s reverse it. Let’s go to PowerShell and open a new PowerShell window.

This is all Windows. I can type ipconfig, which will give me my IP addresses, but I can filter them using a Linux command. if i do
```bash
ipconfig | wsl grep 10.
```
IF pipe the output to``` wsl grep 10. ``` wsl to invoke a Linux command to show lines that contain 10.

You can also use CAT command in Windows powershell 

```WSL Cat and then my file name```

It’s like Linux and Windows have become one OS.

# The End

And that’s it now you know how to get started with WSL and run Linux right from Windows. 

The command line is yours to explore.





