---
title: aaaCreating web-apps met Django in Azure
description: Een zelfstudie waarin u kennis kunt toorunning een Python-web-app in Azure App Service Web Apps.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a>Web-apps maken met Django in Azure
Deze zelfstudie wordt beschreven hoe tooget gestart Python uitvoert in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken. Als uw app groeit, kunt u schakelen toopaid die als host fungeert, en u ook met alle integreren kunt Hallo andere Azure-services.

U maakt een toepassing met Hallo Django-webframework (Zie andere versies van deze zelfstudie voor [Flask](web-sites-python-create-deploy-flask-app.md) en [Bottle](web-sites-python-create-deploy-bottle-app.md)). U wordt Hallo web-app maken vanuit Azure Marketplace hello, instellen van Git-implementatie en lokaal Hallo opslagplaats klonen. Vervolgens wordt Hallo toepassing lokaal uitvoeren, wijzigingen aanbrengen, doorvoeren en push ze tooAzure. zelfstudie ziet hoe Hallo toodo dit van Windows of Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="prerequisites"></a>Vereisten
* Windows, Mac of Linux
* Python 2.7 of 3.4
* setuptools, pip, virtualenv (alleen Python 2.7)
* Git
* [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Opmerking: dit is optioneel

**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.

### <a name="windows"></a>Windows
Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma. Hiermee installeert u Hallo 32-bits versie van Python, setuptools, pip, virtualenv, enzovoort (32-bits Python is wat wordt geïnstalleerd op Hallo Azure-hostmachines). U kunt Python ook downloaden via [python.org].

Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden. Als u Visual Studio gebruikt, kunt u Hallo geïntegreerde Git-ondersteuning.

Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren. Dit is optioneel, maar als u [Visual Studio], met inbegrip van Hallo gratis Visual Studio Community 2013 of Visual Studio Express 2013 voor Web en Hiermee krijgt u een uitstekende Python IDE.

### <a name="maclinux"></a>Mac/Linux
Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.

## <a name="web-app-creation-on-portal"></a>Web-apps maken via de portal
Hallo eerste stap bij het maken van uw app is toocreate Hallo web-app via Hallo [Azure Portal](https://portal.azure.com).

1. Meld u aan bij hello Azure-Portal en klikt u op Hallo **nieuw** knop in de linkeronderhoek Hallo.
2. Typ in Hallo zoekvak 'python'.
3. Selecteer in de zoekresultaten hello, **Django** (gepubliceerd door PTVS), klikt u vervolgens op **maken**.
4. Hallo nieuwe Django-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor configureren. Klik vervolgens op **Maken**.
5. Configureer Git-publicatie voor uw nieuwe web-app met behulp Hallo-instructies in [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).

## <a name="application-overview"></a>Toepassingsoverzicht
### <a name="git-repository-contents"></a>Inhoud van Git-opslagplaats
Hier volgt een overzicht van Hallo bestanden vindt u in Hallo eerste Git-opslagplaats, die we in de volgende sectie Hallo gaat klonen.

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

Belangrijkste bronnen voor Hallo-toepassing. Bestaat uit 3 pagina's (index, over, contact) met een modelindeling. Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.

    \manage.py

Lokaal beheer en ondersteuning voor de ontwikkelaarsserver. Deze toorun Hallo-toepassing lokaal gebruiken, synchroniseren Hallo-database, enzovoort.

    \db.sqlite3

Standaarddatabase. Bevat de benodigde tabellen voor Hallo toepassing toorun hello, maar bevat geen gebruikers (Synchroniseer Hallo database toocreate een gebruiker).

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

Projectbestanden voor gebruik met [Python Tools for Visual Studio].

    \ptvs_virtualenv_proxy.py

IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.

    \requirements.txt

Externe pakketten nodig voor deze toepassing. Hallo-implementatiescript wordt een pip installatie hello-pakketten die worden vermeld in dit bestand.

    \web.2.7.config
    \web.3.4.config

IIS-configuratiebestanden. Hallo-implementatiescript gebruikt Hallo juiste web.x.y.config en kopieert deze als web.config.

### <a name="optional-files---customizing-deployment"></a>Optionele bestanden - implementatie aanpassen
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Optionele bestanden - Python-runtime
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Aanvullende bestanden op server
Bepaalde bestanden bestaan op Hallo server maar toohello git-opslagplaats niet worden toegevoegd. Deze worden gemaakt door het implementatiescript Hallo.

    \web.config

IIS-configuratiebestand. Gemaakt op basis van web.x.y.config voor elke implementatie.

    \env\

Virtuele Python-omgeving. Gemaakt tijdens de implementatie als een compatibele virtuele omgeving op Hallo web-app nog niet bestaat. Pakketten die worden vermeld in requirements.txt worden via pip geïnstalleerd, maar pip slaat de installatie over als hello-pakketten zijn al geïnstalleerd.

Hallo naast 3 gedeelten wordt beschreven hoe tooproceed Hello web-app-ontwikkeling onder 3 verschillende omgevingen:

* Windows, met Python Tools for Visual Studio
* Windows, met opdrachtregel
* Mac/Linux, met opdrachtregel

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Ontwikkeling van web-apps - Windows - Python Tools for Visual Studio
### <a name="clone-hello-repository"></a>Hallo-opslagplaats klonen
Kloon eerst Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal. Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).

Open Hallo oplossingsbestand (.sln) die is opgenomen in de hoofdmap Hallo van Hallo-opslagplaats.

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a>Een virtuele omgeving maken
U maakt nu een virtuele omgeving voor lokale ontwikkeling. Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.

* Zorg ervoor dat het Hallo-naam van het Hallo-omgeving is `env`.
* Selecteer de basisinterpreter Hallo. Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of op Hallo **toepassingsinstellingen** blade van uw web-app in Azure Portal Hallo).
* Zorg ervoor dat de optie hello-pakketten toodownload en installatie is ingeschakeld.

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

