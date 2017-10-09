---
title: aaaInstalling elastische database taken | Microsoft Docs
description: Installatie van Hallo elastische taak functie doorlopen.
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
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="e749b-103">Overzicht van de taken installeren elastische Database</span><span class="sxs-lookup"><span data-stu-id="e749b-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="e749b-104">[**Elastische Database taken** ](sql-database-elastic-jobs-overview.md) kan worden geïnstalleerd via PowerShell of via hello Azure Classic Portal.You krijgen toegang tot toocreate en beheren van taken met behulp van PowerShell API Hallo alleen als u Hallo PowerShell pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="e749b-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="e749b-105">Daarnaast Hallo PowerShell APIs bieden aanzienlijk meer functionaliteit dan Hallo-portal op dit moment.</span><span class="sxs-lookup"><span data-stu-id="e749b-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="e749b-106">Als u al hebt geïnstalleerd **elastische Database taken** via Hallo Portal van een bestaand **elastische pool**, Hallo nieuwste Powershell voorbeeldweergave scripts tooupgrade uw bestaande installatie.</span><span class="sxs-lookup"><span data-stu-id="e749b-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="e749b-107">U wordt ten zeerste aanbevolen tooupgrade uw installatie-toohello recente **elastische Database taken** onderdelen in volgorde tootake profiteren van nieuwe functionaliteit die PowerShell APIs Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e749b-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e749b-108">Prerequisites</span></span>
* <span data-ttu-id="e749b-109">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e749b-109">An Azure subscription.</span></span> <span data-ttu-id="e749b-110">Zie voor een gratis proefversie [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e749b-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e749b-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e749b-111">Azure PowerShell.</span></span> <span data-ttu-id="e749b-112">Installeer de meest recente versie Hallo Hallo met [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="e749b-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="e749b-113">Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e749b-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e749b-114">[NuGet-opdrachtregelprogramma](https://nuget.org/nuget.exe) gebruikte tooinstall Hallo elastische Database taken pakket is.</span><span class="sxs-lookup"><span data-stu-id="e749b-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="e749b-115">Zie http://docs.nuget.org/docs/start-here/installing-nuget voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e749b-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="e749b-116">Download en Hallo elastische Database taken PowerShell pakket importeren</span><span class="sxs-lookup"><span data-stu-id="e749b-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="e749b-117">Start Microsoft Azure PowerShell-opdrachtvenster en navigeer toohello directory waar u NuGet-opdrachtregelprogramma (nuget.exe) gedownload.</span><span class="sxs-lookup"><span data-stu-id="e749b-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="e749b-118">Downloaden en importeren **elastische Database taken** pakket in de huidige map Hallo Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e749b-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="e749b-119">Hallo **elastische Database taken** bestanden worden geplaatst in de lokale directory Hallo in een map met de naam **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** waar *x.x.xxxx.x* Hallo-versienummer weerspiegelt.</span><span class="sxs-lookup"><span data-stu-id="e749b-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="e749b-120">Hallo PowerShell-cmdlets (met inbegrip van de vereiste client-dll's) bevinden zich in Hallo **tools\ElasticDatabaseJobs** submappen en Hallo tooinstall van PowerShell-scripts, bijwerkt en verwijdert het ook zich bevinden in Hallo  **hulpprogramma's voor** onderliggende map.</span><span class="sxs-lookup"><span data-stu-id="e749b-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="e749b-121">Navigeer toohello extra submap onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Hallo door hulpprogramma's voor een cd, bijvoorbeeld in te voeren:</span><span class="sxs-lookup"><span data-stu-id="e749b-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="e749b-122">Hallo.\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory in $home\Documents\WindowsPowerShell\Modules uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e749b-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="e749b-123">Dit wordt ook automatisch Hallo-module voor gebruik, bijvoorbeeld geïmporteerd:</span><span class="sxs-lookup"><span data-stu-id="e749b-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="e749b-124">Hallo elastische taken databaseonderdelen installeren met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e749b-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="e749b-125">Start een Microsoft Azure PowerShell-opdrachtvenster en navigeer toohello \tools submap onder de map Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x Hallo: Typ cd \tools</span><span class="sxs-lookup"><span data-stu-id="e749b-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="e749b-126">Hallo.\InstallElasticDatabaseJobs.ps1 PowerShell-script uitvoeren en waarden voor de aangevraagde variabelen opgeven.</span><span class="sxs-lookup"><span data-stu-id="e749b-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="e749b-127">Dit script maakt Hallo-onderdelen die worden beschreven [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing) samen met het configureren van hello Azure Cloud Service tooappropriately Hallo afhankelijke onderdelen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e749b-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="e749b-128">Wanneer u deze opdracht een venster uitvoert weergegeven waarin een **gebruikersnaam** en **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="e749b-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="e749b-129">Dit is niet uw Azure-referenties, Hallo-gebruikersnaam en wachtwoord op dat Hallo beheerdersreferenties u toocreate voor de nieuwe server hello wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="e749b-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="e749b-130">Hallo parameters die worden geleverd op voor dit voorbeeld aanroepen kunnen worden gewijzigd voor de gewenste instellingen.</span><span class="sxs-lookup"><span data-stu-id="e749b-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="e749b-131">de volgende Hallo bevat meer informatie over Hallo gedrag van elke parameter:</span><span class="sxs-lookup"><span data-stu-id="e749b-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="e749b-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="e749b-132">Parameter</span></span></th>
    <th><span data-ttu-id="e749b-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e749b-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="e749b-134">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e749b-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="e749b-135">Biedt hello Azure naam van een resourcegroep gemaakt toocontain hello Azure onderdelen van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e749b-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="e749b-136">Deze parameter standaardwaarden te '__ElasticDatabaseJob'.</span><span class="sxs-lookup"><span data-stu-id="e749b-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="e749b-137">Het is niet aanbevolen toochange deze waarde.</span><span class="sxs-lookup"><span data-stu-id="e749b-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="e749b-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="e749b-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="e749b-139">Biedt hello Azure-locatie toobe gebruikt voor hello Azure onderdelen van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e749b-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="e749b-140">Deze parameter standaard toohello locatie VS-midden.</span><span class="sxs-lookup"><span data-stu-id="e749b-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="e749b-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="e749b-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="e749b-142">Geeft het aantal service werknemers tooinstall Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="e749b-143">Deze parameter standaard too1.</span><span class="sxs-lookup"><span data-stu-id="e749b-143">This parameter defaults too1.</span></span> <span data-ttu-id="e749b-144">Een hoger aantal werknemers mag gebruikte tooscale uit Hallo-service en tooprovide hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="e749b-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="e749b-145">Het verdient aanbeveling toouse '2' voor implementaties die hoge beschikbaarheid van Hallo service vereist.</span><span class="sxs-lookup"><span data-stu-id="e749b-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="e749b-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="e749b-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="e749b-147">Hallo VM-grootte biedt voor gebruik binnen Hallo Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e749b-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="e749b-148">Deze parameter standaard tooA0.</span><span class="sxs-lookup"><span data-stu-id="e749b-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="e749b-149">Parameterwaarden van A0/A1/A2/A3 worden geaccepteerd waardoor Hallo worker rol toouse de grootte van een extra klein/klein/gemiddeld/groot, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="e749b-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="e749b-150">Voor meer informatie over grootten voor worker-rol, Zie [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="e749b-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="e749b-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="e749b-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="e749b-152">Hallo serviceniveaudoelstelling voorziet in een Standard-editie.</span><span class="sxs-lookup"><span data-stu-id="e749b-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="e749b-153">Deze parameter standaard tooS0.</span><span class="sxs-lookup"><span data-stu-id="e749b-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="e749b-154">Parameterwaarden van S0/S1/S2/S3 waardoor hello Azure SQL Database worden geaccepteerd toouse Hallo respectieve SLO.</span><span class="sxs-lookup"><span data-stu-id="e749b-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="e749b-155">Zie voor meer informatie over SQL Database Slo's [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="e749b-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="e749b-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="e749b-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="e749b-157">Hallo beheerder gebruikersnaam op voor Hallo nieuw gemaakte Azure SQL Database-server biedt.</span><span class="sxs-lookup"><span data-stu-id="e749b-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="e749b-158">Wanneer niet wordt opgegeven, wordt een PowerShell-venster referenties tooprompt Hallo referenties geopend.</span><span class="sxs-lookup"><span data-stu-id="e749b-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="e749b-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="e749b-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="e749b-160">Biedt Hallo beheerderswachtwoord voor hello Azure SQL Database-server een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e749b-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="e749b-161">Wanneer niet wordt opgegeven, wordt een PowerShell-venster referenties tooprompt Hallo referenties geopend.</span><span class="sxs-lookup"><span data-stu-id="e749b-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="e749b-162">Voor systemen die zijn gericht op een groot aantal taken die worden uitgevoerd op basis van een groot aantal databases parallel met, het is raadzaam toospecify parameters, zoals: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="e749b-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="e749b-163">Bijwerken van een bestaande onderdelen installatie voor elastische Database taken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e749b-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="e749b-164">**Elastische Database taken** binnen een bestaande installatie van de schaal en hoge beschikbaarheid kunnen worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e749b-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="e749b-165">Dit proces kunt u toekomstige upgrades van servicecode zonder toodrop en maak Hallo beheer database.</span><span class="sxs-lookup"><span data-stu-id="e749b-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="e749b-166">Dit proces kan ook worden gebruikt binnen Hallo dezelfde versie toomodify Hallo service VM-grootte of Hallo worker aantal servers.</span><span class="sxs-lookup"><span data-stu-id="e749b-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="e749b-167">tooupdate hello VM-grootte van een installatie, Voer Hallo script met parameters na bijgewerkt toohello waarden van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="e749b-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="e749b-168">Parameter</span><span class="sxs-lookup"><span data-stu-id="e749b-168">Parameter</span></span></th>
  <th><span data-ttu-id="e749b-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e749b-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="e749b-170">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e749b-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="e749b-171">Identificeert hello Azure Resourcegroepnaam gebruikt wanneer Hallo elastische Database taak onderdelen in eerste instantie zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e749b-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="e749b-172">Deze parameter standaardwaarden te '__ElasticDatabaseJob'.</span><span class="sxs-lookup"><span data-stu-id="e749b-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="e749b-173">Omdat het geen aanbevolen toochange deze waarde u mag geen toospecify deze parameter.</span><span class="sxs-lookup"><span data-stu-id="e749b-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="e749b-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="e749b-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="e749b-175">Geeft het aantal service werknemers tooinstall Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="e749b-176">Deze parameter standaard too1.</span><span class="sxs-lookup"><span data-stu-id="e749b-176">This parameter defaults too1.</span></span>  <span data-ttu-id="e749b-177">Een hoger aantal werknemers mag gebruikte tooscale uit Hallo-service en tooprovide hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="e749b-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="e749b-178">Het verdient aanbeveling toouse '2' voor implementaties die hoge beschikbaarheid van Hallo service vereist.</span><span class="sxs-lookup"><span data-stu-id="e749b-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="e749b-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="e749b-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="e749b-180">Hallo VM-grootte biedt voor gebruik binnen Hallo Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e749b-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="e749b-181">Deze parameter standaard tooA0.</span><span class="sxs-lookup"><span data-stu-id="e749b-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="e749b-182">Parameterwaarden van A0/A1/A2/A3 worden geaccepteerd waardoor Hallo worker rol toouse de grootte van een extra klein/klein/gemiddeld/groot, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="e749b-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="e749b-183">Voor meer informatie over grootten voor worker-rol, Zie [elastische Database taken onderdelen en prijzen](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="e749b-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="e749b-184">Hallo elastische Database taken onderdelen met Hallo Portal installeren</span><span class="sxs-lookup"><span data-stu-id="e749b-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="e749b-185">Zodra u hebt [een elastische pool gemaakt](sql-database-elastic-pool-manage-portal.md), kunt u installeren **elastische Database taken** onderdelen tooenable uitvoeren van beheertaken voor elke database in Hallo elastische pool.</span><span class="sxs-lookup"><span data-stu-id="e749b-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="e749b-186">In tegenstelling tot wanneer met behulp van Hallo **elastische Database taken** PowerShell APIs's Hallo interface van de portal is momenteel beperkt tooonly uitvoering op een bestaande toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e749b-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="e749b-187">**Geschatte tijd toocomplete:** 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="e749b-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="e749b-188">Van de dashboardweergave Hallo van de elastische groep via Hallo Hallo [Azure Portal](https://portal.azure.com/#) , klikt u op **maken taak**.</span><span class="sxs-lookup"><span data-stu-id="e749b-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="e749b-189">Als u een taak voor Hallo eerst maakt, moet u **elastische Database taken** door te klikken op **PREVIEW-voorwaarden**.</span><span class="sxs-lookup"><span data-stu-id="e749b-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="e749b-190">Accepteren Hallo voorwaarden door te klikken op Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="e749b-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="e749b-191">Klik in de weergave Hallo installeren 'services' op **taak REFERENTIES**.</span><span class="sxs-lookup"><span data-stu-id="e749b-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Hallo-services te installeren][1]
5. <span data-ttu-id="e749b-193">Typ een gebruikersnaam en wachtwoord voor een database-beheerder. Als onderdeel van Hallo-installatie, wordt een nieuwe Azure SQL Database-server gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e749b-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="e749b-194">In deze nieuwe server Hallo beheer database, ook wel een nieuwe database wordt gemaakt en toocontain Hallo-metagegevens gebruikt voor elastische Database-taken.</span><span class="sxs-lookup"><span data-stu-id="e749b-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="e749b-195">Hallo-gebruikersnaam en wachtwoord hier gemaakte worden gebruikt voor het Hallo-doel van de logboekregistratie in toohello beheer database.</span><span class="sxs-lookup"><span data-stu-id="e749b-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="e749b-196">Een afzonderlijke referentie wordt gebruikt voor het uitvoeren van script Hallo-databases in de pool Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Maak een gebruikersnaam en wachtwoord][2]
6. <span data-ttu-id="e749b-198">Klik op OK om Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-198">Click hello OK button.</span></span> <span data-ttu-id="e749b-199">Hallo-onderdelen worden gemaakt voor u het over enkele minuten in een nieuw [resourcegroep](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e749b-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e749b-200">de nieuwe resourcegroep Hallo is vastgemaakt toohello start board, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e749b-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="e749b-201">Taken nadat deze is gemaakt, elastische database (Cloudservice, SQL-Database, Service Bus en opslag) worden gemaakt in de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![resourcegroep in start board][3]
7. <span data-ttu-id="e749b-203">Als u toocreate probeert of een taak beheren terwijl taken voor elastische database wordt geïnstalleerd bij het opgeven van **referenties** Hallo volgende bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e749b-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Implementatie nog in voortgang][4]

<span data-ttu-id="e749b-205">Als het verwijderen vereist is, verwijdert u de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="e749b-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="e749b-206">Zie [hoe toouninstall Hallo elastische Database onderdelen taak](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="e749b-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e749b-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e749b-207">Next steps</span></span>
<span data-ttu-id="e749b-208">Zorg ervoor dat een referentie met de juiste rechten Hallo voor uitvoering van het script wordt gemaakt op elke database in de groep hello, Zie voor meer informatie [SQL Database beveiligen](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="e749b-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="e749b-209">Zie [maken en beheren van de taken voor een elastische Database](sql-database-elastic-jobs-create-and-manage.md) tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="e749b-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
