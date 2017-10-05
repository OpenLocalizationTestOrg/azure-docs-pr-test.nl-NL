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
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="86382-103">Web-apps maken met Flask in Azure</span><span class="sxs-lookup"><span data-stu-id="86382-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="86382-104">Deze zelfstudie wordt beschreven hoe u Python uitvoert aan de slag [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="86382-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="86382-105">Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86382-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="86382-106">Naarmate uw app groeit, kunt u overstappen op betaalde hosting én profiteren van integratie met alle overige Azure-services.</span><span class="sxs-lookup"><span data-stu-id="86382-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="86382-107">U maakt een toepassing met de Flask-webframework (Zie andere versies van deze zelfstudie voor [Django](web-sites-python-create-deploy-django-app.md) en [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="86382-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="86382-108">U wordt de website van de Azure-galerie maken, instellen van Git-implementatie en kloont de opslagplaats lokaal.</span><span class="sxs-lookup"><span data-stu-id="86382-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="86382-109">Vervolgens voert u de toepassing lokaal uit, brengt u wijzigingen aan, voert u deze door en pusht u ze naar Azure.</span><span class="sxs-lookup"><span data-stu-id="86382-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="86382-110">In de zelfstudie ziet u hoe u dit doet in Windows of Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="86382-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="86382-111">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="86382-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="86382-112">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="86382-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="86382-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="86382-113">Prerequisites</span></span>
* <span data-ttu-id="86382-114">Windows, Mac of Linux</span><span class="sxs-lookup"><span data-stu-id="86382-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="86382-115">Python 2.7 of 3.4</span><span class="sxs-lookup"><span data-stu-id="86382-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="86382-116">setuptools, pip, virtualenv (alleen Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="86382-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="86382-117">Git</span><span class="sxs-lookup"><span data-stu-id="86382-117">Git</span></span>
* <span data-ttu-id="86382-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Opmerking: dit is optioneel</span><span class="sxs-lookup"><span data-stu-id="86382-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="86382-119">**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.</span><span class="sxs-lookup"><span data-stu-id="86382-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="86382-120">Windows</span><span class="sxs-lookup"><span data-stu-id="86382-120">Windows</span></span>
<span data-ttu-id="86382-121">Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="86382-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="86382-122">Hiermee installeert u de 32-bits versie van Python, setuptools, PIP, virtualenv, enzovoort (32-bits Python wordt geïnstalleerd op de Azure-hostmachines).</span><span class="sxs-lookup"><span data-stu-id="86382-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="86382-123">U kunt Python ook downloaden via [python.org].</span><span class="sxs-lookup"><span data-stu-id="86382-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="86382-124">Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.</span><span class="sxs-lookup"><span data-stu-id="86382-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="86382-125">Als u Visual Studio gebruikt, kunt u de geïntegreerde Git-ondersteuning gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86382-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="86382-126">Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.</span><span class="sxs-lookup"><span data-stu-id="86382-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="86382-127">Dit is optioneel, maar als u [Visual Studio] hebt, met inbegrip van de gratis Visual Studio Community 2013 of Visual Studio Express 2013 for Web, beschikt u over een uitstekende Python IDE.</span><span class="sxs-lookup"><span data-stu-id="86382-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="86382-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="86382-128">Mac/Linux</span></span>
<span data-ttu-id="86382-129">Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.</span><span class="sxs-lookup"><span data-stu-id="86382-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="86382-130">Web-app maken in de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="86382-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="86382-131">De eerste stap voor het maken van uw app bestaat uit het maken van een web-app via de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86382-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="86382-132">Meld u aan bij de Azure Portal en klik in de linkerbenedenhoek op de knop **NIEUW**.</span><span class="sxs-lookup"><span data-stu-id="86382-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="86382-133">Klik op **Web en mobiel**.</span><span class="sxs-lookup"><span data-stu-id="86382-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="86382-134">Voer in het zoekvak 'python' in.</span><span class="sxs-lookup"><span data-stu-id="86382-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="86382-135">Selecteer in de lijst met zoekresultaten **Flask**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="86382-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="86382-136">Configureer de nieuwe Flask-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor.</span><span class="sxs-lookup"><span data-stu-id="86382-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="86382-137">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="86382-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="86382-138">Configureer Git-publicatie voor uw nieuwe web-app door de instructies te volgen in [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="86382-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="86382-139">Toepassingsoverzicht</span><span class="sxs-lookup"><span data-stu-id="86382-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="86382-140">Inhoud van Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="86382-140">Git repository contents</span></span>
<span data-ttu-id="86382-141">Hier volgt een overzicht van de bestanden in de eerste Git-opslagplaats. Deze gaat u in het volgende gedeelte klonen.</span><span class="sxs-lookup"><span data-stu-id="86382-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="86382-142">Belangrijkste bronnen voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="86382-142">Main sources for the application.</span></span>  <span data-ttu-id="86382-143">Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.</span><span class="sxs-lookup"><span data-stu-id="86382-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="86382-144">Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.</span><span class="sxs-lookup"><span data-stu-id="86382-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="86382-145">Ondersteuning voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="86382-145">Local development server support.</span></span> <span data-ttu-id="86382-146">Gebruiken deze om de toepassing lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="86382-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="86382-147">Projectbestanden voor gebruik met [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="86382-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="86382-148">IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="86382-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="86382-149">Externe pakketten nodig voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="86382-149">External packages needed by this application.</span></span> <span data-ttu-id="86382-150">Door het implementatiescript wordt een PIP-installatie uitgevoerd voor de pakketten die in het bestand worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="86382-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="86382-151">IIS-configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="86382-151">IIS configuration files.</span></span>  <span data-ttu-id="86382-152">Het implementatiescript maakt gebruik van de juiste web.x.y.config en kopieert deze als web.config.</span><span class="sxs-lookup"><span data-stu-id="86382-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="86382-153">Optionele bestanden - implementatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="86382-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="86382-154">Optionele bestanden - Python-runtime</span><span class="sxs-lookup"><span data-stu-id="86382-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="86382-155">Aanvullende bestanden op server</span><span class="sxs-lookup"><span data-stu-id="86382-155">Additional files on server</span></span>
<span data-ttu-id="86382-156">Bepaalde bestanden bestaan wel op de server, maar worden niet toegevoegd aan de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="86382-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="86382-157">Deze worden gemaakt door het script voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="86382-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="86382-158">IIS-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="86382-158">IIS configuration file.</span></span>  <span data-ttu-id="86382-159">Gemaakt op basis van web.x.y.config voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="86382-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="86382-160">Virtuele Python-omgeving.</span><span class="sxs-lookup"><span data-stu-id="86382-160">Python virtual environment.</span></span>  <span data-ttu-id="86382-161">Gemaakt tijdens de implementatie als een compatibele virtuele omgeving niet al op de app bestaat.</span><span class="sxs-lookup"><span data-stu-id="86382-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="86382-162">De pakketten die worden vermeld in requirements.txt, worden via PIP geïnstalleerd, maar PIP slaat de installatie over als de pakketten al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="86382-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="86382-163">In de volgende drie gedeelten wordt beschreven hoe u verdergaat met de ontwikkeling van de web-app in drie verschillende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="86382-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="86382-164">Windows, met Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86382-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="86382-165">Windows, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="86382-165">Windows, with command line</span></span>
* <span data-ttu-id="86382-166">Mac/Linux, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="86382-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="86382-167">Ontwikkeling van web-apps - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86382-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="86382-168">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="86382-168">Clone the repository</span></span>
<span data-ttu-id="86382-169">Kloon eerst de opslagplaats via de URL die in de Azure Portal is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="86382-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="86382-170">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="86382-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="86382-171">Open het oplossingsbestand (.sln) dat is opgenomen in de hoofdmap van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="86382-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="86382-172">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="86382-172">Create virtual environment</span></span>
<span data-ttu-id="86382-173">U maakt nu een virtuele omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="86382-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="86382-174">Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.</span><span class="sxs-lookup"><span data-stu-id="86382-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="86382-175">Zorg ervoor dat de naam van de omgeving `env` is.</span><span class="sxs-lookup"><span data-stu-id="86382-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="86382-176">Selecteer de basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="86382-176">Select the base interpreter.</span></span>  <span data-ttu-id="86382-177">Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="86382-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="86382-178">Zorg ervoor dat de optie voor het downloaden en installeren van pakketten is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="86382-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="86382-179">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="86382-179">Click **Create**.</span></span>  <span data-ttu-id="86382-180">Hiermee maakt u de virtuele omgeving en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="86382-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="86382-181">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="86382-181">Run using development server</span></span>
<span data-ttu-id="86382-182">Druk op F5 om de foutopsporing te starten. Uw webbrowser wordt automatisch geopend op de pagina die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="86382-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="86382-183">U kunt onderbrekingspunten instellen in de bronnen, de vensters Controle gebruiken, enzovoort.  Zie de [Documentatie bij Python Tools for Visual Studio] voor meer informatie over de verschillende functies.</span><span class="sxs-lookup"><span data-stu-id="86382-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="86382-184">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="86382-184">Make changes</span></span>
<span data-ttu-id="86382-185">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="86382-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="86382-186">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="86382-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="86382-187">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="86382-187">Install more packages</span></span>
<span data-ttu-id="86382-188">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.</span><span class="sxs-lookup"><span data-stu-id="86382-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="86382-189">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="86382-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="86382-190">Als u een pakket wilt installeren, klikt u met de rechtermuisknop op de virtuele omgeving en selecteert u **Python-pakket installeren**.</span><span class="sxs-lookup"><span data-stu-id="86382-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="86382-191">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u `azure`:</span><span class="sxs-lookup"><span data-stu-id="86382-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="86382-192">Klik met de rechtermuisknop op de virtuele omgeving en selecteer **requirements.txt genereren** om requirements.txt bij te werken.</span><span class="sxs-lookup"><span data-stu-id="86382-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="86382-193">Voer vervolgens de wijzigingen aan requirements.txt door in de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="86382-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="86382-194">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="86382-194">Deploy to Azure</span></span>
<span data-ttu-id="86382-195">Als u een implementatie wilt activeren, klikt u op **Synchroniseren** of **Pushen**.</span><span class="sxs-lookup"><span data-stu-id="86382-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="86382-196">Bij een synchronisatie vinden er push- en pullbewerkingen plaats.</span><span class="sxs-lookup"><span data-stu-id="86382-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="86382-197">De eerste implementatie duurt langer dan normaal omdat er een virtuele omgeving wordt gemaakt, er pakketten worden geïnstalleerd en meer.</span><span class="sxs-lookup"><span data-stu-id="86382-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="86382-198">De voortgang van de implementatie wordt niet weergegeven in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86382-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="86382-199">Als u de uitvoer wilt controleren, raadpleegt u het gedeelte [Probleemoplossing - Implementatie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="86382-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="86382-200">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="86382-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="86382-201">Ontwikkeling van web-apps - Windows - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="86382-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="86382-202">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="86382-202">Clone the repository</span></span>
<span data-ttu-id="86382-203">Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe.</span><span class="sxs-lookup"><span data-stu-id="86382-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="86382-204">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="86382-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="86382-205">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="86382-205">Create virtual environment</span></span>
<span data-ttu-id="86382-206">U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="86382-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="86382-207">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.</span><span class="sxs-lookup"><span data-stu-id="86382-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="86382-208">Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="86382-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="86382-209">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="86382-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="86382-210">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="86382-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="86382-211">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="86382-211">Install any external packages required by your application.</span></span> <span data-ttu-id="86382-212">U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="86382-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="86382-213">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="86382-213">Run using development server</span></span>
<span data-ttu-id="86382-214">U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="86382-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="86382-215">In de console worden de URL en de poort vermeld waarnaar de server luistert:</span><span class="sxs-lookup"><span data-stu-id="86382-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="86382-216">Open de betreffende URL in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="86382-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="86382-217">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="86382-217">Make changes</span></span>
<span data-ttu-id="86382-218">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="86382-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="86382-219">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="86382-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="86382-220">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="86382-220">Install more packages</span></span>
<span data-ttu-id="86382-221">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.</span><span class="sxs-lookup"><span data-stu-id="86382-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="86382-222">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="86382-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="86382-223">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:</span><span class="sxs-lookup"><span data-stu-id="86382-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="86382-224">Zorg ervoor dat u requirements.txt bijwerkt:</span><span class="sxs-lookup"><span data-stu-id="86382-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="86382-225">Voer de wijzigingen door:</span><span class="sxs-lookup"><span data-stu-id="86382-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="86382-226">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="86382-226">Deploy to Azure</span></span>
<span data-ttu-id="86382-227">Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:</span><span class="sxs-lookup"><span data-stu-id="86382-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="86382-228">U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.</span><span class="sxs-lookup"><span data-stu-id="86382-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="86382-229">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="86382-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="86382-230">Ontwikkeling van web-apps - Mac/Linux - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="86382-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="86382-231">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="86382-231">Clone the repository</span></span>
<span data-ttu-id="86382-232">Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe.</span><span class="sxs-lookup"><span data-stu-id="86382-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="86382-233">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="86382-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="86382-234">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="86382-234">Create virtual environment</span></span>
<span data-ttu-id="86382-235">U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="86382-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="86382-236">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.</span><span class="sxs-lookup"><span data-stu-id="86382-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="86382-237">Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="86382-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="86382-238">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="86382-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="86382-239">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="86382-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="86382-240">of pyvenv env</span><span class="sxs-lookup"><span data-stu-id="86382-240">or pyvenv env</span></span>

<span data-ttu-id="86382-241">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="86382-241">Install any external packages required by your application.</span></span> <span data-ttu-id="86382-242">U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="86382-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="86382-243">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="86382-243">Run using development server</span></span>
<span data-ttu-id="86382-244">U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="86382-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="86382-245">In de console worden de URL en de poort vermeld waarnaar de server luistert:</span><span class="sxs-lookup"><span data-stu-id="86382-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="86382-246">Open de betreffende URL in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="86382-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="86382-247">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="86382-247">Make changes</span></span>
<span data-ttu-id="86382-248">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="86382-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="86382-249">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="86382-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="86382-250">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="86382-250">Install more packages</span></span>
<span data-ttu-id="86382-251">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.</span><span class="sxs-lookup"><span data-stu-id="86382-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="86382-252">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="86382-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="86382-253">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:</span><span class="sxs-lookup"><span data-stu-id="86382-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="86382-254">Zorg ervoor dat u requirements.txt bijwerkt:</span><span class="sxs-lookup"><span data-stu-id="86382-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="86382-255">Voer de wijzigingen door:</span><span class="sxs-lookup"><span data-stu-id="86382-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="86382-256">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="86382-256">Deploy to Azure</span></span>
<span data-ttu-id="86382-257">Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:</span><span class="sxs-lookup"><span data-stu-id="86382-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="86382-258">U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.</span><span class="sxs-lookup"><span data-stu-id="86382-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="86382-259">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="86382-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="86382-260">Probleemoplossing - Installatie van pakketten</span><span class="sxs-lookup"><span data-stu-id="86382-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="86382-261">Probleemoplossing - Virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="86382-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="86382-262">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86382-262">Next Steps</span></span>
<span data-ttu-id="86382-263">Volg deze koppelingen voor meer informatie over Flask en Python-Tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="86382-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="86382-264">[Flask-documentatie]</span><span class="sxs-lookup"><span data-stu-id="86382-264">[Flask Documentation]</span></span>
* <span data-ttu-id="86382-265">[Documentatie bij Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="86382-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="86382-266">Voor informatie over het gebruik van Azure Table Storage en MongoDB:</span><span class="sxs-lookup"><span data-stu-id="86382-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="86382-267">[Flask- en MongoDB in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="86382-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="86382-268">[Flask- en Azure Table Storage in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="86382-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="86382-269">Zie voor meer informatie, ook de [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="86382-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="86382-270">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="86382-270">What's changed</span></span>
* <span data-ttu-id="86382-271">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="86382-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="86382-272">[Flask- en MongoDB in Azure met Python-Tools voor Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="86382-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="86382-273">[Flask- en Azure Table Storage in Azure met Python-Tools voor Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="86382-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="86382-274">[Azure SDK voor Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="86382-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="86382-275">[Azure SDK voor Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="86382-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="86382-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="86382-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="86382-277">[Git voor Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="86382-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="86382-278">[GitHub voor Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="86382-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="86382-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="86382-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="86382-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="86382-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="86382-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="86382-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="86382-282">[Documentatie bij Python Tools for Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="86382-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="86382-283">[Flask-documentatie]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="86382-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

