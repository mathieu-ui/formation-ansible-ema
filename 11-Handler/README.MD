# Ansible par la pratique (11) – Handler

## Exercice

Création du playbook :

![img](./img/Screenshot_20250325_112612.png)

[Ici se trouve le playbook chrony.yml](playbook.yml)

Première exécution :

![img](./img/Screenshot_20250325_113258.png)

Lors de la première exécution chrony est installer, configurer et restarted.

Réexécution du playbook :

![img](./img/Screenshot_20250325_113317.png)

Quand le playbook est réexécution, vu que chrony n'est pas reconfiguré, il n'est pas redémarré.
