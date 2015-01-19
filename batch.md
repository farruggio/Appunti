https://gist.github.com/fduran/1870429

#!/bin/bash
CURRENT=$(df / | grep / | awk '{ print $5}' | sed 's/%//g')
THRESHOLD=90

if [ "$CURRENT" -gt "$THRESHOLD" ] ; then
    mail -s 'Disk Space Alert' mailid@domainname.com << EOF
Your root partition remaining free space is critically low. Used: $CURRENT%
EOF
fi




#######



#!/bin/sh
# Shell script to monitor or watch the disk space
# It will send an email to $ADMIN, if the (free avilable) percentage 
# of space is >= 90% 
# -------------------------------------------------------------------------
# Copyright (c) 2005 nixCraft project <http://cyberciti.biz/fb/>
# This script is licensed under GNU GPL version 2.0 or above
# -------------------------------------------------------------------------
# This script is part of nixCraft shell script collection (NSSC)
# Visit http://bash.cyberciti.biz/ for more information.
# ----------------------------------------------------------------------
# Linux shell script to watch disk space (should work on other UNIX oses )
# SEE URL: http://www.cyberciti.biz/tips/shell-script-to-watch-the-disk-space.html
# set admin email so that you can get email
ADMIN="me@somewher.com"
# set alert level 90% is default
ALERT=90
df -H | grep -vE '^Filesystem|tmpfs|cdrom' | awk '{ print $5 " " $1 }' | while read output;
do
  #echo $output
  usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1  )
  partition=$(echo $output | awk '{ print $2 }' )
  if [ $usep -ge $ALERT ]; then
    echo "Running out of space \"$partition ($usep%)\" on $(hostname) as on $(date)" | 
     mail -s "Alert: Almost out of disk space $usep" $ADMIN
  fi
done
