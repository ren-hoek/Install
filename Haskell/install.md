mkdir Install/Haskell

cd Install/Haskell
wget https://haskell.org/platform/download/8.0.2/haskell-platform-8.0.2-unknown-posix--minimal-x86_64.tar.gz

check the download by comparing with https://www.haskell.org/platform/#linux-generic
sha256sum haskell-platform-8.0.2-unknown-posix--minimal-x86_64.tar.gz

tar -xvf haskell-platform-8.0.2-unknown-posix--minimal-x86_64.tar.gz
sudo ./install-haskell-platform.sh

need to install libgmp3
sudo apt-get install libgmp3-dev