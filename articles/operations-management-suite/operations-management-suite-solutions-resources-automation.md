---
title: Azure Automation-resources in OMS-oplossingen | Microsoft Docs
description: Oplossingen in OMS omvatten meestal runbooks in Azure Automation voor het automatiseren van processen, zoals het verzamelen en bewakingsgegevens verwerken.  Dit artikel wordt beschreven hoe u runbooks en hun bijbehorende resources opnemen in een oplossing.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="3a950-104">Azure Automation-resources toe te voegen aan een OMS-beheeroplossing (Preview)</span><span class="sxs-lookup"><span data-stu-id="3a950-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="3a950-105">Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="3a950-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="3a950-106">De hieronder beschreven schema kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3a950-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="3a950-107">[Oplossingen voor het beheer in OMS](operations-management-suite-solutions.md) omvatten meestal runbooks in Azure Automation voor het automatiseren van processen, zoals het verzamelen en bewakingsgegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="3a950-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="3a950-108">Automation-accounts bevat naast runbooks, assets, zoals variabelen en schema's die ondersteuning bieden voor de runbooks gebruikt in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3a950-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="3a950-109">Dit artikel wordt beschreven hoe u runbooks en hun bijbehorende resources opnemen in een oplossing.</span><span class="sxs-lookup"><span data-stu-id="3a950-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="3a950-110">De voorbeelden in dit artikel gebruiken parameters en variabelen die zijn vereist of gemeenschappelijke voor beheeroplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="3a950-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3a950-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3a950-111">Prerequisites</span></span>
<span data-ttu-id="3a950-112">In dit artikel wordt ervan uitgegaan dat u al bekend met de volgende informatie bent.</span><span class="sxs-lookup"><span data-stu-id="3a950-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="3a950-113">Hoe [maken van een beheeroplossing](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="3a950-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="3a950-114">De structuur van een [oplossingsbestand](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="3a950-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="3a950-115">Hoe [Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3a950-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="3a950-116">Automation-account</span><span class="sxs-lookup"><span data-stu-id="3a950-116">Automation account</span></span>
<span data-ttu-id="3a950-117">Alle resources in Azure Automation zijn opgenomen in een [Automation-account](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="3a950-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="3a950-118">Zoals beschreven in [OMS werkruimte en de Automation-account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) het Automation-account niet is opgenomen in de oplossing voor beheer, maar moet bestaan voordat de oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="3a950-119">De installatie van de oplossing zal mislukken als het is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="3a950-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="3a950-120">De naam van elke resource Automation bevat de naam van de Automation-account.</span><span class="sxs-lookup"><span data-stu-id="3a950-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="3a950-121">Dit doet u in de oplossing met de **accountName** parameter zoals in het volgende voorbeeld van een runbook-resource.</span><span class="sxs-lookup"><span data-stu-id="3a950-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="3a950-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="3a950-122">Runbooks</span></span>
<span data-ttu-id="3a950-123">Alle runbooks die door de oplossing in het oplossingsbestand gebruikt zodat ze worden gemaakt wanneer de oplossing is geïnstalleerd, moet u opnemen.</span><span class="sxs-lookup"><span data-stu-id="3a950-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="3a950-124">U mag niet de hoofdtekst van het runbook in de sjabloon, dus u moet het runbook publiceren naar een openbaar toegankelijke locatie waar deze kan worden geopend door elke gebruiker installeren van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="3a950-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="3a950-125">[Azure Automation-runbook](../automation/automation-runbook-types.md) resources zijn een type **Microsoft.Automation/automationAccounts/runbooks** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="3a950-126">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="3a950-127">De eigenschappen voor runbooks worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="3a950-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-128">Property</span></span> | <span data-ttu-id="3a950-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="3a950-130">runbookType</span></span> |<span data-ttu-id="3a950-131">Hiermee geeft u de typen van het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="3a950-132">Script - PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="3a950-132">Script - PowerShell script</span></span> <br><span data-ttu-id="3a950-133">PowerShell - PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="3a950-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="3a950-134">GraphPowerShell - grafische PowerShell-script runbook</span><span class="sxs-lookup"><span data-stu-id="3a950-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="3a950-135">GraphPowerShellWorkflow - grafische PowerShell workflow-runbook</span><span class="sxs-lookup"><span data-stu-id="3a950-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="3a950-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="3a950-136">logProgress</span></span> |<span data-ttu-id="3a950-137">Hiermee geeft u op of [records voortgang](../automation/automation-runbook-output-and-messages.md) voor het runbook moet worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="3a950-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="3a950-138">logVerbose</span></span> |<span data-ttu-id="3a950-139">Hiermee geeft u op of [uitgebreide records](../automation/automation-runbook-output-and-messages.md) voor het runbook moet worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="3a950-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-140">description</span></span> |<span data-ttu-id="3a950-141">Optionele beschrijving voor het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="3a950-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="3a950-142">publishContentLink</span></span> |<span data-ttu-id="3a950-143">Hiermee geeft u de inhoud van het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="3a950-144">URI - Uri met de inhoud van het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="3a950-145">Dit is een ps1-bestand voor runbooks met PowerShell en het Script en een geëxporteerde grafisch runbook-bestand voor een Graph-runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="3a950-146">versie - versie van het runbook voor uw eigen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="3a950-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="3a950-147">Automation-taken</span><span class="sxs-lookup"><span data-stu-id="3a950-147">Automation jobs</span></span>
<span data-ttu-id="3a950-148">Wanneer u een runbook in Azure Automation start, wordt een automation-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3a950-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="3a950-149">U kunt een automation-taak resource toevoegen aan uw oplossing automatisch een runbook wordt gestart wanneer het systeem is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="3a950-150">Deze methode wordt doorgaans gebruikt voor het starten van runbooks die worden gebruikt voor de initiële configuratie van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3a950-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="3a950-151">Maak eerst een runbook met regelmatige tussenpozen een [planning](#schedules) en een [taakschema](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="3a950-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="3a950-152">Taak resources zijn een type **Microsoft.Automation/automationAccounts/jobs** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="3a950-153">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="3a950-154">De eigenschappen voor automatisering taken worden beschreven in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="3a950-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="3a950-155">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-155">Property</span></span> | <span data-ttu-id="3a950-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-157">runbook</span><span class="sxs-lookup"><span data-stu-id="3a950-157">runbook</span></span> |<span data-ttu-id="3a950-158">De naam van één entiteit met de naam van het runbook te starten.</span><span class="sxs-lookup"><span data-stu-id="3a950-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="3a950-159">Parameters</span><span class="sxs-lookup"><span data-stu-id="3a950-159">parameters</span></span> |<span data-ttu-id="3a950-160">De entiteit voor elke parameterwaarde vereist voor het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="3a950-161">De taak bevat de runbooknaam en parameterwaarden worden verzonden naar het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="3a950-162">De taak moet [afhankelijk](operations-management-suite-solutions-solution-file.md#resources) het runbook dat deze wordt gestart nadat het runbook moet worden gemaakt voordat de taak.</span><span class="sxs-lookup"><span data-stu-id="3a950-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="3a950-163">Als er meerdere runbooks die moet worden gestart, kunt u de volgorde definiëren wanneer er een taak die afhankelijk zijn van andere taken die eerst moeten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="3a950-164">De naam van de resource van een taak moet een GUID die doorgaans wordt toegewezen door een parameter bevatten.</span><span class="sxs-lookup"><span data-stu-id="3a950-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="3a950-165">Meer informatie over parameters in GUID [om oplossingen te maken in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="3a950-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="3a950-166">Certificaten</span><span class="sxs-lookup"><span data-stu-id="3a950-166">Certificates</span></span>
<span data-ttu-id="3a950-167">[Azure Automation-certificaten](../automation/automation-certificates.md) een soort **Microsoft.Automation/automationAccounts/certificates** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="3a950-168">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="3a950-169">De eigenschappen van bronnen van de certificaten worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="3a950-170">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-170">Property</span></span> | <span data-ttu-id="3a950-171">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="3a950-172">base64Value</span></span> |<span data-ttu-id="3a950-173">Base 64-waarde voor het certificaat.</span><span class="sxs-lookup"><span data-stu-id="3a950-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="3a950-174">vingerafdruk</span><span class="sxs-lookup"><span data-stu-id="3a950-174">thumbprint</span></span> |<span data-ttu-id="3a950-175">Vingerafdruk van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="3a950-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="3a950-176">Referenties</span><span class="sxs-lookup"><span data-stu-id="3a950-176">Credentials</span></span>
<span data-ttu-id="3a950-177">[Azure Automation-referenties](../automation/automation-credentials.md) een soort **Microsoft.Automation/automationAccounts/credentials** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="3a950-178">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="3a950-179">De eigenschappen voor de referentie-resources worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="3a950-180">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-180">Property</span></span> | <span data-ttu-id="3a950-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-182">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="3a950-182">userName</span></span> |<span data-ttu-id="3a950-183">De naam van de gebruiker voor de referentie.</span><span class="sxs-lookup"><span data-stu-id="3a950-183">User name for the credential.</span></span> |
| <span data-ttu-id="3a950-184">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3a950-184">password</span></span> |<span data-ttu-id="3a950-185">Wachtwoord voor de referentie.</span><span class="sxs-lookup"><span data-stu-id="3a950-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="3a950-186">Planningen</span><span class="sxs-lookup"><span data-stu-id="3a950-186">Schedules</span></span>
<span data-ttu-id="3a950-187">[Azure Automation-planningen](../automation/automation-schedules.md) een soort **Microsoft.Automation/automationAccounts/schedules** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="3a950-188">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="3a950-189">De eigenschappen voor resources plannen worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="3a950-190">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-190">Property</span></span> | <span data-ttu-id="3a950-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-192">description</span></span> |<span data-ttu-id="3a950-193">Optionele beschrijving voor de planning.</span><span class="sxs-lookup"><span data-stu-id="3a950-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="3a950-194">startTime</span><span class="sxs-lookup"><span data-stu-id="3a950-194">startTime</span></span> |<span data-ttu-id="3a950-195">Hiermee geeft u de begintijd van een planning als een datum/tijd-object.</span><span class="sxs-lookup"><span data-stu-id="3a950-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="3a950-196">Een tekenreeks kan worden opgegeven als kan worden geconverteerd naar een geldige DateTime.</span><span class="sxs-lookup"><span data-stu-id="3a950-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="3a950-197">IsEnabled</span><span class="sxs-lookup"><span data-stu-id="3a950-197">isEnabled</span></span> |<span data-ttu-id="3a950-198">Hiermee geeft u op of de planning is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3a950-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="3a950-199">Interval</span><span class="sxs-lookup"><span data-stu-id="3a950-199">interval</span></span> |<span data-ttu-id="3a950-200">Het type interval voor de planning.</span><span class="sxs-lookup"><span data-stu-id="3a950-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="3a950-201">dag</span><span class="sxs-lookup"><span data-stu-id="3a950-201">day</span></span><br><span data-ttu-id="3a950-202">uur</span><span class="sxs-lookup"><span data-stu-id="3a950-202">hour</span></span> |
| <span data-ttu-id="3a950-203">Frequentie</span><span class="sxs-lookup"><span data-stu-id="3a950-203">frequency</span></span> |<span data-ttu-id="3a950-204">De frequentie waarmee de planning moet worden geactiveerd in aantal dagen of uren.</span><span class="sxs-lookup"><span data-stu-id="3a950-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="3a950-205">Schema's moeten een begintijd met een waarde groter is dan de huidige tijd hebben.</span><span class="sxs-lookup"><span data-stu-id="3a950-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="3a950-206">U kunt deze waarde kan niet opgeven met een variabele, omdat u er niet toe van weten wanneer deze het wil worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="3a950-207">Gebruik een van de volgende twee strategieën wanneer resources plannen in een oplossing.</span><span class="sxs-lookup"><span data-stu-id="3a950-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="3a950-208">Gebruik een parameter voor de begintijd van de planning.</span><span class="sxs-lookup"><span data-stu-id="3a950-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="3a950-209">Dit wordt de gebruiker gevraagd om een waarde opgeven bij de installatie van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3a950-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="3a950-210">Als u meerdere schema's hebt, kunt u een enkele parameterwaarde kunt gebruiken voor meer dan één.</span><span class="sxs-lookup"><span data-stu-id="3a950-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="3a950-211">Maak de schema's met behulp van een runbook dat wordt gestart wanneer de oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="3a950-212">Hiermee verwijdert u de vereisten van de gebruiker een tijdstip opgeven, maar u mag niet de planning in uw oplossing zodat wordt verwijderd wanneer de oplossing wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3a950-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="3a950-213">Jobplanningen</span><span class="sxs-lookup"><span data-stu-id="3a950-213">Job schedules</span></span>
<span data-ttu-id="3a950-214">Taak schema resources koppelen een runbook met een schema.</span><span class="sxs-lookup"><span data-stu-id="3a950-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="3a950-215">Ze hebben een soort **Microsoft.Automation/automationAccounts/jobSchedules** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="3a950-216">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="3a950-217">De eigenschappen voor taakschema's worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="3a950-218">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-218">Property</span></span> | <span data-ttu-id="3a950-219">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-220">de naam van de planning</span><span class="sxs-lookup"><span data-stu-id="3a950-220">schedule name</span></span> |<span data-ttu-id="3a950-221">Één **naam** entiteit met de naam van de planning.</span><span class="sxs-lookup"><span data-stu-id="3a950-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="3a950-222">Runbooknaam</span><span class="sxs-lookup"><span data-stu-id="3a950-222">runbook name</span></span>  |<span data-ttu-id="3a950-223">Één **naam** entiteit met de naam van het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="3a950-224">Variabelen</span><span class="sxs-lookup"><span data-stu-id="3a950-224">Variables</span></span>
<span data-ttu-id="3a950-225">[Azure Automation-variabelen](../automation/automation-variables.md) een soort **Microsoft.Automation/automationAccounts/variables** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="3a950-226">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="3a950-227">De eigenschappen voor de variabele resources worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="3a950-228">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-228">Property</span></span> | <span data-ttu-id="3a950-229">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-230">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-230">description</span></span> | <span data-ttu-id="3a950-231">Optionele beschrijving voor de variabele.</span><span class="sxs-lookup"><span data-stu-id="3a950-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="3a950-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="3a950-232">isEncrypted</span></span> | <span data-ttu-id="3a950-233">Hiermee geeft u op of de variabele moet worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="3a950-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="3a950-234">type</span><span class="sxs-lookup"><span data-stu-id="3a950-234">type</span></span> | <span data-ttu-id="3a950-235">Deze eigenschap heeft momenteel geen effect.</span><span class="sxs-lookup"><span data-stu-id="3a950-235">This property currently has no effect.</span></span>  <span data-ttu-id="3a950-236">Het gegevenstype van de variabele wordt bepaald door de initiële waarde.</span><span class="sxs-lookup"><span data-stu-id="3a950-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="3a950-237">waarde</span><span class="sxs-lookup"><span data-stu-id="3a950-237">value</span></span> | <span data-ttu-id="3a950-238">De waarde voor de variabele.</span><span class="sxs-lookup"><span data-stu-id="3a950-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="3a950-239">De **type** eigenschap heeft momenteel geen effect op de variabele die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3a950-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="3a950-240">Het gegevenstype voor de variabele wordt bepaald door de waarde.</span><span class="sxs-lookup"><span data-stu-id="3a950-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="3a950-241">Als u de beginwaarde voor de variabele instelt, moet deze worden geconfigureerd als het juiste gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="3a950-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="3a950-242">De volgende tabel bevat de verschillende gegevenstypen toegestane en hun syntaxis.</span><span class="sxs-lookup"><span data-stu-id="3a950-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="3a950-243">Houd er rekening mee dat de waarden in JSON moeten altijd tussen aanhalingstekens met de speciale tekens binnen de aanhalingstekens worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3a950-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="3a950-244">Bijvoorbeeld, zou een string-waarde worden opgegeven door aanhalingstekens rond de tekenreeks (met behulp van het escape-teken (\\)) tijdens een numerieke waarde zou worden opgegeven met een set van aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="3a950-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="3a950-245">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="3a950-245">Data type</span></span> | <span data-ttu-id="3a950-246">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-246">Description</span></span> | <span data-ttu-id="3a950-247">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3a950-247">Example</span></span> | <span data-ttu-id="3a950-248">Wordt omgezet in</span><span class="sxs-lookup"><span data-stu-id="3a950-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="3a950-249">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="3a950-249">string</span></span>   | <span data-ttu-id="3a950-250">Waarde moet tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="3a950-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="3a950-251">'\"Hallo wereld\"'</span><span class="sxs-lookup"><span data-stu-id="3a950-251">"\"Hello world\""</span></span> | <span data-ttu-id="3a950-252">"Hallo wereld"</span><span class="sxs-lookup"><span data-stu-id="3a950-252">"Hello world"</span></span> |
| <span data-ttu-id="3a950-253">numerieke</span><span class="sxs-lookup"><span data-stu-id="3a950-253">numeric</span></span>  | <span data-ttu-id="3a950-254">Numerieke waarde met enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="3a950-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="3a950-255">"64"</span><span class="sxs-lookup"><span data-stu-id="3a950-255">"64"</span></span> | <span data-ttu-id="3a950-256">64</span><span class="sxs-lookup"><span data-stu-id="3a950-256">64</span></span> |
| <span data-ttu-id="3a950-257">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="3a950-257">boolean</span></span>  | <span data-ttu-id="3a950-258">**de waarde True** of **false** tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="3a950-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="3a950-259">Houd er rekening mee dat deze waarde een kleine letter moet.</span><span class="sxs-lookup"><span data-stu-id="3a950-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="3a950-260">'true'</span><span class="sxs-lookup"><span data-stu-id="3a950-260">"true"</span></span> | <span data-ttu-id="3a950-261">De waarde True</span><span class="sxs-lookup"><span data-stu-id="3a950-261">true</span></span> |
| <span data-ttu-id="3a950-262">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="3a950-262">datetime</span></span> | <span data-ttu-id="3a950-263">Geserialiseerde date-waarde.</span><span class="sxs-lookup"><span data-stu-id="3a950-263">Serialized date value.</span></span><br><span data-ttu-id="3a950-264">U kunt de ConvertTo-Json-cmdlet in PowerShell gebruiken voor het genereren van deze waarde voor een bepaalde datum.</span><span class="sxs-lookup"><span data-stu-id="3a950-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="3a950-265">Voorbeeld: get-date ' 24/5/2017 13:14:57 "\\</span><span class="sxs-lookup"><span data-stu-id="3a950-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="3a950-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="3a950-266">ConvertTo-Json</span></span> | <span data-ttu-id="3a950-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="3a950-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="3a950-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="3a950-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="3a950-269">Modules</span><span class="sxs-lookup"><span data-stu-id="3a950-269">Modules</span></span>
<span data-ttu-id="3a950-270">Uw oplossing voor het beheer niet hoeft te definiëren [globale modules](../automation/automation-integration-modules.md) gebruikt door uw runbooks omdat ze altijd beschikbaar zijn in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="3a950-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="3a950-271">U hoeft een resource voor elke andere module die wordt gebruikt door uw runbooks bevatten.</span><span class="sxs-lookup"><span data-stu-id="3a950-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="3a950-272">[Integratiemodules](../automation/automation-integration-modules.md) een soort **Microsoft.Automation/automationAccounts/modules** en hebben de volgende structuur.</span><span class="sxs-lookup"><span data-stu-id="3a950-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="3a950-273">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en wijzig de namen van parameters.</span><span class="sxs-lookup"><span data-stu-id="3a950-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="3a950-274">De eigenschappen voor de module resources worden in de volgende tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="3a950-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="3a950-275">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="3a950-275">Property</span></span> | <span data-ttu-id="3a950-276">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3a950-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a950-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="3a950-277">contentLink</span></span> |<span data-ttu-id="3a950-278">Hiermee geeft u de inhoud van de module.</span><span class="sxs-lookup"><span data-stu-id="3a950-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="3a950-279">URI - Uri met de inhoud van de module.</span><span class="sxs-lookup"><span data-stu-id="3a950-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="3a950-280">Dit is een ps1-bestand voor runbooks met PowerShell en het Script en een geëxporteerde grafisch runbook-bestand voor een Graph-runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="3a950-281">versie - versie van de module voor uw eigen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="3a950-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="3a950-282">Het runbook moet afhankelijk zijn van de bron van de module om ervoor te zorgen dat deze gemaakt voordat het runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="3a950-283">Bijwerken van modules</span><span class="sxs-lookup"><span data-stu-id="3a950-283">Updating modules</span></span>
<span data-ttu-id="3a950-284">Als u een oplossing met een runbook dat gebruikmaakt van een schema bijwerken en de nieuwe versie van uw oplossing een nieuwe module door dat runbook gebruikt is, kan het runbook de oude versie van de module gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3a950-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="3a950-285">U moet de volgende runbooks opnemen in uw oplossing en taak maken voor deze uitvoeren vóór alle andere runbooks.</span><span class="sxs-lookup"><span data-stu-id="3a950-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="3a950-286">Dit zorgt ervoor dat alle modules die worden bijgewerkt als vereist voordat de runbooks worden geladen.</span><span class="sxs-lookup"><span data-stu-id="3a950-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="3a950-287">[Update ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) zorgt ervoor dat alle modules die worden gebruikt door runbooks in uw oplossing de meest recente versie zijn.</span><span class="sxs-lookup"><span data-stu-id="3a950-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="3a950-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) alle resources schema om ervoor te zorgen dat de runbooks is gekoppeld aan deze bij gebruik de meest recente modules opnieuw registreren.</span><span class="sxs-lookup"><span data-stu-id="3a950-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="3a950-289">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3a950-289">Sample</span></span>
<span data-ttu-id="3a950-290">Hier volgt een voorbeeld van een oplossing die opnemen met de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="3a950-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="3a950-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="3a950-291">Runbook.</span></span>  <span data-ttu-id="3a950-292">Dit is een voorbeeldrunbook dat is opgeslagen in een openbare GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="3a950-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="3a950-293">Automation-taak die het runbook wordt gestart wanneer de oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3a950-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="3a950-294">Planning en het schema voor het runbook starten met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="3a950-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="3a950-295">Certificaat.</span><span class="sxs-lookup"><span data-stu-id="3a950-295">Certificate.</span></span>
- <span data-ttu-id="3a950-296">De referentie.</span><span class="sxs-lookup"><span data-stu-id="3a950-296">Credential.</span></span>
- <span data-ttu-id="3a950-297">Variabele.</span><span class="sxs-lookup"><span data-stu-id="3a950-297">Variable.</span></span>
- <span data-ttu-id="3a950-298">Module.</span><span class="sxs-lookup"><span data-stu-id="3a950-298">Module.</span></span>  <span data-ttu-id="3a950-299">Dit is de [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) voor het schrijven van gegevens met logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="3a950-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="3a950-300">In dit voorbeeld worden [standaardoplossing parameters](operations-management-suite-solutions-solution-file.md#parameters) variabelen die meestal in een oplossing in plaats van hardcoderen waarden in de resourcedefinities gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="3a950-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="3a950-301">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a950-301">Next steps</span></span>
* <span data-ttu-id="3a950-302">[Een weergave toevoegen aan uw oplossing](operations-management-suite-solutions-resources-views.md) om verzamelde gegevens te visualiseren.</span><span class="sxs-lookup"><span data-stu-id="3a950-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
