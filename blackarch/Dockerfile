FROM archlinux:latest
ADD https://blackarch.org/strap.sh tmp/strap.sh
RUN \
chmod +x /tmp/strap.sh \
&& /tmp/strap.sh \
&& rm -f /tmp/strap.sh \
&& pacman --noconfirm -Sy archlinux-keyring \
&& yes | pacman -Syy tmux \
