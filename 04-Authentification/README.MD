# Ansible par la pratique (4) – Authentification

## Exercice 1

![img](./img/Screenshot_20250324_103425.png)

Ajout dans /etc/hosts :

```bash
192.168.56.20 target01.sandbox.lan target01
192.168.56.30 target02.sandbox.lan target02
192.168.56.40 target03.sandbox.lan target03 
```

Test de la configuration :

```bash
for HOST in target01 target02 target03; do ping -c 1 -q $HOST; done
```

![img](./img/Screenshot_20250324_104111.png)

Récupération des clés publiques :

```bash
ssh-keyscan -t rsa target01 target02 target03 >> .ssh/known_hosts
```

![img](./img/Screenshot_20250324_104221.png)

> J'active l'authentification par mot de passe.

```bash
ssh-copy-id vagrant@target01
ssh-copy-id vagrant@target02
ssh-copy-id vagrant@target03
```

![img](./img/Screenshot_20250324_104734.png)

Ping ansible des trois neuds :

```bash
ansible all -i target01,target02,target03 -m ping
```

![img](./img/Screenshot_20250324_104848.png)
