---
title: aaaBottle en Azure Table Storage in Azure met Python-Tools 2.2 voor Visual Studio
description: Informatie over hoe toouse hello Python-Tools voor Visual Studio toocreate een Bottle-toepassing die gegevens opslaat in Azure Table Storage en Hallo web app tooAzure App Service Web Apps te implementeren.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Bottle en Azure Table Storage in Azure met Python Tools 2.2 voor Visual Studio
In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] toocreate een eenvoudige web-app met een van de PTVS-voorbeeldsjablonen Hallo worden opgevraagd. Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=GJXDGaEPy94).

Hallo polls web-app definieert een abstractie voor de opslagplaats, zodat u gemakkelijk tussen verschillende soorten opslagplaatsen (In het geheugen, Azure Table Storage MongoDB schakelen kunt).

We leert hoe toocreate een Azure Storage-account, hoe tooconfigure Hallo web app toouse Azure Table Storage en hoe toopublish Hallo web-app te[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zie Hallo [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met MongoDB, Azure Table Storage, MySQL en SQL Database-services. Dit artikel is gericht op App Service, Hallo stappen zijn vergelijkbaar bij het ontwikkelen van [Azure Cloud Services].

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2015
* [Python Tools 2.2 for Visual Studio]
* [Python-Tools 2.2 voor Visual Studio Samples VSIX]
* [Azure SDK-tools voor VS 2015]
* [Python 2.7 32-bits] of [Python 3.4 32-bits]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="create-hello-project"></a>Hallo-Project maken
In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon. We maken van een virtuele omgeving en installeert de vereiste pakketten. Vervolgens voert we Hallo-toepassing lokaal via Hallo standaard in het geheugen opslagplaats.

1. Selecteer in Visual Studio **File**, **New Project**.
2. Hallo projectsjablonen uit Hallo [Python-Tools 2.2 voor Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **voorbeelden**. Selecteer **Polls Bottle-webproject** en klik op OK toocreate Hallo project.
   
     ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. U zult na vragen aan gebruiker tooinstall externe pakketten. Selecteer **Install into a virtual environment**.
   
     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. Selecteer **Python 2.7** of **Python 3.4** als Hallo basisinterpreter.
   
     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. Controleer of de toepassing hello door te drukken werkt `F5`. Hallo-toepassing gebruikt standaard een opslagplaats in het geheugen die geen configuratie vereist. Alle gegevens gaat verloren wanneer Hallo webserver is gestopt.
6. Klik op **Create Sample Polls**, klik op een poll en stem.
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Een Azure Storage-Account maken
toouse-opslagbewerkingen, moet u een Azure storage-account. U kunt een opslagaccount maken met de volgende stappen.

1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).
2. Klik op Hallo **nieuw** pictogram op de voorgrond Hallo Hallo Portal links, klikt u op **gegevens en opslag** > **Opslagaccount**.  Klik op Hallo **maken** knop vervolgens Hallo storage-account een unieke naam geven en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.
   
      ![Snelle invoer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    Wanneer Hallo storage-account is gemaakt, Hallo **meldingen** knop knippert een groene **geslaagd** en blade Hallo van het opslagaccount is geopend dat deze deel uitmaakt van de nieuwe resource toohello tooshow groep die u hebt gemaakt.
3. Klik op Hallo **toegangssleutels** deel in de blade Hallo van het opslagaccount. Let op het Hallo-accountnaam en key1.
   
      ![Sleutels](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    We moet deze informatie tooconfigure uw project in de volgende sectie Hallo.

## <a name="configure-hello-project"></a>Hallo Project configureren
In deze sectie configureert we onze toepassing toouse hello opslagaccount die we zojuist hebben gemaakt. Vervolgens voert we lokaal Hallo-toepassing.

1. In Visual Studio met de rechtermuisknop op het projectknooppunt in Solution Explorer en selecteer **eigenschappen**. Klik op Hallo **Debug** tabblad.
   
     ![Instellingen voor foutopsporing van project](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. Stel Hallo waarden van omgevingsvariabelen die worden vereist door de toepassing hello in **serveropdracht Debug**, **omgeving**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Deze omgevingsvariabelen hello wordt ingesteld wanneer u **foutopsporing starten**. Als u wilt dat Hallo variabelen toobe ingesteld wanneer u **zonder foutopsporing starten**, set Hallo dezelfde waarden onder **Server-opdracht uitvoeren** ook.
   
   U kunt ook met behulp van het Configuratiescherm van Windows hello omgevingsvariabelen definiëren. Dit is een betere optie als u wilt opslaan van referenties in de broncode tooavoid / projectbestand. Houd er rekening mee dat u Visual Studio toorestart voor Hallo nieuwe omgeving waarden toobe beschikbaar toohello toepassing nodig.
3. Hallo-code die wordt geïmplementeerd hello Azure Table Storage opslagplaats **models/azuretablestorage.py**. Zie Hallo [documentatie] voor meer informatie over het toouse Tabelservice van Python.
4. Voer de toepassing hello met `F5`. Polls die zijn gemaakt met **Create Sample Polls** en het Hallo-gegevens die zijn ingediend via stemmen, worden geserialiseerd in Azure Table Storage.
   
   > [!NOTE]
   > Hallo virtuele omgeving voor Python 2.7 kan ertoe leiden dat het einde van een uitzondering in Visual Studio.  Druk op `F5` toocontinue Hallo webproject wordt geladen.
   > 
   > 
5. Blader toohello **over** pagina tooverify die toepassing hello maakt gebruik van Hallo **Azure Table Storage** opslagplaats.
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a>Hello Azure Table Storage verkennen
Het is gemakkelijk tooview en storage-tabellen met Cloud Explorer in Visual Studio bewerken. We gebruiken Server Explorer tooview Hallo inhoud van Hallo polls toepassingstabellen in deze sectie.

> [!NOTE]
> Hiervoor moeten toobe van Microsoft Azure-hulpprogramma's geïnstalleerd, die beschikbaar zijn als onderdeel van Hallo [Azure SDK voor .NET].
> 
> 

1. Open **Cloud Explorer**. Vouw **Opslagaccounts**, uw storage-account, klikt u vervolgens **tabellen**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Dubbelklik op Hallo **polls** of **keuzes** tabel tooview Hallo inhoud van Hallo-tabel in het venster van een document, alsmede entiteiten toevoegen/verwijderen/bewerken.
   
     ![De resultaten van de Query](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a>Hallo web app tooAzure App Service publiceren
Hello Azure .NET SDK biedt een eenvoudige manier toodeploy uw web-app tooAzure App Service.

1. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **publiceren**.
   
     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Klik op **Microsoft Azure Web Apps**.
3. Klik op **nieuw** toocreate een nieuwe web-app.
4. Vul Hallo velden te volgen en klik op **maken**.
   
   * **Web-appnaam**
   * **App Service-plan**
   * **Resourcegroep**
   * **Regio**
   * Laat **databaseserver** instellen te**geen database**
5. Accepteer alle overige standaardwaarden en klik op **Publiceren**.
6. De webbrowser wordt automatisch geopend toohello gepubliceerde web-app. Als u toohello over pagina bladert, ziet u dat deze gebruikmaakt van Hallo **In-Memory** opslagplaats, niet Hallo **Azure Table Storage** opslagplaats.
   
   Dat komt doordat Hallo omgevingsvariabelen zijn niet ingesteld op Hallo Web-Apps-exemplaar in Azure App Service, zodat het Hallo-standaardwaarden die is opgegeven in beslag **settings.py**.

## <a name="configure-hello-web-apps-instance"></a>Hallo-Web-Apps exemplaar configureren
In deze sectie configureert omgevingsvariabelen voor Hallo Web-Apps-exemplaar.

1. In [Azure Portal], Hallo van web-app-blade geopend door te klikken op **Bladeren** > **App Services** > de naam van uw web-app.
2. Klik op de blade van uw web-app **alle instellingen**, klikt u vervolgens op **toepassingsinstellingen**.
3. Schuif omlaag toohello **appinstellingen** en stel de waarden voor Hallo **OPSLAGPLAATS\_naam**, **opslag\_naam** en  **OPSLAG\_sleutel** zoals beschreven in Hallo **configureren Hallo project** sectie hierboven.
   
     ![App-instellingen](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Klik op **Opslaan**. Nadat u hebt ontvangen Hallo meldingen dat Hallo wijzigingen zijn toegepast, klikt u op **Bladeren** van Web-app hoofdblade Hallo.
5. U ziet Hallo web-app werkt zoals verwacht, met behulp van Hallo **Azure Table Storage** opslagplaats.
   
   Gefeliciteerd.
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen toolearn meer over Python-Tools voor Visual Studio, Bottle en Azure Table Storage.

* [Documentatie Python Tools voor Visual Studio]
  * [Webprojecten]
  * [Cloudserviceprojecten]
  * [Foutopsporing op afstand in Microsoft Azure]
* [Bottle-documentatie]
* [Azure Storage]
* [Azure-SDK voor Python]
* [Hoe tooUse Hallo Table Storage-Service met Python]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentatie]:../cosmos-db/table-storage-how-to-use-python.md
[Hoe tooUse Hallo Table Storage-Service met Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK voor .NET]: http://azure.microsoft.com/downloads/
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python-Tools 2.2 voor Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Bottle-documentatie]: http://bottlepy.org/docs/dev/index.html
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Azure-SDK voor Python]: https://github.com/Azure/azure-sdk-for-python
