---
title: aaaSpecifying een Node.js-versie
description: Meer informatie over hoe toospecify Hallo versie van Node.js gebruikt door Azure websites en Cloudservices
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Een Node.js-versie opgeven in een Azure-toepassing
Bij het hosten van een Node.js-toepassing, kunt u tooensure dat uw toepassing gebruikmaakt van een specifieke versie van Node.js. Er zijn verschillende manieren tooaccomplish dit voor toepassingen die worden gehost op Azure.

## <a name="default-versions"></a>Standaardversies
Hallo Node.js versies is verstrekt door Azure worden voortdurend bijgewerkt. Tenzij anders vermeld, standaard-versie die is opgegeven in Hallo Hallo `WEBSITE_NODE_DEFAULT_VERSION` omgevingsvariabele wordt gebruikt. toooverride deze standaardwaarde, Hallo Volg de stappen in de volgende secties van dit artikel

> [!NOTE]
> Als u uw toepassing in een Azure Cloud Service (web- of worker-rol) host, en deze Hallo eerste keer dat u de toepassing hello hebt geïmplementeerd, Azure toouse wordt geprobeerd dezelfde versie van Node.js Hallo als u op uw ontwikkelingsomgeving hebt geïnstalleerd als deze komt overeen met een van Hallo standaardversies beschikbaar zijn op Azure.
>
>

## <a name="versioning-with-packagejson"></a>Versiebeheer voor onderdelen met package.json
Kunt u Hallo-versie van Node.js toobe gebruikt door toe te voegen Hallo na tooyour **package.json** bestand:

    "engines":{"node":version}

Waar *versie* Hallo specifieke versie nummer toouse is. Kunt u complexere voorwaarden voor de versie, zoals:

    "engines":{"node": "0.6.22 || 0.8.x"}

Aangezien 0.6.22 niet een van de Hallo versies beschikbaar zijn in de hostomgeving hello is, hello hoogste versie van Hallo 0,8 reeks die beschikbaar worden gebruikt in plaats daarvan - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Versiebeheer Websites met App-instellingen
Als u de toepassing hello in een Website host, kunt u instellen Hallo omgevingsvariabele **WEBSITE_NODE_DEFAULT_VERSION** toohello gewenste versie.

## <a name="versioning-cloud-services-with-powershell"></a>Versiebeheer Cloudservices met PowerShell
Als u als host voor Hallo-toepassing in een Cloudservice optreden en Hallo-toepassing met Azure PowerShell implementeert, kunt u de standaardversie van Node.js Hallo overschrijven met behulp van Hallo **Set AzureServiceProjectRole** PowerShell-cmdlet. Bijvoorbeeld:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Opmerking Hallo parameters in Hallo hierboven instructie zijn hoofdlettergevoelig.  U kunt controleren of de juiste versie Hallo van Node.js is geselecteerd door te controleren Hallo **engines** eigenschap in uw rol **package.json**.

U kunt ook Hallo **Get-AzureServiceProjectRoleRuntime** tooretrieve een lijst met Node.js versies beschikbaar voor toepassingen die als Cloudservice wordt gehost.  Controleer altijd of Hallo-versie van Node.js afhankelijk van uw project zich in deze lijst.

## <a name="using-a-custom-version-with-azure-websites"></a>Met behulp van een aangepaste versie met Azure Websites
Hoewel Azure verschillende standaardversies zijn van Node.js biedt, kunt u toouse een versie die wordt standaard niet opgegeven. Als uw toepassing als een Azure-Website wordt gehost, u kunt dit doen met behulp van Hallo **iisnode.yml** bestand. Hallo doorlopen volgende stappen Hallo proces van het gebruik van een aangepaste versie van Node.Js met een Azure-Website:

1. Een nieuwe map maken en maak vervolgens een **server.js** bestand binnen Hallo-directory. Hallo **server.js** -bestand moet Hallo volgende bevatten:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Hallo Node.js-versie wordt gebruikt wanneer u Hallo website bladert wordt weergegeven.
2. Maak een nieuwe Website en de opmerking Hallo-naam van Hallo-site. Hallo volgende wordt bijvoorbeeld Hallo [Azure-opdrachtregelprogramma's] toocreate een nieuwe Azure-Website met de naam **MijnWebsite**, en schakel vervolgens een Git-opslagplaats voor Hallo-website.

        azure site create mywebsite --git
3. Maak een nieuwe map met de naam **bin** als een onderliggend element van Hallo map waarin zich Hallo **server.js** bestand.
4. Downloaden van de specifieke versie van Hallo **node.exe** (versie van Windows hello) dat u wenst dat toouse met uw toepassing. Bijvoorbeeld, Hallo na gebruikt **curl** toodownload versie 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Hallo opslaan **node.exe** -bestand in Hallo **bin** map die eerder is gemaakt.
5. Maakt een **iisnode.yml** bestanden per Hallo dezelfde map als Hallo **server.js** bestand en voeg vervolgens Hallo inhoud toohello na **iisnode.yml** bestand:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Dit pad is waar hello **node.exe** bestand in uw project worden geplaatst wanneer u uw toepassing toohello Azure-Website hebt gepubliceerd.
6. Uw toepassing publiceren. Bijvoorbeeld: nadat ik een nieuwe website eerder met de Hallo--git parameter gemaakt, hello volgende opdrachten wordt toevoegen Hallo toepassing bestanden toomy lokale Git-opslagplaats en push ze toohello website opslagplaats:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Nadat de toepassing hello is gepubliceerd, opent u Hallo-website in een browser. U ziet een bericht weergegeven ' Hallo van Azure actief knooppunt versie: v0.8.1 '.

## <a name="next-steps"></a>Volgende stappen
Nu u weet hoe toospecify Hallo versie van Node.js wordt gebruikt door uw toepassing, kunt u nagaan hoe te[werken met modules], [bouwen en implementeren van een Node.js-website](app-service-web/app-service-web-get-started-nodejs.md), en [hoe toouse hello Azure Opdrachtregelprogramma's voor Mac en Linux].

Zie voor meer informatie, Hallo [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).

[hoe toouse hello Azure Opdrachtregelprogramma's voor Mac en Linux]:cli-install-nodejs.md
[Azure-opdrachtregelprogramma's]:cli-install-nodejs.md
[werken met modules]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
