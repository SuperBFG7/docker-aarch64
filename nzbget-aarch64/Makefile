all: nzbget-aarch64

nzbget-aarch64: build tag

force: force-build tag

build:
	sudo docker build \
		-t superbfg7/nzbget-aarch64 \
		--build-arg "UID=`id -u kodi`" \
		--build-arg "GID=`id -g kodi`" .

force-build:
	sudo docker build --no-cache \
		-t superbfg7/nzbget-aarch64 \
		--build-arg "UID=`id -u kodi`" \
		--build-arg "GID=`id -g kodi`" .

tag: build
	sudo docker tag superbfg7/nzbget-aarch64 superbfg7/nzbget-aarch64:`/usr/bin/pacman -Sp --print-format %v nzbget`

create:
	sudo docker rename nzbget nzbget_old
	sudo docker create \
		--name=nzbget \
		-v /etc/localtime:/etc/localtime:ro \
		-v /opt/nzbget:/config \
		-v /data/video/nzb/downloads:/downloads \
		-p 6789:6789 \
		superbfg7/nzbget-aarch64

restart:
	sudo docker stop nzbget_old
	sudo docker start nzbget

cleanup:
	sudo docker rm nzbget_old

clean:
	sudo docker rm nzbget
	sudo docker rmi superbfg7/nzbget-aarch64

install:
	sudo cp -i nzbget.service /etc/systemd/system/
	@echo systemctl enable nzbget
	@echo systemctl start nzbget
