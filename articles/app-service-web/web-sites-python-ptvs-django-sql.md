---
title: aaaDjango en SQL-Database in Azure met Python-Tools 2.2 voor Visual Studio
description: Informatie over hoe toouse hello Python-Tools voor Visual Studio toocreate een Django-web-app die gegevens opslaat in een SQL database-exemplaar en deze tooAzure App Service Web Apps te implementeren.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Django en SQL Database in Azure met Python Tools 2.2 for Visual Studio
In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] toocreate een eenvoudige web-app met een van de PTVS-voorbeeldsjablonen Hallo worden opgevraagd. Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

We leert hoe toouse een SQL-database gehost op Azure, hoe tooconfigure Hallo web app toouse een SQL-database en hoe toopublish web-app te Hallo[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zie Hallo [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met Azure Table Storage, MySQL en SQL Database-services. Dit artikel is gericht op App Service, Hallo stappen zijn vergelijkbaar bij het ontwikkelen van [Azure Cloud Services].

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2015
* [Python 2.7 32-bits]
* [Python Tools 2.2 for Visual Studio]
* [Python-Tools 2.2 voor Visual Studio Samples VSIX]
* [Azure SDK-tools voor VS 2015]
* Django 1.9 of hoger

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a name="create-hello-project"></a>Hallo-Project maken
In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon. We maken van een virtuele omgeving en installeert de vereiste pakketten. Maakt een lokale database met behulp van sqlite. Vervolgens voert we lokaal Hallo web-app.

1. Selecteer in Visual Studio **File**, **New Project**.
2. Hallo projectsjablonen uit Hallo [Python-Tools 2.2 voor Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **voorbeelden**. Selecteer **Polls Django Web Project** en klik op OK toocreate Hallo project.

     ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. U zult na vragen aan gebruiker tooinstall externe pakketten. Selecteer **Install into a virtual environment**.

     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Selecteer **Python 2.7** als Hallo basisinterpreter.

     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.  Selecteer vervolgens **Django Create Superuser**.
6. Hiermee opent u een Django-beheerconsole en maakt u een sqlite-database in de projectmap Hallo. Ga als volgt Hallo prompts toocreate een gebruiker.
7. Controleer of de toepassing hello door te drukken werkt <kbd>F5</kbd>.
8. Klik op **aanmelden** van de navigatiebalk Hallo Hallo boven.

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Voer Hallo referenties voor u gemaakt tijdens het synchroniseren van de database Hallo Hallo-gebruiker.

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Klik op **Create Sample Polls**.

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Klik op een poll en stem.

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Een SQL-database maken
Voor de database hello maken we een Azure SQL database.

U kunt een database maken met de volgende stappen.

1. Meld u aan bij Hallo [Azure Portal].
2. Klik onder aan het navigatiedeelvenster Hallo Hallo op **nieuw**. , klik op **gegevens en opslag** > **SQL-Database**.
3. Configureer Hallo nieuwe SQL-Database door een nieuwe resourcegroep maken en selecteer de juiste locatie Hallo.
4. Zodra het Hallo SQL-Database is gemaakt, klikt u op **openen in Visual Studio** in Hallo databaseblade.
5. Klik op **uw firewall configureren**.
6. In Hallo **firewallinstellingen** blade toevoegen van een firewallregel met **eerste IP-** en **END-IP** toohello openbare IP-adres van uw ontwikkelcomputer ingesteld. Klik op **Opslaan**.

   Hierdoor kunt verbindingen toohello-databaseserver van uw ontwikkelcomputer.
7. Klik in de databaseblade hello, op **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**.
8. Gebruik Hallo kopie knop tooput Hallo waarde van **ADO.NET** op Hallo Klembord.

## <a name="configure-hello-project"></a>Hallo Project configureren
In deze sectie configureert de web-app toouse Hallo SQL database die we zojuist hebben gemaakt. Ook installeren we extra Python-pakketten vereist toouse SQL-databases met Django. Vervolgens voert we lokaal Hallo web-app.

1. Open in Visual Studio **settings.py**, van Hallo *ProjectName* map. Plak tijdelijk Hallo-verbindingsreeks in Hallo-editor. Hallo-verbindingsreeks is in deze indeling:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Bewerk Hallo definitie van `DATABASES` toouse Hallo waarden hierboven.

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. Klik in Solution Explorer onder **Python-omgevingen**, met de rechtermuisknop op de virtuele omgeving Hallo en selecteert u **Install Python Package**.
2. Hallo-pakket installeren `pyodbc` met **pip**.

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Hallo-pakket installeren `django-pyodbc-azure` met **pip**.

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.  Selecteer vervolgens **Django Create Superuser**.

   Hiermee wordt de tabellen voor Hallo SQL-database die wordt gemaakt in de vorige sectie Hallo Hallo gemaakt. Ga als volgt Hallo prompts toocreate een gebruiker die geen toomatch Hallo gebruiker in Hallo sqlite-database gemaakt in de eerste sectie Hallo.
5. Voer de toepassing hello met `F5`. Polls die zijn gemaakt met **Create Sample Polls** en het Hallo-gegevens die zijn ingediend via stemmen, worden geserialiseerd in Hallo SQL-database.

## <a name="publish-hello-web-app-tooazure-app-service"></a>Hallo web app tooAzure App Service publiceren
Hello Azure .NET SDK biedt een eenvoudige manier toodeploy uw web web app tooAzure App Service Web Apps.

1. In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **publiceren**.

     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Klik op **Microsoft Azure Web Apps**.
3. Klik op **nieuw** toocreate een nieuwe web-app.
4. Vul Hallo velden te volgen en klik op **maken**.

   * **Web-appnaam**
   * **App Service-plan**
   * **Resourcegroep**
   * **Regio**
   * Laat **databaseserver** instellen te**geen database**
5. Accepteer alle overige standaardwaarden en klik op **Publiceren**.
6. De webbrowser wordt automatisch geopend toohello gepubliceerde web-app. U ziet Hallo web-app werkt zoals verwacht, met behulp van Hallo **SQL** database gehost in Azure.

   Gefeliciteerd.

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen toolearn meer over Python-Tools voor Visual Studio, Django en SQL-Database.

* [Documentatie Python Tools voor Visual Studio]
  * [Webprojecten]
  * [Cloudserviceprojecten]
  * [Foutopsporing op afstand in Microsoft Azure]
* [Documentatie bij Django]
* [SQL Database]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python-Tools 2.2 voor Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentatie bij Django]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
