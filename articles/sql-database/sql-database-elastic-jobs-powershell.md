---
title: aaaCreate en beheren van elastische taken met behulp van PowerShell | Microsoft Docs
description: PowerShell toomanage Azure SQL Database-groepen gebruikt
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="ee4be-103">Maken en beheren van de SQL-Database van de elastische taken met behulp van PowerShell (preview)</span><span class="sxs-lookup"><span data-stu-id="ee4be-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="ee4be-104">Hallo PowerShell APIs voor **elastische Database taken** (in preview) kunt u definiëren van een groep met databases op basis waarvan de scripts worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="ee4be-105">Dit artikel laat zien hoe toocreate en beheren van **elastische Database taken** met PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="ee4be-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="ee4be-106">Zie [elastische taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee4be-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee4be-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ee4be-107">Prerequisites</span></span>
* <span data-ttu-id="ee4be-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ee4be-108">An Azure subscription.</span></span> <span data-ttu-id="ee4be-109">Zie voor een gratis proefversie [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee4be-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ee4be-110">Een set databases die zijn gemaakt met Hallo-hulpprogramma's voor elastische Database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="ee4be-111">Zie [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ee4be-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="ee4be-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee4be-112">Azure PowerShell.</span></span> <span data-ttu-id="ee4be-113">Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ee4be-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="ee4be-114">**Elastische Database taken** PowerShell pakket: Zie [elastische Database installeren taken](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="ee4be-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="ee4be-115">Selecteer uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="ee4be-115">Select your Azure subscription</span></span>
<span data-ttu-id="ee4be-116">tooselect hello abonnement, moet u uw abonnements-Id (**- SubscriptionId**) of de naam van abonnement (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="ee4be-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="ee4be-117">Als u meerdere abonnementen hebt kunt u Hallo uitvoeren **Get-AzureRmSubscription** cmdlet en kopieer Hallo gewenst abonnementsgegevens van Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="ee4be-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="ee4be-118">Zodra u hebt uw abonnementsgegevens, Hallo commandlet tooset na dit abonnement uitgevoerd als Hallo standaard, namelijk Hallo doel voor het maken en beheren van taken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="ee4be-119">Hallo [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) wordt aanbevolen voor gebruik toodevelop en PowerShell-scripts uitvoeren op Hallo elastische Database taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ee4be-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="ee4be-120">Elastische taken databaseobjecten</span><span class="sxs-lookup"><span data-stu-id="ee4be-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="ee4be-121">Hallo volgende Tabellijsten uit alle objecttypen Hallo van **elastische Database taken** samen met de beschrijving en de relevante PowerShell APIs.</span><span class="sxs-lookup"><span data-stu-id="ee4be-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="ee4be-122">Objecttype</span><span class="sxs-lookup"><span data-stu-id="ee4be-122">Object Type</span></span></th>
    <th><span data-ttu-id="ee4be-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ee4be-123">Description</span></span></th>
    <th><span data-ttu-id="ee4be-124">Gerelateerde PowerShell API 's</span><span class="sxs-lookup"><span data-stu-id="ee4be-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="ee4be-125">Referentie</span><span class="sxs-lookup"><span data-stu-id="ee4be-125">Credential</span></span></td>
    <td><span data-ttu-id="ee4be-126">Gebruikersnaam en wachtwoord toouse bij het verbinden van toodatabases voor uitvoering van scripts of de toepassing van DACPACs.</span><span class="sxs-lookup"><span data-stu-id="ee4be-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="ee4be-127">Hallo-wachtwoord is versleuteld voordat tooand opslaan in Hallo elastische taken van de Database-database worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ee4be-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="ee4be-128">Hallo-wachtwoord worden ontsleuteld door Hallo Hallo referentie gemaakt en dat is geüpload van het script voor installatie Hallo elastische taken van de Database-service.</span><span class="sxs-lookup"><span data-stu-id="ee4be-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="ee4be-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="ee4be-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="ee4be-130">Nieuwe AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="ee4be-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="ee4be-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="ee4be-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="ee4be-132">Script</span><span class="sxs-lookup"><span data-stu-id="ee4be-132">Script</span></span></td>
    <td><span data-ttu-id="ee4be-133">Toobe van Transact-SQL-script gebruikt voor uitvoering tussen databases.</span><span class="sxs-lookup"><span data-stu-id="ee4be-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="ee4be-134">Hallo script moet opgestelde toobe idempotent omdat het Hallo-service wordt opnieuw geprobeerd de uitvoering van script Hallo bij fouten.</span><span class="sxs-lookup"><span data-stu-id="ee4be-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="ee4be-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="ee4be-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="ee4be-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="ee4be-137">Nieuwe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="ee4be-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="ee4be-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="ee4be-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="ee4be-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="ee4be-139">DACPAC</span></span></td>
    <td><span data-ttu-id="ee4be-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">-Gegevenslaagtoepassing </a> toobe toegepast tussen databases van het pakket.</span><span class="sxs-lookup"><span data-stu-id="ee4be-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="ee4be-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="ee4be-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="ee4be-142">Nieuwe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="ee4be-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="ee4be-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="ee4be-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="ee4be-144">Database-doel</span><span class="sxs-lookup"><span data-stu-id="ee4be-144">Database Target</span></span></td>
    <td><span data-ttu-id="ee4be-145">Database- en geef een naam aan wijzen tooan Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="ee4be-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="ee4be-147">Nieuwe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="ee4be-148">Doel van shard-kaart</span><span class="sxs-lookup"><span data-stu-id="ee4be-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="ee4be-149">Combinatie van een doel van de database en een referentie-toobe gebruikt toodetermine informatie opgeslagen in een elastische Database shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ee4be-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="ee4be-151">Nieuwe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="ee4be-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="ee4be-153">Doel van de aangepaste verzameling</span><span class="sxs-lookup"><span data-stu-id="ee4be-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="ee4be-154">Gedefinieerde groep databases toocollectively gebruiken voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="ee4be-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="ee4be-156">Nieuwe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="ee4be-157">Aangepaste verzameling onderliggende doel</span><span class="sxs-lookup"><span data-stu-id="ee4be-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="ee4be-158">Database-doel waarnaar wordt verwezen in een aangepaste verzameling.</span><span class="sxs-lookup"><span data-stu-id="ee4be-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-159">Voeg AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="ee4be-160">Verwijder AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="ee4be-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="ee4be-161">Job</span><span class="sxs-lookup"><span data-stu-id="ee4be-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-162">Definitie van de parameters voor een taak die gebruikt tootrigger uitvoering of toofulfill een planning worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="ee4be-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="ee4be-164">Nieuwe AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="ee4be-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="ee4be-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="ee4be-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="ee4be-166">Uitvoeren van taak</span><span class="sxs-lookup"><span data-stu-id="ee4be-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-167">Container van de benodigde toofulfill taken uitvoeren van een script of toepassen van een DACPAC tooa doel met referenties voor databaseverbindingen met fouten in overeenstemming tooan uitvoeringsbeleid behandeld.</span><span class="sxs-lookup"><span data-stu-id="ee4be-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="ee4be-169">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="ee4be-170">Stop AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="ee4be-171">Wacht AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="ee4be-172">Uitvoering van de taak taak</span><span class="sxs-lookup"><span data-stu-id="ee4be-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-173">De eenheid van werk toofulfill een taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="ee4be-174">Als een taak niet kunnen toosuccessfully uitvoeren, Hallo resulterende uitzondering vastgelegd en een nieuwe, overeenkomende projecttaak worden gemaakt en uitgevoerd in overeenstemming toohello opgegeven uitvoeringsbeleid.</span><span class="sxs-lookup"><span data-stu-id="ee4be-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="ee4be-176">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="ee4be-177">Stop AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="ee4be-178">Wacht AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="ee4be-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="ee4be-179">Taak uitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="ee4be-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-180">Besturingselementen taak uitvoering time-outs, limieten voor nieuwe pogingen en interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="ee4be-181">Elastische taken van de Database bevat een standaarduitvoeringsbeleid taak waardoor in feite oneindige pogingen van de mislukte taak met exponentieel uitstel intervallen tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="ee4be-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="ee4be-183">Nieuwe AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="ee4be-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="ee4be-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="ee4be-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="ee4be-185">Planning</span><span class="sxs-lookup"><span data-stu-id="ee4be-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-186">Specificatie voor uitvoering tootake plaats in een interval van terugkerende of één keer op basis van tijd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="ee4be-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="ee4be-188">Nieuwe AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="ee4be-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="ee4be-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="ee4be-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="ee4be-190">Taak wordt geactiveerd</span><span class="sxs-lookup"><span data-stu-id="ee4be-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="ee4be-191">Een toewijzing tussen een taak en een planning tootrigger taakuitvoering volgens planning toohello.</span><span class="sxs-lookup"><span data-stu-id="ee4be-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="ee4be-192">Nieuwe AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="ee4be-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="ee4be-193">Verwijder AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="ee4be-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="ee4be-194">Ondersteunde elastische Database taken groeperen typen</span><span class="sxs-lookup"><span data-stu-id="ee4be-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="ee4be-195">Hallo-taak uitgevoerd (T-SQL) Transact-SQL-scripts of de toepassing van DACPACs in een groep van databases.</span><span class="sxs-lookup"><span data-stu-id="ee4be-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="ee4be-196">Wanneer een taak verzonden toobe uitgevoerd wordt via aangevraagd een groep van databases, Hallo-taak 'breidt' hello naar onderliggende taken waarbij elk Hallo uitvoert uitgevoerd op een individuele database in het Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="ee4be-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="ee4be-197">Er zijn twee typen groepen die u kunt maken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="ee4be-198">[Shard-toewijzing](sql-database-elastic-scale-shard-map-management.md) groep: wanneer een taak verzonden tootarget een shard-toewijzing is, Hallo taak Hallo shard-toewijzing toodetermine vraagt de huidige set shards en maakt vervolgens onderliggende taken voor elke shard in Hallo shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ee4be-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="ee4be-199">Verzamelgroep voor de aangepaste: een aangepaste set van databases gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="ee4be-200">Wanneer een taak is bedoeld voor een aangepaste verzameling, wordt gemaakt onderliggende taken voor elke database die momenteel in een aangepaste verzameling Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee4be-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="ee4be-201">tooset hello elastische taken voor databaseverbinding</span><span class="sxs-lookup"><span data-stu-id="ee4be-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="ee4be-202">Een verbinding moet toobe set toohello taken *beheer database* voorafgaande toousing Hallo taken API's.</span><span class="sxs-lookup"><span data-stu-id="ee4be-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="ee4be-203">Deze cmdlet uitvoert, activeert een referentie venster toopop up aanvragen Hallo-gebruikersnaam en wachtwoord die zijn gemaakt tijdens de installatie van de taken van de elastische Database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="ee4be-204">Alle voorbeelden in dit onderwerp wordt ervan uitgegaan dat al deze eerste stap is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="ee4be-205">Open een verbinding toohello elastische Database taken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="ee4be-206">Versleutelde referenties binnen Hallo-taken voor elastische Database</span><span class="sxs-lookup"><span data-stu-id="ee4be-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="ee4be-207">Databasereferenties kunnen worden ingevoegd in Hallo taken *beheer database* met het wachtwoord dat is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="ee4be-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="ee4be-208">Is het nodig toostore referenties tooenable taken toobe uitgevoerd op een later tijdstip (met behulp van de taakschema's).</span><span class="sxs-lookup"><span data-stu-id="ee4be-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="ee4be-209">Versleuteling werkt via een certificaat gemaakt als onderdeel van het script voor installatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee4be-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="ee4be-210">Hallo installatiescript maakt en uploads Hallo certificaat in hello Azure Cloud Service voor het ontsleutelen van Hallo opgeslagen gecodeerde wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="ee4be-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="ee4be-211">Hello Azure Cloud Service later slaat de openbare sleutel Hallo binnen Hallo taken *beheer database* waardoor Hallo PowerShell API of de klassieke Azure-Portal interface tooencrypt een verstrekte wachtwoord zonder Hallo certificaat toobe lokaal zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="ee4be-212">Hallo referentie wachtwoorden zijn versleuteld en beveiligd van gebruikers met alleen-lezentoegang tooElastic databaseobjecten taken.</span><span class="sxs-lookup"><span data-stu-id="ee4be-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="ee4be-213">Maar het is mogelijk dat een kwaadwillende gebruiker met lees-/ schrijftoegang tooElastic Database taken objecten tooextract een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ee4be-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="ee4be-214">Referenties zijn ontworpen toobe hele taak uitvoeringen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ee4be-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="ee4be-215">Referenties worden tootarget databases doorgegeven bij het tot stand brengen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="ee4be-216">Er zijn momenteel geen beperkingen op Hallo doeldatabases gebruikt voor elke referentie, kwaadwillende gebruiker kan een database-doel voor een database onder het beheer van Hallo kwaadwillende gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="ee4be-217">Hallo-gebruiker kan vervolgens een taak die gericht is op deze database toogain Hallo referentie wachtwoord starten.</span><span class="sxs-lookup"><span data-stu-id="ee4be-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="ee4be-218">Aanbevolen beveiligingsprocedures voor elastische Database taken omvatten:</span><span class="sxs-lookup"><span data-stu-id="ee4be-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="ee4be-219">Informatie over het gebruik van Hallo-API's tootrusted personen wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="ee4be-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="ee4be-220">Referenties hebt Hallo minimale bevoegdheden nodig tooperform Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="ee4be-221">Meer informatie ziet u binnen dit [autorisatie en machtigingen](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN-artikel.</span><span class="sxs-lookup"><span data-stu-id="ee4be-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="ee4be-222">toocreate een versleutelde referentie voor het uitvoeren van de taak voor databases</span><span class="sxs-lookup"><span data-stu-id="ee4be-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="ee4be-223">een nieuwe versleuteld toocreate referenties, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) vraagt om een gebruikersnaam en wachtwoord die kan worden doorgegeven toohello [ **nieuw AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="ee4be-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="ee4be-224">tooupdate referenties</span><span class="sxs-lookup"><span data-stu-id="ee4be-224">tooupdate credentials</span></span>
<span data-ttu-id="ee4be-225">Wanneer wachtwoorden wijzigen, gebruikt u Hallo [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) en set Hallo **CredentialName** parameter.</span><span class="sxs-lookup"><span data-stu-id="ee4be-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="ee4be-226">een elastische Database shard-toewijzing doel toodefine</span><span class="sxs-lookup"><span data-stu-id="ee4be-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="ee4be-227">een taak op alle databases in een set shard tooexecute (gemaakt met behulp van [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)), een shard-toewijzing met als doel voor Hallo-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee4be-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="ee4be-228">Dit voorbeeld vereist een shard-toepassing gemaakt met behulp van Hallo-clientbibliotheek voor elastische Database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="ee4be-229">Zie [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ee4be-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="ee4be-230">Hallo shard kaart manager-database moet worden ingesteld als het doel van een database en vervolgens Hallo specifieke shard-toewijzing moet worden opgegeven als een doel.</span><span class="sxs-lookup"><span data-stu-id="ee4be-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="ee4be-231">Maken van een T-SQL-Script voor uitvoering tussen databases</span><span class="sxs-lookup"><span data-stu-id="ee4be-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="ee4be-232">Bij het maken van T-SQL-scripts voor de uitvoering van het is raadzaam toobuild ze toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) en robuuste tegen fouten.</span><span class="sxs-lookup"><span data-stu-id="ee4be-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="ee4be-233">Elastische Database-taken opnieuw uitvoeren van het script als een fout optreedt, ongeacht het Hallo-classificatie van Hallo fout wordt aangetroffen die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="ee4be-234">Gebruik Hallo [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate en opslaan van een script voor uitvoering en stel Hallo **- ContentName** en **- CommandText**parameters.</span><span class="sxs-lookup"><span data-stu-id="ee4be-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="ee4be-235">Een nieuw script maken vanuit een bestand</span><span class="sxs-lookup"><span data-stu-id="ee4be-235">Create a new script from a file</span></span>
<span data-ttu-id="ee4be-236">Als Hallo T-SQL-script is gedefinieerd in een bestand, moet u dit tooimport Hallo-script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="ee4be-237">tooupdate een T-SQL-script voor uitvoering tussen databases</span><span class="sxs-lookup"><span data-stu-id="ee4be-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="ee4be-238">Deze updates PowerShell-script Hallo T-SQL-opdrachttekst voor een bestaand script.</span><span class="sxs-lookup"><span data-stu-id="ee4be-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="ee4be-239">Set Hallo variabelen tooreflect Hallo gewenst script definitie toobe set te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="ee4be-240">tooupdate hello definitie tooan bestaand script</span><span class="sxs-lookup"><span data-stu-id="ee4be-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="ee4be-241">toocreate een taak tooexecute een script in een shard-toewijzing</span><span class="sxs-lookup"><span data-stu-id="ee4be-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="ee4be-242">Deze PowerShell-script start een taak voor uitvoering van een script dat op elke shard in een elastische Schaalfunctionaliteit van shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="ee4be-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="ee4be-243">Set Hallo na variabelen tooreflect Hallo gewenst script en het doel:</span><span class="sxs-lookup"><span data-stu-id="ee4be-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="ee4be-244">een taak tooexecute</span><span class="sxs-lookup"><span data-stu-id="ee4be-244">tooexecute a job</span></span>
<span data-ttu-id="ee4be-245">Deze PowerShell-script wordt een bestaande taak uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ee4be-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="ee4be-246">Hallo variabele tooreflect Hallo gewenst taak naam toohave uitgevoerd na bijwerken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="ee4be-247">tooretrieve hello status van het uitvoeren van een enkele taak</span><span class="sxs-lookup"><span data-stu-id="ee4be-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="ee4be-248">Gebruik Hallo [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) en set Hallo **JobExecutionId** parameter tooview Hallo status van taak kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="ee4be-249">Gebruik dezelfde Hallo **Get-AzureSqlJobExecution** cmdlet Hello **voor IncludeChildren** namelijk Hallo specifieke status voor elke taak uitvoeren voor elke parameter tooview Hallo status van onderliggende taak uitvoeringen, de database is gericht door Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="ee4be-250">tooview hello staat tussen meerdere taak uitvoeringen</span><span class="sxs-lookup"><span data-stu-id="ee4be-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="ee4be-251">Hallo [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) heeft meerdere optionele parameters die gebruikt toodisplay worden kunnen meerdere taak uitvoeringen, gefilterd via Hallo opgegeven parameters.</span><span class="sxs-lookup"><span data-stu-id="ee4be-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="ee4be-252">Hallo hieronder toont een aantal Hallo mogelijke manieren toouse Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="ee4be-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="ee4be-253">Alle actieve taken voor de bovenste niveau uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="ee4be-254">Alle bovenste niveau taak uitvoeringen, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="ee4be-255">Alle onderliggende taak uitvoeringen van een opgegeven taak uitvoerings-ID, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="ee4be-256">Ophalen van alle taak uitvoeringen gemaakt met behulp van een planning / taak combinatie, met inbegrip van niet-actieve taken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="ee4be-257">Alle taken die gericht is op een opgegeven shard-kaart, inclusief niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="ee4be-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="ee4be-258">Alle taken die gericht is op een opgegeven aangepaste verzameling, met inbegrip van niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="ee4be-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="ee4be-259">Hallo-lijst met taak taak uitvoeringen binnen het uitvoeren van een specifieke taak ophalen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="ee4be-260">Taak uitvoeren taakdetails ophalen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="ee4be-261">Hallo volgende PowerShell-script kan gebruikte tooview Hallo details van een taak uitvoering van taken, die bijzonder nuttig is bij het opsporen van fouten in uitvoering zijn.</span><span class="sxs-lookup"><span data-stu-id="ee4be-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="ee4be-262">tooretrieve storingen in taak taak uitvoeringen</span><span class="sxs-lookup"><span data-stu-id="ee4be-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="ee4be-263">Hallo **JobTaskExecution object** bevat een eigenschap voor de levenscyclus van taak samen met een berichteigenschap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee4be-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="ee4be-264">Als de uitvoering van de taak een taak is mislukt, Hallo lifecycle eigenschap te worden ingesteld*mislukt* en wordt de berichteigenschap Hallo ingesteld resulterende uitzonderingsbericht toohello en de stack.</span><span class="sxs-lookup"><span data-stu-id="ee4be-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="ee4be-265">Als een taak is mislukt, is het belangrijk tooview Hallo details van de taken die voor een bepaalde taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ee4be-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="ee4be-266">toowait voor een taak uitvoeren toocomplete</span><span class="sxs-lookup"><span data-stu-id="ee4be-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="ee4be-267">Hallo volgende PowerShell-script kan gebruikte toowait voor een taak taak toocomplete zijn:</span><span class="sxs-lookup"><span data-stu-id="ee4be-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="ee4be-268">Maken van een aangepaste uitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="ee4be-268">Create a custom execution policy</span></span>
<span data-ttu-id="ee4be-269">Elastische Database taken ondersteunt het maken van aangepaste uitvoeringsbeleidsregels die kunnen worden toegepast wanneer u taken start.</span><span class="sxs-lookup"><span data-stu-id="ee4be-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="ee4be-270">Uitvoeringsbeleidsregels toestaan op dit moment voor het definiëren van:</span><span class="sxs-lookup"><span data-stu-id="ee4be-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="ee4be-271">Naam: Id voor het uitvoeringsbeleid Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee4be-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="ee4be-272">De time-out van de taak: Totale tijd voordat een taak met elastische taken van de Database, worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="ee4be-273">Eerste Interval voor opnieuw proberen: Interval toowait voordat de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="ee4be-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="ee4be-274">Maximale Interval voor opnieuw proberen: Cap van opnieuw intervallen toouse.</span><span class="sxs-lookup"><span data-stu-id="ee4be-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="ee4be-275">Probeer het opnieuw Interval Backoff Coefficient: Coefficient gebruikt toocalculate Hallo volgende interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="ee4be-276">Hallo volgende formule gebruikt: (eerste Interval voor opnieuw proberen) * Math.pow ((Interval Backoff Coefficient) (nummer van pogingen) - 2).</span><span class="sxs-lookup"><span data-stu-id="ee4be-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="ee4be-277">Maximum aantal pogingen: Hallo maximum aantal nieuwe pogingen pogingen tooperform in een job.</span><span class="sxs-lookup"><span data-stu-id="ee4be-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="ee4be-278">Hallo standaarduitvoeringsbeleid Hallo volgende waarden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="ee4be-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="ee4be-279">Naam: Standaarduitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="ee4be-279">Name: Default execution policy</span></span>
* <span data-ttu-id="ee4be-280">De time-out van de taak: 1 week</span><span class="sxs-lookup"><span data-stu-id="ee4be-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="ee4be-281">Eerste Interval voor opnieuw proberen: 100 milliseconden</span><span class="sxs-lookup"><span data-stu-id="ee4be-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="ee4be-282">Maximale Interval voor opnieuw proberen: 30 minuten</span><span class="sxs-lookup"><span data-stu-id="ee4be-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="ee4be-283">Coefficient Interval opnieuw proberen: 2</span><span class="sxs-lookup"><span data-stu-id="ee4be-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="ee4be-284">Maximum aantal pogingen: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="ee4be-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="ee4be-285">Hallo gewenst uitvoeringsbeleid maken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="ee4be-286">Een aangepaste uitvoeringsbeleid bijwerken</span><span class="sxs-lookup"><span data-stu-id="ee4be-286">Update a custom execution policy</span></span>
<span data-ttu-id="ee4be-287">Hallo gewenst uitvoering beleid tooupdate bijwerken:</span><span class="sxs-lookup"><span data-stu-id="ee4be-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="ee4be-288">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="ee4be-288">Cancel a job</span></span>
<span data-ttu-id="ee4be-289">Elastische Database taken ondersteunt aanvragen van de annulering van taken.</span><span class="sxs-lookup"><span data-stu-id="ee4be-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="ee4be-290">Als taken voor elastische Database een annuleringsverzoek voor een taak die momenteel wordt uitgevoerd detecteert, wordt geprobeerd toostop Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="ee4be-291">Er zijn twee verschillende manieren dat elastische Database taken een annulering kan uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ee4be-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="ee4be-292">Annuleren taken momenteel worden uitgevoerd: als een annulering wordt gedetecteerd, terwijl een taak die momenteel wordt uitgevoerd, een annulering wordt geprobeerd binnen Hallo aspect van Hallo taak momenteel wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="ee4be-293">Bijvoorbeeld: als er een langdurige query die momenteel wordt uitgevoerd wanneer een annulering wordt uitgevoerd, zal er een poging toocancel Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="ee4be-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="ee4be-294">Nieuwe pogingen taak annuleren: als een annulering wordt gedetecteerd door Hallo besturingselement thread voordat een taak voor uitvoering wordt gestart, Hallo besturingselement threads wordt voorkomen Hallo taak starten en Hallo aanvraag declareren als geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="ee4be-295">Als een taak annulering is aangevraagd voor een bovenliggende taak, wordt Hallo annuleringsverzoek ingewilligd voor Hallo bovenliggende taak en alle bijbehorende onderliggende taken.</span><span class="sxs-lookup"><span data-stu-id="ee4be-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="ee4be-296">toosubmit een annuleringsverzoek gebruiken Hallo [ **cmdlet Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) en set Hallo **JobExecutionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="ee4be-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="ee4be-297">een taak toodelete en Taakgeschiedenis asynchroon</span><span class="sxs-lookup"><span data-stu-id="ee4be-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="ee4be-298">Elastische taken van de Database biedt ondersteuning voor asynchrone verwijderen van jobs.</span><span class="sxs-lookup"><span data-stu-id="ee4be-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="ee4be-299">Een taak kan worden gemarkeerd voor verwijdering en Hallo system Hallo taak en de taakgeschiedenis wordt verwijderd nadat alle taak uitvoeringen voor Hallo taak hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="ee4be-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="ee4be-300">Hallo-systeem wordt niet automatisch uitvoeringen van de actieve taak geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="ee4be-301">Aanroepen [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel actieve taak uitvoeringen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="ee4be-302">tootrigger taak verwijderen, gebruik Hallo [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) en set Hallo **JobName** parameter.</span><span class="sxs-lookup"><span data-stu-id="ee4be-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="ee4be-303">het doel van een aangepaste database toocreate</span><span class="sxs-lookup"><span data-stu-id="ee4be-303">toocreate a custom database target</span></span>
<span data-ttu-id="ee4be-304">U kunt aangepaste database doelen voor directe uitvoering of voor insluiting in een aangepaste database wilt definiëren.</span><span class="sxs-lookup"><span data-stu-id="ee4be-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="ee4be-305">Bijvoorbeeld, omdat **elastische pools** zijn nog niet rechtstreeks ondersteund met behulp van PowerShell APIs, kunt u een aangepaste database doel en de aangepaste database verzameling doel op die alle Hallo-databases in de groep Hallo omvat.</span><span class="sxs-lookup"><span data-stu-id="ee4be-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="ee4be-306">Hallo variabelen tooreflect Hallo gewenst databasegegevens volgende instellen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="ee4be-307">een verzameling aangepaste database doel toocreate</span><span class="sxs-lookup"><span data-stu-id="ee4be-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="ee4be-308">Gebruik Hallo [ **nieuw AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine een aangepaste database verzameling doel tooenable uitvoering tussen meerdere gedefinieerde database doelen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="ee4be-309">Na het maken van een databasegroep, kunnen de databases worden gekoppeld aan Hallo aangepaste verzameling doel.</span><span class="sxs-lookup"><span data-stu-id="ee4be-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="ee4be-310">Stel Hallo variabelen tooreflect Hallo gewenste aangepaste verzameling doelconfiguratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee4be-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="ee4be-311">tooadd databases tooa aangepaste database verzameling doel</span><span class="sxs-lookup"><span data-stu-id="ee4be-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="ee4be-312">een database tooa specifieke aangepaste verzameling tooadd gebruiken Hallo [ **toevoegen AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee4be-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="ee4be-313">Hallo-databases binnen een doel van de verzameling aangepaste database controleren</span><span class="sxs-lookup"><span data-stu-id="ee4be-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="ee4be-314">Gebruik Hallo [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve Hallo onderliggende databases binnen een doel van de verzameling aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="ee4be-315">Een taak tooexecute van een script voor een doel van de verzameling aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="ee4be-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="ee4be-316">Gebruik Hallo [ **nieuw AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate een taak op basis van een groep met databases die zijn gedefinieerd door een doel van de verzameling aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="ee4be-317">Elastische taken van de Database wordt Hallo taak uitbreiden naar meerdere onderliggende taken elke overeenkomstige tooa-database die is gekoppeld aan Hallo aangepaste database verzameling doel en zorg ervoor dat Hallo script wordt uitgevoerd tegen elke database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="ee4be-318">Ook is het belangrijk dat scripts idempotent toobe robuuste tooretries zijn.</span><span class="sxs-lookup"><span data-stu-id="ee4be-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="ee4be-319">Gegevens verzamelen over databases</span><span class="sxs-lookup"><span data-stu-id="ee4be-319">Data collection across databases</span></span>
<span data-ttu-id="ee4be-320">U kunt een taak tooexecute een query gebruiken in een groep met databases en Hallo resultaten tooa specifieke tabel verzenden.</span><span class="sxs-lookup"><span data-stu-id="ee4be-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="ee4be-321">Hallo tabel kan worden opgevraagd na Hallo feit toosee Hallo queryresultaat van elke database.</span><span class="sxs-lookup"><span data-stu-id="ee4be-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="ee4be-322">Dit biedt een asynchrone methode tooexecute een query tussen meerdere databases.</span><span class="sxs-lookup"><span data-stu-id="ee4be-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="ee4be-323">Mislukte pogingen worden automatisch verwerkt via de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="ee4be-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="ee4be-324">de opgegeven doeltabel Hallo worden automatisch gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="ee4be-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="ee4be-325">de nieuwe tabel Hallo komt overeen met schema Hallo Hallo heeft een resultatenset geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="ee4be-326">Als meerdere resultatensets worden geretourneerd door een script, verzendt elastische Database taken alleen Hallo eerste toohello doeltabel.</span><span class="sxs-lookup"><span data-stu-id="ee4be-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="ee4be-327">Hallo volgende PowerShell-script een script wordt uitgevoerd en verzamelt de resultaten in een opgegeven tabel.</span><span class="sxs-lookup"><span data-stu-id="ee4be-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="ee4be-328">Dit script wordt ervan uitgegaan dat een T-SQL-script is gemaakt waarmee een enkelvoudig resultaat wordt verkregen set levert en dat er een doel van de verzameling aangepaste database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee4be-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="ee4be-329">Dit script maakt gebruik van Hallo [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee4be-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="ee4be-330">Hallo parameters instellen voor script, referenties en uitvoering van doel:</span><span class="sxs-lookup"><span data-stu-id="ee4be-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="ee4be-331">toocreate en start een taak voor scenario's voor het verzamelen van gegevens</span><span class="sxs-lookup"><span data-stu-id="ee4be-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="ee4be-332">Dit script maakt gebruik van Hallo [ **Start AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ee4be-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="ee4be-333">een taak uitvoeren trigger tooschedule</span><span class="sxs-lookup"><span data-stu-id="ee4be-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="ee4be-334">Hallo volgende PowerShell-script kan worden gebruikt toocreate een terugkerend schema.</span><span class="sxs-lookup"><span data-stu-id="ee4be-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="ee4be-335">Dit script maakt gebruik van een minuut interval maar [ **nieuw AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) biedt ook ondersteuning voor parameters - DayInterval, - HourInterval, - MonthInterval, en -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="ee4be-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="ee4be-336">Schema's die slechts één keer worden uitgevoerd, kunnen worden gemaakt door doorgeven - eenmalige.</span><span class="sxs-lookup"><span data-stu-id="ee4be-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="ee4be-337">Maak een nieuwe planning:</span><span class="sxs-lookup"><span data-stu-id="ee4be-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="ee4be-338">een taak uitgevoerd op een tijdschema tootrigger</span><span class="sxs-lookup"><span data-stu-id="ee4be-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="ee4be-339">Een trigger voor de taak kan worden gedefinieerd toohave uitgevoerd volgens tooa tijdschema van een taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="ee4be-340">Hallo volgende PowerShell-script kan worden gebruikt toocreate een trigger taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="ee4be-341">Gebruik [nieuw AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) en set Hallo variabelen toocorrespond toohello gewenste taak en planning:</span><span class="sxs-lookup"><span data-stu-id="ee4be-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="ee4be-342">tooremove een geplande koppeling toostop taak wordt uitgevoerd volgens schema</span><span class="sxs-lookup"><span data-stu-id="ee4be-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="ee4be-343">toodiscontinue taakuitvoering via een taak worden geactiveerd, Hallo taak trigger opnieuw optreedt, kan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ee4be-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="ee4be-344">Verwijderen van een taak trigger toostop een taak uit te voeren volgens tooa schema met behulp van Hallo [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="ee4be-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="ee4be-345">Triggers gebonden tooa tijd taakschema ophalen</span><span class="sxs-lookup"><span data-stu-id="ee4be-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="ee4be-346">Hallo volgende PowerShell-script kan worden gebruikt tooobtain en Hallo taak triggers geregistreerde tooa bepaald tijdschema weergeven.</span><span class="sxs-lookup"><span data-stu-id="ee4be-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="ee4be-347">tooretrieve taak triggers gebonden tooa taak</span><span class="sxs-lookup"><span data-stu-id="ee4be-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="ee4be-348">Gebruik [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain en weergave van schema's met een geregistreerde taak.</span><span class="sxs-lookup"><span data-stu-id="ee4be-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="ee4be-349">een toepassing-gegevenslaagtoepassingen (DACPAC) voor uitvoering tussen databases toocreate</span><span class="sxs-lookup"><span data-stu-id="ee4be-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="ee4be-350">Zie een DACPAC toocreate [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee4be-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="ee4be-351">een DACPAC toodeploy gebruiken Hallo [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="ee4be-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="ee4be-352">Hallo DACPAC moet toegankelijk toohello service.</span><span class="sxs-lookup"><span data-stu-id="ee4be-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="ee4be-353">Het is aanbevolen tooupload een gemaakte DACPAC tooAzure opslag en maak een [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor Hallo DACPAC.</span><span class="sxs-lookup"><span data-stu-id="ee4be-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="ee4be-354">een toepassing-gegevenslaagtoepassingen (DACPAC) voor uitvoering tussen databases tooupdate</span><span class="sxs-lookup"><span data-stu-id="ee4be-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="ee4be-355">Bestaande DACPACs geregistreerd binnen een elastische Database taken kunnen worden bijgewerkt toopoint toonew URI's.</span><span class="sxs-lookup"><span data-stu-id="ee4be-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="ee4be-356">Gebruik Hallo [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI op een bestaande DACPAC geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="ee4be-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="ee4be-357">een taak tooapply een toepassing-gegevenslaagtoepassingen (DACPAC) voor databases toocreate</span><span class="sxs-lookup"><span data-stu-id="ee4be-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="ee4be-358">Nadat een DACPAC binnen elastische taken van de Database is gemaakt, kan een taak kan tooapply hello DACPAC in een groep met databases worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee4be-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="ee4be-359">Hallo volgende PowerShell-script kan gebruikte toocreate een taak DACPAC via een aangepaste verzameling van databases zijn:</span><span class="sxs-lookup"><span data-stu-id="ee4be-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
