# 修改这里
VERSION ?= 0.0.2
# BUILD_TIME is used for daemon BuildTime in go build.
BUILD_TIME=$(shell date --rfc-3339 s 2> /dev/null | sed -e 's/ /T/')

IMG = serverless-terraform-mysql-creator

fmt:
	go fmt ./...

build-img:
	docker build -t ${IMG}:latest -f Dockerfile .

run:
	docker run -p 9000:9000 --name myTerraform --rm -it ${IMG}:latest

push:
	docker tag ${IMG}:latest registry.cn-hangzhou.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-beijing.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-shanghai.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-huhehaote.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	#docker push registry.cn-hangzhou.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	#docker push registry.cn-beijing.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	docker push registry.cn-shanghai.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}
	docker push registry.cn-huhehaote.aliyuncs.com/fc-demo2/serverless-terraform-mysql-creator:${VERSION}

vendor:
	go mod vendor


build&push: build-img push
