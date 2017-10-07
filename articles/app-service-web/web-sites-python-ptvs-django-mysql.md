---
title: aaaDjango en MySQL in Azure met Python Tools 2.2 voor Visual Studio
description: Informatie over hoe toouse hello Python-Tools voor Visual Studio toocreate een Django-web-app die gegevens opslaat in een MySQL-database-exemplaar en deze tooAzure App Service Web Apps te implementeren.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="34a11-103">Django en MySQL in Azure met Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34a11-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="34a11-104">In deze zelfstudie gebruikt u [Python-Tools voor Visual Studio](https://www.visualstudio.com/vs/python) toocreate een eenvoudige web-app met een van de PTVS-voorbeeldsjablonen Hallo worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="34a11-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="34a11-105">U leert hoe toouse een MySQL-service wordt gehost op Azure, hoe tooconfigure Hallo web app toouse MySQL en hoe Hallo toopublish web-app te[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="34a11-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="34a11-106">Hallo informatie in deze zelfstudie is ook beschikbaar in de volgende video Hallo:</span><span class="sxs-lookup"><span data-stu-id="34a11-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="34a11-107">[PTVS 2.1: Django-app met MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="34a11-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="34a11-108">Zie Hallo [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met Azure Table Storage, MySQL en SQL Database-services.</span><span class="sxs-lookup"><span data-stu-id="34a11-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="34a11-109">Dit artikel is gericht op App Service, Hallo stappen zijn vergelijkbaar bij het ontwikkelen van [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="34a11-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34a11-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34a11-110">Prerequisites</span></span>
* <span data-ttu-id="34a11-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="34a11-111">Visual Studio 2015</span></span>
* <span data-ttu-id="34a11-112">[Python 2.7 32-bits] of [Python 3.4 32-bits]</span><span class="sxs-lookup"><span data-stu-id="34a11-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="34a11-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="34a11-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="34a11-114">[Python-Tools 2.2 voor Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="34a11-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="34a11-115">[Azure SDK-tools voor VS 2015]</span><span class="sxs-lookup"><span data-stu-id="34a11-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="34a11-116">Django 1.9 of hoger</span><span class="sxs-lookup"><span data-stu-id="34a11-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="34a11-117">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="34a11-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="34a11-118">Er is geen creditcard vereist en u bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="34a11-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="34a11-119">Hallo-Project maken</span><span class="sxs-lookup"><span data-stu-id="34a11-119">Create hello Project</span></span>
<span data-ttu-id="34a11-120">In deze sectie maakt u een Visual Studio-project met behulp van een voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="34a11-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="34a11-121">U maakt een virtuele omgeving en installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="34a11-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="34a11-122">U maakt een lokale database met behulp van sqlite.</span><span class="sxs-lookup"><span data-stu-id="34a11-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="34a11-123">Vervolgens voert u lokaal Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="34a11-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="34a11-124">Selecteer in Visual Studio **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="34a11-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="34a11-125">Hallo projectsjablonen uit Hallo [Python-Tools 2.2 voor Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **voorbeelden**.</span><span class="sxs-lookup"><span data-stu-id="34a11-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="34a11-126">Selecteer **Polls Django Web Project** en klik op OK toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="34a11-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="34a11-128">U zult na vragen aan gebruiker tooinstall externe pakketten.</span><span class="sxs-lookup"><span data-stu-id="34a11-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="34a11-129">Selecteer **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="34a11-129">Select **Install into a virtual environment**.</span></span>
   
    ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="34a11-131">Selecteer **Python 2.7** of **Python 3.4** als Hallo basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="34a11-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="34a11-133">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.</span><span class="sxs-lookup"><span data-stu-id="34a11-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="34a11-134">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="34a11-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="34a11-135">Hiermee opent u een Django-beheerconsole en maakt u een sqlite-database in de projectmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="34a11-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="34a11-136">Ga als volgt Hallo prompts toocreate een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="34a11-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="34a11-137">Controleer of de toepassing hello door te drukken werkt `F5`.</span><span class="sxs-lookup"><span data-stu-id="34a11-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="34a11-138">Klik op **aanmelden** van de navigatiebalk Hallo Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="34a11-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Django-navigatiebalk](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="34a11-140">Voer Hallo referenties voor u gemaakt tijdens het synchroniseren van de database Hallo Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="34a11-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Aanmeldscherm](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="34a11-142">Klik op **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="34a11-142">Click **Create Sample Polls**.</span></span>
    
     ![Voorbeeld-polls maken](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="34a11-144">Klik op een poll en stem.</span><span class="sxs-lookup"><span data-stu-id="34a11-144">Click on a poll and vote.</span></span>
    
     ![Stemmen in voorbeeld-polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="34a11-146">Een MySQL-database maken</span><span class="sxs-lookup"><span data-stu-id="34a11-146">Create a MySQL Database</span></span>
<span data-ttu-id="34a11-147">Voor Hallo-database maakt u een gehoste ClearDB MySQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a11-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="34a11-148">Als alternatief kunt u uw eigen virtuele machine maken die wordt uitgevoerd in Azure, en vervolgens MySQL zelf installeren en beheren.</span><span class="sxs-lookup"><span data-stu-id="34a11-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="34a11-149">U kunt een database maken met een gratis abonnement. Ga hiervoor als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="34a11-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="34a11-150">Meld u bij toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="34a11-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="34a11-151">Hallo boven in het navigatiedeelvenster hello, klikt u op **nieuw**, klikt u vervolgens op **gegevens en opslag**, en klik vervolgens op **MySQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="34a11-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="34a11-152">Hallo nieuwe MySQL-database configureren door een nieuwe resourcegroep maken en selecteer Hallo juiste locatie.</span><span class="sxs-lookup"><span data-stu-id="34a11-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="34a11-153">Zodra het Hallo MySQL-database is gemaakt, klikt u op **eigenschappen** in Hallo databaseblade.</span><span class="sxs-lookup"><span data-stu-id="34a11-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="34a11-154">Gebruik Hallo kopie knop tooput Hallo waarde van **VERBINDINGSREEKS** op Hallo Klembord.</span><span class="sxs-lookup"><span data-stu-id="34a11-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="34a11-155">Hallo Project configureren</span><span class="sxs-lookup"><span data-stu-id="34a11-155">Configure hello Project</span></span>
<span data-ttu-id="34a11-156">In deze sectie configureert u de web-app toouse Hallo MySQL-database die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34a11-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="34a11-157">U kunt ook extra Python-pakketten vereist toouse MySQL-databases met Django installeren.</span><span class="sxs-lookup"><span data-stu-id="34a11-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="34a11-158">Vervolgens voert u lokaal Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="34a11-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="34a11-159">Open in Visual Studio **settings.py**, van Hallo *ProjectName* map.</span><span class="sxs-lookup"><span data-stu-id="34a11-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="34a11-160">Plak tijdelijk Hallo-verbindingsreeks in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="34a11-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="34a11-161">Hallo-verbindingsreeks is in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="34a11-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="34a11-162">Wijziging Hallo standaarddatabase **ENGINE** toouse MySQL en stel de waarden voor Hallo **naam**, **gebruiker**, **wachtwoord** en  **HOST** van Hallo **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="34a11-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="34a11-163">Klik in Solution Explorer onder **Python-omgevingen**, met de rechtermuisknop op de virtuele omgeving Hallo en selecteert u **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="34a11-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="34a11-164">Hallo-pakket installeren `mysqlclient` met **pip**.</span><span class="sxs-lookup"><span data-stu-id="34a11-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Het dialoogvenster Install Package](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="34a11-166">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.</span><span class="sxs-lookup"><span data-stu-id="34a11-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="34a11-167">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="34a11-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="34a11-168">Hiermee wordt Hallo tabellen voor Hallo u hebt gemaakt in de vorige sectie Hallo MySQL-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="34a11-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="34a11-169">Ga als volgt Hallo prompts toocreate een gebruiker die geen toomatch Hallo gebruiker in Hallo sqlite-database gemaakt in de eerste sectie Hallo van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="34a11-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="34a11-170">Voer de toepassing hello met `F5`.</span><span class="sxs-lookup"><span data-stu-id="34a11-170">Run hello application with `F5`.</span></span> <span data-ttu-id="34a11-171">Polls die zijn gemaakt met **Create Sample Polls** en het Hallo-gegevens die zijn ingediend via stemmen, worden geserialiseerd in Hallo MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="34a11-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="34a11-172">Hallo web app tooAzure App Service publiceren</span><span class="sxs-lookup"><span data-stu-id="34a11-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="34a11-173">Hello Azure .NET SDK biedt een eenvoudige manier toodeploy uw web-app tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="34a11-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="34a11-174">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="34a11-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="34a11-176">Klik op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="34a11-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="34a11-177">Klik op **nieuw** toocreate een nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="34a11-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="34a11-178">Vul Hallo velden te volgen en klik op **maken**:</span><span class="sxs-lookup"><span data-stu-id="34a11-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="34a11-179">**Web-appnaam**</span><span class="sxs-lookup"><span data-stu-id="34a11-179">**Web App name**</span></span>
   * <span data-ttu-id="34a11-180">**App Service-plan**</span><span class="sxs-lookup"><span data-stu-id="34a11-180">**App Service plan**</span></span>
   * <span data-ttu-id="34a11-181">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="34a11-181">**Resource group**</span></span>
   * <span data-ttu-id="34a11-182">**Regio**</span><span class="sxs-lookup"><span data-stu-id="34a11-182">**Region**</span></span>
   * <span data-ttu-id="34a11-183">Laat **databaseserver** instellen te**geen database**</span><span class="sxs-lookup"><span data-stu-id="34a11-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="34a11-184">Accepteer alle overige standaardwaarden en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="34a11-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="34a11-185">De webbrowser wordt automatisch geopend toohello gepubliceerde web-app.</span><span class="sxs-lookup"><span data-stu-id="34a11-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="34a11-186">U ziet Hallo web-app werkt zoals verwacht, met behulp van Hallo **MySQL** database gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a11-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Webbrowser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="34a11-188">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="34a11-188">Congratulations!</span></span> <span data-ttu-id="34a11-189">U hebt uw tooAzure MySQL gebaseerde web-app gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="34a11-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34a11-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34a11-190">Next steps</span></span>
<span data-ttu-id="34a11-191">Volg deze koppelingen toolearn meer over Python-Tools voor Visual Studio, Django en MySQL.</span><span class="sxs-lookup"><span data-stu-id="34a11-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="34a11-192">[Documentatie Python Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="34a11-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="34a11-193">[Webprojecten]</span><span class="sxs-lookup"><span data-stu-id="34a11-193">[Web Projects]</span></span>
  * <span data-ttu-id="34a11-194">[Cloudserviceprojecten]</span><span class="sxs-lookup"><span data-stu-id="34a11-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="34a11-195">[Foutopsporing op afstand in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="34a11-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="34a11-196">[Documentatie bij Django]</span><span class="sxs-lookup"><span data-stu-id="34a11-196">[Django Documentation]</span></span>
* <span data-ttu-id="34a11-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="34a11-197">[MySQL]</span></span>

<span data-ttu-id="34a11-198">Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="34a11-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python-Tools 2.2 voor Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentatie bij Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
