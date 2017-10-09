---
title: aaaDjango en SQL-Database in Azure met Python-Tools 2.2 voor Visual Studio
description: Informatie over hoe toouse hello Python-Tools voor Visual Studio toocreate een Django-web-app die gegevens opslaat in een SQL database-exemplaar en deze tooAzure App Service Web Apps te implementeren.
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="a62d7-103">Django en SQL Database in Azure met Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a62d7-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="a62d7-104">In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] toocreate een eenvoudige web-app met een van de PTVS-voorbeeldsjablonen Hallo worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="a62d7-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="a62d7-105">Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="a62d7-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="a62d7-106">We leert hoe toouse een SQL-database gehost op Azure, hoe tooconfigure Hallo web app toouse een SQL-database en hoe toopublish web-app te Hallo[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a62d7-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="a62d7-107">Zie Hallo [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met Azure Table Storage, MySQL en SQL Database-services.</span><span class="sxs-lookup"><span data-stu-id="a62d7-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="a62d7-108">Dit artikel is gericht op App Service, Hallo stappen zijn vergelijkbaar bij het ontwikkelen van [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="a62d7-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a62d7-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a62d7-109">Prerequisites</span></span>
* <span data-ttu-id="a62d7-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="a62d7-110">Visual Studio 2015</span></span>
* <span data-ttu-id="a62d7-111">[Python 2.7 32-bits]</span><span class="sxs-lookup"><span data-stu-id="a62d7-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="a62d7-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a62d7-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="a62d7-113">[Python-Tools 2.2 voor Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="a62d7-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="a62d7-114">[Azure SDK-tools voor VS 2015]</span><span class="sxs-lookup"><span data-stu-id="a62d7-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="a62d7-115">Django 1.9 of hoger</span><span class="sxs-lookup"><span data-stu-id="a62d7-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="a62d7-116">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="a62d7-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a62d7-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="a62d7-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="a62d7-118">Hallo-Project maken</span><span class="sxs-lookup"><span data-stu-id="a62d7-118">Create hello Project</span></span>
<span data-ttu-id="a62d7-119">In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="a62d7-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="a62d7-120">We maken van een virtuele omgeving en installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="a62d7-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="a62d7-121">Maakt een lokale database met behulp van sqlite.</span><span class="sxs-lookup"><span data-stu-id="a62d7-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="a62d7-122">Vervolgens voert we lokaal Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="a62d7-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="a62d7-123">Selecteer in Visual Studio **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="a62d7-124">Hallo projectsjablonen uit Hallo [Python-Tools 2.2 voor Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **voorbeelden**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="a62d7-125">Selecteer **Polls Django Web Project** en klik op OK toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="a62d7-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="a62d7-127">U zult na vragen aan gebruiker tooinstall externe pakketten.</span><span class="sxs-lookup"><span data-stu-id="a62d7-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="a62d7-128">Selecteer **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-128">Select **Install into a virtual environment**.</span></span>

     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="a62d7-130">Selecteer **Python 2.7** als Hallo basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="a62d7-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="a62d7-132">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="a62d7-133">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="a62d7-134">Hiermee opent u een Django-beheerconsole en maakt u een sqlite-database in de projectmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="a62d7-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="a62d7-135">Ga als volgt Hallo prompts toocreate een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a62d7-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="a62d7-136">Controleer of de toepassing hello door te drukken werkt <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="a62d7-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="a62d7-137">Klik op **aanmelden** van de navigatiebalk Hallo Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="a62d7-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="a62d7-139">Voer Hallo referenties voor u gemaakt tijdens het synchroniseren van de database Hallo Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a62d7-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="a62d7-141">Klik op **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-141">Click **Create Sample Polls**.</span></span>

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="a62d7-143">Klik op een poll en stem.</span><span class="sxs-lookup"><span data-stu-id="a62d7-143">Click on a poll and vote.</span></span>

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="a62d7-145">Een SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="a62d7-145">Create a SQL Database</span></span>
<span data-ttu-id="a62d7-146">Voor de database hello maken we een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="a62d7-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="a62d7-147">U kunt een database maken met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="a62d7-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="a62d7-148">Meld u aan bij Hallo [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="a62d7-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="a62d7-149">Klik onder aan het navigatiedeelvenster Hallo Hallo op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="a62d7-150">, klik op **gegevens en opslag** > **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="a62d7-151">Configureer Hallo nieuwe SQL-Database door een nieuwe resourcegroep maken en selecteer de juiste locatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a62d7-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="a62d7-152">Zodra het Hallo SQL-Database is gemaakt, klikt u op **openen in Visual Studio** in Hallo databaseblade.</span><span class="sxs-lookup"><span data-stu-id="a62d7-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="a62d7-153">Klik op **uw firewall configureren**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="a62d7-154">In Hallo **firewallinstellingen** blade toevoegen van een firewallregel met **eerste IP-** en **END-IP** toohello openbare IP-adres van uw ontwikkelcomputer ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a62d7-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="a62d7-155">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-155">Click **Save**.</span></span>

   <span data-ttu-id="a62d7-156">Hierdoor kunt verbindingen toohello-databaseserver van uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a62d7-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="a62d7-157">Klik in de databaseblade hello, op **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="a62d7-158">Gebruik Hallo kopie knop tooput Hallo waarde van **ADO.NET** op Hallo Klembord.</span><span class="sxs-lookup"><span data-stu-id="a62d7-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="a62d7-159">Hallo Project configureren</span><span class="sxs-lookup"><span data-stu-id="a62d7-159">Configure hello Project</span></span>
<span data-ttu-id="a62d7-160">In deze sectie configureert de web-app toouse Hallo SQL database die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a62d7-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="a62d7-161">Ook installeren we extra Python-pakketten vereist toouse SQL-databases met Django.</span><span class="sxs-lookup"><span data-stu-id="a62d7-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="a62d7-162">Vervolgens voert we lokaal Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="a62d7-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="a62d7-163">Open in Visual Studio **settings.py**, van Hallo *ProjectName* map.</span><span class="sxs-lookup"><span data-stu-id="a62d7-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="a62d7-164">Plak tijdelijk Hallo-verbindingsreeks in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="a62d7-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="a62d7-165">Hallo-verbindingsreeks is in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="a62d7-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="a62d7-166">Bewerk Hallo definitie van `DATABASES` toouse Hallo waarden hierboven.</span><span class="sxs-lookup"><span data-stu-id="a62d7-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="a62d7-167">Klik in Solution Explorer onder **Python-omgevingen**, met de rechtermuisknop op de virtuele omgeving Hallo en selecteert u **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="a62d7-168">Hallo-pakket installeren `pyodbc` met **pip**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="a62d7-170">Hallo-pakket installeren `django-pyodbc-azure` met **pip**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="a62d7-172">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **Python**, en selecteer vervolgens **Django migreren**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="a62d7-173">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="a62d7-174">Hiermee wordt de tabellen voor Hallo SQL-database die wordt gemaakt in de vorige sectie Hallo Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a62d7-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="a62d7-175">Ga als volgt Hallo prompts toocreate een gebruiker die geen toomatch Hallo gebruiker in Hallo sqlite-database gemaakt in de eerste sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a62d7-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="a62d7-176">Voer de toepassing hello met `F5`.</span><span class="sxs-lookup"><span data-stu-id="a62d7-176">Run hello application with `F5`.</span></span> <span data-ttu-id="a62d7-177">Polls die zijn gemaakt met **Create Sample Polls** en het Hallo-gegevens die zijn ingediend via stemmen, worden geserialiseerd in Hallo SQL-database.</span><span class="sxs-lookup"><span data-stu-id="a62d7-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="a62d7-178">Hallo web app tooAzure App Service publiceren</span><span class="sxs-lookup"><span data-stu-id="a62d7-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="a62d7-179">Hello Azure .NET SDK biedt een eenvoudige manier toodeploy uw web web app tooAzure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="a62d7-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="a62d7-180">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="a62d7-182">Klik op **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="a62d7-183">Klik op **nieuw** toocreate een nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="a62d7-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="a62d7-184">Vul Hallo velden te volgen en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="a62d7-185">**Web-appnaam**</span><span class="sxs-lookup"><span data-stu-id="a62d7-185">**Web App name**</span></span>
   * <span data-ttu-id="a62d7-186">**App Service-plan**</span><span class="sxs-lookup"><span data-stu-id="a62d7-186">**App Service plan**</span></span>
   * <span data-ttu-id="a62d7-187">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="a62d7-187">**Resource group**</span></span>
   * <span data-ttu-id="a62d7-188">**Regio**</span><span class="sxs-lookup"><span data-stu-id="a62d7-188">**Region**</span></span>
   * <span data-ttu-id="a62d7-189">Laat **databaseserver** instellen te**geen database**</span><span class="sxs-lookup"><span data-stu-id="a62d7-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="a62d7-190">Accepteer alle overige standaardwaarden en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="a62d7-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="a62d7-191">De webbrowser wordt automatisch geopend toohello gepubliceerde web-app.</span><span class="sxs-lookup"><span data-stu-id="a62d7-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="a62d7-192">U ziet Hallo web-app werkt zoals verwacht, met behulp van Hallo **SQL** database gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="a62d7-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="a62d7-193">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="a62d7-193">Congratulations!</span></span>

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="a62d7-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a62d7-195">Next steps</span></span>
<span data-ttu-id="a62d7-196">Volg deze koppelingen toolearn meer over Python-Tools voor Visual Studio, Django en SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="a62d7-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="a62d7-197">[Documentatie Python Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="a62d7-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="a62d7-198">[Webprojecten]</span><span class="sxs-lookup"><span data-stu-id="a62d7-198">[Web Projects]</span></span>
  * <span data-ttu-id="a62d7-199">[Cloudserviceprojecten]</span><span class="sxs-lookup"><span data-stu-id="a62d7-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="a62d7-200">[Foutopsporing op afstand in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a62d7-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="a62d7-201">[Documentatie bij Django]</span><span class="sxs-lookup"><span data-stu-id="a62d7-201">[Django Documentation]</span></span>
* <span data-ttu-id="a62d7-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="a62d7-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="a62d7-203">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="a62d7-203">What's changed</span></span>
* <span data-ttu-id="a62d7-204">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a62d7-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python-Tools 2.2 voor Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentatie bij Django]: https://www.djangoproject.com/
[SQL Database]: /documentation/services/sql-database/
