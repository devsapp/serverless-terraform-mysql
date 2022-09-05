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
	docker tag ${IMG}:latest registry.cn-hangzhou.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-shanghai.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-qingdao.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-beijing.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-zhangjiakou.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-huhehaote.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-wulanchabu.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-shenzhen.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-heyuan.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-guangzhou.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker tag ${IMG}:latest registry.cn-chengdu.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}

	docker login -u ${username} -p ${password} registry.cn-hangzhou.aliyuncs.com
	docker push registry.cn-hangzhou.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-shanghai.aliyuncs.com
	docker push registry.cn-shanghai.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-qingdao.aliyuncs.com
	docker push registry.cn-qingdao.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-beijing.aliyuncs.com
	docker push registry.cn-beijing.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-zhangjiakou.aliyuncs.com
	docker push registry.cn-zhangjiakou.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-huhehaote.aliyuncs.com
	docker push registry.cn-huhehaote.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-wulanchabu.aliyuncs.com
	docker push registry.cn-wulanchabu.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-shenzhen.aliyuncs.com
	docker push registry.cn-shenzhen.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-heyuan.aliyuncs.com
	docker push registry.cn-heyuan.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-guangzhou.aliyuncs.com
	docker push registry.cn-guangzhou.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}
	docker login -u ${username} -p ${password} registry.cn-chengdu.aliyuncs.com
	docker push registry.cn-chengdu.aliyuncs.com/serverless_devs/serverless-terraform-mysql-creator:${VERSION}

vendor:
	go mod vendor


build&push: build-img push
