# 介绍

为了方便我们快速开发基于云的分布式微服务应用，Go Micro 提供了一个叫做 Runtime 的 CLI 工具。

## 安装

它是一个二进制可执行文件，我们可以通过以下命令安装到我们的 `$GOPATH/bin` 目录。

```bash
go get github.com/micro/micro/v2
```

或者你也可以直接获取已经编译好的二进制文件。

* 如果你是 MacOS 用户，可以执行以下命令

  ```bash
  curl -fsSL https://raw.githubusercontent.com/micro/micro/master/scripts/install.sh | /bin/bash
  ```

* 如果你是 Linux 用户，可以执行以下命令

  ```bash
  wget -q  https://raw.githubusercontent.com/micro/micro/master/scripts/install.sh -O - | /bin/bash
  ```

* 如果你是 Windows 用户，可以执行以下命令

  ```bash
  powershell -Command "iwr -useb https://raw.githubusercontent.com/micro/micro/master/scripts/install.ps1 | iex"
  ```



安装完成后，检查 `$GOPATH/bin` 是否存在你的系统 PATH 检索路径下，如果没有，需要添加。

在 Terminal 终端中输入 `micro` , 如果看到以下 HELP 界面，证明已经完成安装。

```text
bruce:src/ $ micro
NAME:
   micro - A microservice runtime

USAGE:
   micro [global options] command [command options] [arguments...]

VERSION:
   latest

COMMANDS:
   api         Run the api gateway
   auth        Run the auth service
   login       Login using a token
   whoami      Account information
   bot         Run the chatops bot
   cli         Run the interactive CLI
   call        Call a service e.g micro call greeter Say.Hello '{"name": "John"}
   stream      Create a service stream
   publish     Publish a message to a topic
   stats       Query the stats of a service
   env         Get/set micro cli environment
   file        Move files between your local machine and the server
   list        List items in registry or network
   register    Register an item in the registry
   deregister  Deregister an item in the registry
   get         Get item from registry
   broker      Run the message broker
   health      Check the health of a service
   proxy       Run the service proxy
   router      Run the micro network router
   tunnel      Run the micro network tunnel
   network     Run the micro network node
   registry    Run the service registry
   runtime     Run the micro runtime
   run         Required usage: micro run [source]
   kill        Require usage: micro kill [source]
   update      Require usage: micro update [source]
   services    Require usage: micro services
   status      Require usage: micro status [service] [version]
   logs        Get logs for a service
   debug       Run the micro debug service
   trace       Get tracing info from a service
   server      Run the micro server
   service     Run a micro service
   store       Run the micro store service
   new         Create a service template
   plugin      Plugin commands
   web         Run the web dashboard
   config      Manage configuration values
   init        Run the micro operator
   help, h     Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --client value                       Client for go-micro; rpc [$MICRO_CLIENT]
   --client_request_timeout value       Sets the client request timeout. e.g 500ms, 5s, 1m. Default: 5s [$MICRO_CLIENT_REQUEST_TIMEOUT]
   --client_retries value               Sets the client retries. Default: 1 (default: 1) [$MICRO_CLIENT_RETRIES]
   --client_pool_size value             Sets the client connection pool size. Default: 1 (default: 0) [$MICRO_CLIENT_POOL_SIZE]
   --client_pool_ttl value              Sets the client connection pool ttl. e.g 500ms, 5s, 1m. Default: 1m [$MICRO_CLIENT_POOL_TTL]
   --register_ttl value                 Register TTL in seconds (default: 60) [$MICRO_REGISTER_TTL]
   --register_interval value            Register interval in seconds (default: 30) [$MICRO_REGISTER_INTERVAL]
   --server value                       Server for go-micro; rpc [$MICRO_SERVER]
   --server_name value                  Name of the server. go.micro.srv.example [$MICRO_SERVER_NAME]
   --server_version value               Version of the server. 1.1.0 [$MICRO_SERVER_VERSION]
   --server_id value                    Id of the server. Auto-generated if not specified [$MICRO_SERVER_ID]
   --server_address value               Bind address for the server. 127.0.0.1:8080 [$MICRO_SERVER_ADDRESS]
   --server_advertise value             Used instead of the server_address when registering with discovery. 127.0.0.1:8080 [$MICRO_SERVER_ADVERTISE]
   --server_metadata value              A list of key-value pairs defining metadata. version=1.0.0 [$MICRO_SERVER_METADATA]
   --broker value                       Broker for pub/sub. http, nats, rabbitmq [$MICRO_BROKER]
   --broker_address value               Comma-separated list of broker addresses [$MICRO_BROKER_ADDRESS]
   --profile value                      Debug profiler for cpu and memory stats [$MICRO_DEBUG_PROFILE]
   --registry value                     Registry for discovery. etcd, mdns [$MICRO_REGISTRY]
   --registry_address value             Comma-separated list of registry addresses [$MICRO_REGISTRY_ADDRESS]
   --runtime value                      Runtime for building and running services e.g local, kubernetes (default: "local") [$MICRO_RUNTIME]
   --runtime_source value               Runtime source for building and running services e.g github.com/micro/service (default: "github.com/micro/services") [$MICRO_RUNTIME_SOURCE]
   --selector value                     Selector used to pick nodes for querying [$MICRO_SELECTOR]
   --store value                        Store used for key-value storage [$MICRO_STORE]
   --store_address value                Comma-separated list of store addresses [$MICRO_STORE_ADDRESS]
   --store_database value               Database option for the underlying store [$MICRO_STORE_DATABASE]
   --store_table value                  Table option for the underlying store [$MICRO_STORE_TABLE]
   --transport value                    Transport mechanism used; http [$MICRO_TRANSPORT]
   --transport_address value            Comma-separated list of transport addresses [$MICRO_TRANSPORT_ADDRESS]
   --tracer value                       Tracer for distributed tracing, e.g. memory, jaeger [$MICRO_TRACER]
   --tracer_address value               Comma-separated list of tracer addresses [$MICRO_TRACER_ADDRESS]
   --auth value                         Auth for role based access control, e.g. service [$MICRO_AUTH]
   --auth_id value                      Account ID used for client authentication [$MICRO_AUTH_ID]
   --auth_secret value                  Account secret used for client authentication [$MICRO_AUTH_SECRET]
   --auth_namespace value               Namespace for the services auth account [$MICRO_AUTH_NAMESPACE]
   --auth_public_key value              Public key for JWT auth (base64 encoded PEM) [$MICRO_AUTH_PUBLIC_KEY]
   --auth_private_key value             Private key for JWT auth (base64 encoded PEM) [$MICRO_AUTH_PRIVATE_KEY]
   --auth_provider value                Auth provider used to login user [$MICRO_AUTH_PROVIDER]
   --auth_provider_client_id value      The client id to be used for oauth [$MICRO_AUTH_PROVIDER_CLIENT_ID]
   --auth_provider_client_secret value  The client secret to be used for oauth [$MICRO_AUTH_PROVIDER_CLIENT_SECRET]
   --auth_provider_endpoint value       The enpoint to be used for oauth [$MICRO_AUTH_PROVIDER_ENDPOINT]
   --auth_provider_redirect value       The redirect to be used for oauth [$MICRO_AUTH_PROVIDER_REDIRECT]
   --auth_provider_scope value          The scope to be used for oauth [$MICRO_AUTH_PROVIDER_SCOPE]
   --config value                       The source of the config to be used to get configuration [$MICRO_CONFIG]
   --local                              Enable local only development: Defaults to true. (default: false)
   --enable_acme                        Enables ACME support via Let's Encrypt. ACME hosts should also be specified. (default: false) [$MICRO_ENABLE_ACME]
   --acme_hosts value                   Comma separated list of hostnames to manage ACME certs for [$MICRO_ACME_HOSTS]
   --acme_provider value                The provider that will be used to communicate with Let's Encrypt. Valid options: autocert, certmagic [$MICRO_ACME_PROVIDER]
   --enable_tls                         Enable TLS support. Expects cert and key file to be specified (default: false) [$MICRO_ENABLE_TLS]
   --tls_cert_file value                Path to the TLS Certificate file [$MICRO_TLS_CERT_FILE]
   --tls_key_file value                 Path to the TLS Key file [$MICRO_TLS_KEY_FILE]
   --tls_client_ca_file value           Path to the TLS CA file to verify clients against [$MICRO_TLS_CLIENT_CA_FILE]
   --api_address value                  Set the api address e.g 0.0.0.0:8080 [$MICRO_API_ADDRESS]
   --namespace value                    Set the micro service namespace (default: "micro") [$MICRO_NAMESPACE]
   --proxy_address value                Proxy requests via the HTTP address specified [$MICRO_PROXY_ADDRESS]
   --web_address value                  Set the web UI address e.g 0.0.0.0:8082 [$MICRO_WEB_ADDRESS]
   --network value                      Set the micro network name: local, go.micro [$MICRO_NETWORK]
   --network_address value              Set the micro network address e.g. :9093 [$MICRO_NETWORK_ADDRESS]
   --router_address value               Set the micro router address e.g. :8084 [$MICRO_ROUTER_ADDRESS]
   --gateway_address value              Set the micro default gateway address e.g. :9094 [$MICRO_GATEWAY_ADDRESS]
   --tunnel_address value               Set the micro tunnel address e.g. :8083 [$MICRO_TUNNEL_ADDRESS]
   --api_handler value                  Specify the request handler to be used for mapping HTTP requests to services; {api, proxy, rpc} [$MICRO_API_HANDLER]
   --api_namespace value                Set the namespace used by the API e.g. com.example.api [$MICRO_API_NAMESPACE]
   --web_namespace value                Set the namespace used by the Web proxy e.g. com.example.web [$MICRO_WEB_NAMESPACE]
   --web_url value                      Set the host used for the web dashboard e.g web.example.com [$MICRO_WEB_HOST]
   --enable_stats                       Enable stats (default: false) [$MICRO_ENABLE_STATS]
   --auto_update                        Enable automatic updates (default: false) [$MICRO_AUTO_UPDATE]
   --update_url value                   Set the url to retrieve system updates from (default: "https://go.micro.mu/update") [$MICRO_UPDATE_URL]
   --report_usage                       Report usage statistics (default: true) [$MICRO_REPORT_USAGE]
   --env value, -e value                Override environment [$MICRO_ENV]
   --plugin value                       Comma separated list of plugins e.g broker/rabbitmq, registry/etcd, micro/basic_auth, /path/to/plugin.so [$MICRO_PLUGIN]
   --help, -h                           show help (default: false)
   --version                            print the version (default: false)
```

我们可以看到，micro 命令为我们提供了一系列的 Command ，

## 功能





