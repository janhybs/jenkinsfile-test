

BUILD_TYPE=Debug
PACKAGE_DIR_REMOTE=/var/www/html/static/packages

DID=lib-$(@)
IMAGE=flow123d/base-env

.PHONY : armadillo
armadillo:
	echo "Cascs"

.PHONY : mpich
mpich:
	-@docker rm -f $(DID)
	docker run --rm -di \
			--name=$(DID) \
			--volume=$(CURDIR):/tmp/work \
			$(IMAGE)

	docker exec $(DID) apt-get -y update
	docker exec $(DID) apt-get -y install \
			libboost-program-options-dev \
			libboost-serialization-dev \
			libboost-regex-dev \
			libboost-filesystem-dev \
			cmake

	docker exec $(DID) make -C /tmp/work/$(@) build_type=$(BUILD_TYPE) package
	docker rm -f $(DID)
	scp -r $(CURDIR)/$(@)/packages/* root@ciflow.nti.tul.cz:$(PACKAGE_DIR_REMOTE)/


.PHONY : yamlcpp
yamlcpp:
	-@docker rm -f $(DID)
	docker run --rm -ti \
			--name=$(DID) \
			--volume=$(CURDIR):/tmp/work \
			$(IMAGE)

	# docker exec $(DID) apt-get -y update
	# docker exec $(DID) apt-get -y install \
	# 		cmake

	docker exec $(DID) make -C /tmp/work/$(@) build_type=$(BUILD_TYPE) package
	docker rm -f $(DID)
	scp -r $(CURDIR)/$(@)/packages/* root@ciflow.nti.tul.cz:$(PACKAGE_DIR_REMOTE)/