Klik op **Create**. Dit wordt Hallo virtuele omgeving maken, en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.

### <a name="create-a-superuser"></a>Een beheerder maken
Hallo-database die deel uitmaakt van de toepassing hello heeft geen beheerder opgegeven. In de volgorde toouse Hallo aanmelden functionaliteit van de toepassing hello of Hallo Django-beheerinterface (als u tooenable besluit het), moet u een beheerder toocreate.

Voer dit uit vanaf Hallo opdrachtregel van de projectmap:

    env\scripts\python manage.py createsuperuser

Ga als volgt Hallo prompts tooset Hallo-gebruikersnaam, wachtwoord, enzovoort.

### <a name="run-using-development-server"></a>Uitvoeren met behulp van de ontwikkelaarsserver
Druk op F5 toostart foutopsporing en uw webbrowser wordt automatisch geopend toohello pagina die lokaal wordt uitgevoerd.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

U kunt onderbrekingspunten instellen in het Hallo-bronnen, gebruik Hallo vensters, enzovoort. Zie Hallo [Python-Tools voor Visual Studio-documentatie] Hallo voor meer informatie over de verschillende functies.

### <a name="make-changes"></a>Wijzigingen aanbrengen
U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.

Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a>Meer pakketten installeren
Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.

U kunt extra pakketten installeren via PIP. tooinstall een pakket met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **Install Python Package**.

Bijvoorbeeld: tooinstall hello Azure SDK voor Python, die u hebt u toegang tooAzure storage, servicebus en andere Azure-services, voer `azure`:

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

Met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **requirements.txt genereren** tooupdate requirements.txt.

Voer vervolgens Hallo wijzigingen toorequirements.txt toohello Git-opslagplaats.

### <a name="deploy-tooazure"></a>TooAzure implementeren
tootrigger een implementatie, klikt u op **Sync** of **Push**. Bij een synchronisatie vinden er push- en pullbewerkingen plaats.

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

Hallo eerste implementatie duurt enige tijd als deze, u een virtuele omgeving, pakketten worden geïnstalleerd, enzovoort maakt wordt.

Visual Studio weergeven niet Hallo voortgang van Hallo implementatie. Als u tooreview Hallo uitvoer dat wilt, raadpleegt u Hallo sectie op [probleemoplossing - implementatie](#troubleshooting-deployment).

Blader toohello Azure-URL tooview uw wijzigingen.

## <a name="web-app-development---windows---command-line"></a>Ontwikkeling van web-apps - Windows - opdrachtregel
### <a name="clone-hello-repository"></a>Hallo-opslagplaats klonen
Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe. Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Een virtuele omgeving maken
Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats). Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.

Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of Hallo blade toepassingsinstellingen van uw web-app in Azure Portal Hallo).

Voor Python 2.7:

    c:\python27\python.exe -m virtualenv env

Voor Python 3.4:

    c:\python34\python.exe -m venv env

