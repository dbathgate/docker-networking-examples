# Weave Net

```
$ vagrant up
```

## Installation:

Connect to node1: `vagrant ssh node1`
```
sudo su -

curl --location https://github.com/weaveworks/weave/releases/download/latest_release/weave -o /usr/local/bin/weave
chmod +x /usr/local/bin/weave
```

Launch weave
```
weave launch --host 192.168.33.11
```

Connect to node2: `vagrant ssh node2`
```
sudo su -

curl --location https://github.com/weaveworks/weave/releases/download/latest_release/weave -o /usr/local/bin/weave
chmod +x /usr/local/bin/weave
```

Launch weave using node1 IP as peer `192.168.33.11`
```
weave launch --host 192.168.33.12 192.168.33.11
```

Connect to node2: `vagrant ssh node3`
```
sudo su -

curl --location https://github.com/weaveworks/weave/releases/download/latest_release/weave -o /usr/local/bin/weave
chmod +x /usr/local/bin/weave
```

Launch weave using node1 IP as peer `192.168.33.11`
```
weave launch --host 192.168.33.13 192.168.33.11
```

## Testing

In a new terminal, connect to node2: `vagrant ssh node1`
```
sudo su -

eval $(weave env)
docker run -ti --name bb1 busybox
```

Verify hostname
```
hostname
> bb1.weave.local
```

In a new terminal, connect to node3: `vagrant ssh node2`
```
sudo su -

eval $(weave env)
docker run -ti --name bb2 busybox
```

Verify hostname
```
hostname
> bb2.weave.local
```

In a new terminal, connect to node3: `vagrant ssh node3`
```
sudo su -

eval $(weave env)
docker run -ti --name bb3 busybox
```

Verify hostname
```
hostname
> bb3.weave.local
```

Ping `bb1.weave.local` and `bb2.weave.local` from `bb3.weave.local` running on node3
```
ping bb1.weave.local
> PING bb1.weave.local (10.40.0.0): 56 data bytes
> 64 bytes from 10.40.0.0: seq=0 ttl=64 time=1.219 ms
> 64 bytes from 10.40.0.0: seq=1 ttl=64 time=0.757 ms

ping bb2.weave.local
> PING bb2.weave.local (10.32.0.1): 56 data bytes
> 64 bytes from 10.32.0.1: seq=0 ttl=64 time=1.158 ms
> 64 bytes from 10.32.0.1: seq=1 ttl=64 time=0.471 ms
```
