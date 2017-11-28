---
title: aaaCreating web-apps met Flask in Azure
description: Een zelfstudie waarin u kennis kunt toorunning een Python-web-app in Azure.
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
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="ac5a8-103">Web-apps maken met Flask in Azure</span><span class="sxs-lookup"><span data-stu-id="ac5a8-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="ac5a8-104">Deze zelfstudie wordt beschreven hoe tooget gestart Python uitvoert [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="ac5a8-105">Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="ac5a8-106">Als uw app groeit, kunt u schakelen toopaid die als host fungeert, en u ook met alle integreren kunt Hallo andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="ac5a8-107">U maakt een toepassing met Hallo Flask-webframework (Zie andere versies van deze zelfstudie voor [Django](web-sites-python-create-deploy-django-app.md) en [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="ac5a8-108">U wordt Hallo website maken vanuit hello Azure-galerie, instellen van Git-implementatie en lokaal Hallo opslagplaats klonen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="ac5a8-109">Vervolgens wordt Hallo toepassing lokaal uitvoeren, wijzigingen aanbrengen, doorvoeren en push ze tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="ac5a8-110">zelfstudie ziet hoe Hallo toodo dit van Windows of Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="ac5a8-111">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ac5a8-112">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ac5a8-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ac5a8-113">Prerequisites</span></span>
* <span data-ttu-id="ac5a8-114">Windows, Mac of Linux</span><span class="sxs-lookup"><span data-stu-id="ac5a8-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="ac5a8-115">Python 2.7 of 3.4</span><span class="sxs-lookup"><span data-stu-id="ac5a8-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="ac5a8-116">setuptools, pip, virtualenv (alleen Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="ac5a8-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="ac5a8-117">Git</span><span class="sxs-lookup"><span data-stu-id="ac5a8-117">Git</span></span>
* <span data-ttu-id="ac5a8-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Opmerking: dit is optioneel</span><span class="sxs-lookup"><span data-stu-id="ac5a8-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="ac5a8-119">**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="ac5a8-120">Windows</span><span class="sxs-lookup"><span data-stu-id="ac5a8-120">Windows</span></span>
<span data-ttu-id="ac5a8-121">Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="ac5a8-122">Hiermee installeert u Hallo 32-bits versie van Python, setuptools, pip, virtualenv, enzovoort (32-bits Python is wat wordt geïnstalleerd op Hallo Azure-hostmachines).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="ac5a8-123">U kunt Python ook downloaden via [python.org].</span><span class="sxs-lookup"><span data-stu-id="ac5a8-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="ac5a8-124">Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="ac5a8-125">Als u Visual Studio gebruikt, kunt u Hallo geïntegreerde Git-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="ac5a8-126">Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="ac5a8-127">Dit is optioneel, maar als u [Visual Studio], met inbegrip van Hallo gratis Visual Studio Community 2013 of Visual Studio Express 2013 voor Web en Hiermee krijgt u een uitstekende Python IDE.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="ac5a8-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="ac5a8-128">Mac/Linux</span></span>
<span data-ttu-id="ac5a8-129">Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="ac5a8-130">Web-app op Hallo Azure Portal maken</span><span class="sxs-lookup"><span data-stu-id="ac5a8-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="ac5a8-131">Hallo eerste stap bij het maken van uw app is toocreate Hallo web-app via Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="ac5a8-132">Meld u aan bij hello Azure-Portal en klikt u op Hallo **nieuw** knop in de linkeronderhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="ac5a8-133">Klik op **Web en mobiel**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="ac5a8-134">Typ in Hallo zoekvak 'python'.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="ac5a8-135">Selecteer in de zoekresultaten hello, **Flask**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="ac5a8-136">Hallo nieuwe Flask-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor configureren.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="ac5a8-137">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="ac5a8-138">Configureer Git-publicatie voor uw nieuwe web-app met behulp Hallo-instructies in [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="ac5a8-139">Toepassingsoverzicht</span><span class="sxs-lookup"><span data-stu-id="ac5a8-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="ac5a8-140">Inhoud van Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="ac5a8-140">Git repository contents</span></span>
<span data-ttu-id="ac5a8-141">Hier volgt een overzicht van Hallo bestanden vindt u in Hallo eerste Git-opslagplaats, die we in de volgende sectie Hallo gaat klonen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="ac5a8-142">Belangrijkste bronnen voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-142">Main sources for hello application.</span></span>  <span data-ttu-id="ac5a8-143">Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="ac5a8-144">Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="ac5a8-145">Ondersteuning voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-145">Local development server support.</span></span> <span data-ttu-id="ac5a8-146">Gebruik deze toorun Hallo-toepassing lokaal uit.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="ac5a8-147">Projectbestanden voor gebruik met [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="ac5a8-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="ac5a8-148">IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="ac5a8-149">Externe pakketten nodig voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-149">External packages needed by this application.</span></span> <span data-ttu-id="ac5a8-150">Hallo-implementatiescript wordt een pip installatie hello-pakketten die worden vermeld in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="ac5a8-151">IIS-configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-151">IIS configuration files.</span></span>  <span data-ttu-id="ac5a8-152">Hallo-implementatiescript gebruikt Hallo juiste web.x.y.config en kopieert deze als web.config.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="ac5a8-153">Optionele bestanden - implementatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="ac5a8-154">Optionele bestanden - Python-runtime</span><span class="sxs-lookup"><span data-stu-id="ac5a8-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="ac5a8-155">Aanvullende bestanden op server</span><span class="sxs-lookup"><span data-stu-id="ac5a8-155">Additional files on server</span></span>
<span data-ttu-id="ac5a8-156">Bepaalde bestanden bestaan op Hallo server maar toohello git-opslagplaats niet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="ac5a8-157">Deze worden gemaakt door het implementatiescript Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="ac5a8-158">IIS-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-158">IIS configuration file.</span></span>  <span data-ttu-id="ac5a8-159">Gemaakt op basis van web.x.y.config voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="ac5a8-160">Virtuele Python-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-160">Python virtual environment.</span></span>  <span data-ttu-id="ac5a8-161">Gemaakt tijdens de implementatie als een compatibele virtuele omgeving op Hallo app nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="ac5a8-162">Pakketten die worden vermeld in requirements.txt worden via pip geïnstalleerd, maar pip slaat de installatie over als hello-pakketten zijn al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="ac5a8-163">Hallo naast 3 gedeelten wordt beschreven hoe tooproceed Hello web-app-ontwikkeling onder 3 verschillende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="ac5a8-164">Windows, met Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac5a8-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="ac5a8-165">Windows, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ac5a8-165">Windows, with command line</span></span>
* <span data-ttu-id="ac5a8-166">Mac/Linux, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ac5a8-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="ac5a8-167">Ontwikkeling van web-apps - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac5a8-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="ac5a8-168">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-168">Clone hello repository</span></span>
<span data-ttu-id="ac5a8-169">Kloon eerst Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="ac5a8-170">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="ac5a8-171">Open Hallo oplossingsbestand (.sln) die is opgenomen in de hoofdmap Hallo van Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="ac5a8-172">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="ac5a8-172">Create virtual environment</span></span>
<span data-ttu-id="ac5a8-173">U maakt nu een virtuele omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="ac5a8-174">Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="ac5a8-175">Zorg ervoor dat het Hallo-naam van het Hallo-omgeving is `env`.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="ac5a8-176">Selecteer de basisinterpreter Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-176">Select hello base interpreter.</span></span>  <span data-ttu-id="ac5a8-177">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of op Hallo **toepassingsinstellingen** blade van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="ac5a8-178">Zorg ervoor dat de optie hello-pakketten toodownload en installatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="ac5a8-179">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-179">Click **Create**.</span></span>  <span data-ttu-id="ac5a8-180">Dit wordt Hallo virtuele omgeving maken, en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="ac5a8-181">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="ac5a8-181">Run using development server</span></span>
<span data-ttu-id="ac5a8-182">Druk op F5 toostart foutopsporing en uw webbrowser wordt automatisch geopend toohello pagina die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="ac5a8-183">U kunt onderbrekingspunten instellen in het Hallo-bronnen, gebruik Hallo vensters, enzovoort.  Zie Hallo [Python-Tools voor Visual Studio-documentatie] Hallo voor meer informatie over de verschillende functies.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="ac5a8-184">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-184">Make changes</span></span>
<span data-ttu-id="ac5a8-185">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="ac5a8-186">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="ac5a8-187">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="ac5a8-187">Install more packages</span></span>
<span data-ttu-id="ac5a8-188">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="ac5a8-189">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="ac5a8-190">tooinstall een pakket met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="ac5a8-191">Bijvoorbeeld: tooinstall hello Azure SDK voor Python, die u hebt u toegang tooAzure storage, servicebus en andere Azure-services, voer `azure`:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="ac5a8-192">Met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **requirements.txt genereren** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="ac5a8-193">Voer vervolgens Hallo wijzigingen toorequirements.txt toohello Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="ac5a8-194">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="ac5a8-194">Deploy tooAzure</span></span>
<span data-ttu-id="ac5a8-195">tootrigger een implementatie, klikt u op **Sync** of **Push**.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="ac5a8-196">Bij een synchronisatie vinden er push- en pullbewerkingen plaats.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="ac5a8-197">Hallo eerste implementatie duurt enige tijd als deze, u een virtuele omgeving, pakketten worden geïnstalleerd, enzovoort maakt wordt.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="ac5a8-198">Visual Studio weergeven niet Hallo voortgang van Hallo implementatie.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="ac5a8-199">Als u tooreview Hallo uitvoer dat wilt, raadpleegt u Hallo sectie op [probleemoplossing - implementatie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="ac5a8-200">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="ac5a8-201">Ontwikkeling van web-apps - Windows - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ac5a8-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="ac5a8-202">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-202">Clone hello repository</span></span>
<span data-ttu-id="ac5a8-203">Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="ac5a8-204">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="ac5a8-205">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="ac5a8-205">Create virtual environment</span></span>
<span data-ttu-id="ac5a8-206">Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="ac5a8-207">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="ac5a8-208">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of op Hallo **toepassingsinstellingen** blade van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="ac5a8-209">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="ac5a8-210">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="ac5a8-211">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-211">Install any external packages required by your application.</span></span> <span data-ttu-id="ac5a8-212">U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="ac5a8-213">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="ac5a8-213">Run using development server</span></span>
<span data-ttu-id="ac5a8-214">U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="ac5a8-215">Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="ac5a8-216">Open vervolgens de URL van web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="ac5a8-217">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-217">Make changes</span></span>
<span data-ttu-id="ac5a8-218">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="ac5a8-219">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="ac5a8-220">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="ac5a8-220">Install more packages</span></span>
<span data-ttu-id="ac5a8-221">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="ac5a8-222">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="ac5a8-223">Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="ac5a8-224">Zorg ervoor dat tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="ac5a8-225">Hallo wijzigingen doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="ac5a8-226">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="ac5a8-226">Deploy tooAzure</span></span>
<span data-ttu-id="ac5a8-227">een implementatie tootrigger, push Hallo verandert tooAzure:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="ac5a8-228">Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="ac5a8-229">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="ac5a8-230">Ontwikkeling van web-apps - Mac/Linux - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ac5a8-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="ac5a8-231">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-231">Clone hello repository</span></span>
<span data-ttu-id="ac5a8-232">Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="ac5a8-233">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="ac5a8-234">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="ac5a8-234">Create virtual environment</span></span>
<span data-ttu-id="ac5a8-235">Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="ac5a8-236">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="ac5a8-237">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of op Hallo **toepassingsinstellingen** blade van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="ac5a8-238">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="ac5a8-239">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="ac5a8-240">of pyvenv env</span><span class="sxs-lookup"><span data-stu-id="ac5a8-240">or pyvenv env</span></span>

<span data-ttu-id="ac5a8-241">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-241">Install any external packages required by your application.</span></span> <span data-ttu-id="ac5a8-242">U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="ac5a8-243">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="ac5a8-243">Run using development server</span></span>
<span data-ttu-id="ac5a8-244">U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="ac5a8-245">Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="ac5a8-246">Open vervolgens de URL van web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="ac5a8-247">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-247">Make changes</span></span>
<span data-ttu-id="ac5a8-248">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="ac5a8-249">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="ac5a8-250">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="ac5a8-250">Install more packages</span></span>
<span data-ttu-id="ac5a8-251">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Flask.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="ac5a8-252">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="ac5a8-253">Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="ac5a8-254">Zorg ervoor dat tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="ac5a8-255">Hallo wijzigingen doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="ac5a8-256">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="ac5a8-256">Deploy tooAzure</span></span>
<span data-ttu-id="ac5a8-257">een implementatie tootrigger, push Hallo verandert tooAzure:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="ac5a8-258">Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="ac5a8-259">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="ac5a8-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="ac5a8-260">Probleemoplossing - Installatie van pakketten</span><span class="sxs-lookup"><span data-stu-id="ac5a8-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="ac5a8-261">Probleemoplossing - Virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="ac5a8-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="ac5a8-262">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ac5a8-262">Next Steps</span></span>
<span data-ttu-id="ac5a8-263">Volg deze koppelingen toolearn meer over Flask en Python-Tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="ac5a8-264">[Flask-documentatie]</span><span class="sxs-lookup"><span data-stu-id="ac5a8-264">[Flask Documentation]</span></span>
* <span data-ttu-id="ac5a8-265">[Python-Tools voor Visual Studio-documentatie]</span><span class="sxs-lookup"><span data-stu-id="ac5a8-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="ac5a8-266">Voor informatie over het gebruik van Azure Table Storage en MongoDB:</span><span class="sxs-lookup"><span data-stu-id="ac5a8-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="ac5a8-267">[Flask- en MongoDB in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ac5a8-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="ac5a8-268">[Flask- en Azure Table Storage in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ac5a8-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="ac5a8-269">Zie voor meer informatie, ook Hallo [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="ac5a8-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ac5a8-270">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="ac5a8-270">What's changed</span></span>
* <span data-ttu-id="ac5a8-271">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ac5a8-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
[Python-Tools voor Visual Studio-documentatie]: http://aka.ms/ptvsdocs
[Flask-documentatie]: http://flask.pocoo.org/ 

