# QUESTION A

In the `06-web.yml` playbook, add a couple of tasks:

* One task to create the directory structure under `/var/www/example.internal/html/`.
* One task to upload our `files/index.html` file to `/var/www/example.internal/html/index.html`.

HINTS:
* The module for creating a directory is, somewhat counterintuitively, called
[ansible.builtin.file](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html)
* If you want to serve files under a non-standard directory (such as the one we create above), we must
  also set the correct SELinux security context type on the directory and files. The context in question
  in this case should be `httpd_sys_content_t` for the `/var/www/example.internal/html/` directory.

# QUESTION B

To each of the tasks that change configuration files in the webserver, add a `register: [variable_name]`.

As an example:

    - name: Set up configuration for HTTPS
      ansible.builtin.copy:
        src: files/https.conf
        dest: /etc/nginx/conf.d/https.conf
      register: result

When the task is run, the result of the task is saved into the variable `result`, which is a dictionary.
This result can be compared in a conditional with the keyword `changed`, such as

    when: result is changed

or

    when: result.changed is true

or

    when: result["changed"] is true

or, more succinctly:

    when: result.changed

or even

    when: result["changed"]

You can check what the variable contains after each task with adding

    - name: Print the value of result
      ansible.builtin.debug:
        var: result

With the use of the `when:` keyword, make a conditional that only restarts the web server if either of
the tasks has had any change.

See https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_conditionals.html#basic-conditionals-with-when

There are several ways to accomplish this, and there is no _best_ way to do this with what we've done so far.

Is this a good way to handle these types of conditionals? What do you think?
Det är bättre än att starta om tjänsterna varje gång. Det minskar på onödiga omstarter som kan leda till driftstörningar, trafikproblem och på verka både användare och system.

# BONUS QUESTION
Imagine you had a playbook with hundreds of tasks to be done on several hosts, and each one of these tasks
might require a restart or reload of a service.

Let's say the goal is to avoid restarts as much as possible to minimize downtime and interruptions; how
would you like the flow to work?

Describe in simple terms what your preferred task flow would look like, not necessarily implemented in
Ansible, but in general terms.

Jag tror bäst är att dem flesta ändringar är i början om det går och sen att det bara behöver starta om så få gånger som det går. På så sätt undviker vi onödiga avbrott och håller tjäsnterna igång så länge som möjligt.
