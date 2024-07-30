---
title: My reMarkable2 Workflow
author: Annabel
date: 2024-05-12 20:28:00 +/-TTTT
categories: 
  - guide
tags: remarkable
---

*Note: This post is a rewrite, as there have been several updates to the rM2 software and to my own usage of it since.*

The [reMarkable](https://remarkable.com/) is one of, if not *the* most popular e-ink tablets available on the market. With its sleek design, (relatively) low price and [active developer community](https://github.com/reHackable), it was the premier choice for me as a student.

The reMarkable runs a custom Linux-based system and users are permitted root access, making mods relatively easy to implement and download.[^1] However, documentation is frequently lacking, resulting in a large barrier to those curious but not familar with this. 

In this article, I'll be discussing my own usage of and mods of the device and issues you may run into when modding it yourself. 

## Toltec
[Toltec](https://toltec-dev.org) is a repository of community-made mods - from [simple utilities to complete apps and games](https://toltec-dev.org/stable/) - that has full support up to version `3.3.2.1666`[^1]. The site itself comes with a disclaimer that installing it on a device on a version later has the chance to brick your device, and should not be done if you truly do not know what you are doing. Therefore, downgrading your device (losing the functionality added from updates in that process) is the only way to utilise Toltec to its full potential.[^2]

## Downpatching your device

If you are on the latest reMarkable version (`3.11.x` and upward) the [traditional means](https://github.com/Jayy001/codexctl) of downloading and installing other version to your device will not work. Refer to [this issue thread](https://github.com/Jayy001/codexctl/issues/71) if you're on that version; else, download and use Codexctl normally. 

The latest version that Toltec fully supports is [`3.3.2.1666`](https://toltec-dev.org/#install-toltec). This occurs as certain packages are not usable on later versions, such as [kernel modules](https://github.com/toltec-dev/toltec/issues/506) and the popular [ddvk-hacks](https://github.com/ddvk/remarkable-hacks). This version is the latest supported by the [`rm2fb` (reMarkable2 framebuffer) project](https://github.com/ddvk/remarkable2-framebuffer), which controls how things are graphically displayed on the reMarkable.

## Mods 

I personally have the following modifications installed on my reMarkable2 running `3.3.2.1666`. Hover over the notes to see my comments on each mod.

| Modification | Notes | Installation Method |
| ------------ | ----- | ------------------- |
| [Toltec](https://toltec-dev.org) | Community repository of mods. | [Script](https://toltec-dev.org/#install-toltec) |
|[Remux](https://rmkit.dev/apps/remux) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="An app launcher is essnetial if you're installing other apps onto your device, as it'll enable you to switch between each app!">App launcher for the reMarkable.</span> | Toltec |
| [Iago](https://rmkit.dev/apps/iago) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="Very helpful since downpatching removes straight line correction, which were introduced in version 3.8.">UI for drawing shapes (circles, bezier curves, lines, etc)</span> | Toltec |
| [zshelf](https://github.com/phthallo/zshelf) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="The original project was unmaintained and out-of-date, so the links lead to my updated fork of the project.">Interface for eBook downloading from Z-Library.</span> | [Instructions](https://github.com/phthallo/zshelf?tab=readme-ov-file#installation) | 
| [KOreader](https://github.com/koreader/koreader/) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="Better than reMarkable's native eBook reader.">External eBook reader.</span> | Toltec | 
| [rmfakecloud](https://github.com/ddvk/rmfakecloud/) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="Awesome!">Self-hosted cloud service.</span> | Toltec | 
| [remarkable_printer](https://github.com/Evidlo/remarkable_printer) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="I use this to easily transfer worksheets from my laptop to my reMarkable.">Allows native printing to your reMarkable.</span> | [Script](https://github.com/Evidlo/remarkable_printer?tab=readme-ov-file#quick-start) |
| [webinterface-onboot](https://github.com/rM-self-serve/webinterface-onboot) | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="All of rM-self-serve's mods here fix tiny issues I didn't even know I had.">Starts the USB web interface on device boot.</span> | Toltec | 
| [webinterface-wifi](https://github.com/rM-self-serve/webinterface-wifi) | Makes the web interface Wi-Fi-accessible. | Toltec | 
| [webinterface-upload-button](https://github.com/rM-self-serve/webinterface-upload-button) | Adds an upload button to the web interface. | Toltec | 
| [recrossable](https://github.com/sandsmark/recrossable/) | Crossword generator for the reMarkable. | Toltec | 


## Other Notes
Some projects aren't available on Toltec and require you to use a script to download it. 

If you're getting TLS errors while running these scripts, and you don't have Toltec installed, this is because the reMarkable2 ships with a version of `wget` (a tool for fetching content on the internet) that does not support HTTPS connections. The Toltec team, which include these binaries with their installation, have released the TLS-supporting ones they use [here](https://github.com/toltec-dev/bootstrap), which you'll need to transfer to your device and convert into an executable to use. 

### Commands
These commands may come in handy.

| Command | Description |
| ------- | ----------- |
| ls | Lists all files in a directory. |
| cd `directory` | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="Use `cd ..` to move back one directory. ">Changes your current working directory to a specified directory.</span> |
| scp `local files` `remote` | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="If connected via cable, remote would be `10.11.99.1`. Use `scp -r` to transfer directories.">Transfers local files to a remote location.</span>|
| chmod +x `file` | Converts `file` into an executable. |
| rm `file` | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="Use `rm -r` to delete a directory with content in it. Else, use `rmdir` to delete an empty directory.">Deletes `file`.</span> |
| cat `file` | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="Use `cat > file` to create a file in editing mode. Press `Ctrl-D` to close and save the file.">Outputs the content of `file` to the terminal.</span> |

### File Locations

| Location | Contents |
| -------- | -------- | 
| `/home/root/.local/share/remarkable/xochitl/` | Notebooks and files from the standard Xochitl interface. |  
| `/usr/share/remarkable/` | <span data-bs-toggle="tooltip" data-bs-placement="top" data-bs-original-title="To customise them, create an image file with dimensions 1872x1404, rename it to any of the appropriate file names and use `scp` to move it here.">Sleep/rebooting/etc screens</span> |

[^1]: Full support entails having the majority of Toltec packages fully tested and usable on a certain version. Packages that do not work on that version will not appear. See [here](https://github.com/toltec-dev/toltec/issues/820) for the current state of 3.x support, which is currently in [testing](https://github.com/toltec-dev/toltec/tree/testing) for version 3.5.2. 
[^2]: An additional note to be aware of is that reMarkable (as of early June 2024) will [drop official reMarkable cloud support](https://www.reddit.com/r/RemarkableTablet/comments/1cmagp9/remarkable_dropping_support_for_the_latestish/) for all devices running older versions of the firmware. 