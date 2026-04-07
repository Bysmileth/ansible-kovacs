# Compte rendu des ateliers de test

## TEST-01

Pour commencer, nous déployons les VMs via Vagrant :

```console
$ vagrant up
```

On peut voir que les machines sont bien en cours de création, et apparaissent dans la liste des machines virtuelles de VirtualBox :

![alt text](test01-create.png)
------------------

Puis nous les détruisons via la commande suivante :

```console
$ vagrant destroy -f
```

On voit dans la liste des machines virtuelles que les machines ont bien été supprimées :

![alt text](test01-destroy.png)
------------------

## TEST-02

De la même manière, nous créons à nouveau les machines que nous avons ajouté via la commande suivante :

```console
$ vagrant box add bento/ubuntu-22.04
$ vagrant up
```

![alt text](test02-up.png)
-----------

Petit à petit, les machines se créent et apparaissent dans la liste des machines virtuelles de VirtualBox :

![alt text](test-02-2-deploy.png)
-----------

Puis nous les détruisons à nouveau via la commande suivante :

```console
$ vagrant destroy -f
```

![Commande destroy](test-02-destroy.png)
------------------