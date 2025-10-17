## QUESTION A

What happens if you run `ansible-inventory --list` in the directory you created above?

```bash
💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 15:12 🌸ansible-inventory --list
{
    "_meta": {
        "hostvars": {
            "192.168.121.119": {
                "ansible_ssh_private_key_file": "/home/claire/devops24/lab_environment/deploy_key",
                "ansible_user": "deploy"
            },
            "192.168.121.17": {
                "ansible_ssh_private_key_file": "/home/claire/devops24/lab_environment/deploy_key",
                "ansible_user": "deploy"
            }
        }
    },
    "all": {
        "children": [
            "ungrouped",
            "db",
            "web"
        ]
    },
    "db": {
        "hosts": [
            "192.168.121.17"
        ]
    },
    "web": {
        "hosts": [
            "192.168.121.119"
        ]
    }
}
```

## QUESTION B

What happens if you run `ansible-inventory --graph` in the directory you created above?
```bash
💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 15:11 🌸ansible-inventory --graph
@all:
  |--@ungrouped:
  |--@db:
  |  |--192.168.121.17
  |--@web:
  |  |--192.168.121.119
```

## QUESTION C

In the `hosts` file, add a new host with the same hostname as the machine you're running
ansible on:

    [controller]
    <hostname_of_your_machine> ansible_connection=local

Now run:

    $ ansible -m ping all

Study the output of this command.

What does the `ansible_connection=local` part mean?


## BONUS QUESTION

The command `ansible-config` can be used for creating, viewing, validating, and listing
Ansible configuration.

Try running

    $ ansible-config --help

Make an initial configuration file with the help of this command, and write it into a file
called `ansible.cfg.init`. HINT: Redirections in the terminal can be done with '>' or 'tee(1)'.

Open this file and look at the various options you can configure in Ansible.

In your Ansible working directory where the `ansible.cfg' is, run

    $ ansible-config dump

You should get a pager displaying all available configuration values. How does it differ
from when you run the same command in your usual home directory?