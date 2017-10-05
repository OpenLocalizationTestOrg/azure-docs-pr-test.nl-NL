---
title: Maken en beheren van elastische taken met behulp van PowerShell | Microsoft Docs
description: PowerShell gebruikt voor het beheren van Azure SQL Database-groepen
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="bd90c-103">Maken en beheren van de SQL-Database van de elastische taken met behulp van PowerShell (preview)</span><span class="sxs-lookup"><span data-stu-id="bd90c-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="bd90c-104">De PowerShell-APIs voor **elastische Database taken** (in preview) kunt u definiëren van een groep met databases op basis waarvan de scripts worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="bd90c-105">In dit artikel laat zien hoe maken en beheren van **elastische Database taken** met PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="bd90c-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="bd90c-106">Zie [elastische taken overzicht](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd90c-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bd90c-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bd90c-107">Prerequisites</span></span>
* <span data-ttu-id="bd90c-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bd90c-108">An Azure subscription.</span></span> <span data-ttu-id="bd90c-109">Zie voor een gratis proefversie [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd90c-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bd90c-110">Een set databases die zijn gemaakt met de hulpprogramma's van elastische Database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="bd90c-111">Zie [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bd90c-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="bd90c-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd90c-112">Azure PowerShell.</span></span> <span data-ttu-id="bd90c-113">Zie voor gedetailleerde informatie [Installeren en configureren van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bd90c-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="bd90c-114">**Elastische Database taken** PowerShell pakket: Zie [elastische Database installeren taken](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="bd90c-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="bd90c-115">Selecteer uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="bd90c-115">Select your Azure subscription</span></span>
<span data-ttu-id="bd90c-116">Om het abonnement te selecteren moet u uw abonnements-Id (**- SubscriptionId**) of de naam van abonnement (**- SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="bd90c-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="bd90c-117">U kunt uitvoeren als u meerdere abonnementen hebt de **Get-AzureRmSubscription** cmdlet en kopieert u de informatie over het gewenste abonnement uit de resultatenset is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bd90c-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="bd90c-118">Zodra u de abonnementsgegevens van uw hebt, voer de volgende cmdlet als u dit abonnement de standaard, namelijk het doel voor het maken en beheren van taken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="bd90c-119">De [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) wordt aanbevolen voor gebruik ontwikkelen en uitvoeren van PowerShell-scripts uitvoeren op de elastische Database-taken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="bd90c-120">Elastische taken databaseobjecten</span><span class="sxs-lookup"><span data-stu-id="bd90c-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="bd90c-121">De volgende tabel geeft een lijst van alle objecttypen van **elastische Database taken** samen met de beschrijving en de relevante PowerShell APIs.</span><span class="sxs-lookup"><span data-stu-id="bd90c-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="bd90c-122">Objecttype</span><span class="sxs-lookup"><span data-stu-id="bd90c-122">Object Type</span></span></th>
    <th><span data-ttu-id="bd90c-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bd90c-123">Description</span></span></th>
    <th><span data-ttu-id="bd90c-124">Gerelateerde PowerShell API 's</span><span class="sxs-lookup"><span data-stu-id="bd90c-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="bd90c-125">Referentie</span><span class="sxs-lookup"><span data-stu-id="bd90c-125">Credential</span></span></td>
    <td><span data-ttu-id="bd90c-126">Gebruikersnaam en het wachtwoord moet worden gebruikt wanneer verbinding maken met databases voor uitvoering van scripts of de toepassing van DACPACs.</span><span class="sxs-lookup"><span data-stu-id="bd90c-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="bd90c-127">Het wachtwoord wordt versleuteld vóór het verzenden naar en opslaan in de database van de elastische Database-taken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="bd90c-128">Het wachtwoord worden ontsleuteld door de service elastische Database-taken via de referentie is gemaakt en dat is geüpload van het script voor installatie.</span><span class="sxs-lookup"><span data-stu-id="bd90c-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="bd90c-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="bd90c-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="bd90c-130">Nieuwe AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="bd90c-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="bd90c-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="bd90c-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="bd90c-132">Script</span><span class="sxs-lookup"><span data-stu-id="bd90c-132">Script</span></span></td>
    <td><span data-ttu-id="bd90c-133">Transact-SQL-script moet worden gebruikt voor uitvoering tussen databases.</span><span class="sxs-lookup"><span data-stu-id="bd90c-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="bd90c-134">Het script moet worden gemaakt voor de idempotent worden omdat de service wordt opnieuw geprobeerd de uitvoering van het script op fouten.</span><span class="sxs-lookup"><span data-stu-id="bd90c-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bd90c-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bd90c-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="bd90c-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="bd90c-137">Nieuwe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bd90c-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bd90c-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="bd90c-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="bd90c-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="bd90c-139">DACPAC</span></span></td>
    <td><span data-ttu-id="bd90c-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">-Gegevenslaagtoepassing </a> pakket moet worden toegepast voor databases.</span><span class="sxs-lookup"><span data-stu-id="bd90c-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="bd90c-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bd90c-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bd90c-142">Nieuwe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bd90c-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bd90c-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="bd90c-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="bd90c-144">Database-doel</span><span class="sxs-lookup"><span data-stu-id="bd90c-144">Database Target</span></span></td>
    <td><span data-ttu-id="bd90c-145">Database- en de naam die verwijst naar een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="bd90c-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bd90c-147">Nieuwe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="bd90c-148">Doel van shard-kaart</span><span class="sxs-lookup"><span data-stu-id="bd90c-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="bd90c-149">De combinatie van een doel van de database en een referentie om te worden gebruikt om informatie opgeslagen in een elastische Database shard-toewijzing te bepalen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bd90c-151">Nieuwe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bd90c-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="bd90c-153">Doel van de aangepaste verzameling</span><span class="sxs-lookup"><span data-stu-id="bd90c-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="bd90c-154">Gedefinieerde groep met databases gezamenlijk gebruiken voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="bd90c-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bd90c-156">Nieuwe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="bd90c-157">Aangepaste verzameling onderliggende doel</span><span class="sxs-lookup"><span data-stu-id="bd90c-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="bd90c-158">Database-doel waarnaar wordt verwezen in een aangepaste verzameling.</span><span class="sxs-lookup"><span data-stu-id="bd90c-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-159">Voeg AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="bd90c-160">Verwijder AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="bd90c-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bd90c-161">Job</span><span class="sxs-lookup"><span data-stu-id="bd90c-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-162">Definitie van de parameters voor een taak die kan worden gebruikt voor het activeren van uitvoering of om te voldoen aan een schema.</span><span class="sxs-lookup"><span data-stu-id="bd90c-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="bd90c-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="bd90c-164">Nieuwe AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="bd90c-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="bd90c-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="bd90c-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bd90c-166">Uitvoeren van taak</span><span class="sxs-lookup"><span data-stu-id="bd90c-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-167">Container van taken die nodig zijn om te voldoen aan het uitvoeren van een script of een DACPAC toepassen op een doel met referenties voor databaseverbindingen met fouten verwerkt overeenkomstig een beleid kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bd90c-169">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bd90c-170">Stop AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bd90c-171">Wacht AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="bd90c-172">Uitvoering van de taak taak</span><span class="sxs-lookup"><span data-stu-id="bd90c-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-173">De eenheid van werk om te voldoen aan een taak.</span><span class="sxs-lookup"><span data-stu-id="bd90c-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="bd90c-174">Als een taak kan niet met succes uitvoeren, wordt de resulterende uitzonderingsbericht vastgelegd en een nieuwe, overeenkomende projecttaak worden gemaakt en uitgevoerd volgens het opgegeven uitvoeringsbeleid.</span><span class="sxs-lookup"><span data-stu-id="bd90c-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bd90c-176">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bd90c-177">Stop AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bd90c-178">Wacht AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bd90c-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="bd90c-179">Taak uitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="bd90c-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-180">Besturingselementen taak uitvoering time-outs, limieten voor nieuwe pogingen en interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="bd90c-181">Elastische taken van de Database bevat een standaarduitvoeringsbeleid taak waardoor in feite oneindige pogingen van de mislukte taak met exponentieel uitstel intervallen tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="bd90c-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="bd90c-183">Nieuwe AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="bd90c-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="bd90c-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="bd90c-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bd90c-185">Planning</span><span class="sxs-lookup"><span data-stu-id="bd90c-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-186">Specificatie voor het uitvoeren van plaatsvinden in een interval van terugkerende of één keer op basis van tijd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="bd90c-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="bd90c-188">Nieuwe AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="bd90c-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="bd90c-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="bd90c-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bd90c-190">Taak wordt geactiveerd</span><span class="sxs-lookup"><span data-stu-id="bd90c-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="bd90c-191">Een toewijzing tussen een taak en een schema wilt uitvoeren volgens de planning van de taak.</span><span class="sxs-lookup"><span data-stu-id="bd90c-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bd90c-192">Nieuwe AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="bd90c-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="bd90c-193">Verwijder AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="bd90c-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="bd90c-194">Ondersteunde elastische Database taken groeperen typen</span><span class="sxs-lookup"><span data-stu-id="bd90c-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="bd90c-195">De taak uitgevoerd (T-SQL) Transact-SQL-scripts of de toepassing van DACPACs in een groep van databases.</span><span class="sxs-lookup"><span data-stu-id="bd90c-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="bd90c-196">Wanneer een taak wordt verzonden om te worden uitgevoerd in een groep met databases, de taak 'wordt uitgebreid' de in onderliggende taken waarbij elk de aangevraagde uitgevoerd op een individuele database in de groep uitvoert.</span><span class="sxs-lookup"><span data-stu-id="bd90c-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="bd90c-197">Er zijn twee typen groepen die u kunt maken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="bd90c-198">[Shard-toewijzing](sql-database-elastic-scale-shard-map-management.md) groep: als een taak wordt verzonden naar een shard-toewijzing met als doel, de taak query de shard-kaart om te bepalen van de huidige set shards en maakt vervolgens onderliggende taken voor elke shard in de shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="bd90c-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="bd90c-199">Verzamelgroep voor de aangepaste: een aangepaste set van databases gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="bd90c-200">Wanneer een taak is bedoeld voor een aangepaste verzameling, wordt gemaakt onderliggende taken voor elke database die momenteel in de verzameling aangepaste.</span><span class="sxs-lookup"><span data-stu-id="bd90c-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="bd90c-201">Taken voor het instellen van de elastische Database verbinding</span><span class="sxs-lookup"><span data-stu-id="bd90c-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="bd90c-202">Een verbinding moet worden ingesteld op de taken *beheer database* voorafgaand aan de taken API's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bd90c-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="bd90c-203">Deze cmdlet uitvoert, activeert een referentie-venster moet worden aanvragen van de gebruikersnaam en wachtwoord die zijn gemaakt tijdens de installatie van de elastische Database taken weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd90c-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="bd90c-204">Alle voorbeelden in dit onderwerp wordt ervan uitgegaan dat al deze eerste stap is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="bd90c-205">Open een verbinding met de elastische Database taken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="bd90c-206">Versleutelde referenties binnen de taken voor elastische Database</span><span class="sxs-lookup"><span data-stu-id="bd90c-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="bd90c-207">Databasereferenties kunnen worden ingevoegd in de taken *beheer database* met het wachtwoord dat is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="bd90c-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="bd90c-208">Het is nodig voor het opslaan van referenties in voor het inschakelen van de taken worden uitgevoerd op een later tijdstip (met behulp van de taakschema's).</span><span class="sxs-lookup"><span data-stu-id="bd90c-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="bd90c-209">Versleuteling werkt via een certificaat gemaakt als onderdeel van het script voor installatie.</span><span class="sxs-lookup"><span data-stu-id="bd90c-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="bd90c-210">Het installatiescript maakt en uploadt het certificaat in de Azure-Cloudservice voor het ontsleutelen van de opgeslagen gecodeerde wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="bd90c-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="bd90c-211">De Azure Cloud Service later slaat de openbare sleutel in de taken *beheer database* waardoor de interface PowerShell API of de klassieke Azure-Portal voor het versleutelen van een opgegeven wachtwoord zonder het certificaat moet lokaal zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="bd90c-212">De referentie-wachtwoorden zijn versleuteld en beveiligd van gebruikers met alleen-lezentoegang voor elastische Database taken objecten.</span><span class="sxs-lookup"><span data-stu-id="bd90c-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="bd90c-213">Maar het is mogelijk dat een kwaadwillende gebruiker met lees-/ schrijftoegang tot elastische Database taken objecten om op te halen van een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="bd90c-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="bd90c-214">Referenties zijn ontworpen om opnieuw worden gebruikt voor uitvoering.</span><span class="sxs-lookup"><span data-stu-id="bd90c-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="bd90c-215">Referenties worden doorgegeven aan de doeldatabases bij het tot stand brengen van verbindingen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="bd90c-216">Er zijn momenteel geen beperkingen op de doeldatabases die worden gebruikt voor elke referentie, kwaadwillende gebruiker kan een database-doel voor een database onder het beheer van de kwaadwillende gebruiker toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="bd90c-217">De gebruiker kan vervolgens een taak die gericht is op deze database voor het verkrijgen van de referentie-wachtwoord starten.</span><span class="sxs-lookup"><span data-stu-id="bd90c-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="bd90c-218">Aanbevolen beveiligingsprocedures voor elastische Database taken omvatten:</span><span class="sxs-lookup"><span data-stu-id="bd90c-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="bd90c-219">Gebruik van de API's naar vertrouwde personen te beperken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="bd90c-220">Referenties hoeven de minimaal benodigde bevoegdheden nodig zijn voor de taak met taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bd90c-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="bd90c-221">Meer informatie ziet u binnen dit [autorisatie en machtigingen](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN-artikel.</span><span class="sxs-lookup"><span data-stu-id="bd90c-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="bd90c-222">Een versleutelde referentie voor de taakuitvoering van de voor databases maken</span><span class="sxs-lookup"><span data-stu-id="bd90c-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="bd90c-223">Een nieuwe versleutelde referentie maken de [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) vraagt om een gebruikersnaam en wachtwoord die kan worden doorgegeven aan de [ **cmdlet New-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="bd90c-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="bd90c-224">Referenties bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd90c-224">To update credentials</span></span>
<span data-ttu-id="bd90c-225">Wanneer wachtwoorden wijzigen, gebruikt de [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) en stel de **CredentialName** parameter.</span><span class="sxs-lookup"><span data-stu-id="bd90c-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="bd90c-226">Een elastische Database shard-toewijzing doel definiëren</span><span class="sxs-lookup"><span data-stu-id="bd90c-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="bd90c-227">Uitvoeren van een taak op alle databases in een set shard (gemaakt met behulp van [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)), een shard-toewijzing gebruiken als het doel van de database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="bd90c-228">Dit voorbeeld vereist een shard-toepassing gemaakt met behulp van de clientbibliotheek voor elastische Database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="bd90c-229">Zie [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bd90c-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="bd90c-230">De shard kaart manager-database moet worden ingesteld als het doel van een database en vervolgens de specifieke shard-toewijzing moet worden opgegeven als een doel.</span><span class="sxs-lookup"><span data-stu-id="bd90c-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="bd90c-231">Maken van een T-SQL-Script voor uitvoering tussen databases</span><span class="sxs-lookup"><span data-stu-id="bd90c-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="bd90c-232">Bij het maken van T-SQL-scripts voor de uitvoering van het is raadzaam om te bouwen om te worden [idempotent](https://en.wikipedia.org/wiki/Idempotence) en robuuste tegen fouten.</span><span class="sxs-lookup"><span data-stu-id="bd90c-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="bd90c-233">Elastische Database-taken opnieuw uitvoeren van het script als een fout optreedt, ongeacht de indeling van de fout wordt aangetroffen die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="bd90c-234">Gebruik de [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) maken en opslaan van een script voor uitvoering en stel de **- ContentName** en **- CommandText** parameters.</span><span class="sxs-lookup"><span data-stu-id="bd90c-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="bd90c-235">Een nieuw script maken vanuit een bestand</span><span class="sxs-lookup"><span data-stu-id="bd90c-235">Create a new script from a file</span></span>
<span data-ttu-id="bd90c-236">Als de T-SQL-script is gedefinieerd in een bestand, gebruikt u dit voor het importeren van het script:</span><span class="sxs-lookup"><span data-stu-id="bd90c-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="bd90c-237">Bijwerken van een T-SQL-script voor uitvoering tussen databases</span><span class="sxs-lookup"><span data-stu-id="bd90c-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="bd90c-238">Deze PowerShell-script de T-SQL-opdrachttekst voor een bestaand script-updates.</span><span class="sxs-lookup"><span data-stu-id="bd90c-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="bd90c-239">Stel de volgende variabelen in overeenstemming met de definitie van de gewenste script moet worden ingesteld:</span><span class="sxs-lookup"><span data-stu-id="bd90c-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="bd90c-240">Bijwerken van de definitie voor een bestaand script</span><span class="sxs-lookup"><span data-stu-id="bd90c-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="bd90c-241">Een taak voor het uitvoeren van een script in een shard-toewijzing te maken</span><span class="sxs-lookup"><span data-stu-id="bd90c-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="bd90c-242">Deze PowerShell-script start een taak voor uitvoering van een script dat op elke shard in een elastische Schaalfunctionaliteit van shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="bd90c-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="bd90c-243">Stel de volgende variabelen in overeenstemming met de gewenste script en de doelserver:</span><span class="sxs-lookup"><span data-stu-id="bd90c-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="bd90c-244">Als een taak wilt uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bd90c-244">To execute a job</span></span>
<span data-ttu-id="bd90c-245">Deze PowerShell-script wordt een bestaande taak uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="bd90c-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="bd90c-246">Update de volgende variabele in overeenstemming met de naam van de gewenste taak hebt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="bd90c-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="bd90c-247">De status van de taakuitvoering van een enkele ophalen</span><span class="sxs-lookup"><span data-stu-id="bd90c-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="bd90c-248">Gebruik de [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) en stel de **JobExecutionId** parameter om de status van de taakuitvoering weer te geven.</span><span class="sxs-lookup"><span data-stu-id="bd90c-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="bd90c-249">Gebruik van dezelfde **Get-AzureSqlJobExecution** cmdlet uit met de **voor IncludeChildren** -parameter voor de status van onderliggende taak uitvoeringen, namelijk de specifieke status voor elke taak uitgevoerd op elke database weergeven gericht door de taak.</span><span class="sxs-lookup"><span data-stu-id="bd90c-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="bd90c-250">De status tussen uitvoeringen van meerdere taak weergeven</span><span class="sxs-lookup"><span data-stu-id="bd90c-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="bd90c-251">De [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) heeft meerdere optionele parameters die kunnen worden gebruikt om meerdere taak uitvoeringen, gefilterd via de opgegeven parameters weer te geven.</span><span class="sxs-lookup"><span data-stu-id="bd90c-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="bd90c-252">Het volgende voorbeeld toont een aantal mogelijke manieren waarop Get-AzureSqlJobExecution gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="bd90c-253">Alle actieve taken voor de bovenste niveau uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="bd90c-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="bd90c-254">Alle bovenste niveau taak uitvoeringen, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="bd90c-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="bd90c-255">Alle onderliggende taak uitvoeringen van een opgegeven taak uitvoerings-ID, met inbegrip van niet-actieve taak uitvoeringen ophalen:</span><span class="sxs-lookup"><span data-stu-id="bd90c-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="bd90c-256">Ophalen van alle taak uitvoeringen gemaakt met behulp van een planning / taak combinatie, met inbegrip van niet-actieve taken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="bd90c-257">Alle taken die gericht is op een opgegeven shard-kaart, inclusief niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="bd90c-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="bd90c-258">Alle taken die gericht is op een opgegeven aangepaste verzameling, met inbegrip van niet-actieve taken worden opgehaald:</span><span class="sxs-lookup"><span data-stu-id="bd90c-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="bd90c-259">Ophalen van de lijst van de taak taak uitvoeringen binnen een specifieke taak kan worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="bd90c-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="bd90c-260">Taak uitvoeren taakdetails ophalen:</span><span class="sxs-lookup"><span data-stu-id="bd90c-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="bd90c-261">De volgende PowerShell-script kan worden gebruikt om de details van een taak uitvoering van taken, die bijzonder nuttig is bij het opsporen van fouten in uitvoering weer te geven.</span><span class="sxs-lookup"><span data-stu-id="bd90c-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="bd90c-262">Storingen in uitvoering taak ophalen</span><span class="sxs-lookup"><span data-stu-id="bd90c-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="bd90c-263">De **JobTaskExecution object** bevat een eigenschap voor de levenscyclus van de taak samen met een berichteigenschap.</span><span class="sxs-lookup"><span data-stu-id="bd90c-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="bd90c-264">Als de uitvoering van de taak een taak is mislukt, de levenscyclus van de eigenschap wordt ingesteld op *mislukt* en de berichteigenschap zal worden ingesteld op de resulterende uitzonderingsbericht en de stack.</span><span class="sxs-lookup"><span data-stu-id="bd90c-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="bd90c-265">Als een taak is mislukt, is het belangrijk om de details van taken waarvoor is mislukt voor een bepaalde taak weer te geven.</span><span class="sxs-lookup"><span data-stu-id="bd90c-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="bd90c-266">Wachttijd voor het uitvoeren van een taak te voltooien</span><span class="sxs-lookup"><span data-stu-id="bd90c-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="bd90c-267">De volgende PowerShell-script kan worden gebruikt om te wachten op een taak te voltooien:</span><span class="sxs-lookup"><span data-stu-id="bd90c-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="bd90c-268">Maken van een aangepaste uitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="bd90c-268">Create a custom execution policy</span></span>
<span data-ttu-id="bd90c-269">Elastische Database taken ondersteunt het maken van aangepaste uitvoeringsbeleidsregels die kunnen worden toegepast wanneer u taken start.</span><span class="sxs-lookup"><span data-stu-id="bd90c-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="bd90c-270">Uitvoeringsbeleidsregels toestaan op dit moment voor het definiëren van:</span><span class="sxs-lookup"><span data-stu-id="bd90c-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="bd90c-271">Naam: Id voor het uitvoeringsbeleid.</span><span class="sxs-lookup"><span data-stu-id="bd90c-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="bd90c-272">De time-out van de taak: Totale tijd voordat een taak met elastische taken van de Database, worden geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="bd90c-273">Eerste Interval voor opnieuw proberen: Interval moet worden gewacht voordat de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="bd90c-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="bd90c-274">Maximale Interval voor opnieuw proberen: Cap intervallen voor opnieuw proberen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="bd90c-275">Opnieuw proberen Interval Backoff Coefficient: Coefficient die wordt gebruikt voor het berekenen van de volgende interval tussen nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="bd90c-276">De volgende formule wordt gebruikt: (eerste Interval voor opnieuw proberen) * Math.pow ((Interval Backoff Coefficient) (nummer van pogingen) - 2).</span><span class="sxs-lookup"><span data-stu-id="bd90c-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="bd90c-277">Maximum aantal pogingen: Het maximum aantal probeer het opnieuw probeert uit te voeren in een job.</span><span class="sxs-lookup"><span data-stu-id="bd90c-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="bd90c-278">Het standaarduitvoeringsbeleid maakt gebruik van de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="bd90c-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="bd90c-279">Naam: Standaarduitvoeringsbeleid</span><span class="sxs-lookup"><span data-stu-id="bd90c-279">Name: Default execution policy</span></span>
* <span data-ttu-id="bd90c-280">De time-out van de taak: 1 week</span><span class="sxs-lookup"><span data-stu-id="bd90c-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="bd90c-281">Eerste Interval voor opnieuw proberen: 100 milliseconden</span><span class="sxs-lookup"><span data-stu-id="bd90c-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="bd90c-282">Maximale Interval voor opnieuw proberen: 30 minuten</span><span class="sxs-lookup"><span data-stu-id="bd90c-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="bd90c-283">Coefficient Interval opnieuw proberen: 2</span><span class="sxs-lookup"><span data-stu-id="bd90c-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="bd90c-284">Maximum aantal pogingen: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="bd90c-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="bd90c-285">Maak de gewenste uitvoeringsbeleid:</span><span class="sxs-lookup"><span data-stu-id="bd90c-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="bd90c-286">Een aangepaste uitvoeringsbeleid bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd90c-286">Update a custom execution policy</span></span>
<span data-ttu-id="bd90c-287">Werk het gewenste uitvoeringsbeleid om bij te werken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="bd90c-288">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="bd90c-288">Cancel a job</span></span>
<span data-ttu-id="bd90c-289">Elastische Database taken ondersteunt aanvragen van de annulering van taken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="bd90c-290">Als taken voor elastische Database een annuleringsverzoek voor een taak die momenteel wordt uitgevoerd detecteert, wordt geprobeerd de taak te stoppen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="bd90c-291">Er zijn twee verschillende manieren dat elastische Database taken een annulering kan uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bd90c-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="bd90c-292">Annuleren taken momenteel worden uitgevoerd: als een annulering wordt gedetecteerd, terwijl een taak die momenteel wordt uitgevoerd, een annulering wordt geprobeerd binnen het momenteel wordt uitgevoerd aspect van de taak.</span><span class="sxs-lookup"><span data-stu-id="bd90c-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="bd90c-293">Bijvoorbeeld: als er een langdurige query die momenteel wordt uitgevoerd wanneer een annulering wordt uitgevoerd, zal er een poging om de query te annuleren.</span><span class="sxs-lookup"><span data-stu-id="bd90c-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="bd90c-294">Nieuwe pogingen taak annuleren: als een annulering wordt gedetecteerd door de besturingselement-thread voordat een taak voor uitvoering wordt gestart, de besturingselement-thread wordt voorkomen dat de taak starten en declareren van de aanvraag als geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="bd90c-295">Als een taak annulering is aangevraagd voor een bovenliggende taak, wordt de annuleringsaanvraag gehonoreerd voor de bovenliggende taak en alle bijbehorende onderliggende taken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="bd90c-296">Gebruik hiervoor een annuleringsaanvraag indienen, de [ **cmdlet Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) en stel de **JobExecutionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="bd90c-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="bd90c-297">Verwijderen van een taak en Taakgeschiedenis asynchroon</span><span class="sxs-lookup"><span data-stu-id="bd90c-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="bd90c-298">Elastische taken van de Database biedt ondersteuning voor asynchrone verwijderen van jobs.</span><span class="sxs-lookup"><span data-stu-id="bd90c-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="bd90c-299">Een taak kan worden gemarkeerd voor verwijdering en het systeem de taak en de taakgeschiedenis wordt verwijderd nadat alle uitvoeringen van de taak voor de taak hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="bd90c-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="bd90c-300">Het systeem wordt niet automatisch uitvoeringen van de actieve taak geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="bd90c-301">Aanroepen [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) uitvoeringen van de actieve taak annuleren.</span><span class="sxs-lookup"><span data-stu-id="bd90c-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="bd90c-302">Gebruiken om te verwijderen van een taak activeren, de [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) en stel de **JobName** parameter.</span><span class="sxs-lookup"><span data-stu-id="bd90c-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="bd90c-303">Om het doel van een aangepaste database te maken</span><span class="sxs-lookup"><span data-stu-id="bd90c-303">To create a custom database target</span></span>
<span data-ttu-id="bd90c-304">U kunt aangepaste database doelen voor directe uitvoering of voor insluiting in een aangepaste database wilt definiëren.</span><span class="sxs-lookup"><span data-stu-id="bd90c-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="bd90c-305">Bijvoorbeeld, omdat **elastische pools** zijn nog niet rechtstreeks ondersteund met behulp van PowerShell APIs, kunt u een aangepaste database doel en de aangepaste database verzameling target dit alle databases in de pool omvat.</span><span class="sxs-lookup"><span data-stu-id="bd90c-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="bd90c-306">De volgende variabelen in overeenstemming met de gewenste databasegegevens instellen:</span><span class="sxs-lookup"><span data-stu-id="bd90c-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="bd90c-307">Om een doel van de verzameling aangepaste database te maken</span><span class="sxs-lookup"><span data-stu-id="bd90c-307">To create a custom database collection target</span></span>
<span data-ttu-id="bd90c-308">Gebruik de [ **nieuw AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet voor het definiëren van een doel van de verzameling aangepaste database zodat kan worden uitgevoerd via meerdere gedefinieerde database doelen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="bd90c-309">Na het maken van een databasegroep, kunnen de databases worden gekoppeld aan het doel van de aangepaste verzameling.</span><span class="sxs-lookup"><span data-stu-id="bd90c-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="bd90c-310">Stel de volgende variabelen in overeenstemming met de configuratie van de gewenste aangepaste verzameling doel:</span><span class="sxs-lookup"><span data-stu-id="bd90c-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="bd90c-311">Databases toevoegen aan een doel van de verzameling aangepaste database</span><span class="sxs-lookup"><span data-stu-id="bd90c-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="bd90c-312">Een database toevoegen aan een specifieke aangepaste verzameling gebruik de [ **toevoegen AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd90c-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="bd90c-313">Bekijk de databases binnen een verzameling aangepaste database doel</span><span class="sxs-lookup"><span data-stu-id="bd90c-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="bd90c-314">Gebruik de [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet voor het ophalen van de onderliggende databases binnen een doel van de verzameling aangepaste database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="bd90c-315">Een taak voor het uitvoeren van een script voor een doel van de verzameling aangepaste database maken</span><span class="sxs-lookup"><span data-stu-id="bd90c-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="bd90c-316">Gebruik de [ **nieuw AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet een taak op basis van een groep met databases die zijn gedefinieerd door een doel van de verzameling aangepaste database te maken.</span><span class="sxs-lookup"><span data-stu-id="bd90c-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="bd90c-317">Elastische taken van de Database wordt de taak uitbreiden naar meerdere onderliggende taken elke overeenkomt met een database die is gekoppeld aan het doel van de verzameling aangepaste database en zorg ervoor dat het script wordt uitgevoerd tegen elke database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="bd90c-318">Ook is het belangrijk dat scripts idempotent zijn flexibel omgaan met nieuwe pogingen worden.</span><span class="sxs-lookup"><span data-stu-id="bd90c-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="bd90c-319">Gegevens verzamelen over databases</span><span class="sxs-lookup"><span data-stu-id="bd90c-319">Data collection across databases</span></span>
<span data-ttu-id="bd90c-320">Een taak kunt u een query uitvoeren in een groep van databases en de resultaten naar een specifieke tabel verzenden.</span><span class="sxs-lookup"><span data-stu-id="bd90c-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="bd90c-321">De tabel kan worden opgevraagd achteraf om te zien van het queryresultaat van elke database.</span><span class="sxs-lookup"><span data-stu-id="bd90c-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="bd90c-322">Dit biedt een asynchrone methode voor het uitvoeren van een query tussen meerdere databases.</span><span class="sxs-lookup"><span data-stu-id="bd90c-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="bd90c-323">Mislukte pogingen worden automatisch verwerkt via de nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="bd90c-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="bd90c-324">De opgegeven doeltabel wordt automatisch gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="bd90c-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="bd90c-325">De nieuwe tabel komt overeen met het schema van de geretourneerde resultatenset.</span><span class="sxs-lookup"><span data-stu-id="bd90c-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="bd90c-326">Als meerdere resultatensets worden geretourneerd door een script, wordt taken voor elastische Database alleen het eerste verzonden naar de doeltabel.</span><span class="sxs-lookup"><span data-stu-id="bd90c-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="bd90c-327">De volgende PowerShell-script een script wordt uitgevoerd en de resultaten in een opgegeven tabel verzamelt.</span><span class="sxs-lookup"><span data-stu-id="bd90c-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="bd90c-328">Dit script wordt ervan uitgegaan dat een T-SQL-script is gemaakt waarmee een enkelvoudig resultaat wordt verkregen set levert en dat er een doel van de verzameling aangepaste database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bd90c-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="bd90c-329">Dit script maakt gebruik van de [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd90c-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="bd90c-330">Stel de parameters voor het script, referenties en uitvoering van doel:</span><span class="sxs-lookup"><span data-stu-id="bd90c-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="bd90c-331">Maken en start een taak voor scenario's voor het verzamelen van gegevens</span><span class="sxs-lookup"><span data-stu-id="bd90c-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="bd90c-332">Dit script maakt gebruik van de [ **Start AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd90c-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="bd90c-333">Een taak uitvoeren trigger plannen</span><span class="sxs-lookup"><span data-stu-id="bd90c-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="bd90c-334">De volgende PowerShell-script kan worden gebruikt voor het maken van een terugkerend schema.</span><span class="sxs-lookup"><span data-stu-id="bd90c-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="bd90c-335">Dit script maakt gebruik van een minuut interval maar [ **nieuw AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) biedt ook ondersteuning voor parameters - DayInterval, - HourInterval, - MonthInterval, en -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="bd90c-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="bd90c-336">Schema's die slechts één keer worden uitgevoerd, kunnen worden gemaakt door doorgeven - eenmalige.</span><span class="sxs-lookup"><span data-stu-id="bd90c-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="bd90c-337">Maak een nieuwe planning:</span><span class="sxs-lookup"><span data-stu-id="bd90c-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="bd90c-338">Om een taak uitgevoerd op een tijdschema te activeren</span><span class="sxs-lookup"><span data-stu-id="bd90c-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="bd90c-339">Een trigger voor de taak kan worden gedefinieerd als een taak uitgevoerd volgens een tijdschema hebben.</span><span class="sxs-lookup"><span data-stu-id="bd90c-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="bd90c-340">De volgende PowerShell-script kan worden gebruikt voor het maken van een trigger taak.</span><span class="sxs-lookup"><span data-stu-id="bd90c-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="bd90c-341">Gebruik [nieuw AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) en stel de volgende variabelen in overeenstemming met de gewenste taak en planning:</span><span class="sxs-lookup"><span data-stu-id="bd90c-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="bd90c-342">Verwijderen van een associatie met geplande taak wordt uitgevoerd volgens schema stoppen</span><span class="sxs-lookup"><span data-stu-id="bd90c-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="bd90c-343">Als u wilt stoppen met het uitvoeren van terugkerende taak via een trigger taak, kan de trigger taak worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="bd90c-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="bd90c-344">Verwijderen van een trigger taak om te stoppen van een taak uit te voeren volgens een schema met de [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="bd90c-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="bd90c-345">Taak triggers die zijn gebonden aan een tijdschema ophalen</span><span class="sxs-lookup"><span data-stu-id="bd90c-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="bd90c-346">De volgende PowerShell-script kan worden gebruikt om te verkrijgen en weergeven van de taak triggers geregistreerd voor een bepaald tijdschema.</span><span class="sxs-lookup"><span data-stu-id="bd90c-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="bd90c-347">Voor het ophalen van de taak triggers die is gebonden aan een taak</span><span class="sxs-lookup"><span data-stu-id="bd90c-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="bd90c-348">Gebruik [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) verkrijgen en schema's met een geregistreerde taak weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bd90c-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="bd90c-349">Maken van een toepassing-gegevenslaagtoepassingen (DACPAC) voor uitvoering voor databases</span><span class="sxs-lookup"><span data-stu-id="bd90c-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="bd90c-350">Zie het maken van een DACPAC [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd90c-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="bd90c-351">Gebruik voor het implementeren van een DACPAC de [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="bd90c-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="bd90c-352">De DACPAC moet toegankelijk zijn voor de service.</span><span class="sxs-lookup"><span data-stu-id="bd90c-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="bd90c-353">Het beste een gemaakte DACPAC uploaden naar Azure Storage en maak een [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor de DACPAC.</span><span class="sxs-lookup"><span data-stu-id="bd90c-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="bd90c-354">Een toepassing-gegevenslaagtoepassingen (DACPAC) voor uitvoering tussen databases bijwerken</span><span class="sxs-lookup"><span data-stu-id="bd90c-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="bd90c-355">Bestaande DACPACs geregistreerd binnen een elastische Database taken kunnen worden bijgewerkt om te verwijzen naar een nieuwe URI's.</span><span class="sxs-lookup"><span data-stu-id="bd90c-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="bd90c-356">Gebruik de [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) geregistreerd DACPAC de DACPAC-URI op een bestaande bijwerken:</span><span class="sxs-lookup"><span data-stu-id="bd90c-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="bd90c-357">Een taak voor het toepassen van een toepassing-gegevenslaagtoepassingen (DACPAC) voor databases te maken</span><span class="sxs-lookup"><span data-stu-id="bd90c-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="bd90c-358">Nadat een DACPAC binnen elastische taken van de Database is gemaakt, kunt u een taak gemaakt voor het toepassen van de DACPAC voor een groep met databases.</span><span class="sxs-lookup"><span data-stu-id="bd90c-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="bd90c-359">De volgende PowerShell-script kan worden gebruikt voor het maken van een taak DACPAC via een aangepaste verzameling van databases:</span><span class="sxs-lookup"><span data-stu-id="bd90c-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
