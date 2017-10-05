---
title: Een Node.js-toepassing voor virtuele Linux-Machines in Azure implementeren
description: Informatie over het implementeren van een Node.js-toepassing voor virtuele Linux-machines in Azure.
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
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a>Een Node.js-toepassing voor virtuele Linux-Machines in Azure implementeren
Deze zelfstudie ziet een Node.js-toepassing maken en implementeren op Linux virtuele machines in Azure wordt uitgevoerd. De instructies in deze zelfstudie kunnen worden uitgevoerd in elk besturingssysteem waarmee Node.js kan worden uitgevoerd.

U leert hoe:

* Fork- en kloon een GitHub-opslagplaats met een eenvoudige toepassing voor TODO;
* Maken en configureren van twee virtuele Linux-machines in Azure om het starten van de toepassing.
* De toepassing door om updates te pushen naar de virtuele machine van de webserver-frontend herhalen.

> [!NOTE]
> Voor deze zelfstudie hebt voltooid, moet u een GitHub-account en een Microsoft Azure-account en de mogelijkheid om met Git van een ontwikkelcomputer.
> 
> Als u geen een GitHub-account hebt, kunt u zich aanmeldt [hier](https://github.com/join).
> 
> Als u hebt een [Microsoft Azure](https://azure.microsoft.com/) -account, u kunt zich aanmelden voor een gratis proefversie [hier](https://azure.microsoft.com/pricing/free-trial/). Dit ook loodst u door het registratieproces voor een [Microsoft-Account](http://account.microsoft.com) als u nog geen een. Als u een Visual Studio-abonnee bent, u kunt ook [activeren van uw voordelen als MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Als u geen git op uw ontwikkelcomputer, als u een Macintosh of Windows-machine, installeert u git van [hier](http://www.git-scm.com). Als u Linux installeren met het meest geschikt is voor u, mechanisme, zoals git `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a>Vertakken en klonen de TODO-toepassing
De TODO-toepassing die wordt gebruikt door deze zelfstudie implementeert een eenvoudige web-front via een MongoDB-exemplaar waarin een takenlijsten wordt bijgehouden. Ga na het aanmelden met GitHub, [hier](https://github.com/stepro/node-todo) te vinden van de toepassing en vertakken met behulp van de koppeling in de rechterbovenhoek. Dit moet een opslagplaats maken in uw account met de naam *accountname*/node-todo.

Nu op uw ontwikkelcomputer deze opslagplaats klonen:

    git clone https://github.com/accountname/node-todo.git

We gebruiken deze lokale kloon van de opslagplaats enigszins hoger als u wijzigingen aanbrengt aan de broncode.

## <a name="creating-and-configuring-the-linux-virtual-machines"></a>Maken en configureren van de virtuele Linux-Machines
Azure biedt uitstekende ondersteuning voor onbewerkte compute gebruik van Linux virtuele machines. Dit deel van de zelfstudie ziet u hoe u kunt eenvoudig ronddraaien van twee Linux virtuele machines en implementeert de TODO-toepassing, de front-end web uitgevoerd op één en het MongoDB-exemplaar op de andere.

### <a name="creating-virtual-machines"></a>Maken van virtuele Machines
De eenvoudigste manier om een nieuwe virtuele machine maken in Azure is de Azure Portal gebruiken. Klik op [hier](https://portal.azure.com) aanmelden en starten van de Azure-Portal in uw webbrowser. Nadat de Azure Portal is geladen, kunt u de volgende stappen:

* Klik op de koppeling '+ Nieuw';
* De categorie "Compute" kiest en kiest u 'Ubuntu Server 14.04 TNS';
* Selecteer het implementatiemodel ' Resource Manager ' en klik op 'Maken';
* Vul in de basisbeginselen deze richtlijnen te volgen:
  * Geef een naam die u later; eenvoudig kunt herkennen
  * Voor deze zelfstudie kiest wachtwoordverificatie;
  * Een nieuwe resourcegroep maken met de naam van een identificeerbaar.
* Voor de grootte van de virtuele Machine is 'A1 standaard' een redelijke keuze voor deze zelfstudie.
* Zorg ervoor dat het schijftype is 'Standaard' voor extra instellingen en de overige standaardinstellingen accepteren.
* Ere van het maken op de pagina overzicht.

Voer de bovenstaande procedure tweemaal voor het maken van twee virtuele Linux-machines, één voor de web-frontend en één voor de MongoDB-exemplaar. Maken van de virtuele machines duurt ongeveer 5 tot 10 minuten.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Een DNS-vermelding toe te wijzen voor virtuele Machines
Virtuele machines in Azure gemaakt worden standaard alleen toegankelijk zijn via een openbaar IP-adres zoals 1.2.3.4. We maken de machines meer gemakkelijk kan worden geïdentificeerd door toe te wijzen DNS-vermeldingen.

Zodra de portal geeft aan dat de virtuele machines zijn gemaakt, klik op de koppeling 'Virtuele machines' in de navigatiebalk links en zoek uw machines. Voor elke computer:

* Zoek de Essentials-tabblad en klik op het openbare IP-adres.
* Toewijzen van een label van DNS-naam in de openbare IP-adresconfiguratie en opslaan.

De portal zorgt ervoor dat de opgegeven naam beschikbaar is. Na het opslaan van de configuratie van uw virtuele machines hebben hostnamen vergelijkbaar met `machinename.region.cloudapp.azure.com`.

### <a name="connecting-to-the-virtual-machines"></a>Verbinding maken met de virtuele Machines
Wanneer uw virtuele machines zijn ingericht, zijn ze vooraf geconfigureerd voor het toestaan van externe verbindingen via SSH. Dit is het mechanisme dat wordt gebruikt om de virtuele machines configureren. Als u van Windows voor de ontwikkeling gebruikmaakt, moet u een SSH-client krijgen als u nog geen een. Een algemene keuze hier is PuTTY dat kan worden gedownload van [hier](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Macintosh- en Linux-OSes worden geleverd met een versie van SSH vooraf zijn geïnstalleerd.

### <a name="configuring-the-web-frontend-virtual-machine"></a>De virtuele Machine van de webserver-Frontend configureren
SSH met de web frontend-machine die u hebt gemaakt met PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma. U ziet een welkomstbericht gevolgd door een opdrachtprompt.

Eerst laten we controleren of git en knooppunt zijn beide geïnstalleerd:

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Sinds de toepassing web frontend op sommige systeemeigen Node.js-modules vertrouwt, moeten we ook installeert de essentiële van build-hulpprogramma's:

    sudo apt-get install -y build-essential

Tot slot gaan we installeert u een Node.js-toepassing aangeroepen *permanent*, waarmee Node.js servertoepassingen uit te voeren:

    sudo npm install -g forever

Dit zijn alle afhankelijkheden die nodig zijn op deze virtuele machine moeten kunnen maken van de toepassing web frontend uitvoeren, dus gaan we aan dat wordt uitgevoerd. We gaan een bare kloon van de GitHub-opslagplaats die u eerder forked zodat u eenvoudig updates aan de virtuele machine publiceren (komen aan bod in dit scenario update later) en de bare kloon zodat deze versie van de opslagplaats die daadwerkelijk kan worden uitgevoerd te klonen maken om dit te doen.

Vanaf basismap (~), voer de volgende opdrachten (vervangen *accountname* met de naam van uw GitHub-gebruikersaccount):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Nu de knooppunt-todo-map en voert u deze opdrachten uit:

    npm install
    forever start server.js

Web-frontend van de toepassing nu wordt uitgevoerd, maar er is één stap voordat u toegang hebt tot de toepassing van een webbrowser. De virtuele machine die u hebt gemaakt, wordt beveiligd door een Azure-resource aangeroepen een *netwerkbeveiligingsgroep*, die voor u is gemaakt bij het inrichten van de virtuele machine. Deze bron kan op dit moment alleen externe aanvragen op poort 22 worden doorgestuurd naar de virtuele machine, waardoor de SSH-communicatie met de computer, maar niets anders. Dus als u wilt weergeven van de TODO-toepassing die is geconfigureerd om uit te voeren op poort 8080, moet deze poort ook worden geopend.

Ga terug naar de Azure Portal en de volgende stappen uit:

* Klik op 'Resourcegroepen' in de navigatiebalk links;
* Selecteer de resourcegroep met de virtuele machine;
* Selecteer in de resulterende lijst met resources de netwerkbeveiligingsgroep (één met een pictogram schild);
* Kies in de eigenschappen 'inkomende beveiligingsregels';
* Klik in de werkbalk op "Toevoegen";
* Geef een naam op zoals 'standaard-toestaan-todo';
* Stel het protocol op de 'TCP';
* Stel het doelpoortbereik naar '8080';
* Klik op OK en wacht totdat de beveiligingsregel moet worden gemaakt.

Nadat deze regel is gemaakt, de toepassing TODO iedereen op internet zichtbaar is en u kunt bladeren, bijvoorbeeld met een URL, zoals:

    http://machinename.region.cloudapp.azure.com:8080

U ziet dat hoewel we de MongoDB-virtuele machine nog niet hebt geconfigureerd, de TODO-toepassing wordt weergegeven behoorlijk functioneel te laten. Dit is omdat de bron-opslagplaats is vastgelegd om een vooraf geïmplementeerde MongoDB-exemplaar te gebruiken. Wanneer we de MongoDB-virtuele machine hebt geconfigureerd, wordt er Ga terug en wijzig de broncode voor het gebruik van onze persoonlijke MongoDB-exemplaar in plaats daarvan.

### <a name="configuring-the-mongodb-virtual-machine"></a>De MongoDB-virtuele Machine configureren
SSH met de tweede computer die u hebt gemaakt met PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma. Na de behandeling van het welkomstbericht en een opdrachtprompt, installeer MongoDB (deze instructies zijn genomen [hier](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

MongoDB is standaard geconfigureerd zodat deze alleen toegankelijk is lokaal. Voor deze zelfstudie wordt we MongoDB configureren zodat deze kan worden geopend op de virtuele machine van de toepassing. Open het bestand /etc/mongod.conf in een context sudo en zoek de `# network interfaces` sectie. Wijzig de `net.bindIp` configuratiewaarde voor `0.0.0.0`.

> [!NOTE]
> Deze configuratie is voor de doeleinden van deze zelfstudie alleen. Het is **niet** een aanbevolen beveiligingsprocedure en mag niet worden gebruikt in een productieomgeving.
> 
> 

Nu moet u de MongoDB-service is gestart:

    sudo service mongod restart

MongoDB werkt via poort 27017 standaard. Op dezelfde manier die we nodig om te open poort 8080 op de virtuele machine van de webserver-frontend, moeten we dus open poort 27017 op de virtuele machine van MongoDB.

Ga terug naar de Azure Portal en de volgende stappen uit:

* Klik op 'Resourcegroepen' in de navigatiebalk links;
* Selecteer de resourcegroep met de virtuele machine van MongoDB;
* Selecteer in de resulterende lijst met resources de netwerkbeveiligingsgroep (één met een pictogram schild) met dezelfde naam die u hebt opgegeven op de virtuele machine van MongoDB;
* Kies in de eigenschappen 'inkomende beveiligingsregels';
* Klik in de werkbalk op "Toevoegen";
* Geef een naam op zoals 'standaard-toestaan-mongo';
* Stel het protocol op de 'TCP';
* Stel het doelpoortbereik naar '27017';
* Klik op OK en wacht totdat de beveiligingsregel moet worden gemaakt.

## <a name="iterating-on-the-todo-application"></a>Doorlopen van de TODO-toepassing
Tot nu toe hebben we twee virtuele Linux-machines ingericht: één met de toepassing web frontend en één die MongoDB-exemplaar wordt uitgevoerd. Maar er is een probleem - ingerichte MongoDB-exemplaar is niet werkelijk nog gebruikmaakt van de web-frontend. Laten we dit oplossen door web-front-code voor het gebruik van een omgevingsvariabele in plaats van een exemplaar vastgelegde bijwerken.

### <a name="changing-the-todo-application"></a>Het wijzigen van de TODO-toepassing
Open op uw ontwikkelcomputer waarop u eerst de opslagplaats knooppunt todo hebt gekloond, de `node-todo/config/database.js` -bestand in uw favoriete editor en wijzig de waarde van de url van de vastgelegde waarde zoals `mongodb://...` naar `process.env.MONGODB`.

Uw wijzigingen en push naar de GitHub-master:

    git commit -am "Get MongoDB instance from env"
    git push origin master

Helaas publiceren niet dit de wijziging op de virtuele machine van de webserver-frontend. Laten we enkele meer wijzigingen aanbrengen aan dat de virtuele machine om in te schakelen van een eenvoudige maar effectieve mechanisme voor het publiceren van updates, zodat u snel het effect van de wijzigingen in de productieomgeving kunt zien.

### <a name="configuring-the-web-frontend-virtual-machine"></a>De virtuele Machine van de webserver-Frontend configureren
Intrekken dat we eerder een bare kloon van de opslagplaats knooppunt todo op de virtuele machine van de webserver-frontend gemaakt. Het blijkt dat deze actie gemaakt met een nieuwe externe Git waarvoor wijzigingen kunnen worden geactiveerd. Eenvoudig pushen naar dit externe geeft niet erg echter het model snelle herhaling die ontwikkelaars zoekt werkte op hun code.

Wat we willen graag kunnen doen is Zorg ervoor dat de actieve TODO-toepassing wordt automatisch bijgewerkt wanneer er een push naar de externe opslagplaats op de virtuele machine optreedt, is. Dit is gelukkig gemakkelijk te bereiken met git.

GIT wordt een aantal hooks die worden aangeroepen op bepaalde tijden om te reageren op in de opslagplaats uitgevoerde acties. Deze worden opgegeven met behulp van de shell-scripts in de opslagplaats `hooks` map. De hook dat meest van toepassing is voor het scenario met automatische updates is het `post-update` gebeurtenis.

In een SSH-sessie op de virtuele machine van de webserver-frontend, wijzigt u in de `~/node-todo.git/hooks` directory en voegt u de volgende inhoud naar een bestand met de naam `post-update` (vervangen `machinename` en `region` met uw gegevens van de virtuele machine MongoDB):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Zorg ervoor dat dit bestand is uitvoerbaar bestand met de volgende opdracht:

    chmod 755 post-update

Dit script zorgt ervoor dat de huidige servertoepassing is gestopt, de code in de gekloonde opslagplaats wordt bijgewerkt naar de meest recente bijgewerkte afhankelijkheden is voldaan en de server opnieuw is opgestart. Ook zorgt ervoor dat de omgeving in voorbereiding voor het ontvangen van de eerste toepassingsupdate om de MongoDB-exemplaar van een omgevingsvariabele is geconfigureerd.

### <a name="configuring-your-development-machine"></a>Configureren van uw ontwikkelcomputer
Nu gaan we aan uw ontwikkelcomputer aangesloten op de virtuele machine van de webserver-frontend. Dit is net zo eenvoudig als het toevoegen van de bare-opslagplaats op de virtuele machine als een externe. Voer de volgende opdracht om dit te doen (vervangen *gebruiker* met de naam van de virtuele machine aanmelding voor uw web-frontend en *machinename* en *regio* indien nodig):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

Dit is alles dat nodig is om in te schakelen pushen of wijzigingen van kracht publiceert, van de virtuele machine van de webserver-frontend.

### <a name="publishing-updates"></a>Publicatie-Updates
Laten we de een wijziging die is gedaan tot nu toe zodat ons eigen MongoDB-exemplaar wordt gebruikt door de toepassing publiceren:

    git push azure master

U ziet de uitvoer is vergelijkbaar met het volgende:

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
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
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

Nadat deze opdracht is voltooid, probeert u het vernieuwen van de toepassing in een webbrowser. U moet mogelijk dat de takenlijst die hier wordt gepresenteerd is leeg en niet langer gebonden aan het gedeelde geïmplementeerde MongoDB-exemplaar.

Zorg voor het voltooien van de zelfstudie, wijziging van een andere, beter zichtbaar. Open het node-todo/public/index.html-bestand met behulp van uw favoriete editor op uw ontwikkelcomputer. Zoek de header jumbotron en wijzig de titel van het 'Ik ben een Todo-aholic' naar 'Ik ben een Todo-aholic op Azure!'.

Nu gaan we doorvoeren:

    git commit -am "Azurify the title"

Deze tijd, de wijziging gaat publiceren naar Azure voordat u deze terug naar de GitHub-repo:

    git push azure master

Zodra deze opdracht is voltooid, vernieuw de webpagina en ziet u de wijzigingen. Omdat ze er goed uitziet, push de wijziging terug naar de oorsprong externe: 

    git push origin master

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe een Node.js-toepassing uitvoeren en deze implementeren op Linux-machines in Azure wordt uitgevoerd. Zie voor meer informatie over virtuele Linux-machines in Azure, [Inleiding tot Linux op Azure](/documentation/articles/virtual-machines-linux-introduction/).

In het [Node.js Developer Center](/develop/nodejs/) vindt u meer informatie over het ontwikkelen van Node.js-toepassingen in Azure.

