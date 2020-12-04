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
- 5° Fare il Checkpoint :heavy_check_mark: per essere sicuri che si abbia configurato bene il file e che funzioni, con il comando --> **_ping www.google.com_** , in questo caso cerchera di mettersi in contatto con il server della google ma se si desidera provare con un'altra macchina bastera sostituire **_ www.google.com _** con la destinazione desiderata.

Passo 3: Creazione dei server web
---
- 1° Digidando il comando --> **_cd /var/www_** ci si sposta nella directory che conterra le pagine html.
- 2° Digitare il comando --> **_sudo mkdir_** si va a creare la cartella che conterra la pagina html.
- 3° Digitare il comando --> **_cd /etc/apache2/sites-available_** per spostarsi nella cartella dove bisogna creare un nuovo file di configurazione per il nuovo server, con il comando --> **_sudo cp 000-default.conf x.conf_** dove x e il nome del file che si vuole creare.
- 4° Dopo aver creato il nuovo file x.conf scrivere il commando --> **_sudo nano x.conf_** e togliere il comento da **_ServerName_** e scrivere il nome che si vuole dare al server, succesivamente cambiare il percoso del **_DocumentRoot_** ed inserire quello relativo alla cartella creata nel punto 3.2. che contiene il file html. Salvare tutto ed uscire.
- 5° Digitare il comando --> **_sudo a2ensite x.conf_** per attivare il server, n.b. a posto della x mettere il nome dato.
- 6° Fare il Checkpoint :heavy_check_mark: per verificare che il server e la sua configurazione funzioni bisogna aprire un qualsiasi browser andando a digitare nella bara di ricerca il **_ServerName_** inserito prima nella configurazione nel punto 3.4.  Se viene visualizzata la pagina inserita in **_DocumentRoot_** significa che tutto è andato a buon fine.
- 7° Ripetere il **_Passo 3_** per tutti i server che si vuole creare

Passo 4:Creazione Utenti
---
La creazione degli utenti permettera a ogni utente di gestire la propria pagina html da remoto e senza andare ad interferire con le atre possibili pagine html.

- 1° Installare **_vsftpd_** digitando il comando --> **_sudo apt-get install vsftpd_**
- 2° Digitare il comando --> **_sudo useradd -s /bin/bash -d /var/www/cartellaPerSito -m nomeUtente_** per creare un utente, al posto di **_cartellaPerSito_** mettere il nome dato alla cartella e al posto di **_nomeUtente_** mettere il nome del utende di quel sito.
- 3° Digitare il comando --> **_sudo passwd nomeUtente_** per creare la password di quel utente, al posto di nomeUtente diggitare il utente creato nel punto 4.2.
- 4° Fare il Checkpoint :heavy_check_mark: per verificare che l'opperazione sia andata a buon fine bisogna fare il logout da Ubuntu e rientrare uttilizando le credenziali create prima. Se l'accesso va a buon fine è possibile che possa l'utente modificare le pagine html.
- 5° Ripetere il **_Passo 4_** per creare gli utenti corrispondenti a ogni sito.
