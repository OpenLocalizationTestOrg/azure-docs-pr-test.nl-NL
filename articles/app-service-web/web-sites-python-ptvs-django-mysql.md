---
title: Django en MySQL in Azure met Python Tools 2.2 for Visual Studio
description: Leer hoe u de Python Tools for Visual Studio gebruikt om een Django-web-app te maken waarin gegevens worden opgeslagen in een MySQL-database, en deze vervolgens in Azure App Service-web-apps te implementeren.
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
ms.openlocfilehash: fd85337ecdc638a4c18065a0ce94f697da8197f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="8d376-103">Django en MySQL in Azure met Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d376-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="8d376-104">In deze zelfstudie gebruikt u [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) om een eenvoudige poll-web-app te maken met een van de PTVS-voorbeeldsjablonen.</span><span class="sxs-lookup"><span data-stu-id="8d376-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="8d376-105">U leert hoe u een MySQL-service gebruikt die wordt gehost in Azure, hoe u de web-app kunt configureren voor het gebruik van MySQL en hoe u de web-app publiceert naar [Azure App Service-web-apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="8d376-105">You'll learn how to use a MySQL service hosted on Azure, how to configure the web app to use MySQL, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="8d376-106">De informatie in deze zelfstudie is ook beschikbaar in de volgende video:</span><span class="sxs-lookup"><span data-stu-id="8d376-106">The information contained in this tutorial is also available in the following video:</span></span>
> 
> <span data-ttu-id="8d376-107">[PTVS 2.1: Django-app met MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="8d376-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="8d376-108">Raadpleeg het [Python Developer Center] voor meer artikelen over het ontwikkelen van Azure App Service-web-apps met PTVS met behulp van Bottle-, Flask- en Django-webframeworks, met Azure Table Storage-, MySQL- en SQL Database-services.</span><span class="sxs-lookup"><span data-stu-id="8d376-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="8d376-109">Dit artikel is gericht op App Service, maar voor het ontwikkelen van [Azure Cloud Services] volgt u soortgelijk stappen.</span><span class="sxs-lookup"><span data-stu-id="8d376-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d376-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d376-110">Prerequisites</span></span>
* <span data-ttu-id="8d376-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8d376-111">Visual Studio 2015</span></span>
* <span data-ttu-id="8d376-112">[Python 2.7 32-bits] of [Python 3.4 32-bits]</span><span class="sxs-lookup"><span data-stu-id="8d376-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="8d376-113">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8d376-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="8d376-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="8d376-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="8d376-115">[Azure SDK-tools voor VS 2015]</span><span class="sxs-lookup"><span data-stu-id="8d376-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="8d376-116">Django 1.9 of hoger</span><span class="sxs-lookup"><span data-stu-id="8d376-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of the the previous include. -->

> [!NOTE]
> <span data-ttu-id="8d376-117">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="8d376-117">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8d376-118">Er is geen creditcard vereist en u bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="8d376-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="8d376-119">Het project maken</span><span class="sxs-lookup"><span data-stu-id="8d376-119">Create the Project</span></span>
<span data-ttu-id="8d376-120">In deze sectie maakt u een Visual Studio-project met behulp van een voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="8d376-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="8d376-121">U maakt een virtuele omgeving en installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="8d376-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="8d376-122">U maakt een lokale database met behulp van sqlite.</span><span class="sxs-lookup"><span data-stu-id="8d376-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="8d376-123">Vervolgens voert u de toepassing lokaal uit.</span><span class="sxs-lookup"><span data-stu-id="8d376-123">Then you'll run the application locally.</span></span>

1. <span data-ttu-id="8d376-124">Selecteer in Visual Studio **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="8d376-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="8d376-125">De projectsjablonen uit de [Python Tools 2.2 for Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **Samples**.</span><span class="sxs-lookup"><span data-stu-id="8d376-125">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="8d376-126">Selecteer **Polls Django Web Project** en klik op OK om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="8d376-126">Select **Polls Django Web Project** and click OK to create the project.</span></span>
   
    ![Het dialoogvenster New Project](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="8d376-128">U wordt gevraagd om externe pakketten te installeren.</span><span class="sxs-lookup"><span data-stu-id="8d376-128">You will be prompted to install external packages.</span></span> <span data-ttu-id="8d376-129">Selecteer **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="8d376-129">Select **Install into a virtual environment**.</span></span>
   
    ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="8d376-131">Selecteer **Python 2.7** of **Python 3.4** als basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="8d376-131">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
    ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="8d376-133">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Python**. Selecteer vervolgens **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="8d376-133">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="8d376-134">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="8d376-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="8d376-135">Hiermee wordt in de projectmap een Django-beheerconsole en een sqlite-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d376-135">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="8d376-136">Volg de aanwijzingen voor het maken van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8d376-136">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="8d376-137">Controleer of de toepassing werkt, door te drukken op `F5`.</span><span class="sxs-lookup"><span data-stu-id="8d376-137">Confirm that the application works by pressing `F5`.</span></span>
8. <span data-ttu-id="8d376-138">Klik in de navigatiebalk bovenaan op **Log in**.</span><span class="sxs-lookup"><span data-stu-id="8d376-138">Click **Log in** from the navigation bar at the top.</span></span>
   
    ![Django-navigatiebalk](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="8d376-140">Voer de referenties in voor de gebruiker die u hebt gemaakt tijdens het synchroniseren van de database.</span><span class="sxs-lookup"><span data-stu-id="8d376-140">Enter the credentials for the user you created when you synchronized the database.</span></span>
   
    ![Aanmeldscherm](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="8d376-142">Klik op **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="8d376-142">Click **Create Sample Polls**.</span></span>
    
     ![Voorbeeld-polls maken](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="8d376-144">Klik op een poll en stem.</span><span class="sxs-lookup"><span data-stu-id="8d376-144">Click on a poll and vote.</span></span>
    
     ![Stemmen in voorbeeld-polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="8d376-146">Een MySQL-database maken</span><span class="sxs-lookup"><span data-stu-id="8d376-146">Create a MySQL Database</span></span>
<span data-ttu-id="8d376-147">Voor de database maakt u een gehoste ClearDB MySQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d376-147">For the database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="8d376-148">Als alternatief kunt u uw eigen virtuele machine maken die wordt uitgevoerd in Azure, en vervolgens MySQL zelf installeren en beheren.</span><span class="sxs-lookup"><span data-stu-id="8d376-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="8d376-149">U kunt een database maken met een gratis abonnement. Ga hiervoor als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="8d376-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="8d376-150">Meld u aan bij de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="8d376-150">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="8d376-151">Klik boven in het navigatiedeelvenster achtereenvolgens op **NIEUW**, **Gegevens en opslag** en **MySQL-database**.</span><span class="sxs-lookup"><span data-stu-id="8d376-151">At the Top of the navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="8d376-152">Configureer de nieuwe MySQL-database door een nieuwe resourcegroep te maken en hiervoor de juiste locatie te selecteren.</span><span class="sxs-lookup"><span data-stu-id="8d376-152">Configure the new MySQL database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="8d376-153">Nadat de MySQL-database is gemaakt, klikt u op de databaseblade op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="8d376-153">Once the MySQL database is created, click **Properties** in the database blade.</span></span>
5. <span data-ttu-id="8d376-154">Gebruik de knop Kopiëren om de waarde van **VERBINDINGSREEKS** op het klembord te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8d376-154">Use the copy button to put the value of **CONNECTION STRING** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="8d376-155">Het project configureren</span><span class="sxs-lookup"><span data-stu-id="8d376-155">Configure the Project</span></span>
<span data-ttu-id="8d376-156">In deze sectie configureert u de web-app voor het gebruik van de MySQL-database die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d376-156">In this section, you'll configure our web app to use the MySQL database you just created.</span></span> <span data-ttu-id="8d376-157">U kunt ook extra Python-pakketten installeren die vereist zijn voor het gebruik van MySQL-databases met Django.</span><span class="sxs-lookup"><span data-stu-id="8d376-157">You'll also install additional Python packages required to use MySQL databases with Django.</span></span> <span data-ttu-id="8d376-158">Vervolgens voert u de web-app lokaal uit.</span><span class="sxs-lookup"><span data-stu-id="8d376-158">Then you'll run the web app locally.</span></span>

1. <span data-ttu-id="8d376-159">Open in Visual Studio **settings.py** vanuit de map *ProjectName*.</span><span class="sxs-lookup"><span data-stu-id="8d376-159">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="8d376-160">Plak de verbindingsreeks tijdelijk in de editor.</span><span class="sxs-lookup"><span data-stu-id="8d376-160">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="8d376-161">De verbindingsreeks heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8d376-161">The connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="8d376-162">Wijzig de standaarddatabase **ENGINE** voor het gebruik van MySQL en stel de waarden voor **NAME**, **USER**, **PASSWORD** en **HOST** van de **CONNECTIONSTRING** in.</span><span class="sxs-lookup"><span data-stu-id="8d376-162">Change the default database **ENGINE** to use MySQL, and set the values for **NAME**, **USER**, **PASSWORD** and **HOST** from the **CONNECTIONSTRING**.</span></span>
   
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
2. <span data-ttu-id="8d376-163">Klik onder **Python-omgevingen** in Solution Explorer met de rechtermuisknop op de virtuele omgeving en selecteer **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="8d376-163">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="8d376-164">Installeer het pakket `mysqlclient` met behulp van **pip**.</span><span class="sxs-lookup"><span data-stu-id="8d376-164">Install the package `mysqlclient` using **pip**.</span></span>
   
    ![Het dialoogvenster Install Package](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="8d376-166">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Python**. Selecteer vervolgens **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="8d376-166">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="8d376-167">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="8d376-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="8d376-168">Hiermee maakt u de tabellen voor de MySQL-database die u in de vorige sectie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d376-168">This will create the tables for the MySQL database you created in the previous section.</span></span> <span data-ttu-id="8d376-169">Volg de aanwijzingen voor het maken van een gebruiker. De gebruiker hoeft niet dezelfde te zijn als de gebruiker in de sqlite-database die in de eerste sectie van dit artikel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d376-169">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section of this article.</span></span>
5. <span data-ttu-id="8d376-170">Voer de toepassing uit met `F5`.</span><span class="sxs-lookup"><span data-stu-id="8d376-170">Run the application with `F5`.</span></span> <span data-ttu-id="8d376-171">Polls die zijn gemaakt met **Create Sample Polls** en de gegevens die zijn ingediend via stemmen, worden geserialiseerd in de MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="8d376-171">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the MySQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="8d376-172">De web-app publiceren naar Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8d376-172">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="8d376-173">De Azure SDK voor .NET biedt een eenvoudige manier om uw web-app in Azure App Service te implementeren.</span><span class="sxs-lookup"><span data-stu-id="8d376-173">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="8d376-174">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8d376-174">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
    ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="8d376-176">Klik op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="8d376-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="8d376-177">Klik op **Nieuw** om een nieuwe web-app te maken.</span><span class="sxs-lookup"><span data-stu-id="8d376-177">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="8d376-178">Vul de volgende velden in en klik op **Maken**:</span><span class="sxs-lookup"><span data-stu-id="8d376-178">Fill in the following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="8d376-179">**Web-appnaam**</span><span class="sxs-lookup"><span data-stu-id="8d376-179">**Web App name**</span></span>
   * <span data-ttu-id="8d376-180">**App Service-plan**</span><span class="sxs-lookup"><span data-stu-id="8d376-180">**App Service plan**</span></span>
   * <span data-ttu-id="8d376-181">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="8d376-181">**Resource group**</span></span>
   * <span data-ttu-id="8d376-182">**Regio**</span><span class="sxs-lookup"><span data-stu-id="8d376-182">**Region**</span></span>
   * <span data-ttu-id="8d376-183">Laat **Databaseserver** ingesteld op **Geen database**.</span><span class="sxs-lookup"><span data-stu-id="8d376-183">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="8d376-184">Accepteer alle overige standaardwaarden en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8d376-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="8d376-185">De gepubliceerde web-app wordt automatisch geopend in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8d376-185">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="8d376-186">De web-app hoort nu correct te werken met behulp van de **MySQL**-database gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d376-186">You should see the web app working as expected, using the **MySQL** database hosted on Azure.</span></span>
   
    ![Webbrowser](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="8d376-188">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="8d376-188">Congratulations!</span></span> <span data-ttu-id="8d376-189">U hebt uw op MySQL gebaseerde web-app gepubliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="8d376-189">You have successfully published your MySQL-based web app to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d376-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d376-190">Next steps</span></span>
<span data-ttu-id="8d376-191">Volg deze koppelingen voor meer informatie over Python Tools for Visual Studio, Django en MySQL.</span><span class="sxs-lookup"><span data-stu-id="8d376-191">Follow these links to learn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="8d376-192">[Documentatie Python Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="8d376-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="8d376-193">[Webprojecten]</span><span class="sxs-lookup"><span data-stu-id="8d376-193">[Web Projects]</span></span>
  * <span data-ttu-id="8d376-194">[Cloudserviceprojecten]</span><span class="sxs-lookup"><span data-stu-id="8d376-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="8d376-195">[Foutopsporing op afstand in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="8d376-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="8d376-196">[Documentatie bij Django]</span><span class="sxs-lookup"><span data-stu-id="8d376-196">[Django Documentation]</span></span>
* <span data-ttu-id="8d376-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="8d376-197">[MySQL]</span></span>

<span data-ttu-id="8d376-198">Raadpleeg het [Python Developer Center](/develop/python/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8d376-198">For more information, see the [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
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
