---
title: aaaSet van Apache Tomcat op een virtuele Linux-machine | Microsoft Docs
description: Meer informatie over hoe tooset van Apache Tomcat7 met behulp van Azure Virtual Machines waarop Linux wordt uitgevoerd.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Tomcat7 instellen op een virtuele Linux-machine met Azure
Apache Tomcat (of gewoon Tomcat, ook voorheen ondersteuning Tomcat) is een open-source-webserver en de servlet-container die is ontwikkeld door Hallo Apache Software Foundation (AVP). Tomcat implementeert Hallo Java Servlet en Hallo Java Server Pages (JSP) specificaties van Sun Microsystems. Tomcat biedt een pure HTTP Java web server-omgeving in welke toorun Java-code. In de eenvoudigste configuratie hello, Tomcat uitgevoerd in een proces één besturingssysteem. Dit proces wordt uitgevoerd voor een virtuele Java-machine (JVM). Alle HTTP-aanvragen van een browser tooTomcat wordt verwerkt als een afzonderlijke thread in Hallo Tomcat-proces.  

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over hoe toouse Hallo klassieke implementatiemodel. U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken. toouse een Resource Manager-sjabloon toodeploy een VM Ubuntu met Open JDK en Tomcat, Zie [in dit artikel](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

In dit artikel leert u Tomcat7 installeren op een Linux-installatiekopie en deze implementeren in Azure.  

U leert:  

* Hoe toocreate een virtuele machine in Azure.
* Hoe hello tooprepare virtuele machine voor Tomcat7.
* Hoe tooinstall Tomcat7.

Ervan wordt uitgegaan dat u al een Azure-abonnement hebt.  Als u niet, u kunt zich aanmelden voor een gratis proefversie op [hello Azure-website](https://azure.microsoft.com/). Als u een MSDN-abonnement hebt, raadpleegt u [speciale prijzen voor Microsoft Azure: MSDN, MPN en BizSpark voordelen](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn meer informatie over Azure, Zie [wat is Azure?](https://azure.microsoft.com/overview/what-is-azure/).

In dit artikel wordt ervan uitgegaan dat u een werkende basiskennis hebben van Tomcat- en Linux.  

## <a name="phase-1-create-an-image"></a>Fase 1: Een installatiekopie maken
In deze fase maakt u een virtuele machine met behulp van een Linux-installatiekopie in Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Stap 1: Een SSH-sleutel voor verificatie genereren
SSH is een belangrijk hulpprogramma voor systeembeheerders. Configureren van de toegangsbeveiliging op basis van een wachtwoord human bepaald wordt echter niet aanbevolen. Kwaadwillende gebruikers kunnen in uw systeem op basis van een gebruikersnaam en een zwak wachtwoord verbreken.

goed nieuws Hello, is er een manier tooleave RAS openen en u geen zorgen over wachtwoorden. Deze methode bestaat van verificatie met asymmetrische cryptografie. Hallo is persoonlijke sleutel van de gebruiker Hallo die Hallo-verificatie verleent. U kunt zelfs Hallo gebruikersaccount vergrendelen toonot wachtwoord authenticatie toestaan.

Een ander voordeel van deze methode is dat u niet verschillende wachtwoorden toosign in toodifferent servers hoeft. U kunt verifiëren met behulp van Hallo persoonlijke persoonlijke sleutel op alle servers, waarmee wordt voorkomen dat u tooremember met verschillende wachtwoorden.



Volg deze stappen toogenerate Hallo SSH-verificatiesleutel.

1. Download en installeer PuTTYgen van Hallo volgende locatie: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Puttygen.exe worden uitgevoerd.
3. Klik op **genereren** toogenerate Hallo sleutels. U kunt in Hallo-proces aanvraaggrootte vergroten door bewegende Hallo muis over Hallo leeg gebied in Hallo-venster.  
   ![PuTTY sleutel Generator schermafbeelding Hallo nieuwe sleutel knop genereren][1]
4. Nadat het Hallo proces genereren, wordt Puttygen.exe uw nieuwe openbare sleutel weergegeven.  
   ![PuTTY sleutel Generator schermafbeelding van de nieuwe openbare sleutel Hallo en Hallo persoonlijke sleutel knop Opslaan][2]
5. Selecteer en kopieer de openbare sleutel Hallo en opslaan in een bestand met de naam publicKey.pem. Klik niet op **openbare sleutel opslaan**, omdat Hallo opgeslagen bestandsindeling van de openbare sleutel verschilt van de openbare sleutel Hallo we willen.
6. Klik op **persoonlijke sleutel opslaan**, en opslaan in een bestand met de naam privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Stap 2: Maak Hallo afbeelding in hello Azure-portal
1. In Hallo [portal](https://portal.azure.com/), klikt u op **nieuw** in Hallo taak balk toocreate een afbeelding. Kies vervolgens Hallo Linux installatiekopie die is gebaseerd op uw behoeften. Hallo wordt volgende voorbeeld Hallo Ubuntu 14.04 installatiekopie.
![Schermopname van het Hallo-portal die ziet u de nieuwe knop Hallo][3]

2. Voor **hostnaam**, geef de naam Hallo voor Hallo URL dat u en Internet-clients tooaccess deze virtuele machine gebruiken. Hallo laatste deel van Hallo DNS-naam, bijvoorbeeld tomcatdemo definiëren. Azure wordt Hallo URL vervolgens als tomcatdemo.cloudapp.net gegenereerd.  

3. Voor **SSH verificatiesleutel**, Hallo sleutelwaarde van Hallo publicKey.pem bestand de openbare sleutel Hallo gegenereerd door PuTTYgen bevat kopiëren.  
![Sleutel voor SSH-gebruikersverificatie vak Hallo-portal][4]

4. Andere instellingen naar wens configureren en klik vervolgens op **maken**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Fase 2: Uw virtuele machine voorbereiden voor Tomcat7
In deze fase wordt u een eindpunt voor Tomcat verkeer configureren en vervolgens verbinding tooyour nieuwe virtuele machine.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Stap 1: Open Hallo HTTP-poort tooallow-webtoegang
Eindpunten in Azure bestaan uit een protocol TCP of UDP, samen met een openbare en particuliere poort. Hallo is persoonlijke Hallo poort Hallo service luistert tooon Hallo virtuele machine. Hallo openbare poort is Hallo-poort die hello Azure cloudservice luistert tooexternally voor binnenkomend verkeer op basis van het Internet.  

TCP-poort 8080 is Hallo standaardpoortnummer dat Tomcat toolisten gebruikt. Als deze poort wordt geopend met een Azure-eindpunt, u en andere internetclients hebben toegang tot Tomcat-pagina's.  

1. Klik in de portal Hallo op **Bladeren** > **virtuele machines**, en klik vervolgens op Hallo virtuele machine die u hebt gemaakt.  
   ![Schermafbeelding van de map van de virtuele machines Hallo][5]
2. tooadd een eindpunt tooyour virtuele machine, klikt u op Hallo **eindpunten** vak.
   ![Schermafbeelding van Hallo eindpunten vak][6]
3. Klik op **Add**.  

   1. Voor het Hallo-eindpunt, voer een naam voor Hallo eindpunt in **eindpunt**, en voer dan 80 in **openbare poort**.  

      Als u deze too80 instellen, hoeft u geen tooinclude Hallo poortnummer in Hallo-URL die is gebruikt tooaccess Tomcat. Bijvoorbeeld: http://tomcatdemo.cloudapp.net.    

      Als u instellen dat deze tooanother waarde, zoals 81, moet u tooadd Hallo poort nummer toohello URL tooaccess Tomcat. Bijvoorbeeld: http://tomcatdemo.cloudapp.net:81 /.
   2. Voer 8080 in **particuliere poort**. Standaard luistert Tomcat op TCP-poort 8080. Als u Hallo standaard listen-poort Tomcat hebt gewijzigd, moet u bijwerken **particuliere poort** toobe Hallo hetzelfde als het Hallo Tomcat listen-poort.  
      ![Schermopname van gebruikersinterface waarin de opdracht, de openbare poort en het particuliere poort toevoegen][7]
4. Klik op **OK** tooadd Hallo eindpunt tooyour virtuele machine.

### <a name="step-2-connect-toohello-image-you-created"></a>Stap 2: Verbinding maken met toohello-installatiekopie die u hebt gemaakt
U kunt een SSH-hulpprogramma tooconnect tooyour virtuele machine. In dit voorbeeld gebruiken we PuTTY.  

1. Hallo DNS-naam van uw virtuele machine ophalen van Hallo-portal.
    1. Klik op **Bladeren** > **virtuele machines**.
    2. Hallo-naam van uw virtuele machine selecteren en klik vervolgens op **eigenschappen**.
    3. In Hallo **eigenschappen** tegel, kijkt u in Hallo **domeinnaam** tooget Hallo DNS-naam.  

2. Hallo-poortnummer voor SSH-verbindingen van Hallo ophalen **SSH** vak.  
![Schermafbeelding van Hallo SSH-verbinding-poortnummer][8]

3. Download [PuTTY](http://www.putty.org/).  

4. Nadat u hebt gedownload, klikt u op Hallo uitvoerbaar bestand Putty.exe. In de PuTTY-configuratie, Hallo basisopties configureren met de hostnaam Hallo en het poortnummer dat is verkregen van Hallo eigenschappen van de virtuele machine.   
![Schermafbeelding van Hallo PuTTY-configuratie host naam en het poortnummer opties][9]

5. Klik in het linkerdeelvenster Hallo **verbinding** > **SSH** > **Auth**, en klik vervolgens op **Bladeren** toospecify Hallo-locatie van Hallo privateKey.ppk bestand. Hallo privateKey.ppk bestand bevat Hallo persoonlijke sleutel die wordt gegenereerd door PuTTYgen eerder in Hallo ' stap 1: een installatiekopie maken ' sectie van dit artikel.  
![Schermafbeelding van Hallo verbinding directory-hiërarchie en de knop Bladeren][10]

6. Klik op **Open**. U wordt mogelijk door een berichtvenster gewaarschuwd. Als u hebt geconfigureerd Hallo DNS-naam en het poortnummer juist, klikt u op **Ja**.
![Schermafbeelding van Hallo-melding][11]

7. U na vragen aan gebruiker tooenter zijn uw gebruikersnaam.  
![Schermopname die laat waar zien tooenter gebruikersnaam][12]

8. Hallo-gebruikersnaam die u hebt toocreate Hallo virtuele machine in Hallo gebruikt invoeren ' stap 1: een installatiekopie maken '-rubriek eerder in dit artikel. U ziet ongeveer Hallo volgende:  
![Schermafbeelding van Hallo verificatie bevestigen][13]

## <a name="phase-3-install-software"></a>Fase 3: Installeren van software
In deze fase installeert u Hallo Java runtime environment, Tomcat7 en andere onderdelen Tomcat7.  

### <a name="java-runtime-environment"></a>Java runtime-omgeving
Tomcat is geschreven in Java. Er zijn twee soorten Java Development Kit (JDKs), OpenJDK en Oracle JDK. U kunt Hallo gewenste.  

> [!NOTE]
> Beide JDKs bijna Hallo dezelfde voor Hallo klassen in Hallo Java API-code hebben, maar Hallo code voor de virtuele machine van Hallo verschilt. OpenJDK doorgaans toouse open bibliotheken, terwijl Oracle JDK doorgaans toouse zijn gesloten. Oracle JDK heeft meer klassen en enkele fouten opgelost en Oracle JDK stabieler dan OpenJDK is.

#### <a name="install-openjdk"></a>OpenJDK installeren  

Gebruik hello opdracht toodownload OpenJDK te volgen.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* een directory toocontain toocreate Hallo JDK-bestanden:  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK bestanden naar Hallo/usr/lib/jvm/map:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Oracle JDK installeren


Hallo volgende opdracht toodownload Oracle JDK uit Hallo Oracle-website gebruiken.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* een directory toocontain toocreate Hallo JDK-bestanden:  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK bestanden naar Hallo/usr/lib/jvm/map:  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset Oracle JDK als de standaard virtuele Java-machine Hallo:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Bevestig dat de Java-installatie geslaagd is
U kunt een opdracht zoals Hallo tootest volgen als Hallo Java runtime environment juist is geïnstalleerd:  

    java -version  

Als u OpenJDK hebt geïnstalleerd, ziet u een bericht zoals volgende Hallo: ![geslaagde OpenJDK installatie bericht][14]

Als u Oracle JDK hebt geïnstalleerd, ziet u een bericht zoals volgende Hallo: ![geslaagde Oracle JDK installatie bericht][15]

### <a name="install-tomcat7"></a>Tomcat7 installeren
Gebruik hello opdracht tooinstall Tomcat7 te volgen.  

    sudo apt-get install tomcat7  

Als u Tomcat7 niet gebruikt, gebruikt u de juiste variatie Hallo van deze opdracht.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Bevestig dat Tomcat7 installatie geslaagd is
toocheck als Tomcat7 is geïnstalleerd, bladert u tooyour Tomcat-server van DNS-naam. In dit artikel is Hallo voorbeeld-URL http://tomcatexample.cloudapp.net/. Als u een bericht zoals Hallo volgende ziet, is Tomcat7 juist geïnstalleerd.
![Bericht Tomcat7 installatie is voltooid][16]

### <a name="install-other-tomcat7-components"></a>Andere onderdelen Tomcat7 installeren
Er zijn andere optionele Tomcat-onderdelen die u kunt installeren.  

Gebruik Hallo **sudo apt cache zoeken tomcat7** opdracht toosee alle beschikbare Hallo-onderdelen. Hallo opdrachten tooinstall volgen enkele nuttige onderdelen gebruiken.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Fase 4: Tomcat7 configureren
In deze fase, moet u Tomcat beheren.

### <a name="start-and-stop-tomcat7"></a>Starten en stoppen Tomcat7
Hallo Tomcat7 server wordt automatisch gestart wanneer u deze installeert. U kunt deze ook starten met de volgende opdracht Hallo:   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

status van de tooview Hallo van Tomcat7:

    sudo /etc/init.d/tomcat7 status

toorestart Tomcat-services: 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Tomcat7 beheer
U kunt Hallo Tomcat gebruiker configuration file tooset bewerken van uw beheerdersreferenties. Hallo volgende opdracht gebruiken:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Hier volgt een voorbeeld:  
![Schermafbeelding van Hallo sudo vi opdrachtuitvoer][17]  

> [!NOTE]
> Maak een sterk wachtwoord voor de gebruikersnaam van de Hallo beheerder.  

Na het bewerken van dit bestand, moet u Tomcat7 services opnieuw starten met Hallo opdracht tooensure dat Hallo wijzigingen van kracht te volgen:  

    sudo /etc/init.d/tomcat7 restart  

Open uw browser en voer **http://<your tomcat server DNS name>manager/html** zoals Hallo URL. Hallo-URL is bijvoorbeeld Hallo in dit artikel http://tomcatexample.cloudapp.net/manager/html.  

Nadat u verbinding maakt ziet u iets dergelijks toohello volgende:  
![Schermopname van Hallo Tomcat Web Application Manager][18]

## <a name="common-issues"></a>Algemene problemen
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Geen toegang tot Hallo virtuele machine met Tomcat en Moodle vanaf Internet Hallo
#### <a name="symptom"></a>Symptoom  
  Tomcat wordt uitgevoerd, maar u Hallo Tomcat standaardpagina met uw browser niet zien.
#### <a name="possible-root-cause"></a>Mogelijke hoofdoorzaken   

  * Hallo Tomcat listen-poort is niet hetzelfde als de particuliere poort van de virtuele machine-eindpunt voor Tomcat verkeer Hallo Hallo.  

     Controleer uw openbare poort en de persoonlijke eindpunt poortinstellingen en zorg ervoor dat Hallo particuliere poort is hetzelfde als Tomcat Hallo Hallo poort luistert. Zie ' stap 1: een installatiekopie maken ' sectie van dit artikel voor instructies over het configureren van eindpunten voor uw virtuele machine.  

     toodetermine Hallo Tomcat poort luisteren, open /etc/httpd/conf/httpd.conf (Red Hat release) of /etc/tomcat7/server.xml (Debian-versie). Standaard is Hallo Tomcat listen-poort 8080. Hier volgt een voorbeeld:  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Als u een virtuele machine zoals Debian of Ubuntu en u wilt dat toochange Hallo standaard poort van Tomcat luisteren (bijvoorbeeld 8081) gebruikt, moet u ook Hallo-poort voor het besturingssysteem Hallo openen. Open eerst Hallo-profiel:  

        sudo vi /etc/default/tomcat7  

     Vervolgens Opmerkingen bij de laatste regel Hallo en wijzigt u 'Nee' te 'Ja'.  

        AUTHBIND=yes
  2. Hallo-firewall is uitgeschakeld door Hallo listen-poort van Tomcat.

     U kunt alleen Hallo Tomcat standaardpagina van de lokale host Hallo zien. Hallo-probleem is waarschijnlijk dat Hallo-poort geluisterd tooby Tomcat is, door Hallo-firewall is geblokkeerd. U kunt Hallo w3m hulpprogramma toobrowse Hallo webpagina gebruiken. Hallo volgende opdrachten installeren w3m en toohello Tomcat standaardpagina bladeren:  


        sudo yum installeren w3m w3m-img


        w3m http://localhost: 8080  
#### <a name="solution"></a>Oplossing

  * Als Hallo Tomcat listen-poort is niet dezelfde als de particuliere poort Hallo van Hallo-eindpunt voor verkeer toohello virtuele machine hello, hoeft u particuliere poort Hallo wijzigen toobe Hallo hetzelfde als het Hallo Tomcat listen-poort.   
  2. Als Hallo probleem wordt veroorzaakt door een firewall/iptables, voegt u Hallo regels te/etc/sysconfig/iptables te volgen. de tweede regel Hallo is alleen nodig voor https-verkeer:  

      -A -p tcp -m tcp--port 80 -j accepteren invoer

      -A -p tcp -m tcp--Port 443 -j accepteren invoer  

     > [!IMPORTANT]
     > Zorg Hallo voorgaande regels boven alle regels die u zou toegang, zoals de volgende Hallo globaal beperken: - een invoer -j afwijzen--afwijzen-met icmp host verboden



tooreload hello iptables, Hallo volgende opdracht uitvoeren:

    service iptables restart

Dit is getest op CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>De toegang is geweigerd tijdens het uploaden van project-bestanden te/var/lib/tomcat7/webapps /
#### <a name="symptom"></a>Symptoom
  Als u een virtuele machine voor SFTP-client (zoals FileZilla) tooconnect tooyour gebruiken en navigeer te/var/lib/tomcat7/webapps/toopublish uw site, krijgt u een fout bericht vergelijkbaar toohello volgende:  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Mogelijke hoofdoorzaken
  U hebt geen machtigingen tooaccess hello /var/lib/tomcat7/webapps map.  
#### <a name="solution"></a>Oplossing  
  U moet de machtiging tooget van Hallo root-account. U kunt Hallo eigendom van die map wijzigen via hoofdmap toohello gebruikersnaam die u hebt gebruikt toen u Hallo machine ingericht. Hier volgt een voorbeeld met Hallo azureuser accountnaam:  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Hallo -R optie tooapply Hallo machtigingen voor alle bestanden in een map te gebruiken.  

  Met deze opdracht werkt ook voor mappen. Hallo -R-optie wijzigingen Hallo machtigingen voor alle bestanden en mappen in Hallo-directory. Hier volgt een voorbeeld:  

     sudo chown -R username:group directory  

  Deze opdracht wijzigt eigendom (gebruiker en groep) voor alle bestanden en mappen die zich binnen het Hallo-directory.  

  Hallo volgende opdracht alleen wijzigt Hallo machtiging Hallo mapdirectory. Hallo-bestanden en mappen in de directory Hallo worden niet gewijzigd.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
