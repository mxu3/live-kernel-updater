test status : no successful kernel change yet performed on updated MX-15 




# live-kernel-updater
This is a bash command line program that changes or updates the kernel on a antiX or MX
live-usb. It can work on a running live-usb (primary) or on a secondary live-usb that is plugged in.

### Quick Start
    from https://github.com/mxu3/live-kernel-updater  download the master.zip with firefox, or:

    sudo apt-get update       # if needed
    sudo apt-get install git  # if needed
    git clone https://github.com/BitJam/live-kernel-updater
    git clone https://github.com/BitJam/cli-shell-utils       ##  contains library bash code
    cd live-kernel-updater
    sudo ./live-kernel-updater

## Synopsis


This program is command line only for the time being.  We try to avoid making your
live-usb unbootable so you need to install a new kernel and then do a
remaster before we will attempt to update the live kernel, i.e. deal with initrd asf..  
We do this by always looking for new kernels inside of the linuxfs file (in /boot) so we
know it will be available upon next boot.

It can update a running live system or a live-usb that you plugged in, e.g. on a SD-card.
You will be prompted with choices if you do not already specify what you want to do via command line options.

The log file is at `/var/log/live-kernel-updater.log` 

It will automatically create a config file for itself at
`/root/.config/live-kernel-updater/live-kernel-updater.conf`


## Usage

```
Usage: live-kernel-updater [options] [command]

Update the kernel on a running antiX or MX live-usb or on an antiX or MX live-usb
that is plugged into another system, like on a secondary USB-thumbdrive.  
The new kernel files must already be installed, i.e. present on the SD-card.
You will be prompted for necessary information missing from command line arguments.

Commands:
   all         All of the commands below
   unpack      Unpack the old initrd
   copy        Copy kernel modules into initrd
   repack      Repack the new initrd
   install     Copy new initrd and vmlinuz to the live boot directory

Options:
  -a --auto             Non-interactive.  Always assume the safe answer
     --color=<xxx>      Set color scheme to off|low|high
  -D --debug            Pause before cleaning up
  -d --device=<device>  live-usb device to update the kernel on
                        (use "live" to force updating a running live system)
  -F --force=XXXX       Force the options specfied:
                             flock:  ignore missing flock program (flock - manage locks from shell scripts)
                               usb:  Allow non-usb devices as target drive (dangerous!)
                             clear:  remove previous initrd directory
  -h --help -?          Show this usage info
  -i --initrd=<name>    Name of initrd file (initrd.gz).  If the name has
                        leading / then treated as full path to alternate initrd
  -I --ignore-config    Ignore the configuration file
  -k --kernel=<kernel>  The version (uname -r) of the new kernel
  -K --keep-old         Keep the old module directory in the initrd
  -p --pretend          Do not actually install the new kernel or initrd.gz (dry run for testing the script)
     --pause=<list>     Pause after certain stages of processing:
                            mount
                            unpack
                            copy
                            repack
                            install

  -q --quiet            Print less info
  -R --reset-config     Write fresh config file with default options
  -v --verbose          Print more info, show commands when run
  -W --write-config     Write/update config file preserving current options

Notes:
  - short options stack. Example: -pq instead of --pretend --quiet
  - options can be intermingled with commands and parameters
  
  - config file: /root/.config/live-kernel-updater/live-kernel-updater.conf
  - the config file will be sourced if it exists
  - it will be created if it does not exist
```
