# Ansible script for Arch Linux (Raspberry Pi)

This playbook will install the following packages:

+ vim, mosh, apacman (packer fork)
+ kodi
+ mopidy, mopidy-spotify

The available variables are defined in `roles/<role>/defaults/main.yml`. Feel free to override the defaults.


## Bootstrap

After preparing your sdcard and booting into Arch Linux, you need to run the`init.yml` playbook. This will install python2 (for Ansible) and setup some basic settings.

I should set the following variables: `hostname`, `sudo_user`, `users`. The `sudo_user` must be in `users` and at least one user must have a ssh key set.
After setting the IP address of your Raspberry Pi in `hosts`, you are ready to initialize your system:

        ansible-playbook -k init.yml -i hosts


## Main Configuration

Since the required packages for ansible are now in place, you can run the main playbook. You must pass the previously defined ssh/sudo user as an argument:

        ansible-playbook -k playbook.yml -i hosts -u <sudo_user>

After running this playbook you may need to restart your Raspberry Pi (eg. hostname changes). Ansible will report a failure - ignore this:

        ansible raspberry-pi -i hosts -a "sudo reboot" -u <sudo_user>


## Notes

+ The complete installation takes up to 45 minutes depending on your sdcard.
+ To speed things up you should point `xbmc_home` to an external harddisk or usb stick.
