# QUESTION A

Create a playbook, `05-web.yml` that copies the local `files/https.conf` file to `/etc/nginx/conf.d/https.conf`,
and acts ONLY on the `web` group from the inventory.

Refer to the official Ansible documentation for this, or work with a classmate to
build a valid and working playbook, preferrably that conforms to Ansible best practices.

Run the playbook with `ansible-playbook` and `--verbose` or `-v` as option:

    $ ansible-playbook -v 05-web.yml

The output from the playbook run contains something that looks suspiciously like JSON, and that contains
a number of keys and values that come from the output of the Ansible module.

What does the output look like the first time you run this playbook?
```bash

💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 13:24 🌸ansible-playbook -v 05-web.yml
Using /home/claire/ansible/ansible.cfg as config file

PLAY [Configure HTTPS on webserver] ****************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************
ok: [192.168.121.119]

TASK [Copy HTTPS configuration file] ***************************************************************************************************
changed: [192.168.121.119] => {"changed": true, "checksum": "1d655a454767051f03ccdf809c3e72b5cf99b5e8", "dest": "/etc/nginx/conf.d/https.conf", "gid": 0, "group": "root", "md5sum": "24522e4bdd30550432bd6738589b3b5d", "mode": "0644", "owner": "root", "secontext": "system_u:object_r:httpd_config_t:s0", "size": 466, "src": "/home/deploy/.ansible/tmp/ansible-tmp-1760959515.1033075-233650-23105398151645/source", "state": "file", "uid": 0}

PLAY RECAP *****************************************************************************************************************************
192.168.121.119            : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

What does the output look like the second time you run this playbook?

```bash
💖claire 💕 🎀📁 ~/ansible 💜💙💫⏰ 13:25 🌸ansible-playbook -v 05-web.yml
Using /home/claire/ansible/ansible.cfg as config file

PLAY [Configure HTTPS on webserver] ****************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************
ok: [192.168.121.119]

TASK [Copy HTTPS configuration file] ***************************************************************************************************
ok: [192.168.121.119] => {"changed": false, "checksum": "1d655a454767051f03ccdf809c3e72b5cf99b5e8", "dest": "/etc/nginx/conf.d/https.conf", "gid": 0, "group": "root", "mode": "0644", "owner": "root", "path": "/etc/nginx/conf.d/https.conf", "secontext": "system_u:object_r:httpd_config_t:s0", "size": 466, "state": "file", "uid": 0}

PLAY RECAP *****************************************************************************************************************************
192.168.121.119            : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

# QUESTION B

Even if we have copied the configuration to the right place, we still do not have a working https service
on port 443 on the machine, which is painfully obvious if we try connecting to this port:

    $ curl -v https://192.168.121.10
    *   Trying 192.168.121.10:443...
    * connect to 192.168.121.10 port 443 from 192.168.121.1 port 56682 failed: Connection refused
    * Failed to connect to 192.168.121.10 port 443 after 0 ms: Could not connect to server
    * closing connection #0
    curl: (7) Failed to connect to 192.168.121.10 port 443 after 0 ms: Could not connect to server

The address above is just an example, and is likely different on your machine. Make sure you use the IP address
of the webserver VM on YOUR machine.

In order to make `nginx` use the new configuration by restarting the service and letting `nginx` re-read
its configuration.

On the machine itself we can do this by:

    [deploy@webserver ~]$ sudo systemctl restart nginx.service

Given what we know about the [ansible.builtin.service](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html),
how can we do this through Ansible?

För att få nginx att läsa in den nya HTTPS konfigurantionen behövde jag lägga till en extra task i min playbook som startar om tjänsten. Jag använde Ansible modulen `ansible.builtin.service` med `state: restarted`. Det gör samma som kommandot `sudo systemctl restart nginx`, fast automatiserat via Ansible.
Efterråt kunde jag ansluta till webbservern både via http(port80) och https(port 443).


Add an extra task to the `05-web.yml` playbook to ensure the service is restarted after the configuration
file is installed.

When you are done, verify that `nginx` serves web pages on both TCP/80 (http) and TCP/443 (https):

    $ curl http://192.168.121.10
    $ curl --insecure https://192.168.121.10

Again, these addresses are just examples, make sure you use the IP of the actual webserver VM.

Note also that `curl` needs the `--insecure` option to establish a connection to a HTTPS server with
a self signed certificate.

# QUESTION C

What is the disadvantage of having a task that _always_ makes sure a service is restarted, even if there is
no configuration change?

En nackdel med att alltid starta om en tjänst, även när ingen konfigurationsändring har gjorts, är att det kan skapa onödiga driftörningar. Om en tjänst som nginx startas om utan anledning kan det tillfälligt stoppa trafiken till webbplatsen, vilket påverkar användare och system som är beroende av den. Det tar också extra tid och resurser vid varje körning av playbooken. däröfr är det bättre att bara starta om tjänsten när något faktiskt har ändrats.


# BONUS QUESTION

There are at least two _other_ modules, in addition to the `ansible.builtin.service` module that can restart
a `systemd` service with Ansible. Which modules are they?
Förutom `ansible.builtin.service` kan man använda modulerna `ansible.builtin.systemd` och `ansible.builtin.command` för att starta om en systemd tjänst. systemd modulen är en mer avancerad och ger fler möjligheter för att hantera tjäsnter, till exempel kontrollera status ller aktivera dem vid uppstart. command-modulen kan också användas för att köra kommando som systemctl restart nginx, men det är mindre smidigt eftersom det inte är lika integrerat med Ansible som de andra alternativen.