---
title: aaaWorking met Node.js-Modules
description: Meer informatie over hoe toowork met Node.js-modules bij gebruik van Azure App Service- of Cloudservices.
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Node.js-modules gebruiken met Azure-toepassingen
Dit document biedt richtlijnen voor het gebruik van Node.js-modules met toepassingen die worden gehost op Azure. Er wordt uitgelegd hoe u ervoor zorgt dat uw toepassing een bepaalde versie van een module gebruikt en dat er systeemeigen modules voor Azure worden gebruikt.

Als u al bekend bent met behulp van Node.js-modules **package.json** en **npm shrinkwrap.json** bestanden, Hallo volgende informatie bevat een kort overzicht van wat in dit artikel wordt beschreven:

* Azure App Service begrijpt **package.json** en **npm shrinkwrap.json** -bestanden en modules op basis van gegevens in deze bestanden kunt installeren.

* Azure Cloud Services verwachten alle modules toobe geïnstalleerd op Hallo ontwikkelomgeving en Hallo **knooppunt\_modules** directory toobe opgenomen als onderdeel van het implementatiepakket Hallo. Het is mogelijk tooenable ondersteuning voor het installeren van modules met behulp van **package.json** of **npm shrinkwrap.json** bestanden op Cloudservices; deze configuratie is echter vereist voor aanpassing van Hallo-standaard scripts die worden gebruikt door de Cloud Service-projecten. Voor een voorbeeld van hoe tooconfigure deze omgeving, Zie [Azure opstarten taak toorun npm tooavoid implementeren knooppunt modules installeren](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Virtuele Machines in Azure worden niet beschreven in dit artikel, zoals Hallo implementatie-ervaring op een virtuele machine afhankelijk van het besturingssysteem Hallo gehost door Hallo virtuele Machine is.
> 
> 

## <a name="nodejs-modules"></a>Node.js-Modules
Modules zijn geladen JavaScript-pakketten die specifieke functionaliteit voor uw toepassing bieden. Modules worden meestal geïnstalleerd met behulp van Hallo **npm** opdrachtregelprogramma hulpprogramma, maar sommige modules (zoals Hallo HTTP-module) worden geleverd als onderdeel van Hallo core Node.js-pakket.

Wanneer modules zijn geïnstalleerd, worden ze opgeslagen in Hallo **knooppunt\_modules** map in de hoofdmap Hallo van directory-structuur van uw toepassing. Elke module binnen Hallo **knooppunt\_modules** directory onderhoudt een eigen **knooppunt\_modules** map waarin zich geen modules die afhankelijk is van en dit gedrag wordt herhaald voor elke module alle Hallo manier omlaag Hallo afhankelijkheidsketen. Deze omgeving kunt elke toohave-module geïnstalleerd zijn eigen versievereisten voor Hallo modules dat deze afhankelijk is, maar dit in zeer grote directory-structuur resulteren kan.

Implementatie Hallo **knooppunt\_modules** map als onderdeel van uw toepassing groter Hallo Hallo implementatie vergelijking toousing een **package.json** of  **npm shrinkwrap.json** bestand; echter, wordt gegarandeerd dat Hallo-versies van het Hallo-modules die worden gebruikt in productie dezelfde zijn Hallo als Hallo-modules die worden gebruikt in ontwikkeling.

### <a name="native-modules"></a>Systeemeigen Modules
Hoewel de meeste modules gewoon JavaScript tekstbestanden zijn, zijn sommige modules platform-specifieke binaire installatiekopieën. Deze modules worden gecompileerd tijdens de installatie, meestal met behulp van Python en knooppunt gyp. Omdat Azure Cloud Services zijn afhankelijk van Hallo **knooppunt\_modules** map wordt geïmplementeerd als onderdeel van de toepassing hello, een systeemeigen module opgenomen als onderdeel van modules Hallo geïnstalleerd in een cloudservice werken moet zoals deze was geïnstalleerd en op een Windows-ontwikkelsysteem gecompileerd.

Azure App Service biedt geen ondersteuning voor alle systeemeigen modules en mislukken bij het compileren van modules met specifieke vereisten. Hoewel sommige populaire modules zoals MongoDB optionele systeemeigen afhankelijkheden hebben en zonder deze werken, twee oplossingen bewezen succesvol kunnen werken met bijna alle beschikbare systeemeigen modules vandaag:

* Voer **npm installeren** op een Windows-machine waarop alle Hallo systeemeigen module van vereiste items geïnstalleerd is. Vervolgens implementeert Hallo gemaakt **knooppunt\_modules** map als onderdeel van Hallo toepassing tooAzure App Service.

  * Voor het compileren, Controleer u of overeenkomende architectuur heeft als uw lokale Node.js-installatie en Hallo-versie zo dicht mogelijk toohello die wordt gebruikt bij Azure is (Hallo huidige waarden kunnen worden gecontroleerd op de runtime van eigenschappen **process.arch**en **process.version**).

* Azure App Service kan geconfigureerde tooexecute aangepaste bash of shell-scripts tijdens de implementatie, zodat u Hallo kans tooexecute aangepaste opdrachten en nauwkeurig configureren Hallo manier **npm installeren** wordt uitgevoerd. Voor een video wordt weergegeven hoe tooconfigure die omgeving, Zie [aangepaste Website Implementatiescripts met Kudu].

### <a name="using-a-packagejson-file"></a>Met behulp van een package.json-bestand
Hallo **package.json** bestand is een manier toospecify Hallo op het hoogste niveau afhankelijkheden uw toepassing vereist zodat hello host-platform kunt installeren Hallo afhankelijkheden, in plaats van dat u tooinclude hello **knooppunt \_pakketten** map als onderdeel van Hallo-implementatie. Nadat de toepassing hello is geïmplementeerd, Hallo **npm installeren** opdracht is gebruikte tooparse hello **package.json** bestands- en alle vermelde Hallo-afhankelijkheden te installeren.

Tijdens de ontwikkeling, kunt u Hallo **--opslaan**, **--opslaan dev**, of **--opslaan optionele** parameters bij het installeren van modules tooadd een vermelding voor Hallo module tooyour **package.json** bestand automatisch. Zie voor meer informatie [npm-Installeer](https://docs.npmjs.com/cli/install).

Een mogelijk probleem met de Hallo **package.json** bestand is dat het Hallo-versie voor op het hoogste niveau afhankelijkheden alleen wordt opgegeven. Elke module die is geïnstalleerd kan of kan geen Hallo version Hallo-modules die afhankelijk van is opgeven, en is het mogelijk dat u met een andere afhankelijkheidsketen dan Hallo die wordt gebruikt bij de ontwikkeling eindigen mogelijk.

> [!NOTE]
> Bij het implementeren van tooAzure App Service, als uw <b>package.json</b> bestand verwijst naar een systeemeigen module ziet u mogelijk een foutbericht vergelijkbaar toohello voorbeeld te volgen bij het publiceren van Hallo-toepassing met Git:
> 
> npm ERR! module-name@0.6.0installeren: 'build knooppunt gyp configureren'
> 
> npm ERR! ' cmd "/ c" 'knooppunt gyp configureren build' ' is mislukt: 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Met behulp van een bestand npm shrinkwrap.json
Hallo **npm shrinkwrap.json** bestand is een poging tooaddress Hallo module versioning beperkingen van Hallo **package.json** bestand. Tijdens het Hallo **package.json** bestand bevat alleen versies voor modules die Hallo op het hoogste niveau hello **npm shrinkwrap.json** bestand Hallo versievereisten voor Hallo volledige module afhankelijkheidsketen bevat.

Wanneer uw toepassing gereed voor productie is, kunt u versievereisten vergrendelen en maakt een **npm shrinkwrap.json** bestand met behulp van Hallo **npm verpakking** opdracht. Met deze opdracht gebruikt Hallo-versies die momenteel geïnstalleerd in Hallo **knooppunt\_modules** map, en noteer deze versies toohello **npm shrinkwrap.json** bestand. Nadat de toepassing hello geïmplementeerde toohello hostomgeving zijn, Hallo **npm installeren** opdracht is gebruikte tooparse hello **npm shrinkwrap.json** bestands- en alle vermelde Hallo-afhankelijkheden te installeren. Zie voor meer informatie [npm verpakking](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> Bij het implementeren van tooAzure App Service, als uw <b>npm shrinkwrap.json</b> bestand verwijst naar een systeemeigen module ziet u mogelijk een foutbericht vergelijkbaar toohello voorbeeld te volgen bij het publiceren van Hallo-toepassing met Git:
> 
> npm ERR! module-name@0.6.0installeren: 'build knooppunt gyp configureren'
> 
> npm ERR! ' cmd "/ c" 'knooppunt gyp configureren build' ' is mislukt: 1
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nu dat u begrijpt hoe toouse Node.js-modules met Azure, informatie over hoe te[hello Node.js-versie opgeven], [bouwen en implementeren van een Node.js-web-app](app-service-web/app-service-web-get-started-nodejs.md), en [hoe toouse hello Azure vanaf de opdrachtregel Interface voor Mac en Linux].

Zie voor meer informatie, Hallo [Node.js Developer Center](/nodejs/azure/).

[hello Node.js-versie opgeven]: nodejs-specify-node-version-azure-apps.md
[hoe toouse hello Azure vanaf de opdrachtregel Interface voor Mac en Linux]:cli-install-nodejs.md
[aangepaste Website Implementatiescripts met Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
