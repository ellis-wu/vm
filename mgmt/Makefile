NAME = elliswu/ranchervm
CONTAINER_NAME = myranchervm
VERSION = 0.0.2
NOVNC_VERSION = 0.0.2

.PHONY : all clean build

all: build run

build: noVNC-$(NOVNC_VERSION).tar.gz
	docker build -t $(NAME):$(VERSION) .

noVNC-$(NOVNC_VERSION).tar.gz:
	wget -O noVNC-$(NOVNC_VERSION).tar.gz https://github.com/rancherio/noVNC/archive/v$(NOVNC_VERSION).tar.gz

clean:
	rm -f noVNC-$(NOVNC_VERSION).tar.gz

tag_latest:
	docker tag -f $(NAME):$(VERSION) $(NAME):latest

run:
	docker run -d -v /var/run:/var/run -p 8081:80 -v /var/lib/rancher/vm:/vm --name $(CONTAINER_NAME) $(NAME):$(VERSION)

remove:
	docker stop $(CONTAINER_NAME) && docker rm $(CONTAINER_NAME) && docker rmi $(NAME):$(VERSION)
