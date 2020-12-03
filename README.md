# VEB SERVER
Creazione di un Web Server con Ubuntu e Apache2

Prima di comminciare bisogna fornirsi di una macchina Ubuntu con permessi da administratore

Passo: Installazioni
---
- Installare OpenSSH Server con il comando --> **_apt install openssh-server_**
- Installare Apache 2 con il comando --> **_apt install apache2_**
- Installare Net tools con il comando --> **_apt install net-tools_**

Passo 2: Configurazione della rete
---
- 1° Ci spostiamo nella cartella che contiene la configurazione di rete che si usa con il comando --> **_cd /etc/netplan_**
- 2° Apriamo il file di configurazione della rete con il comando --> **_sudo nano 00-install-config.yaml_**
- 3° Modificare il file affinche rispetti il seguente modello:

       network:
        version: 2
        renderer: networkd
        ethernets:
          eth1:
            addresses: [IndirizzoIP/NotazioneCIDR]
            gateway4: IndirizzoIP Gateway
            nameservers:            
                search: [otherdomain]
                addresses: [IndirizzoIP DNS]
                
- 4° Salvare il file ed uscire
- 5° Fare il Checkpoint :heavy_check_mark: per essere sicuri che si abbia configurato bene il file e che funzioni, con il comando --> **ping www.google.com**, in questo caso cerchera di mettersi in contatto con il server della google ma se si desidera provare con un'altra macchina bastera sostituire **-www.google.com-** con la destinazione desiderata.

Passo 3: Creazione dei server web
---
- 1° 
