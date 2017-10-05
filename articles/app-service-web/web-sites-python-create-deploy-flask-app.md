---
title: Web-apps maken met Flask in Azure
description: Een zelfstudie waarin u kennis maakt voor het uitvoeren van een Python-web-app in Azure.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a>Web-apps maken met Flask in Azure
Deze zelfstudie wordt beschreven hoe u Python uitvoert aan de slag [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).  Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.  Naarmate uw app groeit, kunt u overstappen op betaalde hosting én profiteren van integratie met alle overige Azure-services.

U maakt een toepassing met de Flask-webframework (Zie andere versies van deze zelfstudie voor [Django](web-sites-python-create-deploy-django-app.md) en [Bottle](web-sites-python-create-deploy-bottle-app.md)).  U wordt de website van de Azure-galerie maken, instellen van Git-implementatie en kloont de opslagplaats lokaal.  Vervolgens voert u de toepassing lokaal uit, brengt u wijzigingen aan, voert u deze door en pusht u ze naar Azure.  In de zelfstudie ziet u hoe u dit doet in Windows of Mac/Linux.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
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
Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.  Hiermee installeert u de 32-bits versie van Python, setuptools, PIP, virtualenv, enzovoort (32-bits Python wordt geïnstalleerd op de Azure-hostmachines).  U kunt Python ook downloaden via [python.org].

Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.  Als u Visual Studio gebruikt, kunt u de geïntegreerde Git-ondersteuning gebruiken.

Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.  Dit is optioneel, maar als u [Visual Studio] hebt, met inbegrip van de gratis Visual Studio Community 2013 of Visual Studio Express 2013 for Web, beschikt u over een uitstekende Python IDE.

### <a name="maclinux"></a>Mac/Linux
Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.

## <a name="web-app-create-on-the-azure-portal"></a>Web-app maken in de Azure Portal
De eerste stap voor het maken van uw app bestaat uit het maken van een web-app via de [Azure Portal](https://portal.azure.com). 

1. Meld u aan bij de Azure Portal en klik in de linkerbenedenhoek op de knop **NIEUW**. 
2. Klik op **Web en mobiel**.
3. Voer in het zoekvak 'python' in.
4. Selecteer in de lijst met zoekresultaten **Flask**, klikt u vervolgens op **maken**.
5. Configureer de nieuwe Flask-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor. Klik vervolgens op **Maken**.
6. Configureer Git-publicatie voor uw nieuwe web-app door de instructies te volgen in [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service).

## <a name="application-overview"></a>Toepassingsoverzicht
### <a name="git-repository-contents"></a>Inhoud van Git-opslagplaats
Hier volgt een overzicht van de bestanden in de eerste Git-opslagplaats. Deze gaat u in het volgende gedeelte klonen.

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

Belangrijkste bronnen voor de toepassing.  Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.  Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.

    \runserver.py

Ondersteuning voor lokale ontwikkeling. Gebruiken deze om de toepassing lokaal uitvoeren.

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

Projectbestanden voor gebruik met [Python Tools for Visual Studio].

    \ptvs_virtualenv_proxy.py

IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.

    \requirements.txt

Externe pakketten nodig voor deze toepassing. Door het implementatiescript wordt een PIP-installatie uitgevoerd voor de pakketten die in het bestand worden vermeld.

    \web.2.7.config
    \web.3.4.config

IIS-configuratiebestanden.  Het implementatiescript maakt gebruik van de juiste web.x.y.config en kopieert deze als web.config.

### <a name="optional-files---customizing-deployment"></a>Optionele bestanden - implementatie aanpassen
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a>Optionele bestanden - Python-runtime
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a>Aanvullende bestanden op server
Bepaalde bestanden bestaan wel op de server, maar worden niet toegevoegd aan de Git-opslagplaats.  Deze worden gemaakt door het script voor implementatie.

    \web.config

IIS-configuratiebestand.  Gemaakt op basis van web.x.y.config voor elke implementatie.

    \env\

Virtuele Python-omgeving.  Gemaakt tijdens de implementatie als een compatibele virtuele omgeving niet al op de app bestaat.  De pakketten die worden vermeld in requirements.txt, worden via PIP geïnstalleerd, maar PIP slaat de installatie over als de pakketten al zijn geïnstalleerd.

In de volgende drie gedeelten wordt beschreven hoe u verdergaat met de ontwikkeling van de web-app in drie verschillende omgevingen:

* Windows, met Python Tools for Visual Studio
* Windows, met opdrachtregel
* Mac/Linux, met opdrachtregel

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a>Ontwikkeling van web-apps - Windows - Python Tools for Visual Studio
### <a name="clone-the-repository"></a>De opslagplaats klonen
Kloon eerst de opslagplaats via de URL die in de Azure Portal is opgegeven. Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.

Open het oplossingsbestand (.sln) dat is opgenomen in de hoofdmap van de opslagplaats.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a>Een virtuele omgeving maken
U maakt nu een virtuele omgeving voor lokale ontwikkeling.  Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.

* Zorg ervoor dat de naam van de omgeving `env` is.
* Selecteer de basisinterpreter.  Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).
* Zorg ervoor dat de optie voor het downloaden en installeren van pakketten is ingeschakeld.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

