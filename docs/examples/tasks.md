# Tasks

## Basic Task Interaction

### What is a task UPID?

Most actions on Proxmox services are backed by tasks. These are visible in the web UI
and are created when automation or users request actions be completed.

Tasks are uniquely identified by a UPID which follows the format `UPID:<node_name>:<pid_in_hex>:<pstart_in_hex>:<starttime_in_hex>:<type>:<id (optional)>:<user>@<realm>:`.

For example `UPID:example-node:000AE992:00A21BA7:618C1D55:vzdump:100:root@pam:` or `UPID:example-node:00213D37:01ECA9AD:618F6B8D:aptupdate::root@pam:`.

### Getting Task IDs

The Proxmoxer service instance will maintain a record of all past tasks as well as all currently
active tasks. The list of these tasks can be requested.

```pycon
>>> prox.nodes("mini-pve-0").tasks.get(limit=3, source="all")
[{'id': '103', 'user': 'root@pam', 'pstart': 65597267, 'saved': '0', 'type': 'vzdump', 'pid': 851962, 'upid': 'UPID:mini-pve-0:000CFFFA:03E8EF53:619480BA:vzdump:103:root@pam:', 'node': 'mini-pve-0', 'starttime': 1637122234, 'status': 'RUNNING'}, {'user': 'root@pam', 'endtime': 1637122161, 'id': '', 'upid': 'UPID:mini-pve-0:000CFC5C:03E8D0C3:6194806C:aptupdate::root@pam:', 'node': 'mini-pve-0', 'starttime': 1637122156, 'status': 'OK', 'type': 'aptupdate', 'pid': 851036, 'pstart': 65589443}, {'endtime': 1637121960, 'id': '', 'user': 'root@pam', 'pstart': 65550050, 'pid': 848306, 'type': 'vncshell', 'starttime': 1637121762, 'upid': 'UPID:mini-pve-0:000CF1B2:03E836E2:61947EE2:vncshell::root@pam:', 'node': 'mini-pve-0', 'status': 'OK'}]
```

Additional filters can be found in the [documentation](https://pve.proxmox.com/pve-docs/api-viewer/index.html#/nodes/{node}/tasks).

### Getting Task Details

Each task has associated information on the status of the task and a log of the output of the task.
This data can be collected by using the UPID of the task.

```pycon
>>> prox.nodes("mini-pve-0").tasks("UPID:mini-pve-0:000CFC5C:03E8D0C3:6194806C:aptupdate::root@pam:").status.get()
{'pid': 851036, 'node': 'mini-pve-0', 'type': 'aptupdate', 'upid': 'UPID:mini-pve-0:000CFC5C:03E8D0C3:6194806C:aptupdate::root@pam:', 'status': 'stopped', 'starttime': 1637122156, 'pstart': 65589443, 'id': '', 'exitstatus': 'OK', 'user': 'root@pam'}
>>> prox.nodes("mini-pve-0").tasks("UPID:mini-pve-0:000CFC5C:03E8D0C3:6194806C:aptupdate::root@pam:").log.get()
[{'n': 1, 't': 'starting apt-get update'}, {'t': 'Hit:1 http://ftp.us.debian.org/debian bullseye InRelease', 'n': 2}, {'n': 3, 't': 'Get:2 http://ftp.us.debian.org/debian bullseye-updates InRelease [39.4 kB]'}, {'t': 'Get:3 http://security.debian.org bullseye-security InRelease [44.1 kB]', 'n': 4}, {'n': 5, 't': 'Get:4 http://download.proxmox.com/debian/pve bullseye InRelease [3053 B]'}, {'t': 'Fetched 86.5 kB in 1s (125 kB/s)', 'n': 6}, {'t': 'Reading package lists...', 'n': 7}, {'t': 'TASK OK', 'n': 8}]
```

The status information (for completed tasks) includes information on who, when, where, and
what was done in that task. The log contains a list of dicts which are `{'n': <int_of_line_number>, 't': '<line_text>'}`, one for each line of output.

## Tasks in Progress

While tasks are active, the `status` endpoint returns information on the setup and start of the task
and a status or "running".

### Blocking Until Task is Complete

Many API endpoints will return a task UPID while the task completes in the background. While this
can be useful to allow asynchronous execution, often you may desire to wait (block) for a task to finish.

To @TODO@
