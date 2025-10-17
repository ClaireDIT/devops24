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
När jag kör `ansible-inventory --list` visar Ansible vilka värdar som finns i min inventory fil. Jag ser mina VM och dess ip-addresser vilket jag tar som att ansible kan hitta dem och min hosts-fil fungerar som den ska.
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
När jag körde `ansible-inventory --graph` fick jag i stället en enklara översikt som visar hur strukturen ser ut. den visar att gruppen all innehåller grupperna db och web, och sina respektive ip-adresser.

## QUESTION C

In the `hosts` file, add a new host with the same hostname as the machine you're running
ansible on:

    [controller]
    <hostname_of_your_machine> ansible_connection=local

Now run:

    $ ansible -m ping all

Study the output of this command.

What does the `ansible_connection=local` part mean?
`ansible_connection=local` under contrller antar jag meddelar att min egen dator är värden för ansible och därmed behöver den ej försöka logga in genom ssh. Där med kan den köra kommandona direkt på datorn.

```bash 
💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 15:20 🌸ansible -m ping all
10.6.69.27 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.168.121.119 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.168.121.17 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
När man sen kör ansible -m ping all, så får jag ut också SUCCESS för min egen dator. 

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
```bash
ansible-config --help
usage: ansible-config [-h] [--version] [-v] {list,dump,view,init} ...

View ansible configuration.

positional arguments:
  {list,dump,view,init}
    list                Print all config options
    dump                Dump configuration
    view                View configuration file
    init                Create initial configuration

options:
  --version             show program's version number, config file location, configured module search path, module location, executable location and exit
  -h, --help            show this help message and exit
  -v, --verbose         Causes Ansible to print more debug messages. Adding multiple -v will increase the verbosity, the builtin plugins currently evaluate up
                        to -vvvvvv. A reasonable level to start is -vvv, connection debugging might require -vvvv. This argument may be specified multiple
                        times.

💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 09:39 🌸ansible-config dump > ansible.cfg.init
```
När jag kör ansible-config --help ser jag möjligheterna jag har för att visa, skapa och ändra i ansible inställningarna. 
Med ansible-config dump > ansible.cfg.init skapade jag en fil och skickade standard konfugurantionerna för ansible. Sen när jag kör `ansible-config dump` i min ansible mapp så ser jag aktuella inställningarna som gäller här.

Sen när jag kör samma så får jag också information printat ut.Vilket kan se likadan ut men om man kör en diff på både filerna får man ut vad det skiljer sig i. Utifrån kan jag se att filen i home har standard inställningar medans den i ansible mappen påverkas av ansible.cfg filen och därmed har lite andra inställningar.

```bash
 💖claire 💕 🎀📁 ~ 💜💙💫⏰ 11:15 🌸diff ansible.cfg.init ansible/ansible.cfg.init 
38c38
< CONFIG_FILE() = None
---
> CONFIG_FILE() = /home/claire/ansible/ansible.cfg
67c67
< DEFAULT_HOST_LIST(default) = ['/etc/ansible/hosts']
---
> DEFAULT_HOST_LIST(/home/claire/ansible/ansible.cfg) = ['/home/claire/ansible/hosts']
76c76
< DEFAULT_LOCAL_TMP(default) = /home/claire/.ansible/tmp/ansible-local-160230h88mb8n_
---
> DEFAULT_LOCAL_TMP(default) = /home/claire/.ansible/tmp/ansible-local-160131e10qz7wm
143c143
< HOST_KEY_CHECKING(default) = True
---
> HOST_KEY_CHECKING(/home/claire/ansible/ansible.cfg) = False

```