Klik op **Create**.  Hiermee maakt u de virtuele omgeving en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.

### <a name="run-using-development-server"></a>Uitvoeren met behulp van de ontwikkelaarsserver
Druk op F5 om de foutopsporing te starten. Uw webbrowser wordt automatisch geopend op de pagina die lokaal wordt uitgevoerd.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

U kunt onderbrekingspunten instellen in de bronnen, de vensters Controle gebruiken, enzovoort.  Zie de [Documentatie bij Python Tools for Visual Studio] voor meer informatie over de verschillende functies.

### <a name="make-changes"></a>Wijzigingen aanbrengen
U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.

Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a>Meer pakketten installeren
Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.

U kunt extra pakketten installeren via PIP.  Als u een pakket wilt installeren, klikt u met de rechtermuisknop op de virtuele omgeving en selecteert u **Python-pakket installeren**.

Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u `azure`:

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

Klik met de rechtermuisknop op de virtuele omgeving en selecteer **requirements.txt genereren** om requirements.txt bij te werken.

Voer vervolgens de wijzigingen aan requirements.txt door in de Git-opslagplaats.

### <a name="deploy-to-azure"></a>Implementeren in Azure
Als u een implementatie wilt activeren, klikt u op **Synchroniseren** of **Pushen**.  Bij een synchronisatie vinden er push- en pullbewerkingen plaats.

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

De eerste implementatie duurt langer dan normaal omdat er een virtuele omgeving wordt gemaakt, er pakketten worden geïnstalleerd en meer.

De voortgang van de implementatie wordt niet weergegeven in Visual Studio.  Als u de uitvoer wilt controleren, raadpleegt u het gedeelte [Probleemoplossing - Implementatie](#troubleshooting-deployment).

Blader naar de Azure-URL om uw wijzigingen te bekijken.

## <a name="web-app-development---windows---command-line"></a>Ontwikkeling van web-apps - Windows - opdrachtregel
### <a name="clone-the-repository"></a>De opslagplaats klonen
Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe. Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Een virtuele omgeving maken
U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).  Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.

Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).

Voor Python 2.7:

    c:\python27\python.exe -m virtualenv env

Voor Python 3.4:

    c:\python34\python.exe -m venv env

Installeer alle externe pakketten die voor uw toepassing vereist zijn. U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a>Uitvoeren met behulp van de ontwikkelaarsserver
U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:

    env\scripts\python runserver.py

In de console worden de URL en de poort vermeld waarnaar de server luistert:

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

Open de betreffende URL in uw webbrowser.

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a>Wijzigingen aanbrengen
U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.

Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Meer pakketten installeren
Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.

U kunt extra pakketten installeren via PIP.  Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:

    env\scripts\pip install azure

Zorg ervoor dat u requirements.txt bijwerkt:

    env\scripts\pip freeze > requirements.txt

Voer de wijzigingen door:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a>Implementeren in Azure
Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:

    git push azure master

U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.

Blader naar de Azure-URL om uw wijzigingen te bekijken.

## <a name="web-app-development---maclinux---command-line"></a>Ontwikkeling van web-apps - Mac/Linux - opdrachtregel
### <a name="clone-the-repository"></a>De opslagplaats klonen
Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe. Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a>Een virtuele omgeving maken
U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).  Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.

Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).

Voor Python 2.7:

    python -m virtualenv env

Voor Python 3.4:

    python -m venv env
of pyvenv env

Installeer alle externe pakketten die voor uw toepassing vereist zijn. U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a>Uitvoeren met behulp van de ontwikkelaarsserver
U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:

    env/bin/python runserver.py

In de console worden de URL en de poort vermeld waarnaar de server luistert:

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

Open de betreffende URL in uw webbrowser.

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a>Wijzigingen aanbrengen
U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.

Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a>Meer pakketten installeren
Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.

U kunt extra pakketten installeren via PIP.  Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:

    env/bin/pip install azure

Zorg ervoor dat u requirements.txt bijwerkt:

    env/bin/pip freeze > requirements.txt

Voer de wijzigingen door:

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a>Implementeren in Azure
Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:

    git push azure master

U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.

Blader naar de Azure-URL om uw wijzigingen te bekijken.

## <a name="troubleshooting---package-installation"></a>Probleemoplossing - Installatie van pakketten
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Probleemoplossing - Virtuele omgeving
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Volgende stappen
Volg deze koppelingen voor meer informatie over Flask en Python-Tools voor Visual Studio: 

* [Flask-documentatie]
* [Documentatie bij Python Tools for Visual Studio]

Voor informatie over het gebruik van Azure Table Storage en MongoDB:

* [Flask- en MongoDB in Azure met Python-Tools voor Visual Studio]
* [Flask- en Azure Table Storage in Azure met Python-Tools voor Visual Studio]

Zie voor meer informatie, ook de [Python Developer Center](/develop/python/).

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

<!--Link references-->
[Flask- en MongoDB in Azure met Python-Tools voor Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask- en Azure Table Storage in Azure met Python-Tools voor Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

<!--External Link references-->
[Azure SDK voor Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Azure SDK voor Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git voor Windows]: http://msysgit.github.io/
[GitHub voor Windows]: https://windows.github.com/
[Python Tools for Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Documentatie bij Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Flask-documentatie]: http://flask.pocoo.org/ 

