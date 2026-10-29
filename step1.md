# structure of Ansible
- <img width="591" height="537" alt="image" src="https://github.com/user-attachments/assets/ed40eb5c-0f06-4439-90da-54387f0a1b2b" />
- control-node -> our ansible server that control the managed nodes
- Managed nodes -> these are some hosts ansible can manage
- inventory -> this allows ansible (control-node) to manage hosts


----

# how to build an inventory ??
- make inventory.ini or inventory.yaml (look there for more clear)
- make sure that you can access the host through the IP so make an authorized key in order to ssh into it using ansible
- add to it the ips of the hosts that you want to manage
- then run
```
ansible-inventory -i inventory.ini --list
#then test the group names inside inventory
ansible app -m ping  -i inventory.ini
```

# how to build a playbook
- make playbook.yml
- playbook -> list of plays that define the order that ansible will take in order to finish his operation
- play -> an ordered list of tasks -> maps managed nodes in inventory
- Task -> single module that ansible performs
- Module -> code that ansible runs on managed nodes.
- to run playbook
```
ansible-playbook -i inventory.ini playbook.yaml
```

---
# Some filtering techniques
- define default value
```
//if you want to put value in case -> our some_variable isn't found
{{ some_variable | default(5) }}
//if you want to set a variable mandatory so that without it -> you will got an error
{{ variable | mandatory }}
//in case the first condition -> true -> our ternary should bring true else false
{{ (status == 'needs_restart') | ternary('restart', 'continue') }}
//in case you want to add new value if the output of the condition was null -> add omit
{{ enabled | ternary('no shutdown', 'shutdown', omit) }}
//in case you want to split data
{{ fruits | split(',') }}
.....
```
