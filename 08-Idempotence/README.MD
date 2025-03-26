# Ansible par la pratique (8) – Idempotence

## Exercice

Pour la réalisation de l'exercice, je réalise deux playbooks, composés de plusieurs plays. Le premier réalise les tâches d'installation et de copie de fichier. Le second désinstalle les packet et supprime les fichiers.

### Playbook 1

```yaml
- name : Install package
  hosts: all
  gather_facts: false
  tasks:
    - name: Ensure tree, git and nmap is present
      ansible.builtin.package:
        name:
          - tree
          - git
          - nmap
        state: present
- name: Copy file
  hosts: all
  gather_facts: false
  tasks:
    - name: Ensure that exemple3 is present
      ansible.builtin.copy:
        src: /etc/fstab
        dest: /tmp/test3.txt
- name: Show disk space
  hosts: all
  gather_facts: false
  tasks:
    - name: Show 
      ansible.builtin.shell: df -h /
      register: result
    - name: Print return
      ansible.builtin.debug:
        msg: "Resultat {{result}}"
```

Voici l'ouput après quelques runs :

![img](./img/Screenshot_20250325_093041.png)

### Playbook 2

```yaml
- name : Uninstall package
  hosts: all
  gather_facts: false
  tasks:
    - name: Ensure tree, git and nmap is absent
      ansible.builtin.package:
        name:
          - tree
          - git
          - nmap
        state: absent
- name: Delete file
  hosts: all
  gather_facts: false
  tasks:
    - name: Ensure file is removed
      ansible.builtin.file:
        path: /tmp/test3.txt
        state: absent
- name: Show disk space
  hosts: all
  gather_facts: false
  tasks:
    - name: Show 
      ansible.builtin.shell: df -h /
      register: result
    - name: Print return
      ansible.builtin.debug:
        msg: "Resultat {{result}}"
```

Voici l'output au premier run :

![img](./img/Screenshot_20250325_093224.png)

Après le premier run on voit bien l'idempotence :

![img](./img/Screenshot_20250325_093318.png)

### Comparaison

![img](./img/Screenshot_20250325_093605.png)

![img](./img/Screenshot_20250325_093616.png)

Quand on compare les espaces disque, on remarque que le disque est plus vide après les désinstallations et suppression. 

Cependant ce qui est intéressant de noté, c'est que le module ansible.builtin.shell est par défaut toujours en changed, il faut rajouter un changed_when pour fix nos propres conditions de changement.
