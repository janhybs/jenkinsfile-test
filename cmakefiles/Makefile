

BUILD_TYPE=Debug
PACKAGE_DIR_REMOTE=/var/www/html/static/packages

DID=lib-$(@)
IMAGE=flow123d/base-env


LIBS := mpich yamlcpp armadillo petsc bddcml

.PHONY : $(LIBS)
$(LIBS):
	-@docker rm -f $(DID)
	docker run --rm -di \
			--name=$(DID) \
			--volume=$(CURDIR):/tmp/work \
			$(IMAGE)

	docker exec $(DID) make -C /tmp/work/$(@) build_type=$(BUILD_TYPE) package
	docker rm -f $(DID)
	scp -r $(CURDIR)/$(@)/packages/* root@ciflow.nti.tul.cz:$(PACKAGE_DIR_REMOTE)/
