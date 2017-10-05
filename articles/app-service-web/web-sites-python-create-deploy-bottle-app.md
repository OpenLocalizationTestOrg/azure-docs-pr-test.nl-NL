---
title: Python-web-apps met Bottle in Azure
description: Een zelfstudie waarin u leert hoe u een Python-web-app uitvoert in Azure App Service Web Apps.
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
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="ff51d-103">Web-apps maken met Bottle in Azure</span><span class="sxs-lookup"><span data-stu-id="ff51d-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="ff51d-104">Deze zelfstudie wordt beschreven hoe u Python uitvoert in Azure App Service Web Apps aan de slag.</span><span class="sxs-lookup"><span data-stu-id="ff51d-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="ff51d-105">Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff51d-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="ff51d-106">Naarmate uw app groeit, kunt u overstappen op betaalde hosting én profiteren van integratie met alle overige Azure-services.</span><span class="sxs-lookup"><span data-stu-id="ff51d-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="ff51d-107">Maakt u een WebApp met behulp van Bottle-webframework (Zie andere versies van deze zelfstudie voor [Django](web-sites-python-create-deploy-django-app.md) en [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="ff51d-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="ff51d-108">U maakt de web-app via Azure Marketplace, u configureert Git-implementatie en u kloont de opslagplaats lokaal.</span><span class="sxs-lookup"><span data-stu-id="ff51d-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="ff51d-109">U wordt de web-app lokaal uitvoeren, wijzigingen aanbrengen, doorvoeren en push ze [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ff51d-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="ff51d-110">In de zelfstudie ziet u hoe u dit doet in Windows of Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="ff51d-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="ff51d-111">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="ff51d-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ff51d-112">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="ff51d-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ff51d-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ff51d-113">Prerequisites</span></span>
* <span data-ttu-id="ff51d-114">Windows, Mac of Linux</span><span class="sxs-lookup"><span data-stu-id="ff51d-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="ff51d-115">Python 2.7 of 3.4</span><span class="sxs-lookup"><span data-stu-id="ff51d-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="ff51d-116">setuptools, pip, virtualenv (alleen Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="ff51d-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="ff51d-117">Git</span><span class="sxs-lookup"><span data-stu-id="ff51d-117">Git</span></span>
* <span data-ttu-id="ff51d-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Opmerking: dit is optioneel</span><span class="sxs-lookup"><span data-stu-id="ff51d-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="ff51d-119">**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.</span><span class="sxs-lookup"><span data-stu-id="ff51d-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="ff51d-120">Windows</span><span class="sxs-lookup"><span data-stu-id="ff51d-120">Windows</span></span>
<span data-ttu-id="ff51d-121">Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="ff51d-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="ff51d-122">Hiermee installeert u de 32-bits versie van Python, setuptools, PIP, virtualenv, enzovoort (32-bits Python wordt geïnstalleerd op de Azure-hostmachines).</span><span class="sxs-lookup"><span data-stu-id="ff51d-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="ff51d-123">U kunt Python ook downloaden via [python.org].</span><span class="sxs-lookup"><span data-stu-id="ff51d-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="ff51d-124">Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.</span><span class="sxs-lookup"><span data-stu-id="ff51d-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="ff51d-125">Als u Visual Studio gebruikt, kunt u de geïntegreerde Git-ondersteuning gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff51d-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="ff51d-126">Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.</span><span class="sxs-lookup"><span data-stu-id="ff51d-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="ff51d-127">Dit is optioneel, maar als u [Visual Studio] hebt, met inbegrip van de gratis Visual Studio Community 2013 of Visual Studio Express 2013 for Web, beschikt u over een uitstekende Python IDE.</span><span class="sxs-lookup"><span data-stu-id="ff51d-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="ff51d-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="ff51d-128">Mac/Linux</span></span>
<span data-ttu-id="ff51d-129">Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.</span><span class="sxs-lookup"><span data-stu-id="ff51d-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="ff51d-130">Web-Apps maken in de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ff51d-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="ff51d-131">De eerste stap voor het maken van uw app bestaat uit het maken van een web-app via de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff51d-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="ff51d-132">Meld u aan bij de Azure Portal en klik in de linkerbenedenhoek op de knop **NIEUW**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="ff51d-133">Voer in het zoekvak 'python' in.</span><span class="sxs-lookup"><span data-stu-id="ff51d-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="ff51d-134">Selecteer in de lijst met zoekresultaten **Bottle**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="ff51d-135">Configureer de nieuwe Bottle-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor.</span><span class="sxs-lookup"><span data-stu-id="ff51d-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="ff51d-136">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="ff51d-137">Configureer Git-publicatie voor uw nieuwe web-app door de instructies te volgen in [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="ff51d-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="ff51d-138">Toepassingsoverzicht</span><span class="sxs-lookup"><span data-stu-id="ff51d-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="ff51d-139">Inhoud van Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="ff51d-139">Git repository contents</span></span>
<span data-ttu-id="ff51d-140">Hier volgt een overzicht van de bestanden in de eerste Git-opslagplaats. Deze gaat u in het volgende gedeelte klonen.</span><span class="sxs-lookup"><span data-stu-id="ff51d-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="ff51d-141">Belangrijkste bronnen voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff51d-141">Main sources for the application.</span></span> <span data-ttu-id="ff51d-142">Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.</span><span class="sxs-lookup"><span data-stu-id="ff51d-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="ff51d-143">Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.</span><span class="sxs-lookup"><span data-stu-id="ff51d-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="ff51d-144">Ondersteuning voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="ff51d-144">Local development server support.</span></span> <span data-ttu-id="ff51d-145">Gebruiken deze om de toepassing lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ff51d-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="ff51d-146">Projectbestanden voor gebruik met [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="ff51d-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="ff51d-147">IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="ff51d-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="ff51d-148">Externe pakketten nodig voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff51d-148">External packages needed by this application.</span></span> <span data-ttu-id="ff51d-149">Door het implementatiescript wordt een PIP-installatie uitgevoerd voor de pakketten die in het bestand worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="ff51d-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="ff51d-150">IIS-configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="ff51d-150">IIS configuration files.</span></span> <span data-ttu-id="ff51d-151">Het implementatiescript maakt gebruik van de juiste web.x.y.config en kopieert deze als web.config.</span><span class="sxs-lookup"><span data-stu-id="ff51d-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="ff51d-152">Optionele bestanden - implementatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="ff51d-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="ff51d-153">Optionele bestanden - Python-runtime</span><span class="sxs-lookup"><span data-stu-id="ff51d-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="ff51d-154">Aanvullende bestanden op server</span><span class="sxs-lookup"><span data-stu-id="ff51d-154">Additional files on server</span></span>
<span data-ttu-id="ff51d-155">Bepaalde bestanden bestaan wel op de server, maar worden niet toegevoegd aan de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ff51d-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="ff51d-156">Deze worden gemaakt door het script voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="ff51d-157">IIS-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="ff51d-157">IIS configuration file.</span></span> <span data-ttu-id="ff51d-158">Gemaakt op basis van web.x.y.config voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="ff51d-159">Virtuele Python-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ff51d-159">Python virtual environment.</span></span> <span data-ttu-id="ff51d-160">Wordt gemaakt tijdens de implementatie als er in de web-app nog geen compatibele virtuele omgeving bestaat.</span><span class="sxs-lookup"><span data-stu-id="ff51d-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="ff51d-161">De pakketten die worden vermeld in requirements.txt, worden via PIP geïnstalleerd, maar PIP slaat de installatie over als de pakketten al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ff51d-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="ff51d-162">In de volgende drie gedeelten wordt beschreven hoe u verdergaat met de ontwikkeling van de web-app in drie verschillende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="ff51d-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="ff51d-163">Windows, met Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff51d-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="ff51d-164">Windows, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ff51d-164">Windows, with command line</span></span>
* <span data-ttu-id="ff51d-165">Mac/Linux, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ff51d-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="ff51d-166">Web-ontwikkeling van apps - Windows - Python-Tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff51d-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="ff51d-167">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="ff51d-167">Clone the repository</span></span>
<span data-ttu-id="ff51d-168">Kloon eerst de opslagplaats via de url die is opgegeven in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff51d-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="ff51d-169">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="ff51d-170">Open het oplossingsbestand (.sln) dat is opgenomen in de hoofdmap van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ff51d-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="ff51d-171">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="ff51d-171">Create virtual environment</span></span>
<span data-ttu-id="ff51d-172">U maakt nu een virtuele omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="ff51d-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="ff51d-173">Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="ff51d-174">Zorg ervoor dat de naam van de omgeving `env` is.</span><span class="sxs-lookup"><span data-stu-id="ff51d-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="ff51d-175">Selecteer de basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="ff51d-175">Select the base interpreter.</span></span> <span data-ttu-id="ff51d-176">Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="ff51d-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="ff51d-177">Zorg ervoor dat de optie voor het downloaden en installeren van pakketten is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ff51d-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="ff51d-178">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-178">Click **Create**.</span></span> <span data-ttu-id="ff51d-179">Hiermee maakt u de virtuele omgeving en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ff51d-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="ff51d-180">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="ff51d-180">Run using development server</span></span>
<span data-ttu-id="ff51d-181">Druk op F5 om de foutopsporing te starten. Uw webbrowser wordt automatisch geopend op de pagina die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ff51d-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="ff51d-182">U kunt onderbrekingspunten instellen in de bronnen, de vensters Controle gebruiken, enzovoort. Zie de [Documentatie bij Python Tools for Visual Studio] voor meer informatie over de verschillende functies.</span><span class="sxs-lookup"><span data-stu-id="ff51d-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="ff51d-183">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="ff51d-183">Make changes</span></span>
<span data-ttu-id="ff51d-184">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ff51d-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="ff51d-185">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="ff51d-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="ff51d-186">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="ff51d-186">Install more packages</span></span>
<span data-ttu-id="ff51d-187">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Bottle.</span><span class="sxs-lookup"><span data-stu-id="ff51d-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="ff51d-188">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="ff51d-188">You can install additional packages using pip.</span></span> <span data-ttu-id="ff51d-189">Als u een pakket wilt installeren, klikt u met de rechtermuisknop op de virtuele omgeving en selecteert u **Python-pakket installeren**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="ff51d-190">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u `azure`:</span><span class="sxs-lookup"><span data-stu-id="ff51d-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="ff51d-191">Klik met de rechtermuisknop op de virtuele omgeving en selecteer **requirements.txt genereren** om requirements.txt bij te werken.</span><span class="sxs-lookup"><span data-stu-id="ff51d-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="ff51d-192">Voer vervolgens de wijzigingen aan requirements.txt door in de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ff51d-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="ff51d-193">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="ff51d-193">Deploy to Azure</span></span>
<span data-ttu-id="ff51d-194">Als u een implementatie wilt activeren, klikt u op **Synchroniseren** of **Pushen**.</span><span class="sxs-lookup"><span data-stu-id="ff51d-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="ff51d-195">Bij een synchronisatie vinden er push- en pullbewerkingen plaats.</span><span class="sxs-lookup"><span data-stu-id="ff51d-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="ff51d-196">De eerste implementatie duurt langer dan normaal omdat er een virtuele omgeving wordt gemaakt, er pakketten worden geïnstalleerd en meer.</span><span class="sxs-lookup"><span data-stu-id="ff51d-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="ff51d-197">De voortgang van de implementatie wordt niet weergegeven in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff51d-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="ff51d-198">Als u de uitvoer wilt controleren, raadpleegt u het gedeelte [Probleemoplossing - Implementatie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="ff51d-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="ff51d-199">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ff51d-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="ff51d-200">Ontwikkeling van Web-Apps - Windows - opdracht regel</span><span class="sxs-lookup"><span data-stu-id="ff51d-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="ff51d-201">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="ff51d-201">Clone the repository</span></span>
<span data-ttu-id="ff51d-202">Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe.</span><span class="sxs-lookup"><span data-stu-id="ff51d-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="ff51d-203">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="ff51d-204">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="ff51d-204">Create virtual environment</span></span>
<span data-ttu-id="ff51d-205">U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="ff51d-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="ff51d-206">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="ff51d-207">Zorg ervoor dat u het gebruik van dezelfde versie van Python gebruikt die is geselecteerd voor uw web-app (in runtime.txt of op de blade toepassingsinstellingen voor uw web-app in de Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="ff51d-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="ff51d-208">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ff51d-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="ff51d-209">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ff51d-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="ff51d-210">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="ff51d-210">Install any external packages required by your application.</span></span> <span data-ttu-id="ff51d-211">U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="ff51d-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="ff51d-212">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="ff51d-212">Run using development server</span></span>
<span data-ttu-id="ff51d-213">U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ff51d-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="ff51d-214">In de console worden de URL en de poort vermeld waarnaar de server luistert:</span><span class="sxs-lookup"><span data-stu-id="ff51d-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="ff51d-215">Open de betreffende URL in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="ff51d-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="ff51d-216">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="ff51d-216">Make changes</span></span>
<span data-ttu-id="ff51d-217">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ff51d-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="ff51d-218">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="ff51d-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="ff51d-219">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="ff51d-219">Install more packages</span></span>
<span data-ttu-id="ff51d-220">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Bottle.</span><span class="sxs-lookup"><span data-stu-id="ff51d-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="ff51d-221">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="ff51d-221">You can install additional packages using pip.</span></span> <span data-ttu-id="ff51d-222">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:</span><span class="sxs-lookup"><span data-stu-id="ff51d-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="ff51d-223">Zorg ervoor dat u requirements.txt bijwerkt:</span><span class="sxs-lookup"><span data-stu-id="ff51d-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="ff51d-224">Voer de wijzigingen door:</span><span class="sxs-lookup"><span data-stu-id="ff51d-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="ff51d-225">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="ff51d-225">Deploy to Azure</span></span>
<span data-ttu-id="ff51d-226">Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:</span><span class="sxs-lookup"><span data-stu-id="ff51d-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="ff51d-227">U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.</span><span class="sxs-lookup"><span data-stu-id="ff51d-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="ff51d-228">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ff51d-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="ff51d-229">Ontwikkeling van web-apps - Mac/Linux - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ff51d-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="ff51d-230">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="ff51d-230">Clone the repository</span></span>
<span data-ttu-id="ff51d-231">Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe.</span><span class="sxs-lookup"><span data-stu-id="ff51d-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="ff51d-232">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="ff51d-233">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="ff51d-233">Create virtual environment</span></span>
<span data-ttu-id="ff51d-234">U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="ff51d-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="ff51d-235">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.</span><span class="sxs-lookup"><span data-stu-id="ff51d-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="ff51d-236">Zorg ervoor dat u dezelfde versie van Python gebruikt die is geselecteerd voor uw web-app (in runtime.txt of op de blade Toepassingsinstellingen van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="ff51d-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="ff51d-237">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ff51d-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="ff51d-238">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ff51d-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="ff51d-239">of pyvenv env</span><span class="sxs-lookup"><span data-stu-id="ff51d-239">or pyvenv env</span></span>

<span data-ttu-id="ff51d-240">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="ff51d-240">Install any external packages required by your application.</span></span> <span data-ttu-id="ff51d-241">U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="ff51d-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="ff51d-242">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="ff51d-242">Run using development server</span></span>
<span data-ttu-id="ff51d-243">U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ff51d-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="ff51d-244">In de console worden de URL en de poort vermeld waarnaar de server luistert:</span><span class="sxs-lookup"><span data-stu-id="ff51d-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="ff51d-245">Open de betreffende URL in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="ff51d-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="ff51d-246">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="ff51d-246">Make changes</span></span>
<span data-ttu-id="ff51d-247">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="ff51d-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="ff51d-248">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="ff51d-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="ff51d-249">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="ff51d-249">Install more packages</span></span>
<span data-ttu-id="ff51d-250">Uw toepassing heeft mogelijk afhankelijkheden buiten Python en Bottle.</span><span class="sxs-lookup"><span data-stu-id="ff51d-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="ff51d-251">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="ff51d-251">You can install additional packages using pip.</span></span> <span data-ttu-id="ff51d-252">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:</span><span class="sxs-lookup"><span data-stu-id="ff51d-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="ff51d-253">Zorg ervoor dat u requirements.txt bijwerkt:</span><span class="sxs-lookup"><span data-stu-id="ff51d-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="ff51d-254">Voer de wijzigingen door:</span><span class="sxs-lookup"><span data-stu-id="ff51d-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="ff51d-255">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="ff51d-255">Deploy to Azure</span></span>
<span data-ttu-id="ff51d-256">Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:</span><span class="sxs-lookup"><span data-stu-id="ff51d-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="ff51d-257">U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.</span><span class="sxs-lookup"><span data-stu-id="ff51d-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="ff51d-258">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ff51d-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="ff51d-259">Probleemoplossing - Installatie van pakketten</span><span class="sxs-lookup"><span data-stu-id="ff51d-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="ff51d-260">Probleemoplossing - Virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="ff51d-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="ff51d-261">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff51d-261">Next Steps</span></span>
<span data-ttu-id="ff51d-262">Volg deze koppelingen voor meer informatie over Bottle en Python-Tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ff51d-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="ff51d-263">[Bottle-documentatie]</span><span class="sxs-lookup"><span data-stu-id="ff51d-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="ff51d-264">[Documentatie bij Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ff51d-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="ff51d-265">Voor informatie over het gebruik van Azure Table Storage en MongoDB:</span><span class="sxs-lookup"><span data-stu-id="ff51d-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="ff51d-266">[Bottle en MongoDB in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ff51d-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="ff51d-267">[Bottle en Azure Table Storage in Azure met Python-Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="ff51d-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ff51d-268">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="ff51d-268">What's changed</span></span>
* <span data-ttu-id="ff51d-269">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ff51d-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="ff51d-270">[Bottle en MongoDB in Azure met Python-Tools voor Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="ff51d-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="ff51d-271">[Bottle en Azure Table Storage in Azure met Python-Tools voor Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="ff51d-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="ff51d-272">[Azure SDK voor Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="ff51d-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="ff51d-273">[Azure SDK voor Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="ff51d-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="ff51d-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="ff51d-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="ff51d-275">[Git voor Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="ff51d-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="ff51d-276">[GitHub voor Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="ff51d-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="ff51d-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="ff51d-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="ff51d-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="ff51d-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="ff51d-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="ff51d-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="ff51d-280">[Documentatie bij Python Tools for Visual Studio]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="ff51d-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="ff51d-281">[Bottle-documentatie]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="ff51d-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

