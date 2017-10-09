---
title: Automation-resources aaaAzure in OMS-oplossingen | Microsoft Docs
description: Oplossingen in OMS omvatten meestal runbooks in Azure Automation tooautomate processen zoals het verzamelen en bewakingsgegevens verwerken.  Dit artikel wordt beschreven hoe tooinclude runbooks en hun verwante resources in een oplossing.
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
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="46a2f-104">Toevoegen van Azure Automation-resources tooan OMS beheeroplossing (Preview)</span><span class="sxs-lookup"><span data-stu-id="46a2f-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="46a2f-105">Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="46a2f-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="46a2f-106">De hieronder beschreven schema is onderwerp toochange.</span><span class="sxs-lookup"><span data-stu-id="46a2f-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="46a2f-107">[Oplossingen voor het beheer in OMS](operations-management-suite-solutions.md) omvatten meestal runbooks in Azure Automation tooautomate processen zoals het verzamelen en bewakingsgegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="46a2f-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="46a2f-108">Bovendien toorunbooks, omvat Automation-accounts activa zoals variabelen en schema's die ondersteuning bieden voor Hallo runbooks gebruikt in Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="46a2f-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="46a2f-109">Dit artikel wordt beschreven hoe tooinclude runbooks en hun verwante resources in een oplossing.</span><span class="sxs-lookup"><span data-stu-id="46a2f-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="46a2f-110">Hallo voorbeelden in dit artikel gebruiken parameters en variabelen die zijn beide vereist of algemene toomanagement oplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="46a2f-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="46a2f-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="46a2f-111">Prerequisites</span></span>
<span data-ttu-id="46a2f-112">In dit artikel wordt ervan uitgegaan dat u al bekend bent met Hallo informatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="46a2f-113">Hoe te[maken van een beheeroplossing](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="46a2f-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="46a2f-114">Hallo structuur van een [oplossingsbestand](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="46a2f-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="46a2f-115">Hoe te[Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="46a2f-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="46a2f-116">Automation-account</span><span class="sxs-lookup"><span data-stu-id="46a2f-116">Automation account</span></span>
<span data-ttu-id="46a2f-117">Alle resources in Azure Automation zijn opgenomen in een [Automation-account](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="46a2f-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="46a2f-118">Zoals beschreven in [OMS werkruimte en de Automation-account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Hallo Automation-account niet is opgenomen in de oplossing voor het beheer van hello, maar moet bestaan voordat het Hallo-oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="46a2f-119">Als het is niet beschikbaar, mislukken Hallo oplossing installatie.</span><span class="sxs-lookup"><span data-stu-id="46a2f-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="46a2f-120">Hallo-naam van elke resource Automation omvat Hallo-naam van de Automation-account.</span><span class="sxs-lookup"><span data-stu-id="46a2f-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="46a2f-121">Dit wordt gedaan Hallo-oplossing met Hallo **accountName** parameter zoals in Hallo voorbeeld van een runbook-resource te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="46a2f-122">Runbooks</span><span class="sxs-lookup"><span data-stu-id="46a2f-122">Runbooks</span></span>
<span data-ttu-id="46a2f-123">Alle runbooks die wordt gebruikt door Hallo-oplossing in het oplossingsbestand hello, zodat ze worden gemaakt wanneer het Hallo-oplossing is geïnstalleerd, moet u opnemen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="46a2f-124">U mag geen Hallo-hoofdtekst van het runbook in de sjabloon Hallo Hallo echter bevatten zodat u Hallo runbook tooa openbaar toegankelijke locatie waar deze kan worden geopend door elke gebruiker installeren van uw oplossing moet publiceren.</span><span class="sxs-lookup"><span data-stu-id="46a2f-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="46a2f-125">[Azure Automation-runbook](../automation/automation-runbook-types.md) resources zijn een type **Microsoft.Automation/automationAccounts/runbooks** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="46a2f-126">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="46a2f-127">Hallo-eigenschappen voor runbooks worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-128">Property</span></span> | <span data-ttu-id="46a2f-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="46a2f-130">runbookType</span></span> |<span data-ttu-id="46a2f-131">Hiermee geeft u Hallo Hallo runbook typen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="46a2f-132">Script - PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="46a2f-132">Script - PowerShell script</span></span> <br><span data-ttu-id="46a2f-133">PowerShell - PowerShell-werkstroom</span><span class="sxs-lookup"><span data-stu-id="46a2f-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="46a2f-134">GraphPowerShell - grafische PowerShell-script runbook</span><span class="sxs-lookup"><span data-stu-id="46a2f-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="46a2f-135">GraphPowerShellWorkflow - grafische PowerShell workflow-runbook</span><span class="sxs-lookup"><span data-stu-id="46a2f-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="46a2f-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="46a2f-136">logProgress</span></span> |<span data-ttu-id="46a2f-137">Hiermee geeft u op of [records voortgang](../automation/automation-runbook-output-and-messages.md) voor Hallo runbook moet worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="46a2f-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="46a2f-138">logVerbose</span></span> |<span data-ttu-id="46a2f-139">Hiermee geeft u op of [uitgebreide records](../automation/automation-runbook-output-and-messages.md) voor Hallo runbook moet worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="46a2f-140">description</span><span class="sxs-lookup"><span data-stu-id="46a2f-140">description</span></span> |<span data-ttu-id="46a2f-141">Optionele beschrijving voor het Hallo-runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="46a2f-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="46a2f-142">publishContentLink</span></span> |<span data-ttu-id="46a2f-143">Hiermee geeft u Hallo inhoud van het Hallo-runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="46a2f-144">URI - inhoud-Uri toohello van Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="46a2f-145">Dit is een ps1-bestand voor runbooks met PowerShell en het Script en een geëxporteerde grafisch runbook-bestand voor een Graph-runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="46a2f-146">versie - versie van de runbook Hallo voor uw eigen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="46a2f-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="46a2f-147">Automation-taken</span><span class="sxs-lookup"><span data-stu-id="46a2f-147">Automation jobs</span></span>
<span data-ttu-id="46a2f-148">Wanneer u een runbook in Azure Automation start, wordt een automation-taak gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46a2f-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="46a2f-149">U kunt een automation-taak resource tooyour oplossing tooautomatically start een runbook toevoegen als oplossing voor het beheer van Hallo is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="46a2f-150">Deze methode is gewoonlijk gebruikte toostart runbooks die worden gebruikt voor de initiële configuratie van Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="46a2f-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="46a2f-151">maken van een runbook met regelmatige tussenpozen toostart een [planning](#schedules) en een [taakschema](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="46a2f-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="46a2f-152">Taak resources zijn een type **Microsoft.Automation/automationAccounts/jobs** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="46a2f-153">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="46a2f-154">Hallo-eigenschappen voor automatisering taken worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-155">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-155">Property</span></span> | <span data-ttu-id="46a2f-156">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-157">runbook</span><span class="sxs-lookup"><span data-stu-id="46a2f-157">runbook</span></span> |<span data-ttu-id="46a2f-158">Één naam-entiteit met de naam van de Hallo van Hallo runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="46a2f-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="46a2f-159">parameters</span><span class="sxs-lookup"><span data-stu-id="46a2f-159">parameters</span></span> |<span data-ttu-id="46a2f-160">De entiteit voor elke parameterwaarde vereist voor Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="46a2f-161">Hallo-taak bevat Hallo runbooknaam en elke parameter waarden toobe toohello runbook verzonden.</span><span class="sxs-lookup"><span data-stu-id="46a2f-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="46a2f-162">Hallo-taak moet [afhankelijk](operations-management-suite-solutions-solution-file.md#resources) hello runbook dat deze wordt gestart sinds Hallo runbook moet worden gemaakt voordat het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="46a2f-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="46a2f-163">Als er meerdere runbooks die moet worden gestart, kunt u de volgorde definiëren wanneer er een taak die afhankelijk zijn van andere taken die eerst moeten worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="46a2f-164">Hallo-naam van een resource van de taak moet een GUID die doorgaans wordt toegewezen door een parameter bevatten.</span><span class="sxs-lookup"><span data-stu-id="46a2f-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="46a2f-165">Meer informatie over parameters in GUID [om oplossingen te maken in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="46a2f-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="46a2f-166">Certificaten</span><span class="sxs-lookup"><span data-stu-id="46a2f-166">Certificates</span></span>
<span data-ttu-id="46a2f-167">[Azure Automation-certificaten](../automation/automation-certificates.md) een soort **Microsoft.Automation/automationAccounts/certificates** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="46a2f-168">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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



<span data-ttu-id="46a2f-169">Hallo-eigenschappen van bronnen van de certificaten worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-170">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-170">Property</span></span> | <span data-ttu-id="46a2f-171">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="46a2f-172">base64Value</span></span> |<span data-ttu-id="46a2f-173">De waarde van de Base 64 voor Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="46a2f-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="46a2f-174">vingerafdruk</span><span class="sxs-lookup"><span data-stu-id="46a2f-174">thumbprint</span></span> |<span data-ttu-id="46a2f-175">Vingerafdruk voor Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="46a2f-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="46a2f-176">Referenties</span><span class="sxs-lookup"><span data-stu-id="46a2f-176">Credentials</span></span>
<span data-ttu-id="46a2f-177">[Azure Automation-referenties](../automation/automation-credentials.md) een soort **Microsoft.Automation/automationAccounts/credentials** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="46a2f-178">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


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

<span data-ttu-id="46a2f-179">Hallo-eigenschappen voor de referentie-bronnen worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-180">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-180">Property</span></span> | <span data-ttu-id="46a2f-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-182">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="46a2f-182">userName</span></span> |<span data-ttu-id="46a2f-183">De gebruikersnaam voor Hallo referentie.</span><span class="sxs-lookup"><span data-stu-id="46a2f-183">User name for hello credential.</span></span> |
| <span data-ttu-id="46a2f-184">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="46a2f-184">password</span></span> |<span data-ttu-id="46a2f-185">Wachtwoord voor het Hallo-referentie.</span><span class="sxs-lookup"><span data-stu-id="46a2f-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="46a2f-186">Planningen</span><span class="sxs-lookup"><span data-stu-id="46a2f-186">Schedules</span></span>
<span data-ttu-id="46a2f-187">[Azure Automation-planningen](../automation/automation-schedules.md) een soort **Microsoft.Automation/automationAccounts/schedules** en hebben Hallo Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="46a2f-188">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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

<span data-ttu-id="46a2f-189">Hallo-eigenschappen voor schema-bronnen worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-190">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-190">Property</span></span> | <span data-ttu-id="46a2f-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-192">description</span><span class="sxs-lookup"><span data-stu-id="46a2f-192">description</span></span> |<span data-ttu-id="46a2f-193">Optionele beschrijving voor Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="46a2f-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="46a2f-194">startTime</span><span class="sxs-lookup"><span data-stu-id="46a2f-194">startTime</span></span> |<span data-ttu-id="46a2f-195">Hiermee geeft u de begintijd Hallo van een planning als een datum/tijd-object.</span><span class="sxs-lookup"><span data-stu-id="46a2f-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="46a2f-196">Een tekenreeks kan worden opgegeven als geconverteerde tooa geldige DateTime.</span><span class="sxs-lookup"><span data-stu-id="46a2f-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="46a2f-197">IsEnabled</span><span class="sxs-lookup"><span data-stu-id="46a2f-197">isEnabled</span></span> |<span data-ttu-id="46a2f-198">Hiermee geeft u op of het Hallo-schema is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="46a2f-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="46a2f-199">interval</span><span class="sxs-lookup"><span data-stu-id="46a2f-199">interval</span></span> |<span data-ttu-id="46a2f-200">Hallo type interval voor Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="46a2f-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="46a2f-201">dag</span><span class="sxs-lookup"><span data-stu-id="46a2f-201">day</span></span><br><span data-ttu-id="46a2f-202">uur</span><span class="sxs-lookup"><span data-stu-id="46a2f-202">hour</span></span> |
| <span data-ttu-id="46a2f-203">frequency</span><span class="sxs-lookup"><span data-stu-id="46a2f-203">frequency</span></span> |<span data-ttu-id="46a2f-204">Frequentie waarmee Hallo planning moet worden geactiveerd in aantal dagen of uren.</span><span class="sxs-lookup"><span data-stu-id="46a2f-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="46a2f-205">Schema's moeten een begintijd met een waarde groter dan Hallo huidige tijd hebben.</span><span class="sxs-lookup"><span data-stu-id="46a2f-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="46a2f-206">U kunt deze waarde kan niet opgeven met een variabele omdat u er niet toe van weten wanneer het gaat toobe geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="46a2f-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="46a2f-207">Gebruik een van de Hallo twee strategieën bij gebruik van resources plannen in een oplossing te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="46a2f-208">Gebruik een parameter voor de begintijd Hallo van Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="46a2f-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="46a2f-209">Dit wordt gevraagd om Hallo gebruiker tooprovide een waarde wanneer ze Hallo-oplossing installeren.</span><span class="sxs-lookup"><span data-stu-id="46a2f-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="46a2f-210">Als u meerdere schema's hebt, kunt u een enkele parameterwaarde kunt gebruiken voor meer dan één.</span><span class="sxs-lookup"><span data-stu-id="46a2f-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="46a2f-211">Maak Hallo schema's met behulp van een runbook dat wordt gestart wanneer het Hallo-oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="46a2f-212">Hiermee verwijdert u de vereiste Hallo van Hallo gebruiker toospecify, maar u mag niet Hallo plannen in uw oplossing zodat deze worden verwijderd wanneer het Hallo-oplossing is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="46a2f-213">Jobplanningen</span><span class="sxs-lookup"><span data-stu-id="46a2f-213">Job schedules</span></span>
<span data-ttu-id="46a2f-214">Taak schema resources koppelen een runbook met een schema.</span><span class="sxs-lookup"><span data-stu-id="46a2f-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="46a2f-215">Ze hebben een soort **Microsoft.Automation/automationAccounts/jobSchedules** en hebben Hallo Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="46a2f-216">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

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


<span data-ttu-id="46a2f-217">Hallo-eigenschappen voor taakschema's worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-218">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-218">Property</span></span> | <span data-ttu-id="46a2f-219">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-220">de naam van de planning</span><span class="sxs-lookup"><span data-stu-id="46a2f-220">schedule name</span></span> |<span data-ttu-id="46a2f-221">Één **naam** entiteit met de naam van het schema Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="46a2f-222">Runbooknaam</span><span class="sxs-lookup"><span data-stu-id="46a2f-222">runbook name</span></span>  |<span data-ttu-id="46a2f-223">Één **naam** entiteit met de naam van de runbook Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="46a2f-224">Variabelen</span><span class="sxs-lookup"><span data-stu-id="46a2f-224">Variables</span></span>
<span data-ttu-id="46a2f-225">[Azure Automation-variabelen](../automation/automation-variables.md) een soort **Microsoft.Automation/automationAccounts/variables** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="46a2f-226">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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

<span data-ttu-id="46a2f-227">Hallo-eigenschappen voor de variabele resources worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-228">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-228">Property</span></span> | <span data-ttu-id="46a2f-229">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-230">description</span><span class="sxs-lookup"><span data-stu-id="46a2f-230">description</span></span> | <span data-ttu-id="46a2f-231">Optionele beschrijving voor Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="46a2f-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="46a2f-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="46a2f-232">isEncrypted</span></span> | <span data-ttu-id="46a2f-233">Hiermee geeft u op of Hallo variabele moet worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="46a2f-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="46a2f-234">type</span><span class="sxs-lookup"><span data-stu-id="46a2f-234">type</span></span> | <span data-ttu-id="46a2f-235">Deze eigenschap heeft momenteel geen effect.</span><span class="sxs-lookup"><span data-stu-id="46a2f-235">This property currently has no effect.</span></span>  <span data-ttu-id="46a2f-236">Hallo-gegevenstype van Hallo variabele wordt bepaald door de beginwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="46a2f-237">waarde</span><span class="sxs-lookup"><span data-stu-id="46a2f-237">value</span></span> | <span data-ttu-id="46a2f-238">De waarde voor Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="46a2f-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="46a2f-239">Hallo **type** eigenschap heeft momenteel geen effect op Hallo variabele wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46a2f-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="46a2f-240">Hallo-gegevenstype voor Hallo variabele wordt bepaald door het Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="46a2f-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="46a2f-241">Als u de beginwaarde voor de variabele Hallo Hallo instelt, moet deze worden geconfigureerd als het juiste gegevenstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="46a2f-242">Hallo volgende tabel biedt Hallo verschillende gegevenstypen toegestane en de syntaxis.</span><span class="sxs-lookup"><span data-stu-id="46a2f-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="46a2f-243">Er rekening mee dat de waarden in JSON verwachte tooalways tussen aanhalingstekens met de speciale tekens in Hallo aanhalingstekens staan.</span><span class="sxs-lookup"><span data-stu-id="46a2f-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="46a2f-244">Bijvoorbeeld, zou een string-waarde worden opgegeven door aanhalingstekens rond het Hallo-tekenreeks (met behulp van Hallo escape-teken (\\)) tijdens een numerieke waarde zou worden opgegeven met een set van aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="46a2f-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="46a2f-245">Gegevenstype</span><span class="sxs-lookup"><span data-stu-id="46a2f-245">Data type</span></span> | <span data-ttu-id="46a2f-246">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-246">Description</span></span> | <span data-ttu-id="46a2f-247">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="46a2f-247">Example</span></span> | <span data-ttu-id="46a2f-248">Wordt omgezet te</span><span class="sxs-lookup"><span data-stu-id="46a2f-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="46a2f-249">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="46a2f-249">string</span></span>   | <span data-ttu-id="46a2f-250">Waarde moet tussen dubbele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="46a2f-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="46a2f-251">'\"Hallo wereld\"'</span><span class="sxs-lookup"><span data-stu-id="46a2f-251">"\"Hello world\""</span></span> | <span data-ttu-id="46a2f-252">"Hallo wereld"</span><span class="sxs-lookup"><span data-stu-id="46a2f-252">"Hello world"</span></span> |
| <span data-ttu-id="46a2f-253">numerieke</span><span class="sxs-lookup"><span data-stu-id="46a2f-253">numeric</span></span>  | <span data-ttu-id="46a2f-254">Numerieke waarde met enkele aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="46a2f-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="46a2f-255">"64"</span><span class="sxs-lookup"><span data-stu-id="46a2f-255">"64"</span></span> | <span data-ttu-id="46a2f-256">64</span><span class="sxs-lookup"><span data-stu-id="46a2f-256">64</span></span> |
| <span data-ttu-id="46a2f-257">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="46a2f-257">boolean</span></span>  | <span data-ttu-id="46a2f-258">**de waarde True** of **false** tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="46a2f-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="46a2f-259">Houd er rekening mee dat deze waarde een kleine letter moet.</span><span class="sxs-lookup"><span data-stu-id="46a2f-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="46a2f-260">'true'</span><span class="sxs-lookup"><span data-stu-id="46a2f-260">"true"</span></span> | <span data-ttu-id="46a2f-261">De waarde True</span><span class="sxs-lookup"><span data-stu-id="46a2f-261">true</span></span> |
| <span data-ttu-id="46a2f-262">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="46a2f-262">datetime</span></span> | <span data-ttu-id="46a2f-263">Geserialiseerde date-waarde.</span><span class="sxs-lookup"><span data-stu-id="46a2f-263">Serialized date value.</span></span><br><span data-ttu-id="46a2f-264">U kunt op deze waarde Hallo ConvertTo-Json cmdlet in PowerShell toogenerate gebruiken voor een bepaalde datum.</span><span class="sxs-lookup"><span data-stu-id="46a2f-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="46a2f-265">Voorbeeld: get-date ' 24/5/2017 13:14:57 "\\</span><span class="sxs-lookup"><span data-stu-id="46a2f-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="46a2f-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="46a2f-266">ConvertTo-Json</span></span> | <span data-ttu-id="46a2f-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="46a2f-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="46a2f-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="46a2f-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="46a2f-269">Modules</span><span class="sxs-lookup"><span data-stu-id="46a2f-269">Modules</span></span>
<span data-ttu-id="46a2f-270">Uw beheeroplossing voor hoeft niet toodefine [globale modules](../automation/automation-integration-modules.md) gebruikt door uw runbooks omdat ze altijd beschikbaar zijn in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="46a2f-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="46a2f-271">U hoeft tooinclude een resource voor elke andere module die wordt gebruikt door uw runbooks.</span><span class="sxs-lookup"><span data-stu-id="46a2f-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="46a2f-272">[Integratiemodules](../automation/automation-integration-modules.md) een soort **Microsoft.Automation/automationAccounts/modules** en hebben Hallo structuur te volgen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="46a2f-273">Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

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


<span data-ttu-id="46a2f-274">Hallo-eigenschappen van bronnen van de module worden beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="46a2f-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="46a2f-275">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="46a2f-275">Property</span></span> | <span data-ttu-id="46a2f-276">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="46a2f-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="46a2f-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="46a2f-277">contentLink</span></span> |<span data-ttu-id="46a2f-278">Hiermee geeft u Hallo inhoud van het Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="46a2f-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="46a2f-279">URI - Uri toohello inhoud van het Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="46a2f-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="46a2f-280">Dit is een ps1-bestand voor runbooks met PowerShell en het Script en een geëxporteerde grafisch runbook-bestand voor een Graph-runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="46a2f-281">versie - versie van de module Hallo voor uw eigen bijhouden.</span><span class="sxs-lookup"><span data-stu-id="46a2f-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="46a2f-282">Hallo runbook moet afhankelijk van Hallo module resource tooensure voordat Hallo runbook gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46a2f-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="46a2f-283">Bijwerken van modules</span><span class="sxs-lookup"><span data-stu-id="46a2f-283">Updating modules</span></span>
<span data-ttu-id="46a2f-284">Als u een oplossing met een runbook dat gebruikmaakt van een schema bijwerken en Hallo nieuwe versie van uw oplossing een nieuwe module die wordt gebruikt door dat runbook heeft, kan Hallo runbook Hallo oude versie van de module hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46a2f-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="46a2f-285">U moet nemen Hallo runbooks in uw oplossing te volgen en maken van een taak toorun toe voordat alle andere runbooks.</span><span class="sxs-lookup"><span data-stu-id="46a2f-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="46a2f-286">Dit zorgt ervoor dat alle modules die worden bijgewerkt als vereist voordat Hallo runbooks zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="46a2f-287">[Update ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) zorgt ervoor dat alle Hallo-modules die worden gebruikt door runbooks in uw oplossing de meest recente versie Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="46a2f-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="46a2f-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) alle Hallo planning resources tooensure dat Hallo runbooks toothem met gebruik Hallo nieuwste modules gekoppeld opnieuw registreren.</span><span class="sxs-lookup"><span data-stu-id="46a2f-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="46a2f-289">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="46a2f-289">Sample</span></span>
<span data-ttu-id="46a2f-290">Hier volgt een voorbeeld van een oplossing die bevatten die Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="46a2f-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="46a2f-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="46a2f-291">Runbook.</span></span>  <span data-ttu-id="46a2f-292">Dit is een voorbeeldrunbook dat is opgeslagen in een openbare GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="46a2f-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="46a2f-293">Automation-taak die Hallo runbook wordt gestart wanneer Hallo-oplossing is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="46a2f-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="46a2f-294">Planning en taak plannen toostart hello runbook met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="46a2f-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="46a2f-295">Certificaat.</span><span class="sxs-lookup"><span data-stu-id="46a2f-295">Certificate.</span></span>
- <span data-ttu-id="46a2f-296">De referentie.</span><span class="sxs-lookup"><span data-stu-id="46a2f-296">Credential.</span></span>
- <span data-ttu-id="46a2f-297">Variabele.</span><span class="sxs-lookup"><span data-stu-id="46a2f-297">Variable.</span></span>
- <span data-ttu-id="46a2f-298">Module.</span><span class="sxs-lookup"><span data-stu-id="46a2f-298">Module.</span></span>  <span data-ttu-id="46a2f-299">Dit is Hallo [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) voor het schrijven van gegevens tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="46a2f-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="46a2f-300">voorbeeld gebruikt Hallo [standaardoplossing parameters](operations-management-suite-solutions-solution-file.md#parameters) variabelen die meestal in een oplossing als gebruikt wordt toohardcoding waarden in de resourcedefinities Hallo geboden.</span><span class="sxs-lookup"><span data-stu-id="46a2f-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


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
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="46a2f-301">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46a2f-301">Next steps</span></span>
* <span data-ttu-id="46a2f-302">[Toevoegen van een oplossing voor weergave tooyour](operations-management-suite-solutions-resources-views.md) toovisualize gegevens verzameld.</span><span class="sxs-lookup"><span data-stu-id="46a2f-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
