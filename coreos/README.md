# Fedora CoreOS
This section of my repository contains the Butane config file that gets my CoreOS build up and running. This requires a computer with a TPM chip with version 2.0 or later in order to take advantage of `LUKS+TPM`.

# Setting up for the first time

## Butane
There are a couple things you would have to edit in the Butane file before proceeding to the next step. This install, by default, has a user named `core`, whose password is `passwd`. Also, you can see under `ssh_authorized_keys` my personal public keys. You want to change these before loading up CoreOS so you won't have to worry about having to change passwords.
1. Run `podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt`, then enter your desired password on the prompt. This would then output a hashed version of your password. Replace the value of `password_hash` under `passwd` with this output.
2. Generate (or copy, if you already have) a public SSH key over to `ssh_authorized_keys`. You can copy more than one if you want.
