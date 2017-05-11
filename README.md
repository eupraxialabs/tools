dockerfiles-centos-tools
========================

Dockerfile to build a very useful tools image on CentOS 7

[Tools image](http://developerblog.redhat.com/2015/03/11/introducing-the-rhel-container-for-rhel-atomic-host/) is intended to be used as [Super Privileged Container](http://developerblog.redhat.com/2014/11/06/introducing-a-super-privileged-container-concept/) (SPC) to extend the set of tools provided by Atomic Host. More tips how to use the image can be found at [Project Atomic blog](http://www.projectatomic.io/blog/2015/09/introducing-the-fedora-tools-image-for-fedora-atomic-host/).

To build, copy the sources down from GitHub and call:


```
    # docker build --rm -t eupraxialabs/tools:1.1 .
```

To run:

1. Not running on Atomic Host? Install the `atomic` tool with:
   ```
   # yum install atomic
   ```
2. If you are at Atomic Host, you have `atomic` tool pre-installed and thus you can directly call

   ```
   # atomic run eupraxialabs/tools:1.1
   ```

   to get a shell in the tools container, or

   ```
   # atomic run eupraxialabs/tools:1.1 <command>
   ```

   to run a specific command. For example:

   ```
   # atomic run eupraxialabs/tools:1.1 man systemd
   ```

`atomic` tool uses image labels to figure out the `docker run` command. You can check the [RUN label](https://github.com/projectatomic/atomic/blob/master/docs/atomic-run.1.md) by calling

```
docker inspect -f '{{.Config.Labels.RUN}}' eupraxialabs/tools
```
Let's look at a special tool while inside the container. The command ssh-import-id will allow us to easy add users that need to ssh into any Atomic Host. It does this by pulling a public key from either Launchpad or GitHub and appending it to a <user>/.ssh/authorized_keys file.

```
[root@atomic1 /]# ssh-import-id gh:davidjbrewer --output /host/home/centos/.ssh/authorized_keys



```
