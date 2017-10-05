---
title: Django en SQL Database in Azure met Python Tools 2.2 for Visual Studio
description: Informatie over het gebruik van de Python Tools for Visual Studio een Django-web-app die gegevens in een SQL database-exemplaar opslaat maken en deze implementeren in Azure App Service Web Apps.
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="f4bc5-103">Django en SQL Database in Azure met Python Tools 2.2 for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4bc5-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="f4bc5-104">In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] voor het maken van een eenvoudige polls web-app met een van de PTVS-voorbeeldsjablonen.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="f4bc5-105">Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="f4bc5-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="f4bc5-106">We het gebruik van een SQL-database gehost op Azure, het configureren van de web-app voor het gebruik van een SQL-database en de web-app te publiceren leert [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f4bc5-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="f4bc5-107">Zie de [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met Azure Table Storage, MySQL en SQL Database-services.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="f4bc5-108">Dit artikel is gericht op App Service, maar voor het ontwikkelen van [Azure Cloud Services] volgt u soortgelijk stappen.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4bc5-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4bc5-109">Prerequisites</span></span>
* <span data-ttu-id="f4bc5-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="f4bc5-110">Visual Studio 2015</span></span>
* <span data-ttu-id="f4bc5-111">[Python 2.7 32-bits]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="f4bc5-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="f4bc5-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="f4bc5-114">[Azure SDK-tools voor VS 2015]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="f4bc5-115">Django 1.9 of hoger</span><span class="sxs-lookup"><span data-stu-id="f4bc5-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f4bc5-116">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f4bc5-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="f4bc5-118">Het project maken</span><span class="sxs-lookup"><span data-stu-id="f4bc5-118">Create the Project</span></span>
<span data-ttu-id="f4bc5-119">In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="f4bc5-120">We maken van een virtuele omgeving en installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="f4bc5-121">Maakt een lokale database met behulp van sqlite.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="f4bc5-122">Er wordt vervolgens de web-app lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="f4bc5-123">Selecteer in Visual Studio **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="f4bc5-124">De projectsjablonen uit de [Python Tools 2.2 for Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **Samples**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="f4bc5-125">Selecteer **Polls Django Web Project** en klik op OK om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Het dialoogvenster New Project](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="f4bc5-127">U wordt gevraagd om externe pakketten te installeren.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="f4bc5-128">Selecteer **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-128">Select **Install into a virtual environment**.</span></span>

     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="f4bc5-130">Selecteer **Python 2.7** als basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="f4bc5-132">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Python**. Selecteer vervolgens **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="f4bc5-133">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="f4bc5-134">Hiermee wordt in de projectmap een Django-beheerconsole en een sqlite-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="f4bc5-135">Volg de aanwijzingen voor het maken van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="f4bc5-136">Controleer of de toepassing door te drukken werkt <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="f4bc5-137">Klik in de navigatiebalk bovenaan op **Log in**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="f4bc5-139">Voer de referenties in voor de gebruiker die u hebt gemaakt tijdens het synchroniseren van de database.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="f4bc5-141">Klik op **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-141">Click **Create Sample Polls**.</span></span>

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="f4bc5-143">Klik op een poll en stem.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-143">Click on a poll and vote.</span></span>

      ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="f4bc5-145">Een SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="f4bc5-145">Create a SQL Database</span></span>
<span data-ttu-id="f4bc5-146">Voor de database maakt u een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="f4bc5-147">U kunt een database maken met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="f4bc5-148">Meld u aan bij de [Azure-Portal].</span><span class="sxs-lookup"><span data-stu-id="f4bc5-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="f4bc5-149">Klik onderaan in het navigatievenster op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="f4bc5-150">, klik op **gegevens en opslag** > **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="f4bc5-151">De nieuwe SQL-Database configureren door een nieuwe resourcegroep maken en selecteer de juiste locatie.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="f4bc5-152">Nadat de SQL-Database is gemaakt, klikt u op **openen in Visual Studio** in de databaseblade.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="f4bc5-153">Klik op **uw firewall configureren**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="f4bc5-154">In de **firewallinstellingen** blade toevoegen van een firewallregel met **eerste IP-** en **END-IP** ingesteld op het openbare IP-adres van uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="f4bc5-155">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-155">Click **Save**.</span></span>

   <span data-ttu-id="f4bc5-156">Hierdoor kunnen verbindingen met de databaseserver van uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="f4bc5-157">Klik in de databaseblade op **eigenschappen**, klikt u vervolgens op **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="f4bc5-158">Gebruik de knop kopiëren om de waarde van **ADO.NET** op het Klembord.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="f4bc5-159">Het project configureren</span><span class="sxs-lookup"><span data-stu-id="f4bc5-159">Configure the Project</span></span>
<span data-ttu-id="f4bc5-160">In deze sectie configureert de web-app voor het gebruik van de SQL-database die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="f4bc5-161">Installeren we ook extra Python-pakketten vereist voor het gebruik van SQL-databases met Django.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="f4bc5-162">Er wordt vervolgens de web-app lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="f4bc5-163">Open in Visual Studio **settings.py** vanuit de map *ProjectName*.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="f4bc5-164">Plak de verbindingsreeks tijdelijk in de editor.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="f4bc5-165">De verbindingsreeks heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="f4bc5-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="f4bc5-166">Bewerk de definitie van `DATABASES` als u de bovenstaande waarden.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="f4bc5-167">Klik onder **Python-omgevingen** in Solution Explorer met de rechtermuisknop op de virtuele omgeving en selecteer **Install Python Package**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="f4bc5-168">Installeer het pakket `pyodbc` met behulp van **pip**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="f4bc5-170">Installeer het pakket `django-pyodbc-azure` met behulp van **pip**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Python dialoogvenster Install Package](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="f4bc5-172">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Python**. Selecteer vervolgens **Django Migrate**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="f4bc5-173">Selecteer vervolgens **Django Create Superuser**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="f4bc5-174">Hiermee maakt u de tabellen voor de SQL-database die in de vorige sectie is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="f4bc5-175">Volg de aanwijzingen voor het maken van een gebruiker die niet moet overeenkomen met de gebruiker in de sqlite-database gemaakt in de eerste sectie.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="f4bc5-176">Voer de toepassing uit met `F5`.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-176">Run the application with `F5`.</span></span> <span data-ttu-id="f4bc5-177">Polls die zijn gemaakt met **Create Sample Polls** en de gegevens die zijn ingediend via stemmen, worden geserialiseerd in de SQL-database.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="f4bc5-178">De web-app publiceren naar Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4bc5-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="f4bc5-179">De Azure .NET SDK biedt een eenvoudige manier om uw web-web-app implementeren op Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="f4bc5-180">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="f4bc5-182">Klik op **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="f4bc5-183">Klik op **Nieuw** om een nieuwe web-app te maken.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="f4bc5-184">Vul de volgende velden in en klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="f4bc5-185">**Web-appnaam**</span><span class="sxs-lookup"><span data-stu-id="f4bc5-185">**Web App name**</span></span>
   * <span data-ttu-id="f4bc5-186">**App Service-plan**</span><span class="sxs-lookup"><span data-stu-id="f4bc5-186">**App Service plan**</span></span>
   * <span data-ttu-id="f4bc5-187">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="f4bc5-187">**Resource group**</span></span>
   * <span data-ttu-id="f4bc5-188">**Regio**</span><span class="sxs-lookup"><span data-stu-id="f4bc5-188">**Region**</span></span>
   * <span data-ttu-id="f4bc5-189">Laat **Databaseserver** ingesteld op **Geen database**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="f4bc5-190">Accepteer alle overige standaardwaarden en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="f4bc5-191">De gepubliceerde web-app wordt automatisch geopend in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="f4bc5-192">U ziet de web-app werkt zoals verwacht, met behulp van de **SQL** database gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="f4bc5-193">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-193">Congratulations!</span></span>

     ![Webbrowser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="f4bc5-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4bc5-195">Next steps</span></span>
<span data-ttu-id="f4bc5-196">Volg deze koppelingen voor meer informatie over Python Tools for Visual Studio, Django en SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="f4bc5-197">[Documentatie Python Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="f4bc5-198">[Webprojecten]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-198">[Web Projects]</span></span>
  * <span data-ttu-id="f4bc5-199">[Cloudserviceprojecten]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="f4bc5-200">[Foutopsporing op afstand in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="f4bc5-201">[Documentatie bij Django]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-201">[Django Documentation]</span></span>
* <span data-ttu-id="f4bc5-202">[SQL Database]</span><span class="sxs-lookup"><span data-stu-id="f4bc5-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f4bc5-203">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="f4bc5-203">What's changed</span></span>
* <span data-ttu-id="f4bc5-204">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f4bc5-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="f4bc5-205">[Python Developer Center]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="f4bc5-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="f4bc5-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="f4bc5-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="f4bc5-207">[Azure-Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="f4bc5-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="f4bc5-208">[Python-Tools voor Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="f4bc5-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="f4bc5-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="f4bc5-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="f4bc5-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="f4bc5-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="f4bc5-211">[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="f4bc5-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="f4bc5-212">[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="f4bc5-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="f4bc5-213">[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="f4bc5-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="f4bc5-214">[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="f4bc5-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="f4bc5-215">[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="f4bc5-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="f4bc5-216">[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="f4bc5-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="f4bc5-217">[Documentatie bij Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="f4bc5-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="f4bc5-218">[SQL Database]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="f4bc5-218">[SQL Database]: /documentation/services/sql-database/</span></span>
