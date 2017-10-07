---
title: aaaDjango en MySQL in Azure met Python Tools 2.2 voor Visual Studio
description: Informatie over hoe toouse hello Python-Tools voor Visual Studio toocreate een Django-web-app die gegevens opslaat in een MySQL-database-exemplaar en deze tooAzure App Service Web Apps te implementeren.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a>Django en MySQL in Azure met Python Tools 2.2 for Visual Studio
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

In deze zelfstudie gebruikt u [Python-Tools voor Visual Studio](https://www.visualstudio.com/vs/python) toocreate een eenvoudige web-app met een van de PTVS-voorbeeldsjablonen Hallo worden opgevraagd. U leert hoe toouse een MySQL-service wordt gehost op Azure, hoe tooconfigure Hallo web app toouse MySQL en hoe Hallo toopublish web-app te[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

> [!NOTE]
> Hallo informatie in deze zelfstudie is ook beschikbaar in de volgende video Hallo:
> 
> [PTVS 2.1: Django-app met MySQL][video]
> 
> 

Zie Hallo [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met Azure Table Storage, MySQL en SQL Database-services. Dit artikel is gericht op App Service, Hallo stappen zijn vergelijkbaar bij het ontwikkelen van [Azure Cloud Services].

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2015
* [Python 2.7 32-bits] of [Python 3.4 32-bits]
* [Python Tools 2.2 for Visual Studio]
* [Python-Tools 2.2 voor Visual Studio Samples VSIX]
* [Azure SDK-tools voor VS 2015]
* Django 1.9 of hoger

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. Er is geen creditcard vereist en u bent nergens toe verplicht.
> 
> 

## <a name="create-hello-project"></a>Hallo-Project maken
In deze sectie maakt u een Visual Studio-project met behulp van een voorbeeldsjabloon. U maakt een virtuele omgeving en installeert de vereiste pakketten. U maakt een lokale database met behulp van sqlite. Vervolgens voert u lokaal Hallo-toepassing.

1. Selecteer in Visual Studio **File**, **New Project**.
2. Hallo projectsjablonen uit Hallo [Python-Tools 2.2 voor Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **voorbeelden**. Selecteer **Polls Django Web Project** en klik op OK toocreate Hallo project.
   
    ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. U zult na vragen aan gebruiker tooinstall externe pakketten. Selecteer **Install into a virtual environment**.
   
    ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. Selecteer **Python 2.7** of **Python 3.4** als Hallo basisinterpreter.
   
    ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.  Selecteer vervolgens **Django Create Superuser**.
6. Hiermee opent u een Django-beheerconsole en maakt u een sqlite-database in de projectmap Hallo. Ga als volgt Hallo prompts toocreate een gebruiker.
7. Controleer of de toepassing hello door te drukken werkt `F5`.
8. Klik op **aanmelden** van de navigatiebalk Hallo Hallo boven.
   
    ![Django-navigatiebalk](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. Voer Hallo referenties voor u gemaakt tijdens het synchroniseren van de database Hallo Hallo-gebruiker.
   
    ![Aanmeldscherm](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. Klik op **Create Sample Polls**.
    
     ![Voorbeeld-polls maken](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. Klik op een poll en stem.
    
     ![Stemmen in voorbeeld-polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a>Een MySQL-database maken
Voor Hallo-database maakt u een gehoste ClearDB MySQL-database in Azure.

Als alternatief kunt u uw eigen virtuele machine maken die wordt uitgevoerd in Azure, en vervolgens MySQL zelf installeren en beheren.

U kunt een database maken met een gratis abonnement. Ga hiervoor als volgt te werk.

1. Meld u bij toohello [Azure Portal].
2. Hallo boven in het navigatiedeelvenster hello, klikt u op **nieuw**, klikt u vervolgens op **gegevens en opslag**, en klik vervolgens op **MySQL-Database**.
3. Hallo nieuwe MySQL-database configureren door een nieuwe resourcegroep maken en selecteer Hallo juiste locatie.
4. Zodra het Hallo MySQL-database is gemaakt, klikt u op **eigenschappen** in Hallo databaseblade.
5. Gebruik Hallo kopie knop tooput Hallo waarde van **VERBINDINGSREEKS** op Hallo Klembord.

## <a name="configure-hello-project"></a>Hallo Project configureren
In deze sectie configureert u de web-app toouse Hallo MySQL-database die u zojuist hebt gemaakt. U kunt ook extra Python-pakketten vereist toouse MySQL-databases met Django installeren. Vervolgens voert u lokaal Hallo web-app.

1. Open in Visual Studio **settings.py**, van Hallo *ProjectName* map. Plak tijdelijk Hallo-verbindingsreeks in Hallo-editor. Hallo-verbindingsreeks is in deze indeling:
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    Wijziging Hallo standaarddatabase **ENGINE** toouse MySQL en stel de waarden voor Hallo **naam**, **gebruiker**, **wachtwoord** en  **HOST** van Hallo **CONNECTIONSTRING**.
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. Klik in Solution Explorer onder **Python-omgevingen**, met de rechtermuisknop op de virtuele omgeving Hallo en selecteert u **Install Python Package**.
3. Hallo-pakket installeren `mysqlclient` met **pip**.
   
    ![Het dialoogvenster Install Package](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.  Selecteer vervolgens **Django Create Superuser**.
   
    Hiermee wordt Hallo tabellen voor Hallo u hebt gemaakt in de vorige sectie Hallo MySQL-database gemaakt. Ga als volgt Hallo prompts toocreate een gebruiker die geen toomatch Hallo gebruiker in Hallo sqlite-database gemaakt in de eerste sectie Hallo van dit artikel.
5. Voer de toepassing hello met `F5`. Polls die zijn gemaakt met **Create Sample Polls** en het Hallo-gegevens die zijn ingediend via stemmen, worden geserialiseerd in Hallo MySQL-database.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Hallo web app tooAzure App Service publiceren
Hello Azure .NET SDK biedt een eenvoudige manier toodeploy uw web-app tooAzure App Service.

1. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **publiceren**.
   
    ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. Klik op **Microsoft Azure App Service**.
3. Klik op **nieuw** toocreate een nieuwe web-app.
4. Vul Hallo velden te volgen en klik op **maken**:
   
   * **Web-appnaam**
   * **App Service-plan**
   * **Resourcegroep**
   * **Regio**
   * Laat **databaseserver** instellen te**geen database**
5. Accepteer alle overige standaardwaarden en klik op **Publiceren**.
6. De webbrowser wordt automatisch geopend toohello gepubliceerde web-app. U ziet Hallo web-app werkt zoals verwacht, met behulp van Hallo **MySQL** database gehost in Azure.
   
    ![Webbrowser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    Gefeliciteerd. U hebt uw tooAzure MySQL gebaseerde web-app gepubliceerd.

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen toolearn meer over Python-Tools voor Visual Studio, Django en MySQL.

* [Documentatie Python Tools voor Visual Studio]
  * [Webprojecten]
  * [Cloudserviceprojecten]
  * [Foutopsporing op afstand in Microsoft Azure]
* [Documentatie bij Django]
* [MySQL]

Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).

<!--Link references-->

[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python-Tools 2.2 voor Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentatie bij Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
