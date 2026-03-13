#!/bin/sh

#Exit if command fails or variable is unset
set -eu

# Update package lists
sudo apt-get update

# Steam packages need multiverse and i386 support on Ubuntu
sudo dpkg --add-architecture i386
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y multiverse
sudo apt-get update

#Install dependencies
sudo apt-get install -y \
	git \
	jq \
	fzf \
	iputils-ping \
	geoip-bin \
	whois \
	curl \
	coreutils \
	grep \
	procps \
	psmisc \
	sed \
	gawk \
	gpg \
	steamcmd \
    fonts-noto-color-emoji

#Install gum (not in the official repos)
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://repo.charm.sh/apt/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/charm.gpg
echo "deb [signed-by=/etc/apt/keyrings/charm.gpg] https://repo.charm.sh/apt/ * *" | sudo tee /etc/apt/sources.list.d/charm.list
sudo apt update && sudo apt install gum -y

#Clonig the GitHub repository over HTTPS
git clone https://github.com/WoozyMasta/dayz-ctl.git
cd dayz-ctl

#Fix for the Error:
#url: (60) SSL certificate OpenSSL verify result: unable to get local issuer certificate (20)
#More details here: https://curl.se/docs/sslcerts.html

#curl failed to verify the legitimacy of the server and therefore could not
#establish a secure connection to it. To learn more about this situation and
#how to fix it, please visit the webpage mentioned above.

#By not verifying the legitimacy of the ssl certificate for dayz.com
sed -i 's/curl -sSfLA/curl -k -sSfLA/g' dayz-ctl

#run the script
./dayz-ctl