Installeer alle externe pakketten die voor uw toepassing vereist zijn. U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a>Een beheerder maken
Hallo-database die deel uitmaakt van de toepassing hello heeft geen beheerder opgegeven. In de volgorde toouse Hallo aanmelden functionaliteit van de toepassing hello of Hallo Django-beheerinterface (als u tooenable besluit het), moet u een beheerder toocreate.

Voer dit uit vanaf Hallo opdrachtregel van de projectmap:

    env\scripts\python manage.py createsuperuser

Ga als volgt Hallo prompts tooset Hallo-gebruikersnaam, wachtwoord, enzovoort.

### <a name="run-using-development-server"></a>Uitvoeren met behulp van de ontwikkelaarsserver
U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:

    env\scripts\python manage.py runserver

Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

Open vervolgens de URL van web browser toothat.

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a>Wijzigingen aanbrengen
U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.

Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Meer pakketten installeren
Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.

U kunt extra pakketten installeren via PIP. Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:

    env\scripts\pip install azure

Zorg ervoor dat tooupdate requirements.txt:

    env\scripts\pip freeze > requirements.txt

Hallo wijzigingen doorvoeren:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>TooAzure implementeren
een implementatie tootrigger, push Hallo verandert tooAzure:

    git push azure master

Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.

Blader toohello Azure-URL tooview uw wijzigingen.

## <a name="web-app-development---maclinux---command-line"></a>Ontwikkeling van web-apps - Mac/Linux - opdrachtregel
### <a name="clone-hello-repository"></a>Hallo-opslagplaats klonen
Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe. Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a>Een virtuele omgeving maken
Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats). Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.

Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of Hallo blade toepassingsinstellingen van uw web-app in Azure Portal Hallo).

Voor Python 2.7:

    python -m virtualenv env

Voor Python 3.4:

    python -m venv env

of

    pyvenv env

Installeer alle externe pakketten die voor uw toepassing vereist zijn. U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a>Een beheerder maken
Hallo-database die deel uitmaakt van de toepassing hello heeft geen beheerder opgegeven. In de volgorde toouse Hallo aanmelden functionaliteit van de toepassing hello of Hallo Django-beheerinterface (als u tooenable besluit het), moet u een beheerder toocreate.

Voer dit uit vanaf Hallo opdrachtregel van de projectmap:

    env/bin/python manage.py createsuperuser

Ga als volgt Hallo prompts tooset Hallo-gebruikersnaam, wachtwoord, enzovoort.

### <a name="run-using-development-server"></a>Uitvoeren met behulp van de ontwikkelaarsserver
U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:

    env/bin/python manage.py runserver

Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

Open vervolgens de URL van web browser toothat.

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a>Wijzigingen aanbrengen
U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.

Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Meer pakketten installeren
Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.

U kunt extra pakketten installeren via PIP. Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:

    env/bin/pip install azure

Zorg ervoor dat tooupdate requirements.txt:

    env/bin/pip freeze > requirements.txt

Hallo wijzigingen doorvoeren:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a>TooAzure implementeren
een implementatie tootrigger, push Hallo verandert tooAzure:

    git push azure master

Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.

Blader toohello Azure-URL tooview uw wijzigingen.

## <a name="troubleshooting---package-installation"></a>Probleemoplossing - Installatie van pakketten
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Probleemoplossing - Virtuele omgeving
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a>Probleemoplossing - Statische bestanden
Django heeft Hallo concept van het verzamelen van statische bestanden. Dit duurt alle Hallo statische bestanden vanuit hun oorspronkelijke locatie en kopieert ze tooa één map. Voor deze toepassing, worden ze gekopieerd te`/static`.

Dit gebeurt omdat statische bestanden mogelijk afkomstig zijn van andere Django-apps. Bijvoorbeeld, bevinden Hallo statische bestanden van Hallo Django-beheerinterfaces zich in een Django-bibliotheeksubmap in Hallo virtuele omgeving. De statische bestanden die door deze toepassing worden gedefinieerd, bevinden zich in `/app/static`. Als u meer Django-apps gebruikt, staan er op meerdere plaatsen statische bestanden.

Wanneer de toepassing hello wordt uitgevoerd in de foutopsporingsmodus, fungeert Hallo toepassing hello statische bestanden vanuit hun oorspronkelijke locatie.

Wanneer Hallo toepassing wordt uitgevoerd in de releasemodus, Hallo toepassing biedt **niet** Hallo statische bestanden. Het is de verantwoordelijkheid Hallo Hallo web server tooserve Hallo bestanden. Voor deze toepassing fungeert IIS Hallo statische bestanden van `/static`.

