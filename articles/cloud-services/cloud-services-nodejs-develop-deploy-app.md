---
title: aaaNode.js Getting Started Guide | Microsoft Docs
description: Ontdek hoe toocreate een eenvoudige Node.js-webtoepassing en tooan Azure cloudservice implementeren.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Bouw en implementeer een Node.js-toepassing tooan Azure Cloud Service

Deze zelfstudie laat zien hoe een eenvoudige Node.js toocreate toepassing die in een Azure Cloud Service wordt uitgevoerd. Cloudservices zijn Hallo bouwstenen van schaalbare cloudtoepassingen in Azure. Ze staan Hallo scheiding en onafhankelijke management en scale-out van de front-end en back-end-onderdelen van uw toepassing.  Cloud Services bieden een robuuste toegewezen virtuele machine voor het op betrouwbare wijze hosten van elke rol.

Zie voor meer informatie over Cloudservices en hoe ze zich verhouden tooAzure Websites en virtuele machines [vergelijking van Azure Websites, Cloudservices en virtuele Machines].

> [!TIP]
> Zoek toobuild een ongecompliceerde website? Als uw scenario alleen een ongecompliceerde website-front-end omvat, kunt u overwegen [een eenvoudige web-app-functie te gebruiken]. U kunt eenvoudig tooa Cloudservice bijwerken naarmate uw web-app groeit en uw vereisten veranderen.

In deze zelfstudie maakt u een eenvoudige webtoepassing gehost binnen een webrol. U wordt Hallo compute-emulator tootest lokaal uw toepassing gebruiken, en vervolgens implementeren met behulp van PowerShell-opdrachtregelprogramma's.

Hallo-toepassing is een eenvoudige 'Hallo wereld'-toepassing:

