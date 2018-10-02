# Ansible modules for Traffic Control - Examples

### Source
* Upstream: [ansible-tc](https://github.com/msuringa/ansible-tc)
* Fork: [rayfordj/ansible-tc](https://github.com/rayfordj/ansible-tc)

## Overview

* Set appropriate values in the yml files
* Execute setup-htb... and setup-filters 
* Configure appropriate net_cls cgroups structure and populate net_cls.classid
  with corresponding major:minor of tc 
* Classify process(es) in desired cgroup net_cls tasks bucket(s)


## Example
```bash
ansible-playbook -i ./inventory setup-htb-qdisc-and-classes.yml

ansible-playbook -i ./inventory setup-filters.yml

mkdir -p /sys/fs/cgroup/net_cls/examples/id{2..6}

for i in {2..6}; do echo 0x0010000"${i}" > /sys/fs/cgroup/net_cls/examples/id"${i}"/net_cls.classid ; done

cgexec -g net_cls:examples/id3 your-command-with-options  &

cgexec -g net_cls:examples/id3 some-other-command-with-options  &

cgexec -g net_cls:examples/id5 yet-another-command-with-options  &

echo "${RUNNING-PID}" > /sys/fs/cgroup/net_cls/examples/id2/tasks

```

