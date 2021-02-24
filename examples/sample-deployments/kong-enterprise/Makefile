define check
	kubectl config current-context | grep $1 || (echo ERROR: wrong cluster && exit 1)
endef

.PHONY: build
build:
	kustomize build .

.PHONY: diff
diff:
	$(call check, minikube)
	kustomize build . | kubectl diff -f - | less -SR

.PHONY: deploy
deploy:
	$(call check, minikube)
	kubectl delete job kong-migrations -n kong
	kustomize build . | kubectl apply -f - | grep -v unchanged
