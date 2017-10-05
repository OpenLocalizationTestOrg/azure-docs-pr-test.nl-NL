---
title: Web-apps maken met Django in Azure
description: Een zelfstudie waarin u leert hoe u een Python-web-app uitvoert in Azure App Service Web Apps.
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
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="f3837-103">Web-apps maken met Django in Azure</span><span class="sxs-lookup"><span data-stu-id="f3837-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="f3837-104">In deze zelfstudie wordt beschreven hoe u Python uitvoert in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f3837-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f3837-105">Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3837-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="f3837-106">Naarmate uw app groeit, kunt u overstappen op betaalde hosting én profiteren van integratie met alle overige Azure-services.</span><span class="sxs-lookup"><span data-stu-id="f3837-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="f3837-107">U maakt een toepassing op basis van het Django-webframework (zie andere versies van deze zelfstudie voor [Flask](web-sites-python-create-deploy-flask-app.md) en [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="f3837-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="f3837-108">U maakt de web-app via Azure Marketplace, u configureert Git-implementatie en u kloont de opslagplaats lokaal.</span><span class="sxs-lookup"><span data-stu-id="f3837-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="f3837-109">Vervolgens voert u de toepassing lokaal uit, brengt u wijzigingen aan, voert u deze door en pusht u ze naar Azure.</span><span class="sxs-lookup"><span data-stu-id="f3837-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="f3837-110">In de zelfstudie ziet u hoe u dit doet in Windows of Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="f3837-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f3837-111">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="f3837-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f3837-112">U hebt geen creditcard nodig en u gaat geen verplichtingen aan.</span><span class="sxs-lookup"><span data-stu-id="f3837-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f3837-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f3837-113">Prerequisites</span></span>
* <span data-ttu-id="f3837-114">Windows, Mac of Linux</span><span class="sxs-lookup"><span data-stu-id="f3837-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="f3837-115">Python 2.7 of 3.4</span><span class="sxs-lookup"><span data-stu-id="f3837-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="f3837-116">setuptools, pip, virtualenv (alleen Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="f3837-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="f3837-117">Git</span><span class="sxs-lookup"><span data-stu-id="f3837-117">Git</span></span>
* <span data-ttu-id="f3837-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Opmerking: dit is optioneel</span><span class="sxs-lookup"><span data-stu-id="f3837-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="f3837-119">**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.</span><span class="sxs-lookup"><span data-stu-id="f3837-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="f3837-120">Windows</span><span class="sxs-lookup"><span data-stu-id="f3837-120">Windows</span></span>
<span data-ttu-id="f3837-121">Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="f3837-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="f3837-122">Hiermee installeert u de 32-bits versie van Python, setuptools, PIP, virtualenv, enzovoort (32-bits Python wordt geïnstalleerd op de Azure-hostmachines).</span><span class="sxs-lookup"><span data-stu-id="f3837-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="f3837-123">U kunt Python ook downloaden via [python.org].</span><span class="sxs-lookup"><span data-stu-id="f3837-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="f3837-124">Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.</span><span class="sxs-lookup"><span data-stu-id="f3837-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="f3837-125">Als u Visual Studio gebruikt, kunt u de geïntegreerde Git-ondersteuning gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3837-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="f3837-126">Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.</span><span class="sxs-lookup"><span data-stu-id="f3837-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="f3837-127">Dit is optioneel, maar als u [Visual Studio] hebt, met inbegrip van de gratis Visual Studio Community 2013 of Visual Studio Express 2013 for Web, beschikt u over een uitstekende Python IDE.</span><span class="sxs-lookup"><span data-stu-id="f3837-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="f3837-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="f3837-128">Mac/Linux</span></span>
<span data-ttu-id="f3837-129">Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.</span><span class="sxs-lookup"><span data-stu-id="f3837-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="f3837-130">Web-apps maken via de portal</span><span class="sxs-lookup"><span data-stu-id="f3837-130">Web App Creation on Portal</span></span>
<span data-ttu-id="f3837-131">De eerste stap voor het maken van uw app bestaat uit het maken van een web-app via de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3837-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f3837-132">Meld u aan bij de Azure Portal en klik in de linkerbenedenhoek op de knop **NIEUW**.</span><span class="sxs-lookup"><span data-stu-id="f3837-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="f3837-133">Voer in het zoekvak 'python' in.</span><span class="sxs-lookup"><span data-stu-id="f3837-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="f3837-134">Selecteer in de zoekresultaten **Django** (gepubliceerd door PTVS), en klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f3837-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="f3837-135">Configureer de nieuwe Django-app door er bijvoorbeeld een nieuw App Service-plan en een nieuwe resourcegroep voor te maken.</span><span class="sxs-lookup"><span data-stu-id="f3837-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="f3837-136">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f3837-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="f3837-137">Configureer Git-publicatie voor uw nieuwe web-app door de instructies te volgen in [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="f3837-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="f3837-138">Toepassingsoverzicht</span><span class="sxs-lookup"><span data-stu-id="f3837-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="f3837-139">Inhoud van Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="f3837-139">Git repository contents</span></span>
<span data-ttu-id="f3837-140">Hier volgt een overzicht van de bestanden in de eerste Git-opslagplaats. Deze gaat u in het volgende gedeelte klonen.</span><span class="sxs-lookup"><span data-stu-id="f3837-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

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

<span data-ttu-id="f3837-141">Belangrijkste bronnen voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3837-141">Main sources for the application.</span></span> <span data-ttu-id="f3837-142">Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.</span><span class="sxs-lookup"><span data-stu-id="f3837-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="f3837-143">Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.</span><span class="sxs-lookup"><span data-stu-id="f3837-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="f3837-144">Lokaal beheer en ondersteuning voor de ontwikkelaarsserver.</span><span class="sxs-lookup"><span data-stu-id="f3837-144">Local management and development server support.</span></span> <span data-ttu-id="f3837-145">Gebruik deze om de toepassing lokaal uit te voeren, de database te synchroniseren, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f3837-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="f3837-146">Standaarddatabase.</span><span class="sxs-lookup"><span data-stu-id="f3837-146">Default database.</span></span> <span data-ttu-id="f3837-147">Bevat de benodigde tabellen voor het uitvoeren van de toepassing, maar bevat geen gebruikers (synchroniseer de database om een gebruiker te maken).</span><span class="sxs-lookup"><span data-stu-id="f3837-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="f3837-148">Projectbestanden voor gebruik met [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f3837-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="f3837-149">IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="f3837-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="f3837-150">Externe pakketten nodig voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3837-150">External packages needed by this application.</span></span> <span data-ttu-id="f3837-151">Door het implementatiescript wordt een PIP-installatie uitgevoerd voor de pakketten die in het bestand worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="f3837-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="f3837-152">IIS-configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="f3837-152">IIS configuration files.</span></span> <span data-ttu-id="f3837-153">Het implementatiescript maakt gebruik van de juiste web.x.y.config en kopieert deze als web.config.</span><span class="sxs-lookup"><span data-stu-id="f3837-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="f3837-154">Optionele bestanden - implementatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="f3837-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="f3837-155">Optionele bestanden - Python-runtime</span><span class="sxs-lookup"><span data-stu-id="f3837-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="f3837-156">Aanvullende bestanden op server</span><span class="sxs-lookup"><span data-stu-id="f3837-156">Additional files on server</span></span>
<span data-ttu-id="f3837-157">Bepaalde bestanden bestaan wel op de server, maar worden niet toegevoegd aan de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f3837-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="f3837-158">Deze worden gemaakt door het script voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="f3837-159">IIS-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="f3837-159">IIS configuration file.</span></span> <span data-ttu-id="f3837-160">Gemaakt op basis van web.x.y.config voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="f3837-161">Virtuele Python-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f3837-161">Python virtual environment.</span></span> <span data-ttu-id="f3837-162">Wordt gemaakt tijdens de implementatie als er in de web-app nog geen compatibele virtuele omgeving bestaat.</span><span class="sxs-lookup"><span data-stu-id="f3837-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="f3837-163">De pakketten die worden vermeld in requirements.txt, worden via PIP geïnstalleerd, maar PIP slaat de installatie over als de pakketten al zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f3837-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="f3837-164">In de volgende drie gedeelten wordt beschreven hoe u verdergaat met de ontwikkeling van de web-app in drie verschillende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="f3837-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="f3837-165">Windows, met Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3837-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="f3837-166">Windows, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="f3837-166">Windows, with command line</span></span>
* <span data-ttu-id="f3837-167">Mac/Linux, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="f3837-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="f3837-168">Ontwikkeling van web-apps - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3837-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="f3837-169">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="f3837-169">Clone the repository</span></span>
<span data-ttu-id="f3837-170">Kloon eerst de opslagplaats via de URL die in de Azure Portal is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f3837-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="f3837-171">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="f3837-172">Open het oplossingsbestand (.sln) dat is opgenomen in de hoofdmap van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f3837-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="f3837-173">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="f3837-173">Create virtual environment</span></span>
<span data-ttu-id="f3837-174">U maakt nu een virtuele omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="f3837-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="f3837-175">Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.</span><span class="sxs-lookup"><span data-stu-id="f3837-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="f3837-176">Zorg ervoor dat de naam van de omgeving `env` is.</span><span class="sxs-lookup"><span data-stu-id="f3837-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="f3837-177">Selecteer de basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="f3837-177">Select the base interpreter.</span></span> <span data-ttu-id="f3837-178">Zorg ervoor dat u dezelfde versie van Python gebruikt als de versie die is geselecteerd voor uw web-app (in runtime.txt of op de blade **Toepassingsinstellingen** van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="f3837-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="f3837-179">Zorg ervoor dat de optie voor het downloaden en installeren van pakketten is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f3837-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="f3837-180">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="f3837-180">Click **Create**.</span></span> <span data-ttu-id="f3837-181">Hiermee maakt u de virtuele omgeving en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f3837-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="f3837-182">Een beheerder maken</span><span class="sxs-lookup"><span data-stu-id="f3837-182">Create a superuser</span></span>
<span data-ttu-id="f3837-183">Voor de database die deel uitmaakt van de toepassing, is geen beheerder opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f3837-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="f3837-184">Als u gebruik wilt maken van de aanmeldfunctionaliteit in de toepassing of van de Django-beheerinterface (als u besluit deze in te schakelen), moet u een beheerder maken.</span><span class="sxs-lookup"><span data-stu-id="f3837-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="f3837-185">Voer dit uit vanaf de opdrachtregel van de projectmap:</span><span class="sxs-lookup"><span data-stu-id="f3837-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f3837-186">Volg de aanwijzingen om de gebruikersnaam, het wachtwoord en meer in te stellen.</span><span class="sxs-lookup"><span data-stu-id="f3837-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f3837-187">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="f3837-187">Run using development server</span></span>
<span data-ttu-id="f3837-188">Druk op F5 om de foutopsporing te starten. Uw webbrowser wordt automatisch geopend op de pagina die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3837-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="f3837-189">U kunt onderbrekingspunten instellen in de bronnen, de vensters Controle gebruiken, enzovoort. Zie de [Documentatie bij Python Tools for Visual Studio] voor meer informatie over de verschillende functies.</span><span class="sxs-lookup"><span data-stu-id="f3837-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="f3837-190">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="f3837-190">Make changes</span></span>
<span data-ttu-id="f3837-191">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f3837-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="f3837-192">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="f3837-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="f3837-193">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="f3837-193">Install more packages</span></span>
<span data-ttu-id="f3837-194">Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.</span><span class="sxs-lookup"><span data-stu-id="f3837-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f3837-195">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="f3837-195">You can install additional packages using pip.</span></span> <span data-ttu-id="f3837-196">Als u een pakket wilt installeren, klikt u met de rechtermuisknop op de virtuele omgeving en selecteert u **Python-pakket installeren**.</span><span class="sxs-lookup"><span data-stu-id="f3837-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="f3837-197">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u `azure`:</span><span class="sxs-lookup"><span data-stu-id="f3837-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="f3837-198">Klik met de rechtermuisknop op de virtuele omgeving en selecteer **requirements.txt genereren** om requirements.txt bij te werken.</span><span class="sxs-lookup"><span data-stu-id="f3837-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="f3837-199">Voer vervolgens de wijzigingen aan requirements.txt door in de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f3837-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="f3837-200">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f3837-200">Deploy to Azure</span></span>
<span data-ttu-id="f3837-201">Als u een implementatie wilt activeren, klikt u op **Synchroniseren** of **Pushen**.</span><span class="sxs-lookup"><span data-stu-id="f3837-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="f3837-202">Bij een synchronisatie vinden er push- en pullbewerkingen plaats.</span><span class="sxs-lookup"><span data-stu-id="f3837-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="f3837-203">De eerste implementatie duurt langer dan normaal omdat er een virtuele omgeving wordt gemaakt, er pakketten worden geïnstalleerd en meer.</span><span class="sxs-lookup"><span data-stu-id="f3837-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="f3837-204">De voortgang van de implementatie wordt niet weergegeven in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3837-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="f3837-205">Als u de uitvoer wilt controleren, raadpleegt u het gedeelte [Probleemoplossing - Implementatie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="f3837-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="f3837-206">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f3837-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="f3837-207">Ontwikkeling van web-apps - Windows - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="f3837-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="f3837-208">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="f3837-208">Clone the repository</span></span>
<span data-ttu-id="f3837-209">Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe.</span><span class="sxs-lookup"><span data-stu-id="f3837-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="f3837-210">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f3837-211">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="f3837-211">Create virtual environment</span></span>
<span data-ttu-id="f3837-212">U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="f3837-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="f3837-213">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.</span><span class="sxs-lookup"><span data-stu-id="f3837-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="f3837-214">Zorg ervoor dat u dezelfde versie van Python gebruikt die is geselecteerd voor uw web-app (in runtime.txt of op de blade Toepassingsinstellingen van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="f3837-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="f3837-215">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f3837-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="f3837-216">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f3837-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="f3837-217">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="f3837-217">Install any external packages required by your application.</span></span> <span data-ttu-id="f3837-218">U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="f3837-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f3837-219">Een beheerder maken</span><span class="sxs-lookup"><span data-stu-id="f3837-219">Create a superuser</span></span>
<span data-ttu-id="f3837-220">Voor de database die deel uitmaakt van de toepassing, is geen beheerder opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f3837-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="f3837-221">Als u gebruik wilt maken van de aanmeldfunctionaliteit in de toepassing of van de Django-beheerinterface (als u besluit deze in te schakelen), moet u een beheerder maken.</span><span class="sxs-lookup"><span data-stu-id="f3837-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="f3837-222">Voer dit uit vanaf de opdrachtregel van de projectmap:</span><span class="sxs-lookup"><span data-stu-id="f3837-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f3837-223">Volg de aanwijzingen om de gebruikersnaam, het wachtwoord en meer in te stellen.</span><span class="sxs-lookup"><span data-stu-id="f3837-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f3837-224">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="f3837-224">Run using development server</span></span>
<span data-ttu-id="f3837-225">U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3837-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="f3837-226">In de console worden de URL en de poort vermeld waarnaar de server luistert:</span><span class="sxs-lookup"><span data-stu-id="f3837-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="f3837-227">Open de betreffende URL in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="f3837-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f3837-228">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="f3837-228">Make changes</span></span>
<span data-ttu-id="f3837-229">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f3837-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="f3837-230">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="f3837-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f3837-231">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="f3837-231">Install more packages</span></span>
<span data-ttu-id="f3837-232">Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.</span><span class="sxs-lookup"><span data-stu-id="f3837-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f3837-233">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="f3837-233">You can install additional packages using pip.</span></span> <span data-ttu-id="f3837-234">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:</span><span class="sxs-lookup"><span data-stu-id="f3837-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="f3837-235">Zorg ervoor dat u requirements.txt bijwerkt:</span><span class="sxs-lookup"><span data-stu-id="f3837-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="f3837-236">Voer de wijzigingen door:</span><span class="sxs-lookup"><span data-stu-id="f3837-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="f3837-237">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f3837-237">Deploy to Azure</span></span>
<span data-ttu-id="f3837-238">Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:</span><span class="sxs-lookup"><span data-stu-id="f3837-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="f3837-239">U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.</span><span class="sxs-lookup"><span data-stu-id="f3837-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f3837-240">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f3837-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="f3837-241">Ontwikkeling van web-apps - Mac/Linux - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="f3837-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="f3837-242">De opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="f3837-242">Clone the repository</span></span>
<span data-ttu-id="f3837-243">Kloon eerst de opslagplaats via de URL die is opgegeven in de Azure Portal. Voeg daarna de Azure-opslagplaats extern toe.</span><span class="sxs-lookup"><span data-stu-id="f3837-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="f3837-244">Zie [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md) (Lokale Git-implementatie naar Azure App Service) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f3837-245">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="f3837-245">Create virtual environment</span></span>
<span data-ttu-id="f3837-246">U maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (voeg deze niet toe aan de opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="f3837-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="f3837-247">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die aan de toepassing werkt, maakt een eigen lokale versie.</span><span class="sxs-lookup"><span data-stu-id="f3837-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="f3837-248">Zorg ervoor dat u dezelfde versie van Python gebruikt die is geselecteerd voor uw web-app (in runtime.txt of op de blade Toepassingsinstellingen van uw web-app in de Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="f3837-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="f3837-249">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="f3837-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="f3837-250">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="f3837-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="f3837-251">of</span><span class="sxs-lookup"><span data-stu-id="f3837-251">or</span></span>

    pyvenv env

<span data-ttu-id="f3837-252">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="f3837-252">Install any external packages required by your application.</span></span> <span data-ttu-id="f3837-253">U kunt het bestand requirements.txt in de hoofdmap van de opslagplaats gebruiken voor het installeren van de pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="f3837-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f3837-254">Een beheerder maken</span><span class="sxs-lookup"><span data-stu-id="f3837-254">Create a superuser</span></span>
<span data-ttu-id="f3837-255">Voor de database die deel uitmaakt van de toepassing, is geen beheerder opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f3837-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="f3837-256">Als u gebruik wilt maken van de aanmeldfunctionaliteit in de toepassing of van de Django-beheerinterface (als u besluit deze in te schakelen), moet u een beheerder maken.</span><span class="sxs-lookup"><span data-stu-id="f3837-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="f3837-257">Voer dit uit vanaf de opdrachtregel van de projectmap:</span><span class="sxs-lookup"><span data-stu-id="f3837-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="f3837-258">Volg de aanwijzingen om de gebruikersnaam, het wachtwoord en meer in te stellen.</span><span class="sxs-lookup"><span data-stu-id="f3837-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f3837-259">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="f3837-259">Run using development server</span></span>
<span data-ttu-id="f3837-260">U kunt de toepassing op een ontwikkelaarsserver starten aan de hand van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f3837-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="f3837-261">In de console worden de URL en de poort vermeld waarnaar de server luistert:</span><span class="sxs-lookup"><span data-stu-id="f3837-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="f3837-262">Open de betreffende URL in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="f3837-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f3837-263">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="f3837-263">Make changes</span></span>
<span data-ttu-id="f3837-264">U kunt nu experimenteren door wijzigingen aan te brengen aan de toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="f3837-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="f3837-265">Nadat u uw wijzigingen hebt getest, kunt u ze in de Git-opslagplaats vastleggen:</span><span class="sxs-lookup"><span data-stu-id="f3837-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f3837-266">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="f3837-266">Install more packages</span></span>
<span data-ttu-id="f3837-267">Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.</span><span class="sxs-lookup"><span data-stu-id="f3837-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f3837-268">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="f3837-268">You can install additional packages using pip.</span></span> <span data-ttu-id="f3837-269">Als u bijvoorbeeld de Azure SDK voor Python wilt installeren, waarmee u toegang krijgt tot Azure Storage, Service Bus en andere Azure-services, typt u:</span><span class="sxs-lookup"><span data-stu-id="f3837-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="f3837-270">Zorg ervoor dat u requirements.txt bijwerkt:</span><span class="sxs-lookup"><span data-stu-id="f3837-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="f3837-271">Voer de wijzigingen door:</span><span class="sxs-lookup"><span data-stu-id="f3837-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="f3837-272">Implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="f3837-272">Deploy to Azure</span></span>
<span data-ttu-id="f3837-273">Als u een implementatie wilt starten, pusht u de wijzigingen naar Azure:</span><span class="sxs-lookup"><span data-stu-id="f3837-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="f3837-274">U ziet de uitvoer van het script voor implementatie, inclusief de uitvoer van het maken van de virtuele omgeving, het installeren van pakketten, het maken van web.config en meer.</span><span class="sxs-lookup"><span data-stu-id="f3837-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f3837-275">Blader naar de Azure-URL om uw wijzigingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f3837-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="f3837-276">Probleemoplossing - Installatie van pakketten</span><span class="sxs-lookup"><span data-stu-id="f3837-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="f3837-277">Probleemoplossing - Virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="f3837-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="f3837-278">Probleemoplossing - Statische bestanden</span><span class="sxs-lookup"><span data-stu-id="f3837-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="f3837-279">Voor Django wordt het concept van het verzamelen van statische bestanden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3837-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="f3837-280">Hierbij worden alle statische bestanden vanuit hun oorspronkelijke locatie gekopieerd naar één map.</span><span class="sxs-lookup"><span data-stu-id="f3837-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="f3837-281">Voor deze toepassing worden ze gekopieerd naar `/static`.</span><span class="sxs-lookup"><span data-stu-id="f3837-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="f3837-282">Dit gebeurt omdat statische bestanden mogelijk afkomstig zijn van andere Django-apps.</span><span class="sxs-lookup"><span data-stu-id="f3837-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="f3837-283">De statische bestanden van Django-beheerinterfaces bevinden zich bijvoorbeeld in een Django-bibliotheeksubmap in de virtuele omgeving.</span><span class="sxs-lookup"><span data-stu-id="f3837-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="f3837-284">De statische bestanden die door deze toepassing worden gedefinieerd, bevinden zich in `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="f3837-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="f3837-285">Als u meer Django-apps gebruikt, staan er op meerdere plaatsen statische bestanden.</span><span class="sxs-lookup"><span data-stu-id="f3837-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="f3837-286">Wanneer de toepassing wordt uitgevoerd in de foutopsporingsmodus, gebruikt de toepassing de statische bestanden van de oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="f3837-287">Wanneer de toepassing wordt uitgevoerd in de releasemodus, maakt de toepassing **geen** gebruik van de statische bestanden.</span><span class="sxs-lookup"><span data-stu-id="f3837-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="f3837-288">Het is de verantwoordelijkheid van de webserver om de bestanden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3837-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="f3837-289">Voor deze toepassing gebruikt IIS de statische bestanden van `/static`.</span><span class="sxs-lookup"><span data-stu-id="f3837-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="f3837-290">De statische bestanden worden automatisch verzameld als onderdeel van het implementatiescript. Eerder verzamelde bestanden worden gewist.</span><span class="sxs-lookup"><span data-stu-id="f3837-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="f3837-291">Dit betekent dat de verzameling plaatsvindt bij elke implementatie. Hierdoor duurt het implementatieproces langer, maar zijn verouderde bestanden niet beschikbaar. Dat voorkomt potentiële beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="f3837-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="f3837-292">Als u het verzamelen van statische bestanden voor uw Django-toepassing wilt overslaan:</span><span class="sxs-lookup"><span data-stu-id="f3837-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="f3837-293">U moet het verzamelen dan handmatig uitvoeren op uw lokale machine:</span><span class="sxs-lookup"><span data-stu-id="f3837-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="f3837-294">Verwijder de map `\static` uit `.gitignore` en voeg deze toe aan de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f3837-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="f3837-295">Probleemoplossing - Instellingen</span><span class="sxs-lookup"><span data-stu-id="f3837-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="f3837-296">Diverse instellingen voor de toepassing kunnen worden gewijzigd in `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="f3837-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="f3837-297">Voor het gemak van ontwikkelaars is de foutopsporingsmodus ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f3837-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="f3837-298">Een handige bijkomstigheid is dat u bij lokale uitvoering afbeeldingen en andere statische inhoud kunt zien zonder dat er statische bestanden hoeven te worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="f3837-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="f3837-299">De foutopsporingsmodus uitschakelen:</span><span class="sxs-lookup"><span data-stu-id="f3837-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="f3837-300">Wanneer foutopsporing is uitgeschakeld, moet de waarde voor `ALLOWED_HOSTS` worden bijgewerkt met de naam van de Azure-host.</span><span class="sxs-lookup"><span data-stu-id="f3837-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="f3837-301">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f3837-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="f3837-302">of als u deze wilt inschakelen:</span><span class="sxs-lookup"><span data-stu-id="f3837-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="f3837-303">In de praktijk wilt u mogelijk iets ingewikkelders doen om te schakelen tussen de foutopsporingsmodus en de releasemodus, en om de hostnaam op te halen.</span><span class="sxs-lookup"><span data-stu-id="f3837-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="f3837-304">U kunt de omgevingsvariabelen instellen via de pagina **CONFIGUREREN** van de Azure Portal. Ga daar naar het gedeelte **App-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="f3837-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="f3837-305">Dit kan handig zijn om waarden in te stellen waarvan u wilt dat ze niet worden weergegeven in de bronnen (verbindingsreeksen, wachtwoorden, enzovoort) en die u anders wilt instellen voor Azure en uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f3837-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="f3837-306">In `settings.py` kunt u met `os.getenv` een query indienen voor de omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="f3837-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="f3837-307">Een database gebruiken</span><span class="sxs-lookup"><span data-stu-id="f3837-307">Using a Database</span></span>
<span data-ttu-id="f3837-308">De database die is opgenomen in de toepassing, is een SQLite-database.</span><span class="sxs-lookup"><span data-stu-id="f3837-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="f3837-309">Dit is een handige en nuttige standaarddatabase die u kunt gebruiken voor ontwikkeling, omdat er vrijwel geen configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="f3837-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="f3837-310">De database is opgeslagen in het bestand db.sqlite3 in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="f3837-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="f3837-311">Azure biedt databaseservices die eenvoudig te gebruiken zijn vanuit een Django-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f3837-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="f3837-312">In de zelfstudies voor het gebruik van [SQL Database] en [MySQL] via een Django-toepassing ziet u de stappen die nodig zijn om de databaseservice te maken en om de database-instellingen te wijzigen in `DjangoWebProject/settings.py`. U ziet er ook welke bibliotheken er moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f3837-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="f3837-313">Als u liever uw eigen databaseservers beheert, kunt u dat doen via virtuele Windows- of Linux-machines die in Azure worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3837-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="f3837-314">Django-beheerinterface</span><span class="sxs-lookup"><span data-stu-id="f3837-314">Django Admin Interface</span></span>
<span data-ttu-id="f3837-315">Wanneer u begint met het bouwen van modellen, moet u de database vullen met gegevens.</span><span class="sxs-lookup"><span data-stu-id="f3837-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="f3837-316">U kunt eenvoudig inhoud toevoegen en interactief bewerken door de Django-beheerinterface te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3837-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="f3837-317">De code voor de beheerinterface is als opmerking opgenomen in de toepassingsbronnen. Omdat de code duidelijk is gemarkeerd, kunt u deze eenvoudig inschakelen (zoek naar 'admin').</span><span class="sxs-lookup"><span data-stu-id="f3837-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="f3837-318">Wanneer de code is ingeschakeld, synchroniseert u de database, voert u de toepassing uit en navigeert u naar `/admin`.</span><span class="sxs-lookup"><span data-stu-id="f3837-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3837-319">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3837-319">Next Steps</span></span>
<span data-ttu-id="f3837-320">Volg deze koppelingen voor meer informatie over Django en Python Tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f3837-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="f3837-321">[Documentatie bij Django]</span><span class="sxs-lookup"><span data-stu-id="f3837-321">[Django Documentation]</span></span>
* <span data-ttu-id="f3837-322">[Documentatie bij Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f3837-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="f3837-323">Voor informatie over het gebruik van SQL Database en MySQL:</span><span class="sxs-lookup"><span data-stu-id="f3837-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="f3837-324">[Django en MySQL in Azure met Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f3837-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="f3837-325">[Django en SQL Database in Azure met Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f3837-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="f3837-326">Raadpleeg het [Python Developer Center](/develop/python/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f3837-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f3837-327">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="f3837-327">What's changed</span></span>
* <span data-ttu-id="f3837-328">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f3837-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django en MySQL in Azure met Python Tools for Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django en SQL Database in Azure met Python Tools for Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
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
[Documentatie bij Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Documentatie bij Django]: https://www.djangoproject.com/
