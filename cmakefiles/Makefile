

BUILD_TYPE=Debug
PACKAGE_DIR_REMOTE=/var/www/html/static/packages

DID=lib-$(@)
IMAGE=flow123d/base-env


LIBS_WITH_MPICH := petsc armadillo yamlcpp

.PHONY : mpich
mpich:
	-@docker rm -f $(DID)
	docker run --rm -di \
			--name=$(DID) \
			--volume=$(CURDIR):/tmp/work \
			$(IMAGE)

	-docker exec $(DID) make -C /tmp/work/$(@) build_type=$(BUILD_TYPE) package
	-docker exec $(DID) chown -Rc $(shell id -u) /tmp/work
	docker rm -f $(DID)
	scp -r $(CURDIR)/$(@)/packages/* builder@ciflow.nti.tul.cz:$(PACKAGE_DIR_REMOTE)/


.PHONY : $(LIBS_WITH_MPICH)
$(LIBS_WITH_MPICH):
	-@docker rm -f $(DID)
	docker run --rm -di \
			--name=$(DID) \
			--volume=$(CURDIR):/tmp/work \
			$(IMAGE)

	-docker exec $(DID) wget -qO /tmp/mpich-3.2.0.deb http://ciflow.nti.tul.cz/static/packages/mpich_3.2.0_$(BUILD_TYPE)/mpich-3.2.0.deb
	-docker exec $(DID) dpkg -i /tmp/mpich-3.2.0.deb
	-docker exec $(DID) rm -rf /tmp/mpich-3.2.0.deb

	-docker exec $(DID) /bin/bash -c "PATH=/usr/local/mpich-3.2.0/bin:\$$PATH make -C /tmp/work/$(@) build_type=$(BUILD_TYPE) package"
	-docker exec $(DID) chown -R $(shell id -u) /tmp/work
	docker rm -f $(DID)
	scp -r $(CURDIR)/$(@)/packages/* builder@ciflow.nti.tul.cz:$(PACKAGE_DIR_REMOTE)/

.PHONY : bddcml
bddcml:
	-@docker rm -f $(DID)
	docker run --rm -di \
			--name=$(DID) \
			--volume=$(CURDIR):/tmp/work \
			$(IMAGE)

	-docker exec $(DID) wget -qO /tmp/mpich-3.2.0.deb http://ciflow.nti.tul.cz/static/packages/mpich_3.2.0_$(BUILD_TYPE)/mpich-3.2.0.deb
	-docker exec $(DID) dpkg -i /tmp/mpich-3.2.0.deb
	-docker exec $(DID) rm -rf /tmp/mpich-3.2.0.deb

	-docker exec $(DID) wget -qO /tmp/petsc_3.6.1.deb http://ciflow.nti.tul.cz/static/packages/petsc_3.6.1_$(BUILD_TYPE)/petsc-3.6.1.deb
	-docker exec $(DID) dpkg -i /tmp/petsc_3.6.1.deb
	-docker exec $(DID) rm -rf /tmp/petsc_3.6.1.deb

	-docker exec $(DID) /bin/bash -c "PATH=/usr/local/mpich-3.2.0/bin:\$$PATH make -C /tmp/work/$(@) build_type=$(BUILD_TYPE) package"
	-docker exec $(DID) chown -Rc $(shell id -u) /tmp/work
	docker rm -f $(DID)
	scp -r $(CURDIR)/$(@)/packages/* builder@ciflow.nti.tul.cz:$(PACKAGE_DIR_REMOTE)/
