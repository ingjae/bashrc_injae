# .bashrc
    작성일자 19년 12월 27일 
    작성자 황인재
    최종 수정일 19년 12월 27일
  

```bash

# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
	# We have color support; assume it's compliant with Ecma-48
	# (ISO/IEC-6429). (Lack of such support is extremely rare, and such
	# a case would tend to support setf rather than setaf.)
	color_prompt=yes
    else
	color_prompt=
    fi
fi

if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

# If this is an xterm set the title to user@host:dir
case "$TERM" in
xterm*|rxvt*)
    PS1="\[\e]0;${debian_chroot:+($debian_chroot)}\u@\h: \w\a\]$PS1"
    ;;
*)
    ;;
esac

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi
#-----------------------------------------------------------------------------
#cd + pwd
#cd() { builtin cd "$@" && pwd; }

#cd + ls 
#cd() { builtin cd "$@" && pwd && ls; }

#short cut
alias at='source ~/tensorflow/bin/activate'
alias sn='shutdown now'
alias op='cd ~/work/md_document/today_issue && code .'

#script save
#alias cdss='cd ~/catkin_ws/src/RSD/src/save_terminal'
#alias cdcap='cd ~/catkin_ws/src/RSD/src/save_success'

#alias rlcap='rosrun image_view image_saver image:=/image_capture'
#alias rsd='rosrun RSD DQNAgent.py'


#gedit .bashrc
alias sb='source ~/.bashrc'
alias eb='gedit ~/.bashrc'

#office
#alias lo='libreoffice --writer'
#alias ch='/usr/bin/google-chrome-stable'

#ROS Control
alias sb='source ~/.bashrc'
alias eb='gedit ~/.bashrc'
alias cw='cd ~/catkin_ws'
alias cs='cd ~/catkin_ws/src'
alias cm='cd ~/catkin_ws && catkin_make'
#
#alias goto='rosservice call /multi_setpoint_local -- POINT'
alias offboard='rostopic pub /multi/set_mode std_msgs/String "offboard"'
alias land='rostopic pub /multi/set_mode std_msgs/String "auto.land"'
alias arm='rostopic pub /multi/arming std_msgs/Bool 1'
alias disarm='rostopic pub /multi/arming std_msgs/Bool 0'

#alias rlworld='roslaunch swarm_ctrl_pkg iitp_test.launch'
#alias rlpid='roslaunch selfie_drone selfie.launch' 
#alias rldetect='roslaunch tensorflow_object_detector usb_cam_detector.launch'
#alias rlssd='roslaunch ssd_people_detector_ros usb_cam_detector.launch'

source  /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash
#source ~/Firmware/Tools/setup_gazebo.bash ~/Firmware ~/Firmware/build/posix_sitl_default
#export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/Firmware
#export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/Firmware/Tools/sitl_gazebo

export ROS_MASTER_URI=http://localhost:11311
export ROS_HOSTNAME=localhost

#export ROS_MASTER_URI=http://192.168.43.116:11311
#export ROS_HOSTNAME=192.168.43.116

#export ROS_MASTER_URI=http://localhost:11311
#export ROS_HOSTNAME=169.254.170.230

function goto() {

    rostopic pub /move_base_simple/goal geometry_msgs/PoseStamped '{header: {stamp: now, frame_id: "map"}, pose: {position: {x: '$1', y: '$2', z: 0.0}, orientation: {w: '$3'}}}'
}

export ROS_LAUNCH_SSH_UNKNOWN=1
export CPLUS_INCLUDE_PATH="$CPLUS_INCLUDE_PATH:/usr/include/python2.7/"

export TURTLEBOT3_MODEL=waffle_pi




  
```

