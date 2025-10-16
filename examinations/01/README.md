# Examination 1 - Understanding SSH and public key authentication

Connect to one of the virtual lab machines through SSH, i.e.

    $ ssh -i deploy_key -l deploy webserver

Study the `.ssh` folder in the home directory of the `deploy` user:

    $ ls -ld ~/.ssh

Look at the contents of the `~/.ssh` directory:

    $ ls -la ~/.ssh/

## QUESTION A

What are the permissions of the `~/.ssh` directory?
drwx------ vilket innebär att ägaren av kalatogen har fulla rättigheter mendans gruppen och andra ej har några rättigheter alls. 

Why are the permissions set in such a way?
Jag tror att det är av säkerhetsskäl i med att denna katalog innerhåller filer med autorized keys och därmed om andra får tillgång till den här informationen så kommer jag kanske kunna koppla upp sig genom ssh och därmed ha tillgång till kontot. 
## QUESTION B

What does the file `~/.ssh/authorized_keys` contain?
den innerhåller just nu en publik nyckel. 

## QUESTION C

When logged into one of the VMs, how can you connect to the
other VM without a password?
om man vill koppla utan lösenord så kan man med hjälp av ssh. Då genererar man nyckelnpar och sedan använder den publika nyckeln från den ena vm och lägger in den i den andra för att slippa använda lösenord men ändå koppla upp sig. 

### Hints:

* man ssh-keygen(1)
* ssh-copy-id(1) or use a text editor

## BONUS QUESTION

Can you run a command on a remote host via SSH? How?
ja det går, efter att man har kört ssh och kommer in så är ma inne i den andra terminalen så det är bara att köra kommandos och det kommer ske på vm man är uppkoplad till. 