---
title: Modding the reMarkable 2 
author: Annabel
date: 2024-04-13 10:56:00 +/-TTTT
categories: 
  - guide
tags: remarkable
---

The [reMarkable](https://remarkable.com/) is one of, if not *the* most popular e-ink tablets available on the market. With its sleek design, (relatively) cheap price and [active developer community](https://github.com/reHackable), it was the premier choice for me as a student.


The reMarkable runs a custom Linux-based system and users are permitted root access, making mods relatively easy to implement and download.[^1] However, documentation is frequently lacking, resulting in a large barrier to those curious but not familar with this. 


In this guide, I'll be walking you through the process I used to mod my reMarkable 2, including the **installation of [KOreader](https://koreader.rocks/)** (an eBook viewer with better support for files - `.epub` ones in particular -  than the reMarkable), the **[reMarkable Printer](https://github.com/Evidlo/remarkable_printer) mod** (to easily send documents from PC to reMarkable), and the easy addition of **custom sleep/suspend/etc screens** without the use of external software. 

Please note that the guide assumes the use of a reMarkable 2 on the latest patch (as of today: 3.10.x), connected with a cable to a device running Windows 10, and is clear enough (I hope) for those with minimal programming proficiency. 

Big thanks to ddvk for their [KOreader toggler (with gesture support!)](https://github.com/ddvk/remarkable-autoinstall/blob/master/rm2/readme.md), and to Evidlo for their work on the [reMarkable Printer](https://github.com/Evidlo/remarkable_printer).

## Why not use Toltec?
There's a fine line between developer and community when it comes to reMarkable mods. 

The easiest way to install mods - using [Toltec](https://toltec-dev.org), a repository of community-made mods  - is significantly limited by the fact it only has full support up to version 2.15.1.1189. reMarkable itself introduced a [new file type](https://support.remarkable.com/s/article/Software-release-3-0) that [broke a lot of mods](https://www.reddit.com/r/RemarkableTablet/comments/10hxe3j/updates_regarding_reverse_engineering_remarkable/) in version 3. Although Toltec may be easier to use, I found it difficult to justify the loss in developer-supported features caused by downpatching to 2.15.1.1189, deciding it was better to stick to a 'newer' version after such a drastic change. Regardless, the majority of mods will require some form of downgrading for full support/functionality.

Whether you choose to do it or not is ultimately up to you, as Toltec's support is likely to be significantly better than anything I can provide. Regardless, I hope this will guide you through simple installation of a few mods. 

> If you plan on installing the `rm2fb` package from Toltec and have already followed this guide, make sure that you uninstall KOreader to avoid conflicts with `rm2fb`. Use the following commands whilst in an SSH session to remove it. See this footnote for explanations of the commands. [^2]
>
>`systemctl stop touchinjector`
>
>`rm /etc/systemd/system/touchinjector.service`
>
>`rm -fr app`
>
>`rm -fr scripts` 
{: .prompt-warning }

## Getting root access to your reMarkable
You'll need root access to modify basically anything on your reMarkable. 

**reMarkable**
1. Navigate to `Settings` via the `Menu`.
2. Go to `About`, then `Copyright and Licenses`.
3. Note down the `Password` and the two IP addresses provided at the bottom of the page. 

The password is required to obtain root access to the reMarkable; the IP addresses refer to the reMarkable itself. If you're connecting via cable, the IP address you should use is always the same (`10.11.99.1`). If you're using Wi-Fi to connect, use the other IP address instead. 

Next, open Command Prompt on your PC. 

**PC**
1. Connect your reMarkable to your PC using a cable (ignore if using Wi-Fi) 
2. Search for Command Prompt, and open it. To gain SSH access, type the following in: 
```shell
ssh root@10.11.99.1
```
3. When prompted, type the password shown on your Remarkable in the steps above. There will not be any text visible as you are typing the password in; this is deliberate.
4. If you see rainbow text reading `ZERO SUGAR` and the line `reMarkable: ~/`, you've succeeded and you now have root access!



## KOreader
### Downpatching to v.3.3.2.1666
KOReader depends on [rm2fb](https://github.com/ddvk/remarkable2-framebuffer/), which is required for KOreader as an external app to 'draw' to its screen. The latest supported version of rm2fb is [v.3.3.2.1666](https://github.com/ddvk/remarkable2-framebuffer/blob/68031728eabeb91711b3c7ff4217c70c1541abde/src/shared/config.cpp#L415), making it necessary to downpatch to that in order to use KOReader.[^3]



This guide will be using [Codexctl](https://github.com/Jayy001/codexctl), an update management system for the reMarkable, to downpatch. 

**PC**
1. Download the latest pre-built binary from the [releases page](https://github.com/Jayy001/codexctl/releases). It should be a `.zip` file called `windows-latest.zip`.
2. Extract the file.
3. Type `cmd` into the file navigator at the top of the extracted folder to open Command Prompt in that location. 
4. Type the following command into that window to install v.3.3.2.1666 on your reMarkable.
```shell
codexctl install 3.3.2.1666
``` 

**reMarkable**
1. On your reMarkable, navigate to Menu > Settings > Software. If all goes well, you should see the reMarkable downloading and installing the 3.3.2.1666 update. It will probably restart after this.
2. Disable Automatic Updates from the same path above.

At this point, your root access from Command Prompt will have been terminated, and any attempts to reconnect will bring up a scary-looking message about being potentially vulnerable to attacks, etc. This will happen after every update/downgrade. To disable this message, do the following:

**PC**
1. Open File Explorer. Paste `%userprofile%\.ssh` into the file navigator at the top. 
2. Open the `known_hosts` file and delete the line containing your reMarkable's IP address, then save the file.

You should now be able to connect via SSH again.

### Downloading a supported version of wget
The majority of reMarkable mods contain `bash` scripts that use [`wget`](https://www.gnu.org/software/wget/) to download further files from online (in this case, ddvk's script downloads a 2022 build of KOreader and the latest rm2fb build). Unfortunately, for some reason reMarkable's version of `wget` is specifically modified to *not* support HTTPS connections.

As an aside - Toltec does cover this during set-up with the use of modified `wget` binaries that support [TLS](https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/). Since they've provided the binaries they used [here](https://github.com/toltec-dev/bootstrap), you will need to download these and transfer them to your reMarkable to bootstrap KOreader installation. 


**PC**
1. Download `wget-v1.21.1-1` from the [Toltec site](https://github.com/toltec-dev/bootstrap). 
2. Navigate to wherever the file was downloaded, and type `cmd` into the file navigator to open Command Prompt in that location.
3. To transfer the file to your reMarkable, type the following into Command Prompt.
```shell
scp wget-v1.21.1-1 root@10.11.99.1 
```
4. To check if the transfer was successful, connect via SSH and type `ls` to list all files in the root of your reMarkable. If you see `wget-v1.21.1-1` there, it worked! 
5. At this point, you'll need to verify whether the file you downloaded is the correct one: that it hasn't been modified or otherwise tampered with. You can do this by verifying the SHA-256 checksum (a unique 'footprint' of the file) against the one provided by the developers. 
```shell
echo "c258140f059d16d24503c62c1fdf747ca843fe4ba8fcd464a6e6bda8c3bbb6b5  wget-v1.21.1-1" | sha256sum -c && bash wget-v1.21.1-1
```
That long string represents the SHA-256 checksum of the original file, which can be found on the [Toltec bootstrap repository](https://github.com/toltec-dev/bootstrap?tab=readme-ov-file). The command then generates the SHA-256 checksum of the `wget` file that you downloaded, and compares it to the original one. If they're the same, you'll see `wget-v1.21.1-1: OK` printed indicating that you have downloaded an original, unmodified file.
6. To use the modified `wget`, you'll need to make the file you downloaded actually executable.
```shell
chmod +x /home/root/wget-v1.21.1-1
```

### Running ddvk's KOreader script
Though [ddvk's KOreader install](https://github.com/ddvk/remarkable-autoinstall/blob/master/rm2/readme.md) is a simple one-liner, I found that it did not work with my setup and later attributed that to the issue with `wget` (see this [conversation in the reMarkable Discord server](https://discord.com/channels/385916768696139794/386181213699702786/1200873645866758306) for more information)

I heavily prefer this over the Toltec-installed KOreader due to its touch gesture support, which allows me to switch between 'reading' and 'writing' mode easily. 


**PC**
1. While still connected via SSH, type `cat > auto_rm2.sh` to create a new file named `auto_rm2.sh`. It will also enter edit mode, prompting you to enter text on a new line. Paste the following code in by right-clicking, then press Ctrl+D to close the file. If you mess up this step, delete the file by typing `rm auto_rm2.sh`, then try again.

```shell
set -e
APPDIR=${APPDIR:-/home/root/apps}
REPOURL="https://raw.githubusercontent.com/ddvk/remarkable-autoinstall/master/rm2"
RM2FBREPO="https://github.com/ddvk/remarkable2-framebuffer/releases/latest/download"
KOREADER="https://github.com/koreader/koreader/releases/download/v2022.10/koreader-remarkable-v2022.10.zip"

mkdir -p $APPDIR
mkdir -p ~/scripts

systemctl stop touchinjector || true

echo "Downloading files..."

if [ ! -d "$APPDIR/koreader" ]; then
    mkdir -p "$APPDIR/koreader"
    /home/root/wget/v1.21.1-1 "$KOREADER" -O /tmp/koreader.zip
    unzip /tmp/koreader.zip -d $APPDIR
fi

if [ ! -d "~/librm2fb_client.so.1.0.1" ]; then
    /home/root/wget/v1.21.1-1 "$RM2FBREPO/librm2fb_client.so.1.0.1" -O ~/librm2fb_client.so.1.0.1
fi

if [ ! -d "~/librm2fb_server.so.1.0.1" ]; then
    /home/root/wget/v1.21.1-1 "$RM2FBREPO/librm2fb_server.so.1.0.1" -O ~/librm2fb_server.so.1.0.1
fi
if [ ! -d "~/apps/touchinjector" ]; then
    /home/root/wget/v1.21.1-1 "$REPOURL/apps/touchinjector" -O ~/apps/touchinjector
fi
if [ ! -d "~/scripts/swipeup.sh" ]; then
    /home/root/wget/v1.21.1-1 "$REPOURL/scripts/swipeup.sh" -O ~/scripts/swipeup.sh
fi
if [ ! -d "~/scripts/ko.sh" ]; then
    /home/root/wget/v1.21.1-1 "$REPOURL/scripts/ko.sh" -O ~/scripts/ko.sh
fi
chmod +x ~/scripts/swipeup.sh
chmod +x ~/scripts/ko.sh
chmod +x ~/apps/touchinjector


echo "udev rule"
cat << EOF > /lib/udev/rules.d/15-systemd-input.rules
ACTION=="add", SUBSYSTEM=="input", TAG+="systemd"
EOF

echo "Systemd unit file"
cat << EOF > /etc/systemd/system/touchinjector.service
[Unit]
Description=touch injector
Requires=dev-input-event0.device dev-input-event1.device dev-input-event2.device
After=xochitl.service opt.mount dev-input-event0.device dev-input-event1.device dev-input-event2.device

[Service]
Environment=HOME=/home/root
ExecStart=$APPDIR/touchinjector

[Install]
WantedBy=multi-user.target
EOF

echo "Starting the touch service..."
systemctl daemon-reload
systemctl enable touchinjector
#systemctl start touchinjector
echo "Reboot the device"
```
(This code has been taken from [ddvk's repository](https://github.com/ddvk/remarkable-autoinstall/blob/master/rm2/auto_rm2.sh). The only modification that have been made to the script is the replacement of all occurrences of  `wget` to the TLS-supported executable version (`/home/root/wget-v1.21.1-1`). You are free to compare it/replace it yourself.)
1. Run the file using `bash auto_rm2.sh`. If it runs successfully, it should prompt you to restart your reMarkable, which you can do from Settings.

If, at any point, you run into an error and wish to restart the KOreader installation, refer to the warning at the top of the page for uninstallation instructions. 


**reMarkable**
1. After the restart, try swiping upwards from the bottom of the screen to the top. If the install worked, you should now be on KOreader's tutorial!



### But wait, where are my books? 
You'll need to transfer your eBook files to the reMarkable. They will not be visible from the standard reMarkable homepage, but you will be able to read them using KOreader.

Ensure all your eBook files are downloaded on your PC and are in a folder of their own.

**PC**
1. Open Command Prompt in the location of the folder containing your books.
2. Run the folllowing command to the contents of that folder to your reMarkable.  **If you wish to move the files, not just copy**, append `&& del *` onto the above command to delete the contents of the folder *after* the files have been copied. It will ask you for confirmation before deleting them.
```shell
scp * root@10.11.99.1:/home/root/ 
```
**If you wish to place your eBooks in a dedicated folder**, you will first need to create that folder on the reMarkable. Start a new SSH session and type `mkdir <foldername>` to create it, replacing `<foldername>` with an actual name, e.g "books". After creating that folder, repeat steps 1 & 2, replacing `/home/root/` with `/home/root/<foldername>`.
3. To check if the files transferred, open a new SSH session and type `ls` (if moved to `/home/root/`) or `ls <foldername>` (if moved to a specific folder). If it lists the names of your eBooks, you're all good to go!

---

[^1]: Yes, it can [run Doom](https://github.com/LinusCDE/doomarkable).
[^2]: [ddvk's KOreader installer](https://github.com/ddvk/remarkable-autoinstall/tree/master/rm2) uses touch gestures to open and close KOreader, instead of having it run automatically (meaning you are unable to access the standard reMarkable homepage without installing a [launcher](https://remarkable.guide/guide/software/launcher.html), like Remux or Oxide). These commands stop the touch injector and delete the directories containing information from the install.
[^3]: [timower](https://github.com/timower) has furthed developed rm2fb with support up to v.3.8.2. If you wish, [use at your own risk](https://github.com/timower/rM2-stuff/discussions/32)