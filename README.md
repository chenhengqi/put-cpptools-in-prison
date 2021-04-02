# Put cpptools in prison

## create CPU and Memory cgroups

```
$ sudo mkdir -p /sys/fs/cgroup/cpu/prison
$ sudo mkdir -p /sys/fs/cgroup/memory/prison
```

## set CPU and Memory limits

```
$ sudo sh -c 'echo 10000 > /sys/fs/cgroup/cpu/prison/cpu.cfs_period_us'
$ sudo sh -c 'echo 1000 > /sys/fs/cgroup/cpu/prison/cpu.cfs_quota_us'
$ sudo sh -c 'echo 131072 > /sys/fs/cgroup/memory/prison/memory.limit_in_bytes'
```

## put cpptools in prison

```shell
#!/bin/bash
for pid in `pgrep cpptools`
do
    sudo sh -c "echo $pid > /sys/fs/cgroup/cpu/prison/cgroup.procs"
    sudo sh -c "echo $pid > /sys/fs/cgroup/memory/prison/cgroup.procs"
done
```
