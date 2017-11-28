---
title: aaaPython web-apps met Bottle in Azure
description: Een zelfstudie waarin u kennis kunt toorunning een Python-web-app in Azure App Service Web Apps.
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="6be36-103">Web-apps maken met Bottle in Azure</span><span class="sxs-lookup"><span data-stu-id="6be36-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="6be36-104">Deze zelfstudie wordt beschreven hoe tooget gestart Python uitvoert in Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="6be36-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="6be36-105">Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6be36-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="6be36-106">Als uw app groeit, kunt u schakelen toopaid die als host fungeert, en u ook met alle integreren kunt Hallo andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="6be36-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="6be36-107">U maakt een web-app met behulp van Hallo Bottle-webframework (Zie andere versies van deze zelfstudie voor [Django](web-sites-python-create-deploy-django-app.md) en [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="6be36-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="6be36-108">U wordt Hallo web-app maken vanuit Azure Marketplace hello, instellen van Git-implementatie en lokaal Hallo opslagplaats klonen.</span><span class="sxs-lookup"><span data-stu-id="6be36-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="6be36-109">U wordt Hallo web-app lokaal uitvoeren, wijzigingen aanbrengen, doorvoeren en push ze te[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="6be36-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="6be36-110">zelfstudie ziet hoe Hallo toodo dit van Windows of Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="6be36-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="6be36-111">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="6be36-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6be36-112">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="6be36-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6be36-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6be36-113">Prerequisites</span></span>
* <span data-ttu-id="6be36-114">Windows, Mac of Linux</span><span class="sxs-lookup"><span data-stu-id="6be36-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="6be36-115">Python 2.7 of 3.4</span><span class="sxs-lookup"><span data-stu-id="6be36-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="6be36-116">setuptools, pip, virtualenv (alleen Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="6be36-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="6be36-117">Git</span><span class="sxs-lookup"><span data-stu-id="6be36-117">Git</span></span>
* <span data-ttu-id="6be36-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Opmerking: dit is optioneel</span><span class="sxs-lookup"><span data-stu-id="6be36-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="6be36-119">**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.</span><span class="sxs-lookup"><span data-stu-id="6be36-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="6be36-120">Windows</span><span class="sxs-lookup"><span data-stu-id="6be36-120">Windows</span></span>
<span data-ttu-id="6be36-121">Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="6be36-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="6be36-122">Hiermee installeert u Hallo 32-bits versie van Python, setuptools, pip, virtualenv, enzovoort (32-bits Python is wat wordt geïnstalleerd op Hallo Azure-hostmachines).</span><span class="sxs-lookup"><span data-stu-id="6be36-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="6be36-123">U kunt Python ook downloaden via [python.org].</span><span class="sxs-lookup"><span data-stu-id="6be36-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="6be36-124">Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.</span><span class="sxs-lookup"><span data-stu-id="6be36-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="6be36-125">Als u Visual Studio gebruikt, kunt u Hallo geïntegreerde Git-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="6be36-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="6be36-126">Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.</span><span class="sxs-lookup"><span data-stu-id="6be36-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="6be36-127">Dit is optioneel, maar als u [Visual Studio], met inbegrip van Hallo gratis Visual Studio Community 2013 of Visual Studio Express 2013 voor Web en Hiermee krijgt u een uitstekende Python IDE.</span><span class="sxs-lookup"><span data-stu-id="6be36-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="6be36-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="6be36-128">Mac/Linux</span></span>
<span data-ttu-id="6be36-129">Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.</span><span class="sxs-lookup"><span data-stu-id="6be36-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="6be36-130">Web-Apps maken op Hallo Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6be36-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="6be36-131">Hallo eerste stap bij het maken van uw app is toocreate Hallo web-app via Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6be36-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="6be36-132">Meld u aan bij hello Azure-Portal en klikt u op Hallo **nieuw** knop in de linkeronderhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="6be36-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="6be36-133">Typ in Hallo zoekvak 'python'.</span><span class="sxs-lookup"><span data-stu-id="6be36-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="6be36-134">Selecteer in de zoekresultaten hello, **Bottle**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6be36-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="6be36-135">Hallo nieuwe Bottle-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor configureren.</span><span class="sxs-lookup"><span data-stu-id="6be36-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="6be36-136">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="6be36-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="6be36-137">Configureer Git-publicatie voor uw nieuwe web-app met behulp Hallo-instructies in [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6be36-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="6be36-138">Toepassingsoverzicht</span><span class="sxs-lookup"><span data-stu-id="6be36-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="6be36-139">Inhoud van Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="6be36-139">Git repository contents</span></span>
<span data-ttu-id="6be36-140">Hier volgt een overzicht van Hallo bestanden vindt u in Hallo eerste Git-opslagplaats, die we in de volgende sectie Hallo gaat klonen.</span><span class="sxs-lookup"><span data-stu-id="6be36-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="6be36-141">Belangrijkste bronnen voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6be36-141">Main sources for hello application.</span></span> <span data-ttu-id="6be36-142">Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.</span><span class="sxs-lookup"><span data-stu-id="6be36-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="6be36-143">Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.</span><span class="sxs-lookup"><span data-stu-id="6be36-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="6be36-144">Ondersteuning voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="6be36-144">Local development server support.</span></span> <span data-ttu-id="6be36-145">Gebruik deze toorun Hallo-toepassing lokaal uit.</span><span class="sxs-lookup"><span data-stu-id="6be36-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="6be36-146">Projectbestanden voor gebruik met [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6be36-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="6be36-147">IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="6be36-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="6be36-148">Externe pakketten nodig voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="6be36-148">External packages needed by this application.</span></span> <span data-ttu-id="6be36-149">Hallo-implementatiescript wordt een pip installatie hello-pakketten die worden vermeld in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="6be36-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="6be36-150">IIS-configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="6be36-150">IIS configuration files.</span></span> <span data-ttu-id="6be36-151">Hallo-implementatiescript gebruikt Hallo juiste web.x.y.config en kopieert deze als web.config.</span><span class="sxs-lookup"><span data-stu-id="6be36-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="6be36-152">Optionele bestanden - implementatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="6be36-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="6be36-153">Optionele bestanden - Python-runtime</span><span class="sxs-lookup"><span data-stu-id="6be36-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="6be36-154">Aanvullende bestanden op server</span><span class="sxs-lookup"><span data-stu-id="6be36-154">Additional files on server</span></span>
<span data-ttu-id="6be36-155">Bepaalde bestanden bestaan op Hallo server maar toohello git-opslagplaats niet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6be36-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="6be36-156">Deze worden gemaakt door het implementatiescript Hallo.</span><span class="sxs-lookup"><span data-stu-id="6be36-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="6be36-157">IIS-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="6be36-157">IIS configuration file.</span></span> <span data-ttu-id="6be36-158">Gemaakt op basis van web.x.y.config voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="6be36-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="6be36-159">Virtuele Python-omgeving.</span><span class="sxs-lookup"><span data-stu-id="6be36-159">Python virtual environment.</span></span> <span data-ttu-id="6be36-160">Gemaakt tijdens de implementatie als een compatibele virtuele omgeving op Hallo web-app nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6be36-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="6be36-161">Pakketten die worden vermeld in requirements.txt worden via pip geïnstalleerd, maar pip slaat de installatie over als hello-pakketten zijn al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6be36-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="6be36-162">Hallo naast 3 gedeelten wordt beschreven hoe tooproceed Hello web-app-ontwikkeling onder 3 verschillende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="6be36-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="6be36-163">Windows, met Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6be36-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="6be36-164">Windows, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6be36-164">Windows, with command line</span></span>
* <span data-ttu-id="6be36-165">Mac/Linux, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6be36-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="6be36-166">Web-ontwikkeling van apps - Windows - Python-Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6be36-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="6be36-167">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="6be36-167">Clone hello repository</span></span>
<span data-ttu-id="6be36-168">Kloon eerst Hallo-opslagplaats met Hallo-url opgegeven op Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="6be36-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="6be36-169">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6be36-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="6be36-170">Open Hallo oplossingsbestand (.sln) die is opgenomen in de hoofdmap Hallo van Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6be36-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="6be36-171">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="6be36-171">Create virtual environment</span></span>
<span data-ttu-id="6be36-172">U maakt nu een virtuele omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="6be36-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="6be36-173">Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.</span><span class="sxs-lookup"><span data-stu-id="6be36-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="6be36-174">Zorg ervoor dat het Hallo-naam van het Hallo-omgeving is `env`.</span><span class="sxs-lookup"><span data-stu-id="6be36-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="6be36-175">Selecteer de basisinterpreter Hallo.</span><span class="sxs-lookup"><span data-stu-id="6be36-175">Select hello base interpreter.</span></span> <span data-ttu-id="6be36-176">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of op Hallo **toepassingsinstellingen** blade van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="6be36-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="6be36-177">Zorg ervoor dat de optie hello-pakketten toodownload en installatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6be36-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="6be36-178">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6be36-178">Click **Create**.</span></span> <span data-ttu-id="6be36-179">Dit wordt Hallo virtuele omgeving maken, en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6be36-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6be36-180">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="6be36-180">Run using development server</span></span>
<span data-ttu-id="6be36-181">Druk op F5 toostart foutopsporing en uw webbrowser wordt automatisch geopend toohello pagina die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6be36-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="6be36-182">U kunt onderbrekingspunten instellen in het Hallo-bronnen, gebruik Hallo vensters, enzovoort. Zie Hallo [Python-Tools voor Visual Studio-documentatie] Hallo voor meer informatie over de verschillende functies.</span><span class="sxs-lookup"><span data-stu-id="6be36-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="6be36-183">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="6be36-183">Make changes</span></span>
<span data-ttu-id="6be36-184">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6be36-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="6be36-185">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="6be36-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="6be36-186">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="6be36-186">Install more packages</span></span>
<span data-ttu-id="6be36-187">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Bottle.</span><span class="sxs-lookup"><span data-stu-id="6be36-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="6be36-188">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="6be36-188">You can install additional packages using pip.</span></span> <span data-ttu-id="6be36-189">tooinstall een pakket met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="6be36-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="6be36-190">Bijvoorbeeld: tooinstall hello Azure SDK voor Python, die u hebt u toegang tooAzure storage, servicebus en andere Azure-services, voer `azure`:</span><span class="sxs-lookup"><span data-stu-id="6be36-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="6be36-191">Met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **requirements.txt genereren** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="6be36-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="6be36-192">Voer vervolgens Hallo wijzigingen toorequirements.txt toohello Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6be36-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="6be36-193">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="6be36-193">Deploy tooAzure</span></span>
<span data-ttu-id="6be36-194">tootrigger een implementatie, klikt u op **Sync** of **Push**.</span><span class="sxs-lookup"><span data-stu-id="6be36-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="6be36-195">Bij een synchronisatie vinden er push- en pullbewerkingen plaats.</span><span class="sxs-lookup"><span data-stu-id="6be36-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="6be36-196">Hallo eerste implementatie duurt enige tijd als deze, u een virtuele omgeving, pakketten worden geïnstalleerd, enzovoort maakt wordt.</span><span class="sxs-lookup"><span data-stu-id="6be36-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="6be36-197">Visual Studio weergeven niet Hallo voortgang van Hallo implementatie.</span><span class="sxs-lookup"><span data-stu-id="6be36-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="6be36-198">Als u tooreview Hallo uitvoer dat wilt, raadpleegt u Hallo sectie op [probleemoplossing - implementatie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="6be36-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="6be36-199">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6be36-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="6be36-200">Ontwikkeling van Web-Apps - Windows - opdracht regel</span><span class="sxs-lookup"><span data-stu-id="6be36-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="6be36-201">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="6be36-201">Clone hello repository</span></span>
<span data-ttu-id="6be36-202">Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe.</span><span class="sxs-lookup"><span data-stu-id="6be36-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="6be36-203">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6be36-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="6be36-204">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="6be36-204">Create virtual environment</span></span>
<span data-ttu-id="6be36-205">Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="6be36-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="6be36-206">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.</span><span class="sxs-lookup"><span data-stu-id="6be36-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="6be36-207">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of Hallo toepassingsinstellingen blade voor uw web-app in hello Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="6be36-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="6be36-208">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6be36-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="6be36-209">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6be36-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="6be36-210">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="6be36-210">Install any external packages required by your application.</span></span> <span data-ttu-id="6be36-211">U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="6be36-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="6be36-212">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="6be36-212">Run using development server</span></span>
<span data-ttu-id="6be36-213">U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6be36-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="6be36-214">Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:</span><span class="sxs-lookup"><span data-stu-id="6be36-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="6be36-215">Open vervolgens de URL van web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="6be36-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="6be36-216">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="6be36-216">Make changes</span></span>
<span data-ttu-id="6be36-217">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6be36-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="6be36-218">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="6be36-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6be36-219">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="6be36-219">Install more packages</span></span>
<span data-ttu-id="6be36-220">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Bottle.</span><span class="sxs-lookup"><span data-stu-id="6be36-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="6be36-221">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="6be36-221">You can install additional packages using pip.</span></span> <span data-ttu-id="6be36-222">Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:</span><span class="sxs-lookup"><span data-stu-id="6be36-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="6be36-223">Zorg ervoor dat tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="6be36-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="6be36-224">Hallo wijzigingen doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="6be36-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="6be36-225">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="6be36-225">Deploy tooAzure</span></span>
<span data-ttu-id="6be36-226">een implementatie tootrigger, push Hallo verandert tooAzure:</span><span class="sxs-lookup"><span data-stu-id="6be36-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="6be36-227">Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.</span><span class="sxs-lookup"><span data-stu-id="6be36-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6be36-228">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6be36-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="6be36-229">Ontwikkeling van web-apps - Mac/Linux - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6be36-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="6be36-230">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="6be36-230">Clone hello repository</span></span>
<span data-ttu-id="6be36-231">Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe.</span><span class="sxs-lookup"><span data-stu-id="6be36-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="6be36-232">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6be36-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="6be36-233">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="6be36-233">Create virtual environment</span></span>
<span data-ttu-id="6be36-234">Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="6be36-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="6be36-235">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.</span><span class="sxs-lookup"><span data-stu-id="6be36-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="6be36-236">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of Hallo blade toepassingsinstellingen van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="6be36-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="6be36-237">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6be36-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="6be36-238">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6be36-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="6be36-239">of pyvenv env</span><span class="sxs-lookup"><span data-stu-id="6be36-239">or pyvenv env</span></span>

<span data-ttu-id="6be36-240">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="6be36-240">Install any external packages required by your application.</span></span> <span data-ttu-id="6be36-241">U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="6be36-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="6be36-242">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="6be36-242">Run using development server</span></span>
<span data-ttu-id="6be36-243">U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6be36-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="6be36-244">Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:</span><span class="sxs-lookup"><span data-stu-id="6be36-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="6be36-245">Open vervolgens de URL van web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="6be36-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="6be36-246">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="6be36-246">Make changes</span></span>
<span data-ttu-id="6be36-247">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6be36-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="6be36-248">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="6be36-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6be36-249">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="6be36-249">Install more packages</span></span>
<span data-ttu-id="6be36-250">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Bottle.</span><span class="sxs-lookup"><span data-stu-id="6be36-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="6be36-251">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="6be36-251">You can install additional packages using pip.</span></span> <span data-ttu-id="6be36-252">Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:</span><span class="sxs-lookup"><span data-stu-id="6be36-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="6be36-253">Zorg ervoor dat tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="6be36-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="6be36-254">Hallo wijzigingen doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="6be36-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="6be36-255">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="6be36-255">Deploy tooAzure</span></span>
<span data-ttu-id="6be36-256">een implementatie tootrigger, push Hallo verandert tooAzure:</span><span class="sxs-lookup"><span data-stu-id="6be36-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="6be36-257">Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.</span><span class="sxs-lookup"><span data-stu-id="6be36-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6be36-258">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6be36-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="6be36-259">Probleemoplossing - Installatie van pakketten</span><span class="sxs-lookup"><span data-stu-id="6be36-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="6be36-260">Probleemoplossing - Virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="6be36-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="6be36-261">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6be36-261">Next Steps</span></span>
<span data-ttu-id="6be36-262">Volg deze koppelingen toolearn meer over Bottle en Python-Tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6be36-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="6be36-263">[Bottle-documentatie]</span><span class="sxs-lookup"><span data-stu-id="6be36-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="6be36-264">[Python-Tools voor Visual Studio-documentatie]</span><span class="sxs-lookup"><span data-stu-id="6be36-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="6be36-265">Voor informatie over het gebruik van Azure Table Storage en MongoDB:</span><span class="sxs-lookup"><span data-stu-id="6be36-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="6be36-266">[Bottle en MongoDB in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6be36-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="6be36-267">[Bottle en Azure Table Storage in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6be36-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6be36-268">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="6be36-268">What's changed</span></span>
* <span data-ttu-id="6be36-269">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6be36-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle en MongoDB in Azure met Python-Tools voor Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle en Azure Table Storage in Azure met Python-Tools voor Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

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
[Bottle-documentatie]: http://bottlepy.org/docs/dev/index.html

