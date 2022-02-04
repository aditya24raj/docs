# Install Instructions

## Arch Linux&#x20;

Some of our friends have started putting together all the install instructions for Arch over on the arch wiki:

{% embed url="https://wiki.archlinux.org/title/Waydroid" %}

## Postmarket OS

Thanks to the Postmarket community, you can also find instructions and troubleshooting tips on their wiki:

{% embed url="https://wiki.postmarketos.org/wiki/Waydroid" %}

## Mobian

The community was kind enough to post the install instructions for Mobian on their Doku pages:

{% embed url="https://wiki.mobian-project.org/doku.php?id=waydroid" %}

## Zorin OS

User @Aman9das has put together a detailed guide for installing Waydroid on Zorin OS:

{% embed url="https://github.com/Aman9das/Waydroid_Setup_Guide" %}

## Sailfish OS

A few of the contributors to sailfishos-open have put together a resource for installing Waydroid on the OS:

{% embed url="https://github.com/sailfishos-open/waydroid" %}

## Ubuntu/Debian Based Install Instructions

### Prerequisites
#### officially supported distributions are focal, hirsute and bullseye.
```bash
lsb_release -sc
```
output of above command should be your distribution name.  
keep it handy. it will be asked during installation.

>this guide may work on any other debian-based distribution,  
>just enter bullseye as your distribution name when asked during installation.
>
>[see guides for non-debian distributions](https://docs.waydro.id/usage/install-on-desktops)

#### wayland
```bash
echo $XDG_SESSION_TYPE
```
output of above command should be wayland  
if not switch to wayland display server first.


### Install Instructions
run the command given below-

```bash
printf "\nenter your distribution name: " && read DISTRO && \
sudo apt install python3 lxc wget ca-certificates && \
sudo wget https://repo.waydro.id/waydroid.gpg -O /usr/share/keyrings/waydroid.gpg && \
sudo sh -c "echo 'deb [signed-by=/usr/share/keyrings/waydroid.gpg] https://repo.waydro.id/ $DISTRO main' > /etc/apt/sources.list.d/waydroid.list" && \
sudo apt update && sudo apt install waydroid && sudo waydroid init && sudo systemctl start waydroid-container &&\
echo -e "\n waydroid installed."
```
launch waydroid from the apps menu.  
first launch(and first launch after reboot) takes a few minutes before waydroid appears.

if waydroid does not appears even after 5-10 minutes, refer Troubleshooting section.

## Troubleshooting

### Manually Starting Waydroid

To start Waydroid without systemctl, you need to follow a few simple steps

**Start the container first:**

```bash
sudo waydroid container start
```

**And in a new terminal tab, start the waydroid session (without** _**sudo**_**):**

```bash
waydroid session start
```

After that starts and you see "Android with user 0 is ready", it is safe to launch an app from the applications menu, or

### Launch Waydroid In Full-Screen Mode:

_(This can be run while Waydroid is running, or used to start it in full-screen mode)_

```bash
waydroid show-full-ui
```

### Launch Waydroid In Multi-Window Mode:

First we need to set the property while a Waydroid session is running:

```bash
waydroid prop set persist.waydroid.multi_windows true
```

After that, we can restart the container:

```
sudo systemctl restart waydroid-container
```

Then we are ready to launch an app, and it will start in multi-window mode

## Reinstalling Waydroid

Sometimes things don't go as planned and you need to remove it all and start over. To do that, follow the steps below:

First, make sure you have stopped the session and containers:

```bash
waydroid session stop
sudo waydroid container stop
```

Then it is safe to remove Waydroid:

```bash
sudo apt remove waydroid
```

After you remove Waydroid, reboot.

Then once logged back in, we need to do a little cleanup:

```bash
sudo rm -rf /var/lib/waydroid /home/.waydroid ~/waydroid ~/.share/waydroid ~/.local/share/applications/*aydroid* ~/.local/share/waydroid
```

Then can reinstall and run the init command again:

```bash
sudo apt install waydroid
sudo waydroid init
```
