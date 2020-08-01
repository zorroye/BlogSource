---
title: FC4 实体机的/etc/rc.d/rc.sysinit
tags:
  - 未分类
id: '87'
date: 2014-11-25 11:40:00
---

#!/bin/bash

#

\# /etc/rc.d/rc.sysinit - run once at boot time

#

\# Taken in part from Miquel van Smoorenburg's bcheckrc.

#

  

HOSTNAME=\`/bin/hostname\`

HOSTTYPE=\`uname -m\`

unamer=\`uname -r\`

  

if \[ -f /etc/sysconfig/network \]; then

    . /etc/sysconfig/network

fi

if \[ -z "$HOSTNAME" -o "$HOSTNAME" = "(none)" \]; then

    HOSTNAME=localhost

fi

  

\# Mount /proc and /sys (done here so volume labels can work with fsck)

mount -n -t proc /proc /proc

if \[ ! -d /proc/bus/usb \]; then

modprobe usbcore >/dev/null 2>&1 && mount -n -t usbfs /proc/bus/usb /proc/bus/usb

else

mount -n -t usbfs /proc/bus/usb /proc/bus/usb

fi

mount -n -t sysfs /sys /sys >/dev/null 2>&1

  

. /etc/init.d/functions

  

\# Check SELinux status

selinuxfs=\`LC\_ALL=C awk '/ selinuxfs / { print $2 }' /proc/mounts\`

SELINUX=

if \[ -n "$selinuxfs" \] && \[ "\`cat /proc/self/attr/current\`" != "kernel" \]; then

if \[ -r $selinuxfs/enforce \] ; then

SELINUX=\`cat $selinuxfs/enforce\`

else

\# assume enforcing if you can't read it

SELINUX=1

fi

fi

  

if \[ -n "$SELINUX" -a -x /sbin/restorecon \] && LC\_ALL=C fgrep -q " /dev " /proc/mounts ; then

/sbin/restorecon  -R /dev 2>/dev/null

fi

  

disable\_selinux() {

echo "\*\*\* Warning -- SELinux is active"

echo "\*\*\* Disabling security enforcement for system recovery."

echo "\*\*\* Run 'setenforce 1' to reenable."

echo "0" > $selinuxfs/enforce

}

  

relabel\_selinux() {

    if \[ -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

chvt 1

    fi

    echo "

         \*\*\* Warning -- SELinux relabel is required. \*\*\*

\*\*\* Disabling security enforcement.         \*\*\*

\*\*\* Relabeling could take a very long time, \*\*\*

\*\*\* depending on file system size.          \*\*\*

"

    echo "0" > $selinuxfs/enforce

    /sbin/fixfiles -f -F relabel > /dev/null 2>&1 

    rm -f  /.autorelabel 

    echo "\*\*\* Enabling security enforcement.         \*\*\*"

    echo $SELINUX > $selinuxfs/enforce

    if \[ -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

chvt 8

    fi

}

  

  

  

if \[ "$HOSTTYPE" != "s390" -a "$HOSTTYPE" != "s390x" \]; then

  last=0

  for i in \`LC\_ALL=C grep '^\[0-9\].\*respawn:/sbin/mingetty' /etc/inittab | sed 's/^.\* tty\\(\[0-9\]\[0-9\]\*\\).\*/\\1/g'\`; do

        > /dev/tty$i

        last=$i

  done

  if \[ $last -gt 0 \]; then

       > /dev/tty$((last+1))

       > /dev/tty$((last+2))

  fi

fi

  

if \[ "$CONSOLETYPE" = "vt" -a -x /sbin/setsysfont \]; then

   echo -n "Setting default font ($SYSFONT): "

   /sbin/setsysfont

   if \[ $? -eq 0 \]; then

      success

   else

      failure

   fi

   echo ; echo

fi

  

\# Print a text banner.

echo -en $"\\t\\tWelcome to "

if LC\_ALL=C fgrep -q "Red Hat" /etc/redhat-release ; then 

 \[ "$BOOTUP" = "color" \] && echo -en "\\\\033\[0;31m"

 echo -en "Red Hat"

 \[ "$BOOTUP" = "color" \] && echo -en "\\\\033\[0;39m"

 PRODUCT=\`sed "s/Red Hat \\(.\*\\) release.\*/\\1/" /etc/redhat-release\`

 echo " $PRODUCT"

elif LC\_ALL=C fgrep -q "Fedora" /etc/redhat-release ; then 

 \[ "$BOOTUP" = "color" \] && echo -en "\\\\033\[0;31m"

 echo -en "Fedora"

 \[ "$BOOTUP" = "color" \] && echo -en "\\\\033\[0;39m"

 PRODUCT=\`sed "s/Fedora \\(.\*\\) release.\*/\\1/" /etc/redhat-release\`

 echo " $PRODUCT"

else

 PRODUCT=\`sed "s/ release.\*//g" /etc/redhat-release\`

 echo "$PRODUCT"

fi

if \[ "$PROMPT" != "no" \]; then

 echo -en $"\\t\\tPress 'I' to enter interactive startup."

 echo

fi

  

\# Fix console loglevel

if \[ -n "$LOGLEVEL" \]; then

/bin/dmesg -n $LOGLEVEL

fi

  

\[ -x /sbin/start\_udev \] && /sbin/start\_udev

  

\# Only read this once.

cmdline=$(cat /proc/cmdline)

  

\# Initialize hardware

if \[ -f /proc/sys/kernel/modprobe \]; then

   if ! strstr "$cmdline" nomodules && \[ -f /proc/modules \] ; then

       sysctl -w kernel.modprobe="/sbin/modprobe" >/dev/null 2>&1

       sysctl -w kernel.hotplug="/sbin/udevsend" >/dev/null 2>&1

   else

       # We used to set this to NULL, but that causes 'failed to exec' messages"

       sysctl -w kernel.modprobe="/bin/true" >/dev/null 2>&1

       sysctl -w kernel.hotplug="/bin/true" >/dev/null 2>&1

   fi

fi

  

echo -n $"Initializing hardware... "

  

ide=""

scsi=""

network=""

audio=""

other=""

eval \`kmodule -d | while read devtype mod ; do

case "$devtype" in

"IDE")ide="$ide $mod"

  echo "ide=\\"$ide"\\";;

"SCSI") scsi="$scsi $mod"

  echo "scsi=\\"$scsi"\\";;

"NETWORK") network="$network $mod"

  echo "network=\\"$network"\\";;

"AUDIO") audio="$audio $mod"

  echo "audio=\\"$audio"\\";;

\*) other="$other $mod"

  echo "other=\\"$other"\\";;

esac

done\`

  

load\_module () {

LC\_ALL=C fgrep -xq "$1" /etc/hotplug/blacklist 2>/dev/null || modprobe $1 >/dev/null 2>&1

}

  

\# IDE

for module in $ide ; do

load\_module $module

done

  

\# SCSI

for module in \`/sbin/modprobe -c | LC\_ALL=C awk '/^alias\[\[:space:\]\]+scsi\_hostadapter\[0-9\]\*\[\[:space:\]\]/ { print $3 }'\` $scsi; do

load\_module $module

done

load\_module floppy

  

echo -n $" storage"

  

\# Network

pushd /etc/sysconfig/network-scripts >/dev/null 2>&1

interfaces=\`ls ifcfg\* | LC\_ALL=C egrep -v '(ifcfg-lo|:|rpmsave|rpmorig|rpmnew)' | \\

            LC\_ALL=C egrep -v '(~|\\.bak)$' | \\

            LC\_ALL=C egrep 'ifcfg-\[A-Za-z0-9\\.\_-\]+$' | \\

   sed 's/^ifcfg-//g' |

   sed 's/\[0-9\]/ &/' | LC\_ALL=C sort -k 1,1 -k 2n | sed 's/ //'\`

  

for i in $interfaces ; do

eval $(LC\_ALL=C fgrep "DEVICE=" ifcfg-$i)

load\_module $DEVICE

done

popd >/dev/null 2>&1

  

for module in $network ; do

load\_module $module

done

  

echo -n $" network"

  

\# Sound

for module in \`/sbin/modprobe -c | LC\_ALL=C awk '/^alias\[\[:space:\]\]+snd-card-\[\[:digit:\]\]+\[\[:space:\]\]/ { print $3 }'\` $audio; do

load\_module $module

done

  

echo -n $" audio"

  

\# Everything else (duck and cover)

for module in $other ; do

load\_module $module

done

  

echo -n $" done"

success

echo

  

\# Load other user-defined modules

for file in /etc/sysconfig/modules/\*.modules ; do

  \[ -x $file \] && $file

done

  

\# Load modules (for backward compatibility with VARs)

if \[ -f /etc/rc.modules \]; then

/etc/rc.modules

fi

  

\# Start the graphical boot, if necessary; /usr may not be mounted yet, so we

\# may have to do this again after mounting

RHGB\_STARTED=0

mount -n /dev/pts

  

if strstr "$cmdline" rhgb && ! strstr "$cmdline" early-login && \[ "$BOOTUP" = "color" -a "$GRAPHICAL" = "yes" -a -x /usr/bin/rhgb \]; then

   LC\_MESSAGES= /usr/bin/rhgb

   RHGB\_STARTED=1

fi

  

\# Configure kernel parameters

update\_boot\_stage RCkernelparam

sysctl -e -p /etc/sysctl.conf >/dev/null 2>&1

  

\# Set the system clock.

update\_boot\_stage RCclock

ARC=0

SRM=0

UTC=0

  

if \[ -f /etc/sysconfig/clock \]; then

   . /etc/sysconfig/clock

  

   # convert old style clock config to new values

   if \[ "${CLOCKMODE}" = "GMT" \]; then

      UTC=true

   elif \[ "${CLOCKMODE}" = "ARC" \]; then

      ARC=true

   fi

fi

  

CLOCKDEF=""

CLOCKFLAGS="$CLOCKFLAGS --hctosys"

  

case "$UTC" in

    yes|true)CLOCKFLAGS="$CLOCKFLAGS --utc"

CLOCKDEF="$CLOCKDEF (utc)" ;;

    no|false)CLOCKFLAGS="$CLOCKFLAGS --localtime"

CLOCKDEF="$CLOCKDEF (localtime)" ;;

esac

case "$ARC" in

    yes|true)CLOCKFLAGS="$CLOCKFLAGS --arc"

CLOCKDEF="$CLOCKDEF (arc)" ;;

esac

case "$SRM" in

    yes|true)CLOCKFLAGS="$CLOCKFLAGS --srm"

CLOCKDEF="$CLOCKDEF (srm)" ;;

esac

  

/sbin/hwclock $CLOCKFLAGS

  

action $"Setting clock $CLOCKDEF: \`date\`" /bin/true

  

if \[ "$CONSOLETYPE" = "vt" -a -x /bin/loadkeys \]; then

 KEYTABLE=

 KEYMAP=

 if \[ -f /etc/sysconfig/console/default.kmap \]; then

  KEYMAP=/etc/sysconfig/console/default.kmap

 else

  if \[ -f /etc/sysconfig/keyboard \]; then

    . /etc/sysconfig/keyboard

  fi

  if \[ -n "$KEYTABLE" -a -d "/lib/kbd/keymaps" \]; then

     KEYMAP="$KEYTABLE.map"

  fi

 fi

 if \[ -n "$KEYMAP" \]; then 

  if \[ -n "$KEYTABLE" \]; then

    echo -n $"Loading default keymap ($KEYTABLE): "

  else

    echo -n $"Loading default keymap: "

  fi

  loadkeys -u $KEYMAP < /dev/tty0 > /dev/tty0 2>/dev/null && \\

     success $"Loading default keymap" || failure $"Loading default keymap"

  echo

 fi

fi

  

\# Set the hostname.

update\_boot\_stage RChostname

action $"Setting hostname ${HOSTNAME}: " hostname ${HOSTNAME}

  

\# Initialiaze ACPI bits

if \[ -d /proc/acpi \]; then

   for module in /lib/modules/$unamer/kernel/drivers/acpi/\* ; do

      insmod $module >/dev/null 2>&1

   done

fi

  

\# configure all zfcp (scsi over fibrechannel) devices before trying to mount them

\# zfcpconf.sh exists only on mainframe

\[ -x /sbin/zfcpconf.sh \] && /sbin/zfcpconf.sh

  

\# RAID setup

update\_boot\_stage RCraid

echo "raidautorun /dev/md0" | nash --quiet

if \[ -f /etc/mdadm.conf \]; then

    /sbin/mdadm -A -s

fi

  

\# LVM2 initialization

if \[ -x /sbin/lvm.static \]; then

    if ! LC\_ALL=C fgrep -q "device-mapper" /proc/devices 2>/dev/null ; then

modprobe dm-mod >/dev/null 2>&1

    fi

    echo "mkdmnod" | /sbin/nash --quiet >/dev/null 2>&1

    \[ -n "$SELINUX" \] && restorecon /dev/mapper/control >/dev/null 2>&1

    if \[ -c /dev/mapper/control -a -x /sbin/lvm.static \]; then

if /sbin/lvm.static vgscan --mknodes --ignorelockingfailure > /dev/null 2>&1 ; then

   action $"Setting up Logical Volume Management:" /sbin/lvm.static vgchange -a y --ignorelockingfailure

fi

    fi

fi

  

if \[ -f /fastboot \] || strstr "$cmdline" fastboot ; then

fastboot=yes

fi

  

if \[ -f /fsckoptions \]; then

fsckoptions=\`cat /fsckoptions\`

fi

  

if \[ -f /forcefsck \] || strstr "$cmdline" forcefsck ; then

fsckoptions="-f $fsckoptions"

elif \[ -f /.autofsck \]; then

\[ -f /etc/sysconfig/autofsck \] && . /etc/sysconfig/autofsck

if \[ "$AUTOFSCK\_DEF\_CHECK" = "yes" \]; then

AUTOFSCK\_OPT="$AUTOFSCK\_OPT -f"

fi

fsckoptions="$AUTOFSCK\_OPT $fsckoptions"

fi

  

if \[ "$BOOTUP" = "color" \]; then

fsckoptions="-C $fsckoptions"

else

fsckoptions="-V $fsckoptions"

fi

  

if \[ -f /etc/sysconfig/readonly-root \]; then

    . /etc/sysconfig/readonly-root

  

    if \[ "$READONLY" = "yes" \]; then

        # Call rc.readonly to set up magic stuff needed for readonly root

        . /etc/rc.readonly

    fi

fi

\_RUN\_QUOTACHECK=0

if \[ -z "$fastboot" -a "$READONLY" != "yes" \]; then

  

        STRING=$"Checking filesystems"

echo $STRING

if \[ "${RHGB\_STARTED}" != "0" -a -w /etc/rhgb/temp/rhgb-console \]; then

fsck -T -A -a $fsckoptions > /etc/rhgb/temp/rhgb-console

else

fsck -T -A -a $fsckoptions

fi

rc=$?

if \[ "$rc" -eq "0" \]; then

success "$STRING"

echo

elif \[ "$rc" -eq "1" \]; then

       passed "$STRING"

echo

elif \[ "$rc" -eq "2" -o "$rc" -eq "3" \]; then 

echo $"Unmounting file systems"

umount -a

mount -n -o remount,ro /

echo $"Automatic reboot in progress."

reboot -f

        fi

        # A return of 4 or higher means there were serious problems.

if \[ $rc -gt 1 \]; then

       if \[ -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

   chvt 1

fi

  

failure "$STRING"

echo

echo

echo $"\*\*\* An error occurred during the file system check."

echo $"\*\*\* Dropping you to a shell; the system will reboot"

echo $"\*\*\* when you leave the shell."

  

                str=$"(Repair filesystem)"

PS1="$str \\# # "; export PS1

\[ "$SELINUX" = "1" \] && disable\_selinux

sulogin

  

echo $"Unmounting file systems"

umount -a

mount -n -o remount,ro /

echo $"Automatic reboot in progress."

reboot -f

elif \[ "$rc" -eq "1" \]; then

\_RUN\_QUOTACHECK=1

fi

if \[ -f /.autofsck -a -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

chvt 8

    fi

fi

\# Unmount the initrd, if necessary

if LC\_ALL=C fgrep -q /initrd /proc/mounts && ! LC\_ALL=C fgrep -q /initrd/loopfs /proc/mounts ; then

   umount /initrd

   /sbin/blockdev --flushbufs /dev/ram0 >/dev/null 2>&1

fi

\# Update quotas if necessary

if \[ X"$\_RUN\_QUOTACHECK" = X1 -a -x /sbin/quotacheck \]; then

if \[ -x /sbin/convertquota \]; then

   # try to convert old quotas

   for mountpt in \`LC\_ALL=C awk '$4 ~ /quota/{print $2}' /etc/mtab\` ; do

if \[ -f "$mountpt/quota.user" \]; then

   action $"Converting old user quota files: " \\

   /sbin/convertquota -u $mountpt && \\

rm -f $mountpt/quota.user

fi

if \[ -f "$mountpt/quota.group" \]; then

   action $"Converting old group quota files: " \\

   /sbin/convertquota -g $mountpt && \\

rm -f $mountpt/quota.group

fi

   done

fi

action $"Checking local filesystem quotas: " /sbin/quotacheck -aRnug

fi

  

\# Remount the root filesystem read-write.

update\_boot\_stage RCmountfs

state=\`LC\_ALL=C awk '/ \\/ / && ($3 !~ /rootfs/) { print $4 }' /proc/mounts\`

\[ "$state" != "rw" -a "$READONLY" != "yes" \] && \\

  action $"Remounting root filesystem in read-write mode: " mount -n -o remount,rw /

  

\# Clean up SELinux labels

if \[ -n "$SELINUX" \]; then

   for file in /etc/mtab /etc/ld.so.cache ; do

   \[ -r $file \] && restorecon $file  >/dev/null 2>&1

   done

fi

  

\# Clear mtab

(> /etc/mtab) &> /dev/null

  

\# Remove stale backups

rm -f /etc/mtab~ /etc/mtab~~

  

\# Enter mounted filesystems into /etc/mtab

mount -f /

mount -f /proc >/dev/null 2>&1

mount -f /sys >/dev/null 2>&1

mount -f /dev/pts >/dev/null 2>&1

mount -f /proc/bus/usb >/dev/null 2>&1

  

\# Mount all other filesystems (except for NFS and /proc, which is already

\# mounted). Contrary to standard usage,

\# filesystems are NOT unmounted in single user mode.

action $"Mounting local filesystems: " mount -a -t nonfs,nfs4,smbfs,ncpfs,cifs,gfs -O no\_netdev

  

if \[ -x /sbin/quotaon \]; then

    action $"Enabling local filesystem quotas: " /sbin/quotaon -aug

fi

  

\# Check to see if a full relabel is needed

if \[ -n "$SELINUX" \]; then 

    if \[ -f /.autorelabel \] || strstr "$cmdline" autorelabel ; then

relabel\_selinux

    fi

else

    if \[ -d /etc/selinux \]; then

        \[ -f /.autorelabel \] || touch /.autorelabel

    fi

fi

  

  

\# Start the graphical boot, if necessary and not done yet.

if strstr "$cmdline" rhgb && ! strstr "$cmdline" early-login && \[ "$RHGB\_STARTED" -eq 0 -a "$BOOTUP" = "color" -a "$GRAPHICAL" = "yes" -a -x /usr/bin/rhgb \]; then

   LC\_MESSAGES= /usr/bin/rhgb

   RHGB\_STARTED=1

fi

  

\# Initialize pseudo-random number generator

if \[ -f "/var/lib/random-seed" \]; then

cat /var/lib/random-seed > /dev/urandom

else

touch /var/lib/random-seed

fi

chmod 600 /var/lib/random-seed

dd if=/dev/urandom of=/var/lib/random-seed count=1 bs=512 2>/dev/null

  

\# Use the hardware RNG to seed the entropy pool, if available

#\[ -x /sbin/rngd -a -c /dev/hw\_random \] && rngd

  

\# Configure machine if necessary.

if \[ -f /.unconfigured \]; then

    if \[ -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

chvt 1

    fi

  

    if \[ -x /usr/bin/system-config-keyboard \]; then

/usr/bin/system-config-keyboard

    fi

    if \[ -x /usr/bin/passwd \]; then 

        /usr/bin/passwd root

    fi

    if \[ -x /usr/sbin/netconfig \]; then

/usr/sbin/netconfig

    fi

    if \[ -x /usr/sbin/timeconfig \]; then

/usr/sbin/timeconfig

    fi

    if \[ -x /usr/sbin/authconfig \]; then

/usr/sbin/authconfig --nostart

    fi

    if \[ -x /usr/sbin/ntsysv \]; then

/usr/sbin/ntsysv --level 35

    fi

  

    # Reread in network configuration data.

    if \[ -f /etc/sysconfig/network \]; then

. /etc/sysconfig/network

  

\# Reset the hostname.

action $"Resetting hostname ${HOSTNAME}: " hostname ${HOSTNAME}

    fi

  

    rm -f /.unconfigured

  

    if \[ -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

chvt 8

    fi

fi

  

\# Clean out /.

rm -f /fastboot /fsckoptions /forcefsck /.autofsck /halt /poweroff &> /dev/null

  

\# Do we need (w|u)tmpx files? We don't set them up, but the sysadmin might...

\_NEED\_XFILES=

\[ -f /var/run/utmpx -o -f /var/log/wtmpx \] && \_NEED\_XFILES=1

  

\# Clean up /var.  I'd use find, but /usr may not be mounted.

for afile in /var/lock/\* /var/run/\* ; do

if \[ -d "$afile" \]; then

  case "$afile" in

\*/news|\*/mon);;

\*/sudo)rm -f $afile/\*/\* ;;

\*/vmware)rm -rf $afile/\*/\* ;;

\*/samba)rm -rf $afile/\*/\* ;;

\*/screen)rm -rf $afile/\* ;;

\*)rm -f $afile/\* ;;

  esac

else

  rm -f $afile

fi

done

rm -f /var/lib/rpm/\_\_db\* &> /dev/null

rm -f /var/gdm/.gdmfifo &> /dev/null

  

\# Reset pam\_console permissions

\[ -x /sbin/pam\_console\_apply \] && /sbin/pam\_console\_apply -r

  

{

\# Clean up utmp/wtmp

\> /var/run/utmp

touch /var/log/wtmp

chgrp utmp /var/run/utmp /var/log/wtmp

chmod 0664 /var/run/utmp /var/log/wtmp

if \[ -n "$\_NEED\_XFILES" \]; then

  > /var/run/utmpx

  touch /var/log/wtmpx

  chgrp utmp /var/run/utmpx /var/log/wtmpx

  chmod 0664 /var/run/utmpx /var/log/wtmpx

fi

  

\# Clean up various /tmp bits

\[ -n "$SELINUX" \] && restorecon /tmp

rm -f /tmp/.X\*-lock /tmp/.lock.\* /tmp/.gdm\_socket /tmp/.s.PGSQL.\*

rm -rf /tmp/.X\*-unix /tmp/.ICE-unix /tmp/.font-unix /tmp/hsperfdata\_\* \\

       /tmp/kde-\* /tmp/ksocket-\* /tmp/mc-\* /tmp/mcop-\* /tmp/orbit-\*  \\

       /tmp/scrollkeeper-\*  /tmp/ssh-\*

\# Make ICE directory

mkdir -m 1777 -p /tmp/.ICE-unix >/dev/null 2>&1

chown root:root /tmp/.ICE-unix

\[ -n "$SELINUX" \] && restorecon /tmp/.ICE-unix >/dev/null 2>&1

  

\# Start up swapping.

update\_boot\_stage RCswap

action $"Enabling swap space: " swapon -a -e

  

\# Set up binfmt\_misc

/bin/mount -t binfmt\_misc none /proc/sys/fs/binfmt\_misc > /dev/null 2>&1

  

\# Initialize the serial ports.

if \[ -f /etc/rc.serial \]; then

. /etc/rc.serial

fi

  

\# If they asked for ide-scsi, load it

if strstr "$cmdline" ide-scsi ; then

modprobe ide-cd >/dev/null 2>&1

modprobe ide-scsi >/dev/null 2>&1

fi

  

\# Boot time profiles. Yes, this should be somewhere else.

if \[ -x /usr/sbin/system-config-network-cmd \]; then

  if strstr "$cmdline" netprofile= ; then

    for arg in $cmdline ; do

        if \[ "${arg##netprofile=}" != "${arg}" \]; then

   /usr/sbin/system-config-network-cmd --profile ${arg##netprofile=}

        fi

    done

  fi

fi

  

\# Now that we have all of our basic modules loaded and the kernel going,

\# let's dump the syslog ring somewhere so we can find it later

dmesg -s 131072 > /var/log/dmesg

  

\# create the crash indicator flag to warn on crashes, offer fsck with timeout

touch /.autofsck &> /dev/null

  

kill -TERM \`/sbin/pidof getkey\` >/dev/null 2>&1

} &

if strstr "$cmdline" confirm ; then

touch /var/run/confirm

fi

if \[ "$PROMPT" != "no" \]; then

/sbin/getkey i && touch /var/run/confirm

fi

wait

  

\# Let rhgb know that we're leaving rc.sysinit

if \[ -x /usr/bin/rhgb-client \] && /usr/bin/rhgb-client --ping ; then

    /usr/bin/rhgb-client --sysinit

fi