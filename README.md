# kratos issue 3156 bug 复现

先说结论，鉴定为进错目录了。

## 工程搭建步骤

1. `kratos new playground` 创建工程。
2. 从 [这里](https://github.com/grpc-ecosystem/grpc-gateway/blob/main/protoc-gen-openapiv2/options/openapiv2.proto) 下载对应文件到 third_party 目录下。
3. 按照 issue 中图片的描述修改 [greeter.proto](./api/helloworld/v1/greeter.proto) 文件。

## 问题复现步骤

```sh
# 在工程根目录
$ cd api/helloworld/v1 
$ kratos proto client greeter.proto 

protoc-gen-openapiv2/options/annotations.proto: File not found.
greeter.proto:6:1: Import "protoc-gen-openapiv2/options/annotations.proto" was not found or had errors.
exit status 1
```

## 正确使用方法

```sh
# 在工程根目录
$ kratos proto client api/helloworld/v1/greeter.proto
proto: api/helloworld/v1/greeter.proto
```

或者直接

```sh
# 在工程根目录
$ make api
```