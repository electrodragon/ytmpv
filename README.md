##Script to play YouTube videos in MPV player with random qualities.
# MPV player and Youtube-dl must be installed
# youtube-dl must have to be latest
# https://github.com/ytdl-org/youtube-dl/blob/master/README.md

#!/bin/bash
if [[ `which mpv` == "" ]]; then
  echo -e "\n  mpv is not installed.\n\n  install using: \n\n  sudo apt-get install mpv\n"
  exit 0
elif [[ `which youtube-dl` == "" ]]; then
  echo -e "\n  youtube-dl is not installed.\n\n  install it: \n\n  https://github.com/ytdl-org/youtube-dl/blob/master/README.md#installation\n"
  exit 0
fi

Show_Manual () {
  echo "|*************************************************************|"
  echo "|                          Paramters:                         |"
  echo "|               aud,144,240,360,480,720,1080,1440             |"
  echo "|*************************************************************|"
  echo "|          aud   -  Plays at Best Audio !                     |"
  echo "|          144   -  Plays at 144p or less available!          |"
  echo "|                            (Default:360)                    |"
  echo "|*************************************************************|"
  echo "|     ytmpv 'https://www.youtube.com/watch?v=FuXNumBwDOM'     |"
  echo "|   ytmpv 720 'https://www.youtube.com/watch?v=BklGhQYKl30'   |"
  echo "|*************************************************************|"
  exit 0
}

Show_Message () {
  echo -e "\n !!! Wrong Paramter Entered !!!\n"
  Show_Manual
}

if [[ "$1" == "" ]]; then
  Show_Manual
elif [[ "$2" == "" ]]; then
  mpv --ytdl-format='bestvideo[height<=?360]+bestaudio/best' "$1"   # Default
else
  case $1 in
    aud)
      mpv "$2" --no-video
      ;;
    144)
    mpv --ytdl-format='bestvideo[height<=?144]+bestaudio/best' "$2"
      ;;
    240)
    mpv --ytdl-format='bestvideo[height<=?240]+bestaudio/best' "$2"
      ;;
    360)
    mpv --ytdl-format='bestvideo[height<=?360]+bestaudio/best' "$2"
      ;;
    480)
    mpv --ytdl-format='bestvideo[height<=?480]+bestaudio/best' "$2"
      ;;
    720)
    mpv --ytdl-format='bestvideo[height<=?720]+bestaudio/best' "$2"
      ;;
    1080)
    mpv --ytdl-format='bestvideo[height<=?1080]+bestaudio/best' "$2"
      ;;
    1440)
    mpv --ytdl-format='bestvideo[height<=?1440]+bestaudio/best' "$2"
      ;;
    *)
    Show_Message
      ;;
  esac
fi

exit 0
