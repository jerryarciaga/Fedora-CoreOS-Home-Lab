# Fedora CoreOS
This section of my repository contains the Butane config file that gets my CoreOS build up and running. This requires a computer with a TPM chip with version 2.0 or later in order to take advantage of `LUKS+TPM`.

# Setting up for the first time

## Butane
There are a couple things you would have to edit in the Butane file before proceeding to the next step. This install, by default, has a user named `core`, whose password is `passwd`. Also, you can see under `ssh_authorized_keys` my personal public keys. You want to change these before loading up CoreOS so you won't have to worry about having to change passwords.
1. Run `podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt`, then enter your desired password on the prompt. This would then output a hashed version of your password. Replace the value of `password_hash` under `passwd` with this output.
2. Generate (or copy, if you already have) a public SSH key over to `ssh_authorized_keys`. You can copy more than one if you want.
3. Run `podman run --interactive --rm quay.io/coreos/butane:release --pretty --strict < homelab.bu > homelab.ign` to produce and Ignition file. The resulting ignition file will be named `homelab.ign`.

## CoreOS ISO
Download the ISO page [here](https://fedoraproject.org/coreos/download?stream=stable#baremetal). Afterwards, you can proceed to the following:
1. Copy the downloaded ISO to a USB device using `dd` or use Ventoy.
2. From your machine's boot menu, select the USB device with the CoreOS ISO. You may want to turn off Secure Boot if you're having issues during boot up.
3. Copy the Ignition file over, the run `sudo coreos-installer install /dev/sda --ignition-file homelab.ign`. It would take a while to copy the necessary config before it's ready for a reboot.
4. Ensure Secure Boot is turned on before rebooting. This will kickstart an automated installation of Fedora CoreOS on your server.
5. You should be able to log on with `core` as your `username` locally or via SSH.
