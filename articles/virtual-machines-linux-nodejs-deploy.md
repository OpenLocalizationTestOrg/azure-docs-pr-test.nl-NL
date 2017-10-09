---
title: aaaDeploy een Node.js-toepassing tooLinux virtuele Machines in Azure
description: Meer informatie over hoe een Node.js toodeploy toepassing tooLinux virtuele machines in Azure.
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Een Node.js-toepassing tooLinux virtuele Machines in Azure implementeren
Deze zelfstudie laat zien hoe tootake een Node.js-toepassing en implementeer het tooLinux virtuele machines in Azure wordt uitgevoerd. Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem waarmee Node.js uitgevoerd.

U leert hoe:

* Fork- en kloon een GitHub-opslagplaats met een eenvoudige toepassing voor TODO;
* Maken en configureren van twee virtuele Linux-machines in Azure toorun Hallo-toepassing.
* De toepassing hello herhalen door te pushen updates toohello web frontend virtuele machine.

> [!NOTE]
> toocomplete deze zelfstudie maakt u een GitHub-account en een Microsoft Azure-account nodig en Hallo mogelijkheid toouse Git van een ontwikkelcomputer.
> 
> Als u geen een GitHub-account hebt, kunt u zich aanmeldt [hier](https://github.com/join).
> 
> Als u hebt een [Microsoft Azure](https://azure.microsoft.com/) -account, u kunt zich aanmelden voor een gratis proefversie [hier](https://azure.microsoft.com/pricing/free-trial/). Dit ook loodst u door Hallo aanmeldingsproces voor een [Microsoft-Account](http://account.microsoft.com) als u nog geen een. Als u een Visual Studio-abonnee bent, u kunt ook [activeren van uw voordelen als MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Als u geen git op uw ontwikkelcomputer, als u een Macintosh of Windows-machine, installeert u git van [hier](http://www.git-scm.com). Als u van Linux gebruikmaakt, installeert u git met Hallo mechanisme meest geschikt is voor u, zoals `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Vertakken en klonen Hallo TODO-toepassing
Hallo TODO-toepassing die wordt gebruikt door deze zelfstudie implementeert een eenvoudige web-front via een MongoDB-exemplaar waarin een takenlijsten wordt bijgehouden. Ga na het aanmelden tooGitHub, [hier](https://github.com/stepro/node-todo) toofind toepassing hello en met behulp van Hallo-koppeling in de rechterbovenhoek Hallo vertakken. Dit moet een opslagplaats maken in uw account met de naam *accountname*/node-todo.

Nu op uw ontwikkelcomputer deze opslagplaats klonen:

    git clone https://github.com/accountname/node-todo.git

We gebruiken deze lokale kloon van de opslagplaats Hallo enigszins hoger als u wijzigingen aanbrengt toohello broncode.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Maken en configureren van Hallo virtuele Linux-Machines
Azure biedt uitstekende ondersteuning voor onbewerkte compute gebruik van Linux virtuele machines. Dit deel van Hallo zelfstudie ziet hoe u kunt eenvoudig ronddraaien van twee Linux virtuele machines en implementeert Hallo TODO toepassing toothem, actieve Hallo web frontend op één en Hallo MongoDB-exemplaar op Hallo andere.

### <a name="creating-virtual-machines"></a>Maken van virtuele Machines
Hallo gemakkelijkste manier toocreate een nieuwe virtuele machine in Azure is toouse hello Azure-Portal. Klik op [hier](https://portal.azure.com) toosign in en start hello Azure-Portal in uw webbrowser. Nadat de hello Azure Portal is geladen, moet u Hallo stappen te volgen:

* Klik op Hallo plusteken (+ nieuw) koppelen;
* Kies Hallo 'Compute' categorie en kiest u 'Ubuntu Server 14.04 TNS';
* Hallo ' Resource Manager '-implementatiemodel selecteren en klik op 'Maken';
* Vul Hallo basisbeginselen van deze richtlijnen te volgen:
  * Geef een naam die u later; eenvoudig kunt herkennen
  * Voor deze zelfstudie kiest wachtwoordverificatie;
  * Een nieuwe resourcegroep maken met de naam van een identificeerbaar.
* Voor Hallo grootte van virtuele Machine is 'A1 standaard' een redelijke keuze voor deze zelfstudie.
* Voor extra instellingen Zorg ervoor dat het schijftype Hallo 'Standaard' en accepteer dat alle overige standaardwaarden Hallo.
* Ere van Hallo maken op de overzichtspagina Hallo.

Uitvoeren van de bovenstaande Hallo tweemaal toocreate twee virtuele Linux-machines, één voor Hallo web frontend en één voor Hallo MongoDB-exemplaar. Maken van virtuele machines van Hallo duurt ongeveer 5 tot 10 minuten.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Een DNS-vermelding toe te wijzen voor virtuele Machines
Virtuele machines in Azure gemaakt worden standaard alleen toegankelijk zijn via een openbaar IP-adres zoals 1.2.3.4. We maken door het toewijzen van DNS-vermeldingen Hallo machines meer gemakkelijk kan worden geïdentificeerd.

Zodra het Hallo-portal geeft aan dat Hallo virtuele machines zijn gemaakt, klikt u op Hallo 'Virtuele machines' koppeling in het linkerdeelvenster navigatiebalk Hallo en zoek uw machines. Voor elke computer:

* Zoek Hallo Essentials tabblad en klik op Hallo openbare IP-adres.
* Een label van DNS-naam toewijzen en sla in Hallo openbare IP-adresconfiguratie.

Hallo portal zorgt ervoor dat u opgeeft Hallo-naam beschikbaar is. Na het opslaan van Hallo configuratie uw virtuele machines hebben vergelijkbare hostnamen te`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Verbinding maken met toohello virtuele Machines
Wanneer uw virtuele machines zijn ingericht, zijn ze vooraf geconfigureerde tooallow externe verbindingen via SSH. Dit is Hallo-mechanisme gebruiken we tooconfigure Hallo virtuele machines. Als u van Windows voor de ontwikkeling gebruikmaakt, moet u een SSH-client tooget als u nog geen een. Een algemene keuze hier is PuTTY dat kan worden gedownload van [hier](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Macintosh- en Linux-OSes worden geleverd met een versie van SSH vooraf zijn geïnstalleerd.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Hallo Web Frontend virtuele Machine configureren
SSH toohello web frontend machine hebt gemaakt met behulp PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma. U ziet een welkomstbericht gevolgd door een opdrachtprompt.

Eerst laten we controleren of git en knooppunt zijn beide geïnstalleerd:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Omdat een van de toepassing hello web frontend vertrouwt op sommige systeemeigen Node.js-modules, moeten we ook tooinstall Hallo essentiële set build hulpprogramma's:

    sudo apt-get install -y build-essential

Tot slot gaan we installeert u een Node.js-toepassing aangeroepen *permanent*, waarmee toorun Node.js server-toepassingen:

    sudo npm install -g forever

Dit zijn alle Hallo afhankelijkheden die op deze virtuele machine toobe kunnen toorun Hallo van de toepassing web frontend nodig, dus gaan we aan dat wordt uitgevoerd. toodo, we gaan een bare kloon van de GitHub-opslagplaats Hallo u eerder forked zodat u eenvoudig updates toohello virtuele machine publiceren (komen aan bod in dit scenario update later) en vervolgens Hallo bare kloon tooprovide klonen een versie van Hallo eerst maken de opslagplaats die daadwerkelijk kan worden uitgevoerd.

Hallo volgende opdrachten vanaf Hallo basismap (~), worden uitgevoerd (vervangen *accountname* met de naam van uw GitHub-gebruikersaccount):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Nu Hallo knooppunt todo-directory in en voer deze opdrachten uit:

    npm install
    forever start server.js

Hallo van de toepassing web frontend wordt nu uitgevoerd, maar er is één stap voordat u toegang hebt tot de toepassing hello vanuit een webbrowser. Hallo wordt virtuele machine die u hebt gemaakt beveiligd door een Azure-resource aangeroepen een *netwerkbeveiligingsgroep*, die voor u bij het inrichten van virtuele machine Hallo is gemaakt. Deze resource kan momenteel alleen externe aanvragen tooport 22 toobe gerouteerd toohello virtuele machine, waardoor de SSH-communicatie met de Hallo machine maar niets anders. Dus in volgorde tooview Hallo TODO-toepassing die geconfigureerd toorun op poort 8080 is, moet deze poort ook toobe die toegankelijk is gemaakt.

Ga terug toohello Azure-Portal en voltooien Hallo stappen te volgen:

* Klik op 'Resourcegroepen' in het linkerdeelvenster navigatiebalk Hallo;
* Selecteer Hallo-resourcegroep met de virtuele machine;
* Selecteer in de resulterende lijst met resources Hallo Hallo netwerkbeveiligingsgroep (hello een met een pictogram schild);
* Kies in de eigenschappen van Hallo 'inkomende beveiligingsregels';
* Klik in het Hallo-werkbalk op "Toevoegen";
* Geef een naam op zoals 'standaard-toestaan-todo';
* Hallo-protocol te instellen 'TCP';
* Hallo doelpoortbereik ingesteld te '8080';
* Klik op OK en wachten op Hallo beveiliging regel toobe gemaakt.

Nadat deze regel is gemaakt, Hallo TODO-toepassing is iedereen zichtbaar op Hallo van internet en u kunt bladeren tooit, bijvoorbeeld met een URL, zoals:

    http://machinename.region.cloudapp.azure.com:8080

U ziet dat hoewel we Hallo MongoDB virtuele machine nog niet hebt geconfigureerd, Hallo TODO-toepassing wordt weergegeven toobe behoorlijk functioneel. Dit is omdat Hallo bron opslagplaats hardcoded toouse vooraf geïmplementeerde MongoDB-exemplaar is. Wanneer we Hallo MongoDB virtuele machine hebt geconfigureerd, wordt er Ga terug en wijzig Hallo source code tooutilize onze persoonlijke MongoDB-exemplaar in plaats daarvan.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Hallo MongoDB virtuele Machine configureren
SSH toohello tweede machine hebt gemaakt met behulp PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma. Na de behandeling Welkom het Hallo-bericht en de opdrachtprompt, installeer MongoDB (deze instructies zijn genomen [hier](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

MongoDB is standaard geconfigureerd zodat deze alleen toegankelijk is lokaal. Voor deze zelfstudie wordt we MongoDB configureren zodat deze kan worden geopend op van de toepassing hello virtuele machine. In een context sudo hello /etc/mongod.conf bestand openen en zoek Hallo `# network interfaces` sectie. Wijziging Hallo `net.bindIp` configuratie waarde te`0.0.0.0`.

> [!NOTE]
> Deze configuratie is voor de toepassing hello van deze zelfstudie alleen. Het is **niet** een aanbevolen beveiligingsprocedure en mag niet worden gebruikt in een productieomgeving.
> 
> 

Nu moet Hallo MongoDB-service is gestart:

    sudo service mongod restart

MongoDB werkt via poort 27017 standaard. Dus in Hallo dezelfde manier dat we tooopen nodig poort 8080 op Hallo web frontend virtuele machine, moeten we tooopen poort 27017 op Hallo MongoDB virtuele machine.

Ga terug toohello Azure-Portal en voltooien Hallo stappen te volgen:

* Klik op 'Resourcegroepen' in het linkerdeelvenster navigatiebalk Hallo;
* Selecteer Hallo-resourcegroep met Hallo MongoDB virtuele machine;
* Selecteer in de resulterende lijst met resources Hallo Hallo netwerkbeveiligingsgroep (hello een met een pictogram schild) met dezelfde naam die u hebt gegeven toohello MongoDB virtuele machine; Hallo
* Kies in de eigenschappen van Hallo 'inkomende beveiligingsregels';
* Klik in het Hallo-werkbalk op "Toevoegen";
* Geef een naam op zoals 'standaard-toestaan-mongo';
* Hallo-protocol te instellen 'TCP';
* Hallo doelpoortbereik ingesteld te '27017';
* Klik op OK en wachten op Hallo beveiliging regel toobe gemaakt.

## <a name="iterating-on-hello-todo-application"></a>Sequentieel op Hallo TODO-toepassing
Tot nu toe hebben we twee virtuele Linux-machines ingericht: één die wordt uitgevoerd van de toepassing hello web frontend en één die MongoDB-exemplaar wordt uitgevoerd. Maar er is een probleem - Hallo ingericht MongoDB-exemplaar is niet werkelijk nog gebruikmaakt van Hallo web frontend. Laten we dit oplossen door Hallo web frontend code toouse bijwerken een omgevingsvariabele in plaats van een vastgelegde-exemplaar.

### <a name="changing-hello-todo-application"></a>Hallo TODO toepassing wijzigen
Open op uw ontwikkelcomputer waarop u eerst gekloond Hallo knooppunt todo-opslagplaats, Hallo `node-todo/config/database.js` -bestand in uw favoriete editor en Hallo url-waarde wijzigen van Hallo vastgelegde waarde zoals `mongodb://...` te`process.env.MONGODB`.

Uw wijzigingen en push toohello GitHub master:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Helaas publiceren niet dit Hallo wijzigen toohello frontend virtuele machine voor het web. We maken een paar meer wijzigingen toothat virtuele machine tooenable een eenvoudige maar effectieve mechanisme voor het publiceren van updates, zodat u snel Hallo effect van wijzigingen in de productieomgeving Hallo Hallo kunt zien.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Hallo Web Frontend virtuele Machine configureren
Intrekken dat we eerder een bare kloon van Hallo knooppunt todo-opslagplaats op Hallo web frontend virtuele machine gemaakt. Het blijkt dat deze actie gemaakt met een nieuwe Git remote toowhich wijzigingen kunnen worden geactiveerd. Eenvoudig pushen toothis externe geeft niet erg echter Hallo snelle herhaling model dat ontwikkelaars zoekt werkte op hun code.

Wat we wilt kunnen toodo toobe is ervoor Hallo actieve TODO-toepassing wordt automatisch bijgewerkt wanneer er een push toohello externe opslagplaats op Hallo virtuele machine optreedt, is. Dit is gelukkig eenvoudig tooachieve met git.

GIT wordt een aantal hooks die worden aangeroepen op bepaalde tijden tooreact tooactions die zijn gemaakt op Hallo-opslagplaats. Deze worden opgegeven met behulp van de shell-scripts in Hallo-opslagplaats `hooks` map. Hallo haakje dat meest van toepassing is voor automatische updates-scenario Hallo Hallo is `post-update` gebeurtenis.

Wijzig in een SSH-sessie toohello web frontend virtuele machine, toohello `~/node-todo.git/hooks` directory en toe te voegen inhoud tooa-bestand met de naam na Hallo `post-update` (vervangen `machinename` en `region` met uw gegevens van de virtuele machine MongoDB):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Zorg ervoor dat dit bestand door het uitvoeren van de volgende opdracht Hallo uitvoerbare bestand is:

    chmod 755 post-update

Dit script zorgt ervoor dat de huidige server-toepassing hello is gestopt, Hallo-code in de gekloonde opslagplaats Hallo bijgewerkte toohello nieuwste is, eventuele bijgewerkte afhankelijkheden is voldaan en Hallo-server opnieuw wordt opgestart. Dit zorgt er ook voor dat die Hallo-omgeving is geconfigureerd als voorbereiding voor het ontvangen van onze eerste toepassing update tooget hello MongoDB-exemplaar van een omgevingsvariabele.

### <a name="configuring-your-development-machine"></a>Configureren van uw ontwikkelcomputer
Nu gaan we aan uw ontwikkelcomputer aangesloten toohello web frontend virtuele machine. Dit is net zo eenvoudig als het Hallo bare-opslagplaats op Hallo virtuele machine als een externe toevoegen. Hallo na toodo opdracht uitvoeren (vervangen *gebruiker* met de naam van de virtuele machine aanmelding voor uw web-frontend en *machinename* en *regio* indien nodig):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Dit is alles wat nodig tooenable pushen of publiceren van kracht is, verandert de toohello web frontend virtuele machine.

### <a name="publishing-updates"></a>Publicatie-Updates
We gaan publiceren Hallo een wijziging die tot nu toe is gemaakt zodat deze toepassing hello ons eigen MongoDB-exemplaar wordt gebruikt:

    git push azure master

Hier ziet u uitvoer vergelijkbare toothis:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Nadat u deze opdracht is voltooid, kunt u Vernieuw Hallo-toepassing in een webbrowser. U moet kunnen toosee dat Hallo takenlijsten die hier wordt gepresenteerd leeg is en niet langer gebonden toohello gedeeld geïmplementeerd MongoDB-exemplaar.

toocomplete hello zelfstudie gaan we een andere, meer zichtbare wijziging aanbrengt. Open op uw ontwikkelcomputer Hallo node-todo/public/index.html bestand met behulp van uw favoriete editor. Zoek Hallo jumbotron header en Hallo titel van het 'Ik ben een Todo-aholic' te 'Ik ben een Todo-aholic op Azure!' wijzigen.

Nu gaan we doorvoeren:

    git commit -am "Azurify hello title"

Deze tijd, gaan we Hallo wijziging tooAzure publiceren voordat u deze GitHub-repo-tooback toohello:

    git push azure master

Wanneer u deze opdracht is voltooid, ziet webpagina Hallo vernieuwen en u Hallo wijzigingen. Omdat ze goed, push Hallo wijziging back toohello oorsprong externe: 

    git push origin master

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe tootake een Node.js-toepassing en implementeer het tooLinux virtuele machines in Azure wordt uitgevoerd. toolearn meer informatie over virtuele Linux-machines in Azure, Zie [tooLinux inleiding op Azure](/documentation/articles/virtual-machines-linux-introduction/).

Voor meer informatie over het toodevelop Node.js-toepassingen in Azure, Zie Hallo [Node.js Developer Center](/develop/nodejs/).

