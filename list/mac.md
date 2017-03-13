Notes / Mac OS X
===

## docker 与 Mac localhost通信
docker-daemon在Mac上的虚拟机（HyperKit）内运行。daemon的127.0.0.1为HyperKit实例而不是Mac。

```text
┌────────────────┐
│   Mac OS X     │
├────────────┐   │
│  HyperKit  │   │
├────────┐   │   │
│ docker │   │   │
```

要让daemon使用在Mac上的服务，手动添加一个ip给lo0接口。然后使用这个地址。

```shell
sudo ifconfig lo0 alias 172.31.255.254
```

这样能让daemon访问Mac上的服务（前提是服务监听了刚才设置的地址）。配合SS可有效加速registry访问速度。


