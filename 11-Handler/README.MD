# Ansible par la pratique (11) – Handler

## Exercice

Creation du playbook :

![img](./img/Screenshot_20250325_112612.png)

[Ici se trouve le playbook chrony.yml](playbook.yml)

Premiere execution :

![img](./img/Screenshot_20250325_113258.png)

Lors de la premiere execution chrony est installer, configurer et restarted.

Re-executions du playbook :

![img](./img/Screenshot_20250325_113317.png)

Quand le playbook est re-executée, vu que chrony n'est pas re-configuré, il n'est pas redémaré.