![Een webbrowser waarin Hallo Hallo wereld-webpagina][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Vereisten
> [!NOTE]
> In deze zelfstudie wordt Azure PowerShell gebruikt waarvoor Windows is vereist.

* Installeer en configureer [Azure Powershell].
* Download en installeer Hallo [Azure SDK voor .NET 2.7]. Installeer in Hallo setup, selecteren:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Een Azure Cloud Service-project maken
Voer Hallo taken toocreate een nieuw Azure Cloud Service-project, samen met Node.js-basisstructuur volgen:

1. Uitvoeren **Windows PowerShell** als Administrator; van Hallo **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**.
2. [Koppel PowerShell] tooyour abonnement.
3. Voer Hallo PowerShell cmdlet toocreate toocreate Hallo project te volgen:

        New-AzureServiceProject helloworld

    ![Hallo resultaat van de helloworld-opdracht Hallo New-AzureService][hello result of hello New-AzureService helloworld command]

    Hallo **New-AzureServiceProject** cmdlet genereert een basisstructuur voor het publiceren van een Node.js-toepassing tooa Service in de Cloud. Deze bevat configuratiebestanden die nodig zijn voor publicatie tooAzure. Hallo cmdlet wijzigt ook uw werkmap voor het toohello van directory voor Hallo-service.

    Hallo-cmdlet maakt Hallo volgende bestanden:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** en **ServiceDefinition.csdef**: Azure-specifieke bestanden die nodig zijn voor het publiceren van uw toepassing. Zie [Overzicht van het maken van een gehoste service voor Azure].
   * **deploymentSettings.json**: lokale instellingen die worden gebruikt door hello Azure PowerShell-cmdlets voor implementatie.
4. Voer Hallo opdracht tooadd een nieuwe Webrol te volgen:

       Add-AzureNodeWebRole

   ![Hallo-uitvoer van de opdracht Add-AzureNodeWebRole Hallo][hello output of hello Add-AzureNodeWebRole command]

   Hallo **Add-AzureNodeWebRole** cmdlet maakt een eenvoudige Node.js-toepassing. Hallo ook gewijzigd **.csfg** en **csdef** tooadd configuratie-items voor de nieuwe rol Hallo-bestanden.

   > [!NOTE]
   > Als u geen rolnaam opgeeft, wordt een standaardnaam gebruikt. U kunt een naam opgeven als eerste Hallo-cmdlet-parameter:`Add-AzureNodeWebRole MyRole`

Hallo Node.js-app is gedefinieerd in Hallo bestand **server.js**, dat zich bevindt in de directory voor de Webrol Hallo Hallo (**WebRole1** standaard). Dit is Hallo code:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Deze code is in wezen Hallo hetzelfde als 'Hallo wereld' Hallo steekproef op Hallo [nodejs.org] website, behalve het Hallo-poortnummer dat is toegewezen door de cloudomgeving Hallo gebruikt.

## <a name="deploy-hello-application-tooazure"></a>Hallo toepassing tooAzure implementeren

> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. U kunt [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) of [u aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Hello Azure downloaden instellingen publiceren
toodeploy uw tooAzure toepassing moet u eerst Hallo publicatie-instellingen voor uw Azure-abonnement downloaden.

1. Voer hello Azure PowerShell-cmdlet te volgen:

       Get-AzurePublishSettingsFile

   Hiermee worden gebruikt. uw browser toonavigate toohello publiceren downloadpagina van instellingen. Hebt u mogelijk na vragen aan gebruiker toolog met een Microsoft-Account. Als dit het geval is, moet u Hallo-account die is gekoppeld aan uw Azure-abonnement gebruiken.

   Hallo gedownload profiel tooa bestandslocatie u gemakkelijk bij kunt opslaan.
2. Voer de volgende cmdlet tooimport Hallo publiceren profiel dat u hebt gedownload:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Na het importeren van Hallo publicatie-instellingen, overweeg dan verwijderen Hallo gedownloade .publishSettings-bestand, omdat dit informatie bevat die iemand zou kunnen tooaccess uw account.

### <a name="publish-hello-application"></a>Hallo toepassing publiceren
toopublish hello volgende opdrachten uitvoeren:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** Hallo-naam voor het Hallo-implementatie. Dit moet een unieke naam, anders Hallo publicatieproces zal mislukken. Hallo **Get-Date** opdracht voegt een datum/tijd-tekenreeks die Hallo naam uniek te maken.
* **-Locatie** geeft Hallo datacenter waarin de toepassing hello zal worden gehost in. een lijst van beschikbare datacenters, gebruik Hallo toosee **Get-AzureLocation** cmdlet.
* **-Launch** opent een browservenster en gaat u toohello gehoste service nadat de implementatie is voltooid.

Nadat de publicatie is uitgevoerd, ziet u een reactie vergelijkbaar toohello volgende:

![Hallo-uitvoer van Hallo opdracht Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Het kan enkele minuten duren voordat Hallo toepassing toodeploy en beschikbaar is wanneer de eerste keer wordt gepubliceerd.

Zodra het Hallo-implementatie is voltooid, wordt een browservenster open en navigeer toohello-cloudservice.

![Een browservenster met Hallo Hallo wereld-pagina. Hallo URL geeft Hallo pagina wordt gehost in Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

Uw toepassing wordt nu uitgevoerd in Azure.

Hallo **Publish-AzureServiceProject** cmdlet voert Hallo stappen te volgen:

1. Hiermee maakt u een pakket toodeploy. Hallo-pakket bevat alle Hallo-bestanden in de toepassingsmap.
2. Er wordt een nieuw **opslagaccount** gemaakt, als dit nog niet bestaat. gebruikte toostore Hallo toepassingspakket is Hello Azure storage-account tijdens de implementatie. Nadat de implementatie is voltooid, kunt u veilig Hallo storage-account verwijderen.
3. Er wordt een nieuwe **cloudservice** gemaakt als deze nog niet bestaat. Een **cloudservice** Hallo container waarin uw toepassing wordt gehost wanneer deze geïmplementeerde tooAzure is. Zie [Overzicht van het maken van een gehoste service voor Azure].
4. Hallo implementatie pakket tooAzure publiceert.

## <a name="stopping-and-deleting-your-application"></a>De toepassing stoppen en verwijderen
Na implementatie van uw toepassing, kunt u toodisable zodat u extra kosten kunt voorkomen. Webrolexemplaren in Azure worden per uur van verbruikte servertijd in rekening gebracht. Er wordt servertijd verbruikt zodra uw toepassing is geïmplementeerd, zelfs als Hallo exemplaren niet worden uitgevoerd en met de status Hallo gestopt.

1. In Hallo Windows PowerShell-venster stopt Hallo service-implementatie gemaakt in de vorige sectie Hallo Hello volgende cmdlet:

       Stop-AzureService

   Hallo-service wordt gestopt, kan dit enkele minuten duren. Wanneer het Hallo-service wordt gestopt, krijgt u een bericht weergegeven dat aangeeft dat deze is gestopt.

   ![Hallo-status van de opdracht Hallo Stop-AzureService][hello status of hello Stop-AzureService command]
2. toodelete hello service aanroep Hallo volgende cmdlet:

       Remove-AzureService

   Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-service.

   Verwijderen van Hallo-service kan enkele minuten duren. U ontvangt een bericht weergegeven dat aangeeft dat het Hallo-service is verwijderd nadat het Hallo-service is verwijderd.

   ![Hallo-status van de opdracht Hallo Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Hallo-service verwijderen Hallo storage-account dat is gemaakt tijdens het Hallo-service is in eerste instantie gepubliceerd niet verwijderd en u blijft toobe kosten in rekening gebracht voor opslag gebruikt. Als niets anders Hallo opslag wordt gebruikt, kunt u toodelete deze.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [Node.js Developer Center].

<!-- URL List -->

[vergelijking van Azure Websites, Cloudservices en virtuele Machines]: ../app-service-web/choose-web-site-cloud-service-vm.md
[een eenvoudige web-app-functie te gebruiken]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure Powershell]: /powershell/azureps-cmdlets-docs
[Azure SDK voor .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Koppel PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Overzicht van het maken van een gehoste service voor Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
