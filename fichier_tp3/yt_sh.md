#!bin/bash

title=$(sudo youtube-dl --get-title $1)
description=$(sudo youtube-dl --get-description $1)
locate=$(locate "$title".mp4)
date=$(date "+%Y/%m/%d %T")

if [ -d "/srv/yt/downloads" ];then

sudo mkdir "/srv/yt/downloads/$title" >> "/dev/null"
sudo youtube-dl -f mp4 -o "/srv/yt/downloads/$title/%(title)s" $1 >> "/dev/null"
sudo touch "/srv/yt/downloads/$title/description" >> "/dev/null"
sudo chmod 777 "/srv/yt/downloads/$title/description"
sudo echo "$description" >> "/srv/yt/downloads/$title/description"
echo "Video $1 was downloaded."
echo "File path : $locate"

else
    exit
fi

if [ -d "/var/log/yt" ];then

echo "[$date]" "Video $1 was downloaded. File path : $locate" >> "/var/log/yt/download.log"

else
    exit
fi