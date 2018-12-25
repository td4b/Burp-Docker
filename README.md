**Docker Container**

This is a Docker Container that houses several useful Pentesting tools.

First and Foremost it offers an GUI to Bursuite that is running in a container.

This is intended to act as a lighweight pentesting toolset. This is super barebones but will be adding additional scripts & utilities as time goes on!

**Install (Pull Docker Image)**
1) Pull the Image.
```bash
docker pull tdub17/pentools:latest
```
2) Install the Dependencies (socat & xquartz)
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null
brew install socat

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null ; brew install caskroom/cask/brew-cask 2> /dev/null
brew cask install xquartz
```

**Usage (Guide)**

1)) Get Local IP.
```bash
IP=$(ifconfig en0 | grep inet | grep -v inet6 | awk '{print $2}')
```
2) Enable Local Port Forwarding, run & minimize this Socket.
```bash
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```
3) Launch Docker Container.
```bash
docker run -tdi -v /tmp/.X11-unix/:/tmp/.X11-unix -e DISPLAY=$IP:0 -p 8080:8080 tdub17/pentools
```

That's it, enjoy :)
