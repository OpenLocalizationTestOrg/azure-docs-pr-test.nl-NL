---
title: Taken voor elastische database installeren | Microsoft Docs
description: Installatie van de functie elastische taak doorlopen.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="49c24-103">Overzicht van de taken installeren elastische Database</span><span class="sxs-lookup"><span data-stu-id="49c24-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="49c24-104">[**Elastische Database taken** ](sql-database-elastic-jobs-overview.md) kan worden geïnstalleerd via PowerShell of via de klassieke Azure-Portal.You toegankelijk is voor het maken en beheren van taken met de PowerShell-API alleen als u het PowerShell-pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="49c24-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="49c24-105">De PowerShell APIs Geef ook aanzienlijk meer functionaliteit dan de portal op dit moment.</span><span class="sxs-lookup"><span data-stu-id="49c24-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="49c24-106">Als u al hebt geïnstalleerd **elastische Database taken** via de Portal van een bestaand **elastische pool**, de meest recente Powershell voorbeeldweergave scripts voor uw bestaande installatie upgraden.</span><span class="sxs-lookup"><span data-stu-id="49c24-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="49c24-107">Het is raadzaam een upgrade naar de meest recente **elastische Database taken** onderdelen om te profiteren van nieuwe functionaliteit beschikbaar gesteld via de PowerShell APIs.</span><span class="sxs-lookup"><span data-stu-id="49c24-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49c24-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="49c24-108">Prerequisites</span></span>
* <span data-ttu-id="49c24-109">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="49c24-109">An Azure subscription.</span></span> <span data-ttu-id="49c24-110">Zie voor een gratis proefversie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49c24-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="49c24-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49c24-111">Azure PowerShell.</span></span> <span data-ttu-id="49c24-112">Installeer de nieuwste versie met de [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="49c24-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="49c24-113">Zie voor gedetailleerde informatie [Installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49c24-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="49c24-114">[NuGet-opdrachtregelprogramma](https://nuget.org/nuget.exe) wordt gebruikt om de taken elastische Database pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="49c24-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="49c24-115">Zie http://docs.nuget.org/docs/start-here/installing-nuget voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="49c24-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="49c24-116">Downloaden en importeren van de elastische Database taken PowerShell-pakket</span><span class="sxs-lookup"><span data-stu-id="49c24-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="49c24-117">Start Microsoft Azure PowerShell-opdrachtvenster en navigeer naar de map waar u NuGet-opdrachtregelprogramma (nuget.exe) gedownload.</span><span class="sxs-lookup"><span data-stu-id="49c24-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="49c24-118">Downloaden en importeren **elastische Database taken** pakket in de huidige map met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="49c24-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="49c24-119">De **elastische Database taken** bestanden worden geplaatst in de lokale map in een map met de naam **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** waar *x.x.xxxx.x* weerspiegelt het versienummer.</span><span class="sxs-lookup"><span data-stu-id="49c24-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="49c24-120">De PowerShell-cmdlets (met inbegrip van de vereiste client-dll's) bevinden zich in de **tools\ElasticDatabaseJobs** submappen en de PowerShell-scripts te installeren, upgraden en verwijderen ook bevinden zich in de **extra** onderliggende map.</span><span class="sxs-lookup"><span data-stu-id="49c24-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="49c24-121">Navigeer naar de submap van de hulpprogramma's onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x door hulpprogramma's voor een cd, bijvoorbeeld in te voeren:</span><span class="sxs-lookup"><span data-stu-id="49c24-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="49c24-122">Voer het script.\InstallElasticDatabaseJobsCmdlets.ps1 om te kopiëren van de map ElasticDatabaseJobs naar $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="49c24-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="49c24-123">Hiermee wordt de module voor gebruik, bijvoorbeeld ook automatisch geïmporteerd:</span><span class="sxs-lookup"><span data-stu-id="49c24-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="49c24-124">De elastische taken databaseonderdelen installeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="49c24-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="49c24-125">Start een Microsoft Azure PowerShell-opdrachtvenster en navigeer naar de submap \tools onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: Typ cd \tools</span><span class="sxs-lookup"><span data-stu-id="49c24-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="49c24-126">De.\InstallElasticDatabaseJobs.ps1 PowerShell-script uitvoeren en waarden voor de aangevraagde variabelen opgeven.</span><span class="sxs-lookup"><span data-stu-id="49c24-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="49c24-127">Dit script maakt de onderdelen beschreven in [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing) samen met de Azure-Cloudservice voor het gebruik van de afhankelijke onderdelen op de juiste wijze configureren.</span><span class="sxs-lookup"><span data-stu-id="49c24-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="49c24-128">Wanneer u deze opdracht een venster uitvoert weergegeven waarin een **gebruikersnaam** en **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="49c24-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="49c24-129">Dit is niet uw Azure-referenties, voer de gebruikersnaam en wachtwoord op dat de administrator-aanmeldgegevens die u wilt maken voor de nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="49c24-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="49c24-130">De parameters die worden geleverd op voor dit voorbeeld aanroepen kunnen worden gewijzigd voor de gewenste instellingen.</span><span class="sxs-lookup"><span data-stu-id="49c24-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="49c24-131">Het volgende bevat meer informatie over het gedrag van elke parameter:</span><span class="sxs-lookup"><span data-stu-id="49c24-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="49c24-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="49c24-132">Parameter</span></span></th>
    <th><span data-ttu-id="49c24-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="49c24-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="49c24-134">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="49c24-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="49c24-135">Bevat de naam van de Azure-resourcegroep gemaakt om de zojuist gemaakte Azure onderdelen bevatten.</span><span class="sxs-lookup"><span data-stu-id="49c24-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="49c24-136">Deze parameter wordt standaard ingesteld op '__ElasticDatabaseJob'.</span><span class="sxs-lookup"><span data-stu-id="49c24-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="49c24-137">Het is niet raadzaam om deze waarde te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="49c24-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="49c24-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="49c24-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="49c24-139">Biedt de Azure-locatie moet worden gebruikt voor de zojuist gemaakte Azure-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="49c24-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="49c24-140">Deze parameter wordt standaard ingesteld op de locatie VS-midden.</span><span class="sxs-lookup"><span data-stu-id="49c24-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="49c24-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="49c24-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="49c24-142">Geeft het aantal werknemers van de service te installeren.</span><span class="sxs-lookup"><span data-stu-id="49c24-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="49c24-143">Deze parameter wordt standaard ingesteld op 1.</span><span class="sxs-lookup"><span data-stu-id="49c24-143">This parameter defaults to 1.</span></span> <span data-ttu-id="49c24-144">Een hoger aantal werknemers kan worden gebruikt voor het schalen van de service en voor maximale beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="49c24-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="49c24-145">Het verdient aanbeveling gebruik '2' voor implementaties die hoge beschikbaarheid van de service vereist.</span><span class="sxs-lookup"><span data-stu-id="49c24-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="49c24-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="49c24-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="49c24-147">De VM-grootte biedt voor gebruik in de Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="49c24-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="49c24-148">Deze parameter wordt standaard ingesteld op A0.</span><span class="sxs-lookup"><span data-stu-id="49c24-148">This parameter defaults to A0.</span></span> <span data-ttu-id="49c24-149">Parameterwaarden van A0/A1/A2/A3, waardoor de werkrol de grootte van een extra klein/klein/gemiddeld/groot, respectievelijk gebruiken worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="49c24-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="49c24-150">Voor meer informatie over grootten voor worker-rol, Zie [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="49c24-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="49c24-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="49c24-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="49c24-152">Biedt de serviceniveaudoelstelling voor een Standard-editie.</span><span class="sxs-lookup"><span data-stu-id="49c24-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="49c24-153">Deze parameter de standaardwaarde S0.</span><span class="sxs-lookup"><span data-stu-id="49c24-153">This parameter defaults to S0.</span></span> <span data-ttu-id="49c24-154">Parameterwaarden van S0/S1/S2/S3, waardoor de Azure SQL Database te gebruiken van de respectieve SLO worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="49c24-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="49c24-155">Zie voor meer informatie over SQL Database Slo's [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="49c24-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="49c24-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="49c24-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="49c24-157">Biedt de beheerder gebruikersnaam op voor de nieuwe Azure SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="49c24-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="49c24-158">Wanneer niet wordt opgegeven, wordt een PowerShell-venster referenties geopend om de referenties gevraagd.</span><span class="sxs-lookup"><span data-stu-id="49c24-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="49c24-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="49c24-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="49c24-160">Biedt het beheerderswachtwoord voor de nieuwe Azure SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="49c24-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="49c24-161">Wanneer niet wordt opgegeven, wordt een PowerShell-venster referenties geopend om de referenties gevraagd.</span><span class="sxs-lookup"><span data-stu-id="49c24-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="49c24-162">Voor systemen die zijn gericht op met een groot aantal taken op basis van een groot aantal databases parallel worden uitgevoerd, wordt aanbevolen, zoals parameters opgeven: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="49c24-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="49c24-163">Bijwerken van een bestaande onderdelen installatie voor elastische Database taken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="49c24-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="49c24-164">**Elastische Database taken** binnen een bestaande installatie van de schaal en hoge beschikbaarheid kunnen worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="49c24-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="49c24-165">Dit proces kan bij toekomstige upgrades van servicecode zonder te verwijderen en opnieuw maken van de database.</span><span class="sxs-lookup"><span data-stu-id="49c24-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="49c24-166">Dit proces kan ook worden gebruikt binnen dezelfde versie om de VM-grootte van de service of het aantal worker-server te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="49c24-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="49c24-167">Voer het volgende script met de parameters die zijn bijgewerkt met de waarden van uw keuze voor het bijwerken van de installatie van een VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="49c24-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="49c24-168">Parameter</span><span class="sxs-lookup"><span data-stu-id="49c24-168">Parameter</span></span></th>
  <th><span data-ttu-id="49c24-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="49c24-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="49c24-170">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="49c24-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="49c24-171">Geeft de naam van de Azure-resourcegroep gebruikt wanneer de onderdelen van de taak elastische Database in eerste instantie zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="49c24-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="49c24-172">Deze parameter wordt standaard ingesteld op '__ElasticDatabaseJob'.</span><span class="sxs-lookup"><span data-stu-id="49c24-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="49c24-173">Aangezien het niet aangeraden wordt om deze waarde te wijzigen, mag u geen om op te geven van deze parameter.</span><span class="sxs-lookup"><span data-stu-id="49c24-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="49c24-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="49c24-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="49c24-175">Geeft het aantal werknemers van de service te installeren.</span><span class="sxs-lookup"><span data-stu-id="49c24-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="49c24-176">Deze parameter wordt standaard ingesteld op 1.</span><span class="sxs-lookup"><span data-stu-id="49c24-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="49c24-177">Een hoger aantal werknemers kan worden gebruikt voor het schalen van de service en voor maximale beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="49c24-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="49c24-178">Het verdient aanbeveling gebruik '2' voor implementaties die hoge beschikbaarheid van de service vereist.</span><span class="sxs-lookup"><span data-stu-id="49c24-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="49c24-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="49c24-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="49c24-180">De VM-grootte biedt voor gebruik in de Cloud-Service.</span><span class="sxs-lookup"><span data-stu-id="49c24-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="49c24-181">Deze parameter wordt standaard ingesteld op A0.</span><span class="sxs-lookup"><span data-stu-id="49c24-181">This parameter defaults to A0.</span></span> <span data-ttu-id="49c24-182">Parameterwaarden van A0/A1/A2/A3, waardoor de werkrol de grootte van een extra klein/klein/gemiddeld/groot, respectievelijk gebruiken worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="49c24-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="49c24-183">Voor meer informatie over grootten voor worker-rol, Zie [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="49c24-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="49c24-184">De elastische taken databaseonderdelen installeren via de Portal</span><span class="sxs-lookup"><span data-stu-id="49c24-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="49c24-185">Zodra u hebt [een elastische pool gemaakt](sql-database-elastic-pool-manage-portal.md), kunt u installeren **elastische Database taken** onderdelen waarmee het uitvoeren van beheertaken voor elke database in de elastische groep.</span><span class="sxs-lookup"><span data-stu-id="49c24-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="49c24-186">In tegenstelling tot wanneer met behulp van de **elastische Database taken** APIs PowerShell, de interface van de portal is momenteel beperkt tot alleen uitvoeren op basis van een bestaande toepassingen.</span><span class="sxs-lookup"><span data-stu-id="49c24-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="49c24-187">**Geschatte duur:** 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="49c24-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="49c24-188">Uit de dashboardweergave van de elastische groep via de [Azure Portal](https://portal.azure.com/#) , klikt u op **maken taak**.</span><span class="sxs-lookup"><span data-stu-id="49c24-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="49c24-189">Als u een taak voor het eerst maakt, moet u **elastische Database taken** door te klikken op **PREVIEW-voorwaarden**.</span><span class="sxs-lookup"><span data-stu-id="49c24-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="49c24-190">De voorwaarden accepteren door te klikken op het selectievakje in.</span><span class="sxs-lookup"><span data-stu-id="49c24-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="49c24-191">Klik in de weergave 'Services installeren' **taak REFERENTIES**.</span><span class="sxs-lookup"><span data-stu-id="49c24-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![De services te installeren][1]
5. <span data-ttu-id="49c24-193">Typ een gebruikersnaam en wachtwoord voor een database-beheerder.</span><span class="sxs-lookup"><span data-stu-id="49c24-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="49c24-194">Een nieuwe Azure SQL Database-server is gemaakt als onderdeel van de installatie.</span><span class="sxs-lookup"><span data-stu-id="49c24-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="49c24-195">In deze nieuwe server bekend als de database, een nieuwe database gemaakt en gebruikt voor de metagegevens voor elastische Database taken bevatten.</span><span class="sxs-lookup"><span data-stu-id="49c24-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="49c24-196">De gebruikersnaam en wachtwoord hier gemaakte worden omwille van de logboekregistratie in voor de database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="49c24-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="49c24-197">Een afzonderlijke referentie wordt gebruikt voor de uitvoering van het script op basis van de databases in de pool.</span><span class="sxs-lookup"><span data-stu-id="49c24-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Maak een gebruikersnaam en wachtwoord][2]
6. <span data-ttu-id="49c24-199">Klik op de knop OK.</span><span class="sxs-lookup"><span data-stu-id="49c24-199">Click the OK button.</span></span> <span data-ttu-id="49c24-200">De onderdelen voor u gemaakt in een paar minuten in een nieuw [resourcegroep](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49c24-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="49c24-201">De nieuwe resourcegroep is vastgemaakt aan de start board, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="49c24-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="49c24-202">Taken nadat deze is gemaakt, elastische database (Cloudservice, SQL-Database, Service Bus en opslag) worden gemaakt in de groep.</span><span class="sxs-lookup"><span data-stu-id="49c24-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![resourcegroep in start board][3]
7. <span data-ttu-id="49c24-204">Als u probeert te maken of beheren van een taak, terwijl de taken van de elastische database wordt geïnstalleerd bij het opgeven van **referenties** ziet u het volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="49c24-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Implementatie nog in voortgang][4]

<span data-ttu-id="49c24-206">Als het verwijderen vereist is, moet u de resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="49c24-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="49c24-207">Zie [verwijderen van de onderdelen van de taak elastische Database](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="49c24-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="49c24-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49c24-208">Next steps</span></span>
<span data-ttu-id="49c24-209">Zorg ervoor dat een referentie met de juiste rechten heeft voor uitvoering van het script wordt gemaakt op elke database in de groep, Zie voor meer informatie [SQL Database beveiligen](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="49c24-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="49c24-210">Zie [maken en beheren van de taken voor een elastische Database](sql-database-elastic-jobs-create-and-manage.md) aan de slag.</span><span class="sxs-lookup"><span data-stu-id="49c24-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
