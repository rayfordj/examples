# Ansible modules for Traffic Control - IMS Examples

### Source
* Upstream: [ansible-tc](https://github.com/msuringa/ansible-tc)
* Fork: [rayfordj/ansible-tc](https://github.com/rayfordj/ansible-tc)

## Overview

* Set hosts and values in the yml files
* Execute setup-htb-qdisc-classes-filters-and-cgroup.net_cls.yml play
* Classify process(es) in desired cgroup net_cls tasks bucket(s)


## Example
```bash
ansible-playbook -i ./inventory setup-htb-qdisc-classes-filters-and-cgroup.net_cls.yml

cgexec -g net_cls:ims/planA your-command-with-options  &

cgexec -g net_cls:ims/planA some-other-command-with-options  &

cgexec -g net_cls:ims/planB yet-another-command-with-options  &

echo "${RUNNING-PID}" > /sys/fs/cgroup/net_cls/ims/planB/tasks

ansible-playbook -i ./inventory modify-class-rate-ceil.yml


```

