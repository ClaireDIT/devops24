# QUESTION A

Refer to the documentation for the [ansible.builtin.service](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html)
module.

How can we make the web server start with an addition of just one line to the playbook above?
state: true   gör att den också startas direkt nu, och inte bara nästa gång systemet startar 

# QUESTION B

You make have noted that the `become: true` statement has moved from a specific task to the beginning
of the playbook, and is on the same indentation level as `tasks:`.

What does this accomplish?
När become: true ligger på samma nivå som tasks: gäller det för hela playbooken. Man slipper upprepa become: true i varje enskild task. Också allt körs med sudo.

# QUESTION C

Copy the above playbook to a new playbook. Call it `04-uninstall-webserver.yml`.

Change the ordering of the two tasks. Make the web server stop, and disable it from starting at boot, and
make sure that `nginx` is uninstalled. Change the `name:` parameter of each task accordingly.

Run the new playbook, then make sure that the web server is not running (you can use `curl` for this), and
log in to the machine and make sure that there are no `nginx` processes running.

Why did we change the order of the tasks in the `04-uninstall-webserver.yml` playbook?
Vi ändrade ordningen i playbooken så att tjänsten först stoppas och autostarten stängs av innan paketet tas bort. Det är viktigt eftersom om vi skulle avinstallera paketet först, skulle systemet inte längre kunna stoppa eller hantera tjänsten, vilket kan orsaka fel. Genom att först stoppa tjänsten och sedan avsinatllera den ser vi till att allt avslutaas på ett rent och kontrollerat sätt utan problem.


# BONUS QUESTION

Consider the output from the tasks above, and what we were actually doing on the machine.

What is a good naming convention for tasks? (What SHOULD we write in the `name:` field`?)

man ska föröska skriva så enkelt det varje task gör så att det blir lätt att förstå vad som händer i playbooken. Till exempel Install nginx, stop nginx osv. 