Hallo verzamelen van statische bestanden gebeurt automatisch als onderdeel van Hallo-implementatiescript wissen eerder verzamelde bestanden. Dit betekent Hallo verzameling plaatsvindt bij elke implementatie, duurt het implementatieproces langer, maar Hiermee zorgt u ervoor dat de verouderde bestanden niet beschikbaar, dat voorkomt potentiële beveiligingsproblemen.

Als u wilt dat tooskip verzamelen van statische bestanden voor uw Django-toepassing:

    \.skipDjango

Vervolgens moet u toodo Hallo verzameling handmatig op uw lokale machine:

    env\scripts\python manage.py collectstatic

Verwijder vervolgens Hallo `\static` map uit `.gitignore` en toe te voegen toohello Git-opslagplaats.

## <a name="troubleshooting---settings"></a>Probleemoplossing - Instellingen
Diverse instellingen voor de toepassing hello kunnen worden gewijzigd in `DjangoWebProject/settings.py`.

Voor het gemak van ontwikkelaars is de foutopsporingsmodus ingeschakeld. Een handige bijkomstigheid van die is, moet u kunnen toosee afbeeldingen en andere statische inhoud bij lokale uitvoering zonder toocollect statische bestanden.

de foutopsporingsmodus toodisable:

    DEBUG = False

Wanneer foutopsporing is uitgeschakeld, de waarde voor Hallo `ALLOWED_HOSTS` behoeften toobe tooinclude hello Azure hostnaam bijgewerkt. Bijvoorbeeld:

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

of tooenable eventuele:

    ALLOWED_HOSTS = (
        '*',
    )

In de praktijk kunt u toodo iets meer complexe toodeal schakelen tussen de foutopsporing en releasemodus, en ophalen van het Hallo-hostnaam.

U kunt omgevingsvariabelen instellen via hello Azure-portal **configureren** pagina in Hallo **appinstellingen** sectie.  Dit kan handig zijn voor het instellen van waarden die u niet kunt tooappear in Hallo bronnen (verbindingsreeksen, wachtwoorden, enzovoort) of dat u wilt dat tooset anders tussen Azure en uw lokale computer zijn. In `settings.py`, u kunt een query Hallo omgevingsvariabelen met `os.getenv`.

## <a name="using-a-database"></a>Een database gebruiken
Hallo-database die is opgenomen in de toepassing hello is een sqlite-database. Dit is een handige en nuttige standaard database toouse voor ontwikkeling, aangezien er bijna geen instellingen vereist. Hallo-database is opgeslagen in bestand DB.sqlite3 in de projectmap Hallo Hallo.

Azure biedt databaseservices die eenvoudig toouse vanuit een Django-toepassing. Zelfstudies voor het gebruik van [SQL-Database] en [MySQL] weergeven vanuit een Django-toepassing hello stappen nodig toocreate Hallo database-service, Hallo database instellingen wijzigen in `DjangoWebProject/settings.py`, en Hallo bibliotheken tooinstall vereist.

Natuurlijk als u liever uw eigen databaseservers toomanage, kunt u doen met behulp van Windows of Linux virtuele machines die worden uitgevoerd op Azure.

## <a name="django-admin-interface"></a>Django-beheerinterface
Wanneer u begint met het bouwen van modellen, moet u toopopulate Hallo database met gegevens. Een eenvoudige manier toodo toevoegen en interactief bewerken van inhoud is toouse hello Django-beheerinterface.

Hallo-code voor het Hallo-beheerinterface uitgecommentarieerd in de toepassingsbronnen hello, maar het duidelijk gemarkeerd, kunt u eenvoudig inschakelen (zoek naar 'admin').

Nadat deze ingeschakeld, Hallo database synchroniseren, Hallo toepassing uitvoeren en te navigeren`/admin`.

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen toolearn meer informatie over Django en Python-Tools voor Visual Studio:

* [Documentatie bij Django]
* [Python-Tools voor Visual Studio-documentatie]

Voor informatie over het gebruik van SQL Database en MySQL:

* [Django en MySQL in Azure met Python Tools for Visual Studio]
* [Django en SQL Database in Azure met Python Tools for Visual Studio]

Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Django en MySQL in Azure met Python Tools for Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django en SQL Database in Azure met Python Tools for Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL-Database]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[Azure SDK voor Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK voor Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git voor Windows]: http://msysgit.github.io/
[GitHub voor Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Python-Tools voor Visual Studio-documentatie]: http://aka.ms/ptvsdocs
[Documentatie bij Django]: https://www.djangoproject.com/
