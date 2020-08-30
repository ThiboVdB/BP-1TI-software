# 1TI Software

## Virtuele machine vagrant commando's
Voor elk van de virtuele machines in deze repository kunnen de volgende commando's gebruikt worden:

| Commando        | Beschrijving           |
| ------------- |-------------|
| ``vagrant up <vm-naam>``   | Virtuele machine creëren en provioning uitvoeren. |
| ``vagrant halt <vm-naam>``     | Virtuele machine afsluiten.      |  
| ``vagrant reload <vm-naam>`` | Virtuele machine herstarten.      |  
| ``vagrant provision <vm-naam>``   | Provisioning fase opnieuw uitvoeren. |
| ``vagrant ssh <vm-naam>``     | Verbinding maken met de command-line interface van de vm.      |  
| ``vagrant destroy <vm-naam>`` | Virtuele machine verwijderen.    |  

## VM Configuratie/customization
Virtuele machine customizations worden gedaan in [vagrant-hosts.yml](./vagrant-hosts.yml).

Voorbeeld:
````
- name: 1ti
  ip: 192.168.56.100 <= ander IP
  box: bento/ubuntu-18.04 <= andere Vagrant Box
  cpus: 4 <= aantal CPU's
  memory: 4096 <= aantal RAM geheugen
````

## 1TI Software VM gebruiken zonder Vagrant
De ``1ti`` virtuele machine kan ook gebruikt worden zonder Vagrant. Eens deze vm gecreëerd en provisioned is, is deze klaar voor gebruik. Echter de "shared folder" wordt niet automatisch gemount.
Dit kan opgelost worden in de instellingen van de vm:

- In de "shared folders" sectie van de instellingen, selecteer de gedeelde folder.
- Vink "auto-mount" aan:
  
![shared-folder](./img/sharedfolder.png)

De andere virtuele machines worden best via ``vagrant ssh`` bereikt.

## Software updates
### Algemene updates
De packages in het OS kunnen geüpdate worden met de commando's:
````
sudo apt update
sudo apt upgrade
````
### Software in playbooks
Software zoals Visual Paradigm wordt geïnstalleerd via een URL. Wanneer software vervangen moet worden volstaat het de link te specificeren bij de variabelen.

Voorbeeld voor Visual Paradigm 16.2 Community Edition:

In [/ansible/vars/oosd_vars.yml](./ansible/vars/oosd_vars.yml):
````[yaml]
oosd_visualparadigm_url: 'https://uk2.dl.visual-paradigm.com/visual-paradigm/vpce16.2/20200801/Visual_Paradigm_CE_16_2_20200801_Linux64_InstallFree.tar.gz'


# Dit kan uit de URL gehaald worden. Let op! Het versienummer moet (indien nodig gespecificeerd worden met een "." bv. '16.2')

oosd_visualparadigm_version: 'Visual_Paradigm_CE_16.2'
````