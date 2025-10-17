## QUESTION A

What does the `ansible.builtin.debug` module actually do?
Modulen `ansible.builtin.debug` används för att skriva ut information i terminalen under körningen av ett playbook. Modulen visar variabler eller meddelande och är användbar för felsökning och kontroll.


## QUESTION B

What is the variable 'ansible_facts' and where does it come from?
Variabeln innehåller infromation som Ansible automatisk samlar in om varje värd innan några uppgifter körs. Dessa fakta inkluderar till exempel operativsystem, IP-adress, hostname och mycket mer. Informationen kommer från modulen"Gathering Facts", som körs i början av varje playbook om den inte är inaktiverad. Tack vare detta kan man referera till faktavärden direkt i playbooks.

## QUESTION C

We now know how to use Ansible to perform changes, and to ensure these changes are still there
next time we run the playbook. This is a concept called _idempotency_.

How do we now remove the software we installed through the playbook above? 

För att ta bort samma program som tidigare installerats kan en ny playbook skapas eller ändra i den första, raden 'state:absent istället för `state:present´.
Detta instruerar Ansible att avinstallera programmen i stället för att installera dem.

Make the playbook remove the exact same software we previously installed. Call the created playbook `03-uninstall-software.yml`.

## BONUS QUESTION

What happens when you run `ansible-playbook` with different options?

Explain what each of these options do:
* --verbose, -vv, -vvv, -vvvv
* --check
* --syntax-check

* --verbose eller -vv, -vvv, -vvvv visar mer detaljerad information om körningen. ju fler v som anges,desto mer detaljerad blir utskriften.

* --check kör playbooken i ett testläge där Ansible bara visar vilka ändringar som skulle göras, utan att faktiskt genomföra dem.

* --syntax-check kontrollerar endast syntaxen i playbook-filen för att säkerställa att den är korrekt formaterad, utan att köra några upppgifter.