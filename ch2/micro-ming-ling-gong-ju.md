# API 命令

## 功能

服务网关是我们微服务架构对外提供服务的入口。



## 启动

GoMicro提供了服务网关的功能，我们可以通过 `micro api` 来启动。

```text
$ micro api
2020-07-22 17:53:34  file=api/api.go:285 level=info service=api Registering API Default Handler at /
2020-07-22 17:53:34  file=http/http.go:90 level=info service=api HTTP API Listening on [::]:8080
2020-07-22 17:53:34  file=v2@v2.9.1/service.go:200 level=info service=api Starting [service] go.micro.api
2020-07-22 17:53:34  file=grpc/grpc.go:864 level=info service=api Server [grpc] Listening on [::]:52784
2020-07-22 17:53:34  file=grpc/grpc.go:697 level=info service=api Registry [mdns] Registering node: go.micro.api-e26b0a56-5bef-4c72-853d-3008afa9498d
```

可以看到此时在我们本机 `localhost:8080` 启动了网关的 HTTP API 监听。同时，网关也在 `localhost:52784` 启动了一个 gRPC Server 服务。

我们来看下 micro api 有哪些可选参数

