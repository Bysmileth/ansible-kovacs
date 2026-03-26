# Atelier 15 – Les variables enregistrées

## Challenge

### Démarrage des VM et placement dans le bon répertoire

Démarrez les VM depuis le répertoire `atelier-15`.

```bash
vagrant up
vagrant ssh ansible
cd /home/vagrant/ansible/projets/ema/playbooks
```

![Démarrage des VM](Capture/1.png)

### Création du playbook kernel.yml

Écrivez un playbook `kernel.yml` qui affiche les informations détaillées du noyau sur tous vos Target Hosts. Utilisez la commande `uname -a` et le module `debug` avec le paramètre `msg`.

```yaml
--- # kernel.yml

- hosts: all
  gather_facts: false

  tasks:
    - name: Get kernel parameters
      command: uname -a
      changed_when: false
      register: kernel_parameters

    - debug:
        msg: "{{ kernel_parameters }}"
...
```

Pour trouver le nom de la partie de la variable à afficher, on lance le playbook afin de voir la partie qui nous intéresse.

![Exécution du playbook kernel.yml](Capture/2.png)

Ici on remarque que c'est la partie `stdout_lines` qui concerne les informations détaillées du noyau donc on l'ajoute.

```yaml
--- # kernel.yml

- hosts: all
  gather_facts: false

  tasks:
    - name: Get kernel parameters
      command: uname -a
      changed_when: false
      register: kernel_parameters

    - debug:
        msg: "{{ kernel_parameters.stdout_lines }}"
...
```

![Exécution du playbook kernel.yml plus fine](Capture/3.png)

### Création du playbook kernel2.yml

Essayez d'obtenir le même résultat en utilisant le paramètre `var` du module `debug`.


```yaml
--- # kernel2.yml

- hosts: all
  gather_facts: false

  tasks:
    - name: Get kernel parameters
      command: uname -a
      changed_when: false
      register: kernel_parameters

    - debug:
        var: kernel_parameters.stdout_lines
...
```

![Exécution fine du playbook kernel.yml](Capture/4.png)

Ici, comme on a déjà observé la partie de la variable qui nous intéresse (`stdout_lines`) dans le playbook `kernel.yml`, on la rajoute directement.

### Création du playbook packages.yml

Écrivez un playbook `packages.yml` qui affiche le nombre total de paquets RPM installés sur les hôtes Rocky et SUSE (`rpm -qa | wc -l`).

```yaml
--- #packages.yml

- hosts: rocky, suse
  gather_facts: false
  
  tasks:
    - name: Count packages
      shell: rpm -qa | wc -l
      changed_when: false
      register: packages

    - name: Display number of installed packages
      debug:
        msg: "{{ packages }}"
...
```

De même que pour le playbook `kernel.yml`, on le lance une fois pour voir et récupérer ce qui intéresse.

![Exécution du playbook packages.yml](Capture/5.png)

```yaml
--- #packages.yml

- hosts: rocky, suse
  gather_facts: false
  tasks:
    - name: Count packages
      shell: rpm -qa | wc -l
      changed_when: false
      register: packages

    - name: Display number of installed packages
      debug:
        msg: "{{ packages.stdout }}"
...
```
![Exécution du playbook packages.yml plus fine](Capture/6.png)
