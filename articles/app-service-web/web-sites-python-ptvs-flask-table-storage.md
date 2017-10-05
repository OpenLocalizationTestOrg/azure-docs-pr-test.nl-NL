---
title: Flask- en Azure Table Storage in Azure met Python Tools 2.2 voor Visual Studio
description: Informatie over het gebruik van de Python Tools for Visual Studio een Flask web-app die gegevens in Azure Table Storage opslaat maken en deze implementeren in Azure App Service Web Apps.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 2e1bc8eebd0b67b965cc70ac4b5dfe03c4720ddf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a>Flask- en Azure Table Storage in Azure met Python Tools 2.2 voor Visual Studio
In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] voor het maken van een eenvoudige polls web-app met een van de PTVS-voorbeeldsjablonen. Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).

De web-app polls definieert een abstractie voor de opslagplaats, zodat u gemakkelijk tussen verschillende soorten opslagplaatsen (In het geheugen, Azure Table Storage MongoDB schakelen kunt).

We het maken van een Azure Storage-account, het configureren van de web-app voor het gebruik van Azure Table Storage en hoe u de web-app publiceert leert [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zie de [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met MongoDB, Azure Table Storage, MySQL en SQL Database-services. Dit artikel is gericht op App Service, maar voor het ontwikkelen van [Azure Cloud Services] volgt u soortgelijk stappen.

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2015
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio Samples VSIX]
* [Azure SDK-tools voor VS 2015]
* [Python 2.7 32-bits] of [Python 3.4 32-bits]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="create-the-project"></a>Het project maken
In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon. We maken van een virtuele omgeving en installeert de vereiste pakketten. Vervolgens voert we de toepassing lokaal via de standaard in het geheugen-opslagplaats.

1. Selecteer in Visual Studio **File**, **New Project**.
2. De projectsjablonen uit de [Python Tools 2.2 for Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **Samples**. Selecteer **Polls Flask-webproject** en klik op OK om het project te maken.
   
     ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. U wordt gevraagd om externe pakketten te installeren. Selecteer **Install into a virtual environment**.
   
     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. Selecteer **Python 2.7** of **Python 3.4** als basisinterpreter.
   
     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. Controleer of de toepassing werkt, door te drukken op `F5`. De toepassing gebruikt standaard een opslagplaats in het geheugen die geen configuratie vereist. Alle gegevens gaat verloren wanneer de webserver is gestopt.
6. Klik op **Create Sample Polls**, klik op een poll en stem.
   
     ![Webbrowser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a>Een Azure Storage-Account maken
Als u wilt gebruiken opslagbewerkingen, moet u een Azure storage-account. U kunt een opslagaccount maken met de volgende stappen.

1. Meld u aan bij de [Azure-Portal](https://portal.azure.com/).
2. Klik op de **nieuw** pictogram op de bovenkant van de Portal links, klikt u op **gegevens en opslag** > **Opslagaccount**. Klik op **maken**, het storage-account een unieke naam geven en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.
   
      ![Snelle invoer](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    Wanneer het opslagaccount is gemaakt, de **meldingen** knop knippert een groene **geslaagd** en het opslagaccount blade geopend om weer te geven dat hoort bij de nieuwe resourcegroep die u hebt gemaakt.
3. Klik op de **toegangstoetsen** deel in het opslagaccount blade. Let op de accountnaam en de key1.
   
      ![Sleutels](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    We nodig deze informatie voor het configureren van uw project in de volgende sectie.

## <a name="configure-the-project"></a>Het project configureren
In deze sectie configureert onze toepassing voor het gebruik van het opslagaccount dat we zojuist hebben gemaakt. We ziet hoe u verbindingsinstellingen ophalen via de Azure-Portal. Er moet vervolgens de toepassing lokaal uitvoeren.

1. In Visual Studio met de rechtermuisknop op het projectknooppunt in Solution Explorer en selecteer **eigenschappen**. Klik op de **Debug** tabblad.
   
     ![Instellingen voor foutopsporing van project](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. Stel de waarden van omgevingsvariabelen die zijn vereist voor de toepassing in **serveropdracht Debug**, **omgeving**.
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   Hiermee wordt de omgevingsvariabelen ingesteld wanneer u **foutopsporing starten**. Als u wilt dat de variabelen worden ingesteld wanneer u **zonder foutopsporing starten**, stelt u de dezelfde waarden onder **Server-opdracht uitvoeren** ook.
   
   U kunt ook met behulp van de Windows-Configuratiescherm omgevingsvariabelen definiëren. Dit is een betere optie als u wilt voorkomen dat opslaan van referenties in de broncode / project bestand. Houd er rekening mee dat u Start Visual Studio voor de nieuwe Omgevingswaarden wilt wel zijn beschikbaar voor de toepassing opnieuw.
3. De code die u de opslagplaats voor Azure Table Storage implementeert is in **models/azuretablestorage.py**. Zie de [documentatie] voor meer informatie over het gebruik van de Service van de tabel met Python.
4. Voer de toepassing uit met `F5`. Polls die zijn gemaakt met **Create Sample Polls** en de gegevens die zijn ingediend via stemmen, worden geserialiseerd in Azure Table Storage.
   
   > [!NOTE]
   > De virtuele omgeving voor Python 2.7 kan ertoe leiden dat het einde van een uitzondering in Visual Studio.  Druk op `F5` om door te gaan met laden van het webproject.
   > 
   > 
5. Blader naar de **over** pagina om te bevestigen dat de toepassing gebruikmaakt van de **Azure Table Storage** opslagplaats.
   
     ![Webbrowser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a>De Azure-tabelopslag verkennen
Het is gemakkelijk weergeven en bewerken van storage-tabellen met Cloud Explorer in Visual Studio. In deze sectie we Server Explorer gebruiken om de inhoud van de toepassing polls tabellen weergeven.

> [!NOTE]
> Hiervoor moet Microsoft Azure-hulpprogramma's worden geïnstalleerd, die beschikbaar als zijn onderdeel van de [Azure SDK voor .NET].
> 
> 

1. Open **Cloud Explorer**. Vouw **Opslagaccounts**, uw storage-account, klikt u vervolgens **tabellen**.
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. Dubbelklik op de **polls** of **keuzes** tabel om de inhoud van de tabel in het venster van een document, evenals toevoegen/verwijderen/bewerken entiteiten weer te geven.
   
     ![De resultaten van de Query](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a>De web-app publiceren naar Azure App Service
De Azure SDK voor .NET biedt een eenvoudige manier om uw web-app in Azure App Service te implementeren.

1. Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Publiceren**.
   
     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. Klik op **Microsoft Azure Web Apps**.
3. Klik op **Nieuw** om een nieuwe web-app te maken.
4. Vul de volgende velden in en klikt u op **maken**.
   
   * **Web-appnaam**
   * **App Service-plan**
   * **Resourcegroep**
   * **Regio**
   * Laat **Databaseserver** ingesteld op **Geen database**.
5. Accepteer alle overige standaardwaarden en klik op **Publiceren**.
6. De gepubliceerde web-app wordt automatisch geopend in uw webbrowser. Als u naar bladeren de pagina, ziet u dat deze gebruikmaakt van de **In-Memory** -opslagplaats, niet de **Azure Table Storage** opslagplaats.
   
   Dat komt doordat de omgevingsvariabelen zijn niet ingesteld op het exemplaar van de Web-Apps in Azure App Service, zodat deze gebruikmaakt van de standaardwaarden die is opgegeven in **settings.py**.

## <a name="configure-the-web-apps-instance"></a>Het exemplaar van de Web-Apps configureren
In deze sectie configureert omgevingsvariabelen voor het exemplaar van de Web-Apps.

1. In [Azure Portal](https://portal.azure.com), opent u de web-app-blade door te klikken op **Bladeren** > **App Services** > de naam van uw web-app.
2. Klik op de blade van uw web-app **alle instellingen**, klikt u vervolgens op **toepassingsinstellingen**.
3. Schuif omlaag naar de **appinstellingen** sectie en stel de waarden voor **OPSLAGPLAATS\_naam**, **opslag\_naam** en **opslag \_Sleutel** zoals beschreven in de **configureren van het project** sectie hierboven.
   
     ![App-instellingen](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. Klik op **Opslaan**. Nadat u de meldingen dat de wijzigingen zijn toegepast hebt ontvangen, klikt u op **Bladeren** van de hoofdblade van Web-app.
5. U ziet de web-app werkt zoals verwacht, met behulp van de **Azure Table Storage** opslagplaats.
   
   Gefeliciteerd.
   
     ![Webbrowser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen voor meer informatie over Python Tools for Visual Studio, Flask en Azure Table Storage.

* [Documentatie Python Tools voor Visual Studio]
  * [Webprojecten]
  * [Cloudserviceprojecten]
  * [Foutopsporing op afstand in Microsoft Azure]
* [Flask-documentatie]
* [Azure Storage]
* [Azure-SDK voor Python]
* [Het gebruik van de Storage-Service van de tabel met Python]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentatie]:../cosmos-db/table-storage-how-to-use-python.md
[Het gebruik van de Storage-Service van de tabel met Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK voor .NET]: http://azure.microsoft.com/downloads/
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Flask-documentatie]: http://flask.pocoo.org/
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Azure-SDK voor Python]: https://github.com/Azure/azure-sdk-for-python
