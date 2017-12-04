# pass-selinux

This policy is designed to work on Fedora (possibly RHEL) to confine pass. Since it concerns passwords, use at your own risk.

The primary goals of this policy module is:
* Deny network access to the program
* Isolate the password file (.password-store) from other programs on the system (only on the private-type branch) 


### Current state:

* All pass functionality works. Git function is untested
* unconfined_u is being used in an unconventional way. It is temporary and only intended as a stop gap for not running a user confined. Eg staff_u


## Installation
```sh
# Clone the repo
git clone https://github.com/georou/pass-selinux.git

# Compile the selinux module (see below)

# Install the SELinux policy module. Compile it before hand to ensure proper compatibility (see below)
semodule -i pass.pp

# Restore all the correct context labels
restorecon -v /usr/bin/pass
```


## How To Compile The Module Locally(Recommended before installing)
Ensure you have the `selinux-policy-devel` package installed.
```sh
# Ensure you have the devel packages
yum install selinux-policy-devel
# Change to the directory containing the .if, .fc & .te files
cd pass-selinux
make -f /usr/share/selinux/devel/Makefile pass.pp
semodule -i pass.pp
```
