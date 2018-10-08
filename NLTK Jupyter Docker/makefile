.PHONY: clean build push

repository := varadtupe
image := nltk_jupyter
tag := $(shell git rev-parse --short HEAD)

clean:
	docker image prune -f
	docker container prune -f
	find . -regex "\(.*__pycache__.*\|*.py[co]\)" -delete

build: clean docker-build docker-tag

# should be used only for automated builds
push: docker-push


# --- docker ---
docker-build:
	docker build -t $(repository)/$(image) .
	#s

docker-tag:
	docker tag \
		$(repository)/$(image) \
		$(registry)/$(repository)/$(image):latest

docker-push:
	docker push $(repository)/$(image):latest
	# docker push varadtupe/nltk_jupyter:latest

# --- utilities ---
run:
	docker-compose build
	docker-compose up --abort-on-container-exit

run-detached:
	docker-compose build
	docker-compose up -d

restart:
	docker-compose down
	docker container prune -f
	docker-compose build
	docker-compose up
