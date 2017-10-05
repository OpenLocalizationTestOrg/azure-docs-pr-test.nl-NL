---
title: Django en SQL Database in Azure met Python Tools 2.2 for Visual Studio
description: Informatie over het gebruik van de Python Tools for Visual Studio een Django-web-app die gegevens in een SQL database-exemplaar opslaat maken en deze implementeren in Azure App Service Web Apps.
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a>Django en SQL Database in Azure met Python Tools 2.2 for Visual Studio
In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] voor het maken van een eenvoudige polls web-app met een van de PTVS-voorbeeldsjablonen. Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).

We het gebruik van een SQL-database gehost op Azure, het configureren van de web-app voor het gebruik van een SQL-database en de web-app te publiceren leert [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

Zie de [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met Azure Table Storage, MySQL en SQL Database-services. Dit artikel is gericht op App Service, maar voor het ontwikkelen van [Azure Cloud Services] volgt u soortgelijk stappen.

## <a name="prerequisites"></a>Vereisten
* Visual Studio 2015
* [Python 2.7 32-bits]
* [Python Tools 2.2 for Visual Studio]
* [Python Tools 2.2 for Visual Studio Samples VSIX]
* [Azure SDK-tools voor VS 2015]
* Django 1.9 of hoger

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
>
>

## <a name="create-the-project"></a>Het project maken
In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon. We maken van een virtuele omgeving en installeert de vereiste pakketten. Maakt een lokale database met behulp van sqlite. Er wordt vervolgens de web-app lokaal uitvoeren.

1. Selecteer in Visual Studio **File**, **New Project**.
2. De projectsjablonen uit de [Python Tools 2.2 for Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **Samples**. Selecteer **Polls Django Web Project** en klik op OK om het project te maken.

     ![Het dialoogvenster New Project](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. U wordt gevraagd om externe pakketten te installeren. Selecteer **Install into a virtual environment**.

     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. Selecteer **Python 2.7** als basisinterpreter.

     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Python**. Selecteer vervolgens **Django Migrate**.  Selecteer vervolgens **Django Create Superuser**.
6. Hiermee wordt in de projectmap een Django-beheerconsole en een sqlite-database gemaakt. Volg de aanwijzingen voor het maken van een gebruiker.
7. Controleer of de toepassing door te drukken werkt <kbd>F5</kbd>.
8. Klik in de navigatiebalk bovenaan op **Log in**.

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. Voer de referenties in voor de gebruiker die u hebt gemaakt tijdens het synchroniseren van de database.

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. Klik op **Create Sample Polls**.

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. Klik op een poll en stem.

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a>Een SQL-database maken
Voor de database maakt u een Azure SQL database.

U kunt een database maken met de volgende stappen.

1. Meld u aan bij de [Azure-Portal].
2. Klik onderaan in het navigatievenster op **nieuw**. , klik op **gegevens en opslag** > **SQL-Database**.
3. De nieuwe SQL-Database configureren door een nieuwe resourcegroep maken en selecteer de juiste locatie.
4. Nadat de SQL-Database is gemaakt, klikt u op **openen in Visual Studio** in de databaseblade.
5. Klik op **uw firewall configureren**.
6. In de **firewallinstellingen** blade toevoegen van een firewallregel met **eerste IP-** en **END-IP** ingesteld op het openbare IP-adres van uw ontwikkelcomputer. Klik op **Opslaan**.

   Hierdoor kunnen verbindingen met de databaseserver van uw ontwikkelcomputer.
7. Klik in de databaseblade op **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**.
8. Gebruik de knop kopiëren om de waarde van **ADO.NET** op het Klembord.

## <a name="configure-the-project"></a>Het project configureren
In deze sectie configureert de web-app voor het gebruik van de SQL-database die we zojuist hebben gemaakt. Installeren we ook extra Python-pakketten vereist voor het gebruik van SQL-databases met Django. Er wordt vervolgens de web-app lokaal uitvoeren.

1. Open in Visual Studio **settings.py** vanuit de map *ProjectName*. Plak de verbindingsreeks tijdelijk in de editor. De verbindingsreeks heeft de volgende indeling:

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

Bewerk de definitie van `DATABASES` als u de bovenstaande waarden.

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

1. Klik onder **Python-omgevingen** in Solution Explorer met de rechtermuisknop op de virtuele omgeving en selecteer **Install Python Package**.
2. Installeer het pakket `pyodbc` met behulp van **pip**.

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. Installeer het pakket `django-pyodbc-azure` met behulp van **pip**.

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Python**. Selecteer vervolgens **Django Migrate**.  Selecteer vervolgens **Django Create Superuser**.

   Hiermee maakt u de tabellen voor de SQL-database die in de vorige sectie is gemaakt. Volg de aanwijzingen voor het maken van een gebruiker die niet moet overeenkomen met de gebruiker in de sqlite-database gemaakt in de eerste sectie.
5. Voer de toepassing uit met `F5`. Polls die zijn gemaakt met **Create Sample Polls** en de gegevens die zijn ingediend via stemmen, worden geserialiseerd in de SQL-database.

## <a name="publish-the-web-app-to-azure-app-service"></a>De web-app publiceren naar Azure App Service
De Azure .NET SDK biedt een eenvoudige manier om uw web-web-app implementeren op Azure App Service Web Apps.

1. Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Publiceren**.

     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. Klik op **Microsoft Azure Web Apps**.
3. Klik op **Nieuw** om een nieuwe web-app te maken.
4. Vul de volgende velden in en klikt u op **maken**.

   * **Web-appnaam**
   * **App Service-plan**
   * **Resourcegroep**
   * **Regio**
   * Laat **Databaseserver** ingesteld op **Geen database**.
5. Accepteer alle overige standaardwaarden en klik op **Publiceren**.
6. De gepubliceerde web-app wordt automatisch geopend in uw webbrowser. U ziet de web-app werkt zoals verwacht, met behulp van de **SQL** database gehost in Azure.

   Gefeliciteerd.

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen voor meer informatie over Python Tools for Visual Studio, Django en SQL-Database.

* [Documentatie Python Tools voor Visual Studio]
  * [Webprojecten]
  * [Cloudserviceprojecten]
  * [Foutopsporing op afstand in Microsoft Azure]
* [Documentatie bij Django]
* [SQL Database]

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure-Portal]: https://portal.azure.com
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentatie bij Django]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
