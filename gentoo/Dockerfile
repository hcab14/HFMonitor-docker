FROM gentoo/stage3-amd64
MAINTAINER Christoph Mayer <hcab14@gmail.com>

RUN	emerge --sync && \
	emerge 	app-editors/vim \
		dev-vcs/git \
		app-portage/layman
RUN	layman -S && \
	sed -i 's/check_official : Yes/check_official : no/' /etc/layman/layman.cfg && \
	layman -a vifino-overlay
WORKDIR /usr/local
RUN	git clone https://github.com/hcab14/HFMonitor-gentoo.git portage && \
	echo 'PORTDIR_OVERLAY="${PORTDIR_OVERLAY} /usr/local/portage"' >> /etc/portage/make.conf
RUN	sed -i 's/USE="/USE="threads python ncurses /' /etc/portage/make.conf && \
	echo '=sci-libs/volk-9999 **'                >> /etc/portage/package.accept_keywords && \
	echo '=media-libs/portaudio-19.06.00 ~amd64' >> /etc/portage/package.accept_keywords && \
	echo '>=dev-libs/boost-1.62.0-r1 context python threads' >> /etc/portage/package.use/boost && \
	emerge net-install/hfmonitor && \
	emerge -NuvD world

