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
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="6e03c-103">Web-apps maken met Django in Azure</span><span class="sxs-lookup"><span data-stu-id="6e03c-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="6e03c-104">Deze zelfstudie wordt beschreven hoe tooget gestart Python uitvoert in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="6e03c-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="6e03c-105">Web Apps biedt beperkte gratis hosting en snelle implementatie. Bovendien kunt u Python gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6e03c-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="6e03c-106">Als uw app groeit, kunt u schakelen toopaid die als host fungeert, en u ook met alle integreren kunt Hallo andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="6e03c-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="6e03c-107">U maakt een toepassing met Hallo Django-webframework (Zie andere versies van deze zelfstudie voor [Flask](web-sites-python-create-deploy-flask-app.md) en [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="6e03c-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="6e03c-108">U wordt Hallo web-app maken vanuit Azure Marketplace hello, instellen van Git-implementatie en lokaal Hallo opslagplaats klonen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="6e03c-109">Vervolgens wordt Hallo toepassing lokaal uitvoeren, wijzigingen aanbrengen, doorvoeren en push ze tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6e03c-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="6e03c-110">zelfstudie ziet hoe Hallo toodo dit van Windows of Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="6e03c-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="6e03c-111">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="6e03c-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6e03c-112">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6e03c-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6e03c-113">Prerequisites</span></span>
* <span data-ttu-id="6e03c-114">Windows, Mac of Linux</span><span class="sxs-lookup"><span data-stu-id="6e03c-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="6e03c-115">Python 2.7 of 3.4</span><span class="sxs-lookup"><span data-stu-id="6e03c-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="6e03c-116">setuptools, pip, virtualenv (alleen Python 2.7)</span><span class="sxs-lookup"><span data-stu-id="6e03c-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="6e03c-117">Git</span><span class="sxs-lookup"><span data-stu-id="6e03c-117">Git</span></span>
* <span data-ttu-id="6e03c-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Opmerking: dit is optioneel</span><span class="sxs-lookup"><span data-stu-id="6e03c-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="6e03c-119">**Opmerking**: TFS-publicatie wordt momenteel niet ondersteund voor Python-projecten.</span><span class="sxs-lookup"><span data-stu-id="6e03c-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="6e03c-120">Windows</span><span class="sxs-lookup"><span data-stu-id="6e03c-120">Windows</span></span>
<span data-ttu-id="6e03c-121">Als u Python 2.7 of 3.4 nog niet hebt geïnstalleerd (32-bits), wordt aangeraden om de [Azure SDK voor Python 2.7] of de [Azure SDK voor Python 3.4] te installeren via het webplatforminstallatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="6e03c-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="6e03c-122">Hiermee installeert u Hallo 32-bits versie van Python, setuptools, pip, virtualenv, enzovoort (32-bits Python is wat wordt geïnstalleerd op Hallo Azure-hostmachines).</span><span class="sxs-lookup"><span data-stu-id="6e03c-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="6e03c-123">U kunt Python ook downloaden via [python.org].</span><span class="sxs-lookup"><span data-stu-id="6e03c-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="6e03c-124">Voor Git wordt [Git voor Windows] of [GitHub voor Windows] aangeraden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="6e03c-125">Als u Visual Studio gebruikt, kunt u Hallo geïntegreerde Git-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="6e03c-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="6e03c-126">Het wordt ook aangeraden om [Python Tools 2.2 for Visual Studio] te installeren.</span><span class="sxs-lookup"><span data-stu-id="6e03c-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="6e03c-127">Dit is optioneel, maar als u [Visual Studio], met inbegrip van Hallo gratis Visual Studio Community 2013 of Visual Studio Express 2013 voor Web en Hiermee krijgt u een uitstekende Python IDE.</span><span class="sxs-lookup"><span data-stu-id="6e03c-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="6e03c-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="6e03c-128">Mac/Linux</span></span>
<span data-ttu-id="6e03c-129">Python en Git moeten al zijn geïnstalleerd, maar zorg ervoor dat u beschikt over Python 2.7 of 3.4.</span><span class="sxs-lookup"><span data-stu-id="6e03c-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="6e03c-130">Web-apps maken via de portal</span><span class="sxs-lookup"><span data-stu-id="6e03c-130">Web App Creation on Portal</span></span>
<span data-ttu-id="6e03c-131">Hallo eerste stap bij het maken van uw app is toocreate Hallo web-app via Hallo [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6e03c-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="6e03c-132">Meld u aan bij hello Azure-Portal en klikt u op Hallo **nieuw** knop in de linkeronderhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e03c-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="6e03c-133">Typ in Hallo zoekvak 'python'.</span><span class="sxs-lookup"><span data-stu-id="6e03c-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="6e03c-134">Selecteer in de zoekresultaten hello, **Django** (gepubliceerd door PTVS), klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6e03c-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="6e03c-135">Hallo nieuwe Django-app, zoals het maken van een nieuw App Service-plan en een nieuwe resourcegroep voor configureren.</span><span class="sxs-lookup"><span data-stu-id="6e03c-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="6e03c-136">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="6e03c-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="6e03c-137">Configureer Git-publicatie voor uw nieuwe web-app met behulp Hallo-instructies in [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6e03c-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="6e03c-138">Toepassingsoverzicht</span><span class="sxs-lookup"><span data-stu-id="6e03c-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="6e03c-139">Inhoud van Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="6e03c-139">Git repository contents</span></span>
<span data-ttu-id="6e03c-140">Hier volgt een overzicht van Hallo bestanden vindt u in Hallo eerste Git-opslagplaats, die we in de volgende sectie Hallo gaat klonen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

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

<span data-ttu-id="6e03c-141">Belangrijkste bronnen voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e03c-141">Main sources for hello application.</span></span> <span data-ttu-id="6e03c-142">Bestaat uit 3 pagina's (index, over, contact) met een modelindeling.</span><span class="sxs-lookup"><span data-stu-id="6e03c-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="6e03c-143">Statische inhoud en scripts bevatten bootstrap, jquery, modernizr en respond.</span><span class="sxs-lookup"><span data-stu-id="6e03c-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="6e03c-144">Lokaal beheer en ondersteuning voor de ontwikkelaarsserver.</span><span class="sxs-lookup"><span data-stu-id="6e03c-144">Local management and development server support.</span></span> <span data-ttu-id="6e03c-145">Deze toorun Hallo-toepassing lokaal gebruiken, synchroniseren Hallo-database, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6e03c-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="6e03c-146">Standaarddatabase.</span><span class="sxs-lookup"><span data-stu-id="6e03c-146">Default database.</span></span> <span data-ttu-id="6e03c-147">Bevat de benodigde tabellen voor Hallo toepassing toorun hello, maar bevat geen gebruikers (Synchroniseer Hallo database toocreate een gebruiker).</span><span class="sxs-lookup"><span data-stu-id="6e03c-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="6e03c-148">Projectbestanden voor gebruik met [Python Tools for Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6e03c-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="6e03c-149">IIS-proxy voor virtuele omgevingen en ondersteuning voor externe PTVS-foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="6e03c-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="6e03c-150">Externe pakketten nodig voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e03c-150">External packages needed by this application.</span></span> <span data-ttu-id="6e03c-151">Hallo-implementatiescript wordt een pip installatie hello-pakketten die worden vermeld in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="6e03c-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="6e03c-152">IIS-configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-152">IIS configuration files.</span></span> <span data-ttu-id="6e03c-153">Hallo-implementatiescript gebruikt Hallo juiste web.x.y.config en kopieert deze als web.config.</span><span class="sxs-lookup"><span data-stu-id="6e03c-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="6e03c-154">Optionele bestanden - implementatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="6e03c-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="6e03c-155">Optionele bestanden - Python-runtime</span><span class="sxs-lookup"><span data-stu-id="6e03c-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="6e03c-156">Aanvullende bestanden op server</span><span class="sxs-lookup"><span data-stu-id="6e03c-156">Additional files on server</span></span>
<span data-ttu-id="6e03c-157">Bepaalde bestanden bestaan op Hallo server maar toohello git-opslagplaats niet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6e03c-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="6e03c-158">Deze worden gemaakt door het implementatiescript Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e03c-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="6e03c-159">IIS-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="6e03c-159">IIS configuration file.</span></span> <span data-ttu-id="6e03c-160">Gemaakt op basis van web.x.y.config voor elke implementatie.</span><span class="sxs-lookup"><span data-stu-id="6e03c-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="6e03c-161">Virtuele Python-omgeving.</span><span class="sxs-lookup"><span data-stu-id="6e03c-161">Python virtual environment.</span></span> <span data-ttu-id="6e03c-162">Gemaakt tijdens de implementatie als een compatibele virtuele omgeving op Hallo web-app nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6e03c-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="6e03c-163">Pakketten die worden vermeld in requirements.txt worden via pip geïnstalleerd, maar pip slaat de installatie over als hello-pakketten zijn al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6e03c-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="6e03c-164">Hallo naast 3 gedeelten wordt beschreven hoe tooproceed Hello web-app-ontwikkeling onder 3 verschillende omgevingen:</span><span class="sxs-lookup"><span data-stu-id="6e03c-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="6e03c-165">Windows, met Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e03c-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="6e03c-166">Windows, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6e03c-166">Windows, with command line</span></span>
* <span data-ttu-id="6e03c-167">Mac/Linux, met opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6e03c-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="6e03c-168">Ontwikkeling van web-apps - Windows - Python Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e03c-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="6e03c-169">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="6e03c-169">Clone hello repository</span></span>
<span data-ttu-id="6e03c-170">Kloon eerst Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="6e03c-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="6e03c-171">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6e03c-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="6e03c-172">Open Hallo oplossingsbestand (.sln) die is opgenomen in de hoofdmap Hallo van Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6e03c-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="6e03c-173">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="6e03c-173">Create virtual environment</span></span>
<span data-ttu-id="6e03c-174">U maakt nu een virtuele omgeving voor lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="6e03c-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="6e03c-175">Klik met de rechtermuisknop op **Python-omgevingen** en selecteer **Virtuele omgeving toevoegen...**.</span><span class="sxs-lookup"><span data-stu-id="6e03c-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="6e03c-176">Zorg ervoor dat het Hallo-naam van het Hallo-omgeving is `env`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="6e03c-177">Selecteer de basisinterpreter Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e03c-177">Select hello base interpreter.</span></span> <span data-ttu-id="6e03c-178">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of op Hallo **toepassingsinstellingen** blade van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="6e03c-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="6e03c-179">Zorg ervoor dat de optie hello-pakketten toodownload en installatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e03c-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="6e03c-180">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e03c-180">Click **Create**.</span></span> <span data-ttu-id="6e03c-181">Dit wordt Hallo virtuele omgeving maken, en worden alle afhankelijkheden uit requirements.txt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="6e03c-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="6e03c-182">Een beheerder maken</span><span class="sxs-lookup"><span data-stu-id="6e03c-182">Create a superuser</span></span>
<span data-ttu-id="6e03c-183">Hallo-database die deel uitmaakt van de toepassing hello heeft geen beheerder opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6e03c-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="6e03c-184">In de volgorde toouse Hallo aanmelden functionaliteit van de toepassing hello of Hallo Django-beheerinterface (als u tooenable besluit het), moet u een beheerder toocreate.</span><span class="sxs-lookup"><span data-stu-id="6e03c-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="6e03c-185">Voer dit uit vanaf Hallo opdrachtregel van de projectmap:</span><span class="sxs-lookup"><span data-stu-id="6e03c-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="6e03c-186">Ga als volgt Hallo prompts tooset Hallo-gebruikersnaam, wachtwoord, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6e03c-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6e03c-187">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="6e03c-187">Run using development server</span></span>
<span data-ttu-id="6e03c-188">Druk op F5 toostart foutopsporing en uw webbrowser wordt automatisch geopend toohello pagina die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e03c-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="6e03c-189">U kunt onderbrekingspunten instellen in het Hallo-bronnen, gebruik Hallo vensters, enzovoort. Zie Hallo [Python-Tools voor Visual Studio-documentatie] Hallo voor meer informatie over de verschillende functies.</span><span class="sxs-lookup"><span data-stu-id="6e03c-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="6e03c-190">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="6e03c-190">Make changes</span></span>
<span data-ttu-id="6e03c-191">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="6e03c-192">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="6e03c-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="6e03c-193">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="6e03c-193">Install more packages</span></span>
<span data-ttu-id="6e03c-194">Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.</span><span class="sxs-lookup"><span data-stu-id="6e03c-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="6e03c-195">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="6e03c-195">You can install additional packages using pip.</span></span> <span data-ttu-id="6e03c-196">tooinstall een pakket met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="6e03c-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="6e03c-197">Bijvoorbeeld: tooinstall hello Azure SDK voor Python, die u hebt u toegang tooAzure storage, servicebus en andere Azure-services, voer `azure`:</span><span class="sxs-lookup"><span data-stu-id="6e03c-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="6e03c-198">Met de rechtermuisknop op de virtuele omgeving Hallo en selecteer **requirements.txt genereren** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="6e03c-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="6e03c-199">Voer vervolgens Hallo wijzigingen toorequirements.txt toohello Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6e03c-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="6e03c-200">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="6e03c-200">Deploy tooAzure</span></span>
<span data-ttu-id="6e03c-201">tootrigger een implementatie, klikt u op **Sync** of **Push**.</span><span class="sxs-lookup"><span data-stu-id="6e03c-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="6e03c-202">Bij een synchronisatie vinden er push- en pullbewerkingen plaats.</span><span class="sxs-lookup"><span data-stu-id="6e03c-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="6e03c-203">Hallo eerste implementatie duurt enige tijd als deze, u een virtuele omgeving, pakketten worden geïnstalleerd, enzovoort maakt wordt.</span><span class="sxs-lookup"><span data-stu-id="6e03c-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="6e03c-204">Visual Studio weergeven niet Hallo voortgang van Hallo implementatie.</span><span class="sxs-lookup"><span data-stu-id="6e03c-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="6e03c-205">Als u tooreview Hallo uitvoer dat wilt, raadpleegt u Hallo sectie op [probleemoplossing - implementatie](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="6e03c-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="6e03c-206">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="6e03c-207">Ontwikkeling van web-apps - Windows - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6e03c-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="6e03c-208">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="6e03c-208">Clone hello repository</span></span>
<span data-ttu-id="6e03c-209">Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe.</span><span class="sxs-lookup"><span data-stu-id="6e03c-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="6e03c-210">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6e03c-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="6e03c-211">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="6e03c-211">Create virtual environment</span></span>
<span data-ttu-id="6e03c-212">Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="6e03c-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="6e03c-213">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.</span><span class="sxs-lookup"><span data-stu-id="6e03c-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="6e03c-214">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of Hallo blade toepassingsinstellingen van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="6e03c-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="6e03c-215">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6e03c-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="6e03c-216">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6e03c-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="6e03c-217">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="6e03c-217">Install any external packages required by your application.</span></span> <span data-ttu-id="6e03c-218">U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="6e03c-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="6e03c-219">Een beheerder maken</span><span class="sxs-lookup"><span data-stu-id="6e03c-219">Create a superuser</span></span>
<span data-ttu-id="6e03c-220">Hallo-database die deel uitmaakt van de toepassing hello heeft geen beheerder opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6e03c-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="6e03c-221">In de volgorde toouse Hallo aanmelden functionaliteit van de toepassing hello of Hallo Django-beheerinterface (als u tooenable besluit het), moet u een beheerder toocreate.</span><span class="sxs-lookup"><span data-stu-id="6e03c-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="6e03c-222">Voer dit uit vanaf Hallo opdrachtregel van de projectmap:</span><span class="sxs-lookup"><span data-stu-id="6e03c-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="6e03c-223">Ga als volgt Hallo prompts tooset Hallo-gebruikersnaam, wachtwoord, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6e03c-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6e03c-224">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="6e03c-224">Run using development server</span></span>
<span data-ttu-id="6e03c-225">U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e03c-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="6e03c-226">Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:</span><span class="sxs-lookup"><span data-stu-id="6e03c-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="6e03c-227">Open vervolgens de URL van web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="6e03c-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="6e03c-228">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="6e03c-228">Make changes</span></span>
<span data-ttu-id="6e03c-229">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="6e03c-230">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="6e03c-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6e03c-231">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="6e03c-231">Install more packages</span></span>
<span data-ttu-id="6e03c-232">Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.</span><span class="sxs-lookup"><span data-stu-id="6e03c-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="6e03c-233">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="6e03c-233">You can install additional packages using pip.</span></span> <span data-ttu-id="6e03c-234">Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:</span><span class="sxs-lookup"><span data-stu-id="6e03c-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="6e03c-235">Zorg ervoor dat tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="6e03c-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="6e03c-236">Hallo wijzigingen doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="6e03c-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="6e03c-237">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="6e03c-237">Deploy tooAzure</span></span>
<span data-ttu-id="6e03c-238">een implementatie tootrigger, push Hallo verandert tooAzure:</span><span class="sxs-lookup"><span data-stu-id="6e03c-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="6e03c-239">Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.</span><span class="sxs-lookup"><span data-stu-id="6e03c-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6e03c-240">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="6e03c-241">Ontwikkeling van web-apps - Mac/Linux - opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6e03c-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="6e03c-242">Hallo-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="6e03c-242">Clone hello repository</span></span>
<span data-ttu-id="6e03c-243">Eerst kloon Hallo-opslagplaats met Hallo-URL opgegeven op Hallo Azure-Portal en hello Azure-opslagplaats toevoegen als een externe.</span><span class="sxs-lookup"><span data-stu-id="6e03c-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="6e03c-244">Zie voor meer informatie [lokale Git-implementatie tooAzure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="6e03c-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="6e03c-245">Een virtuele omgeving maken</span><span class="sxs-lookup"><span data-stu-id="6e03c-245">Create virtual environment</span></span>
<span data-ttu-id="6e03c-246">Maakt een nieuwe virtuele omgeving voor ontwikkelingsdoeleinden (Voeg deze niet toohello opslagplaats).</span><span class="sxs-lookup"><span data-stu-id="6e03c-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="6e03c-247">Virtuele omgevingen in Python kunnen niet worden verplaatst, dus elke ontwikkelaar die werkt op Hallo toepassing hun eigen lokaal maken moet.</span><span class="sxs-lookup"><span data-stu-id="6e03c-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="6e03c-248">Zorg ervoor dat toouse Hallo dezelfde versie van Python die is geselecteerd voor uw web-app (in runtime.txt of Hallo blade toepassingsinstellingen van uw web-app in Azure Portal Hallo).</span><span class="sxs-lookup"><span data-stu-id="6e03c-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="6e03c-249">Voor Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="6e03c-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="6e03c-250">Voor Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="6e03c-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="6e03c-251">of</span><span class="sxs-lookup"><span data-stu-id="6e03c-251">or</span></span>

    pyvenv env

<span data-ttu-id="6e03c-252">Installeer alle externe pakketten die voor uw toepassing vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="6e03c-252">Install any external packages required by your application.</span></span> <span data-ttu-id="6e03c-253">U kunt Hallo requirements.txt bestand in de hoofdmap Hallo Hallo opslagplaats tooinstall hello-pakketten in de virtuele omgeving:</span><span class="sxs-lookup"><span data-stu-id="6e03c-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="6e03c-254">Een beheerder maken</span><span class="sxs-lookup"><span data-stu-id="6e03c-254">Create a superuser</span></span>
<span data-ttu-id="6e03c-255">Hallo-database die deel uitmaakt van de toepassing hello heeft geen beheerder opgegeven.</span><span class="sxs-lookup"><span data-stu-id="6e03c-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="6e03c-256">In de volgorde toouse Hallo aanmelden functionaliteit van de toepassing hello of Hallo Django-beheerinterface (als u tooenable besluit het), moet u een beheerder toocreate.</span><span class="sxs-lookup"><span data-stu-id="6e03c-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="6e03c-257">Voer dit uit vanaf Hallo opdrachtregel van de projectmap:</span><span class="sxs-lookup"><span data-stu-id="6e03c-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="6e03c-258">Ga als volgt Hallo prompts tooset Hallo-gebruikersnaam, wachtwoord, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6e03c-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="6e03c-259">Uitvoeren met behulp van de ontwikkelaarsserver</span><span class="sxs-lookup"><span data-stu-id="6e03c-259">Run using development server</span></span>
<span data-ttu-id="6e03c-260">U kunt Hallo toepassing op een ontwikkelaarsserver starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="6e03c-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="6e03c-261">Hallo console Hallo-URL wordt weergegeven en poort Hallo server luistert naar:</span><span class="sxs-lookup"><span data-stu-id="6e03c-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="6e03c-262">Open vervolgens de URL van web browser toothat.</span><span class="sxs-lookup"><span data-stu-id="6e03c-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="6e03c-263">Wijzigingen aanbrengen</span><span class="sxs-lookup"><span data-stu-id="6e03c-263">Make changes</span></span>
<span data-ttu-id="6e03c-264">U kunt nu experimenteren door wijzigingen toohello toepassingsbronnen en/of sjablonen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="6e03c-265">Nadat u uw wijzigingen hebt getest, ze doorvoeren toohello Git-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="6e03c-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="6e03c-266">Meer pakketten installeren</span><span class="sxs-lookup"><span data-stu-id="6e03c-266">Install more packages</span></span>
<span data-ttu-id="6e03c-267">Uw toepassing bevat mogelijk afhankelijkheden buiten Python en Django.</span><span class="sxs-lookup"><span data-stu-id="6e03c-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="6e03c-268">U kunt extra pakketten installeren via PIP.</span><span class="sxs-lookup"><span data-stu-id="6e03c-268">You can install additional packages using pip.</span></span> <span data-ttu-id="6e03c-269">Bijvoorbeeld tooinstall hello Azure SDK voor Python, waarmee u toegang krijgen tot tooAzure storage, servicebus en andere Azure-services, type:</span><span class="sxs-lookup"><span data-stu-id="6e03c-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="6e03c-270">Zorg ervoor dat tooupdate requirements.txt:</span><span class="sxs-lookup"><span data-stu-id="6e03c-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="6e03c-271">Hallo wijzigingen doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="6e03c-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="6e03c-272">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="6e03c-272">Deploy tooAzure</span></span>
<span data-ttu-id="6e03c-273">een implementatie tootrigger, push Hallo verandert tooAzure:</span><span class="sxs-lookup"><span data-stu-id="6e03c-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="6e03c-274">Hier ziet u uitvoer Hallo van Hallo implementatiescript, met inbegrip van de virtuele omgeving maken, de installatie van pakketten, het maken van web.config.</span><span class="sxs-lookup"><span data-stu-id="6e03c-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="6e03c-275">Blader toohello Azure-URL tooview uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="6e03c-276">Probleemoplossing - Installatie van pakketten</span><span class="sxs-lookup"><span data-stu-id="6e03c-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="6e03c-277">Probleemoplossing - Virtuele omgeving</span><span class="sxs-lookup"><span data-stu-id="6e03c-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="6e03c-278">Probleemoplossing - Statische bestanden</span><span class="sxs-lookup"><span data-stu-id="6e03c-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="6e03c-279">Django heeft Hallo concept van het verzamelen van statische bestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="6e03c-280">Dit duurt alle Hallo statische bestanden vanuit hun oorspronkelijke locatie en kopieert ze tooa één map.</span><span class="sxs-lookup"><span data-stu-id="6e03c-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="6e03c-281">Voor deze toepassing, worden ze gekopieerd te`/static`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="6e03c-282">Dit gebeurt omdat statische bestanden mogelijk afkomstig zijn van andere Django-apps.</span><span class="sxs-lookup"><span data-stu-id="6e03c-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="6e03c-283">Bijvoorbeeld, bevinden Hallo statische bestanden van Hallo Django-beheerinterfaces zich in een Django-bibliotheeksubmap in Hallo virtuele omgeving.</span><span class="sxs-lookup"><span data-stu-id="6e03c-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="6e03c-284">De statische bestanden die door deze toepassing worden gedefinieerd, bevinden zich in `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="6e03c-285">Als u meer Django-apps gebruikt, staan er op meerdere plaatsen statische bestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="6e03c-286">Wanneer de toepassing hello wordt uitgevoerd in de foutopsporingsmodus, fungeert Hallo toepassing hello statische bestanden vanuit hun oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="6e03c-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="6e03c-287">Wanneer Hallo toepassing wordt uitgevoerd in de releasemodus, Hallo toepassing biedt **niet** Hallo statische bestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="6e03c-288">Het is de verantwoordelijkheid Hallo Hallo web server tooserve Hallo bestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="6e03c-289">Voor deze toepassing fungeert IIS Hallo statische bestanden van `/static`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="6e03c-290">Hallo verzamelen van statische bestanden gebeurt automatisch als onderdeel van Hallo-implementatiescript wissen eerder verzamelde bestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="6e03c-291">Dit betekent Hallo verzameling plaatsvindt bij elke implementatie, duurt het implementatieproces langer, maar Hiermee zorgt u ervoor dat de verouderde bestanden niet beschikbaar, dat voorkomt potentiële beveiligingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="6e03c-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="6e03c-292">Als u wilt dat tooskip verzamelen van statische bestanden voor uw Django-toepassing:</span><span class="sxs-lookup"><span data-stu-id="6e03c-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="6e03c-293">Vervolgens moet u toodo Hallo verzameling handmatig op uw lokale machine:</span><span class="sxs-lookup"><span data-stu-id="6e03c-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="6e03c-294">Verwijder vervolgens Hallo `\static` map uit `.gitignore` en toe te voegen toohello Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6e03c-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="6e03c-295">Probleemoplossing - Instellingen</span><span class="sxs-lookup"><span data-stu-id="6e03c-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="6e03c-296">Diverse instellingen voor de toepassing hello kunnen worden gewijzigd in `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="6e03c-297">Voor het gemak van ontwikkelaars is de foutopsporingsmodus ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6e03c-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="6e03c-298">Een handige bijkomstigheid van die is, moet u kunnen toosee afbeeldingen en andere statische inhoud bij lokale uitvoering zonder toocollect statische bestanden.</span><span class="sxs-lookup"><span data-stu-id="6e03c-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="6e03c-299">de foutopsporingsmodus toodisable:</span><span class="sxs-lookup"><span data-stu-id="6e03c-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="6e03c-300">Wanneer foutopsporing is uitgeschakeld, de waarde voor Hallo `ALLOWED_HOSTS` behoeften toobe tooinclude hello Azure hostnaam bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6e03c-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="6e03c-301">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6e03c-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="6e03c-302">of tooenable eventuele:</span><span class="sxs-lookup"><span data-stu-id="6e03c-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="6e03c-303">In de praktijk kunt u toodo iets meer complexe toodeal schakelen tussen de foutopsporing en releasemodus, en ophalen van het Hallo-hostnaam.</span><span class="sxs-lookup"><span data-stu-id="6e03c-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="6e03c-304">U kunt omgevingsvariabelen instellen via hello Azure-portal **configureren** pagina in Hallo **appinstellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="6e03c-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="6e03c-305">Dit kan handig zijn voor het instellen van waarden die u niet kunt tooappear in Hallo bronnen (verbindingsreeksen, wachtwoorden, enzovoort) of dat u wilt dat tooset anders tussen Azure en uw lokale computer zijn.</span><span class="sxs-lookup"><span data-stu-id="6e03c-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="6e03c-306">In `settings.py`, u kunt een query Hallo omgevingsvariabelen met `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="6e03c-307">Een database gebruiken</span><span class="sxs-lookup"><span data-stu-id="6e03c-307">Using a Database</span></span>
<span data-ttu-id="6e03c-308">Hallo-database die is opgenomen in de toepassing hello is een sqlite-database.</span><span class="sxs-lookup"><span data-stu-id="6e03c-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="6e03c-309">Dit is een handige en nuttige standaard database toouse voor ontwikkeling, aangezien er bijna geen instellingen vereist.</span><span class="sxs-lookup"><span data-stu-id="6e03c-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="6e03c-310">Hallo-database is opgeslagen in bestand DB.sqlite3 in de projectmap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e03c-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="6e03c-311">Azure biedt databaseservices die eenvoudig toouse vanuit een Django-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6e03c-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="6e03c-312">Zelfstudies voor het gebruik van [SQL-Database] en [MySQL] weergeven vanuit een Django-toepassing hello stappen nodig toocreate Hallo database-service, Hallo database instellingen wijzigen in `DjangoWebProject/settings.py`, en Hallo bibliotheken tooinstall vereist.</span><span class="sxs-lookup"><span data-stu-id="6e03c-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="6e03c-313">Natuurlijk als u liever uw eigen databaseservers toomanage, kunt u doen met behulp van Windows of Linux virtuele machines die worden uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="6e03c-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="6e03c-314">Django-beheerinterface</span><span class="sxs-lookup"><span data-stu-id="6e03c-314">Django Admin Interface</span></span>
<span data-ttu-id="6e03c-315">Wanneer u begint met het bouwen van modellen, moet u toopopulate Hallo database met gegevens.</span><span class="sxs-lookup"><span data-stu-id="6e03c-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="6e03c-316">Een eenvoudige manier toodo toevoegen en interactief bewerken van inhoud is toouse hello Django-beheerinterface.</span><span class="sxs-lookup"><span data-stu-id="6e03c-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="6e03c-317">Hallo-code voor het Hallo-beheerinterface uitgecommentarieerd in de toepassingsbronnen hello, maar het duidelijk gemarkeerd, kunt u eenvoudig inschakelen (zoek naar 'admin').</span><span class="sxs-lookup"><span data-stu-id="6e03c-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="6e03c-318">Nadat deze ingeschakeld, Hallo database synchroniseren, Hallo toepassing uitvoeren en te navigeren`/admin`.</span><span class="sxs-lookup"><span data-stu-id="6e03c-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e03c-319">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e03c-319">Next Steps</span></span>
<span data-ttu-id="6e03c-320">Volg deze koppelingen toolearn meer informatie over Django en Python-Tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="6e03c-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="6e03c-321">[Documentatie bij Django]</span><span class="sxs-lookup"><span data-stu-id="6e03c-321">[Django Documentation]</span></span>
* <span data-ttu-id="6e03c-322">[Python-Tools voor Visual Studio-documentatie]</span><span class="sxs-lookup"><span data-stu-id="6e03c-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="6e03c-323">Voor informatie over het gebruik van SQL Database en MySQL:</span><span class="sxs-lookup"><span data-stu-id="6e03c-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="6e03c-324">[Django en MySQL in Azure met Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6e03c-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="6e03c-325">[Django en SQL Database in Azure met Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="6e03c-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="6e03c-326">Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="6e03c-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6e03c-327">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="6e03c-327">What's changed</span></span>
* <span data-ttu-id="6e03c-328">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6e03c-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
