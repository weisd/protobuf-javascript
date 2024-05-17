## 使用docker编译protoc-gen-js

运行容器

```
docker run --rm -it -v /path/to/protobuf-javascript:/data --entrypoint=/bin/bash gcr.io/bazel-public/bazel:latest
```

在容器中运行

```
# 编译
bazel build generator/protoc-gen-js

# 安装protoc
PB_REL="https://github.com/protocolbuffers/protobuf/releases"
curl -LO $PB_REL/download/v25.1/protoc-25.1-linux-x86_64.zip
unzip protoc-25.1-linux-x86_64.zip -d $HOME/.local

# 引用编译好的文件
protoc --plugin=protoc-gen-js=/data/bazel-bin/generator/protoc-gen-js --js_out=import_style=commonjs:.  /path/to/proto

```