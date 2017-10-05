---
title: Bewaken van bewerkingen, gebeurtenissen en prestatiemeteritems voor het nsg's | Microsoft Docs
description: Informatie over het inschakelen van tellers, gebeurtenissen en operationele logboekregistratie voor het nsg 's
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: 552f37dd704de25159bc0f0ad34fdae9ed8b73f5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="70a57-103">Logboekanalyses voor netwerkbeveiligingsgroepen (NSG's)</span><span class="sxs-lookup"><span data-stu-id="70a57-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="70a57-104">U kunt de volgende categorieën van diagnostische logboeken inschakelen voor het nsg's:</span><span class="sxs-lookup"><span data-stu-id="70a57-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="70a57-105">**Gebeurtenis:** bevat vermeldingen voor welke NSG regels worden toegepast op virtuele machines en functies op basis van MAC-adres-instantie.</span><span class="sxs-lookup"><span data-stu-id="70a57-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="70a57-106">De status voor deze regels worden verzameld om de 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="70a57-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="70a57-107">**Regelteller:** bevat vermeldingen voor hoe vaak elke NSG regel wordt toegepast om te weigeren of verkeer toestaan.</span><span class="sxs-lookup"><span data-stu-id="70a57-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="70a57-108">Diagnostische logboeken zijn alleen beschikbaar voor het nsg's geïmplementeerd via het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="70a57-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="70a57-109">U kunt Diagnostische logboekregistratie voor het nsg's geïmplementeerd via het klassieke implementatiemodel niet inschakelen.</span><span class="sxs-lookup"><span data-stu-id="70a57-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="70a57-110">Voor een beter begrip van de twee modellen, raadpleegt u de [wat Azure-implementatiemodellen](../resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="70a57-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="70a57-111">Logboekregistratie van activiteit (voorheen bekend als audit- of operationele Logboeken) is standaard ingeschakeld voor het nsg's die zijn gemaakt via de Azure-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="70a57-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="70a57-112">Om te bepalen welke bewerkingen zijn voltooid op het nsg's in het activiteitenlogboek, zoeken naar gegevens die de volgende resourcetypen bevatten:</span><span class="sxs-lookup"><span data-stu-id="70a57-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="70a57-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="70a57-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="70a57-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="70a57-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="70a57-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="70a57-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="70a57-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="70a57-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="70a57-117">Lees de [overzicht van de Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artikel voor meer informatie over activiteitenlogboeken.</span><span class="sxs-lookup"><span data-stu-id="70a57-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="70a57-118">Bijhouden van diagnostische gegevens inschakelen</span><span class="sxs-lookup"><span data-stu-id="70a57-118">Enable diagnostic logging</span></span>

<span data-ttu-id="70a57-119">Diagnostische logboekregistratie moet zijn ingeschakeld voor *elke* NSG die u wenst te verzamelen van gegevens voor.</span><span class="sxs-lookup"><span data-stu-id="70a57-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="70a57-120">De [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel wordt uitgelegd waar diagnostische logboeken kunnen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="70a57-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="70a57-121">Als u een bestaande NSG geen hebt, voer de stappen in de [maken van een netwerkbeveiligingsgroep](virtual-networks-create-nsg-arm-pportal.md) artikel een maken.</span><span class="sxs-lookup"><span data-stu-id="70a57-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="70a57-122">U kunt NSG Diagnostische logboekregistratie met behulp van een van de volgende methoden inschakelen:</span><span class="sxs-lookup"><span data-stu-id="70a57-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="70a57-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="70a57-123">Azure portal</span></span>

<span data-ttu-id="70a57-124">Gebruik de portal voor het inschakelen van logboekregistratie, meld u aan bij de [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70a57-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="70a57-125">Klik op **meer services**, typ *netwerkbeveiligingsgroepen*.</span><span class="sxs-lookup"><span data-stu-id="70a57-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="70a57-126">Selecteer het NSG u logboekregistratie wilt inschakelen voor.</span><span class="sxs-lookup"><span data-stu-id="70a57-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="70a57-127">Volg de instructies voor niet-rekenresources in de [Schakel diagnostische logboeken in de portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artikel.</span><span class="sxs-lookup"><span data-stu-id="70a57-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="70a57-128">Selecteer **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, of beide categorieën van Logboeken.</span><span class="sxs-lookup"><span data-stu-id="70a57-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="70a57-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70a57-129">PowerShell</span></span>

<span data-ttu-id="70a57-130">Voor het gebruik van PowerShell logboekregistratie in te schakelen, volg de instructies in de [Schakel diagnostische logboeken via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artikel.</span><span class="sxs-lookup"><span data-stu-id="70a57-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="70a57-131">Evalueer de volgende informatie voordat u een opdracht invoert in het artikel:</span><span class="sxs-lookup"><span data-stu-id="70a57-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="70a57-132">U kunt bepalen dat de waarde moet worden gebruikt voor de `-ResourceId` parameter door de volgende vervangen [tekst] waar nodig, typt u de opdracht `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="70a57-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="70a57-133">De uitvoer van de ID van de opdracht ziet er ongeveer uit */subscriptions/ [abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span><span class="sxs-lookup"><span data-stu-id="70a57-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="70a57-134">Als u alleen gegevens wilt verzamelen uit logboek categorie toevoegen `-Categories [category]` aan het einde van de opdracht in het artikel, waarbij categorie is *NetworkSecurityGroupEvent* of *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="70a57-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="70a57-135">Als u niet de `-Categories` parameter gegevensverzameling is ingeschakeld voor zowel logboekbestand categorieën.</span><span class="sxs-lookup"><span data-stu-id="70a57-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="70a57-136">Azure-opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="70a57-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="70a57-137">Voor het gebruik van de CLI logboekregistratie in te schakelen, volg de instructies in de [Schakel diagnostische logboeken via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artikel.</span><span class="sxs-lookup"><span data-stu-id="70a57-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="70a57-138">Evalueer de volgende informatie voordat u een opdracht invoert in het artikel:</span><span class="sxs-lookup"><span data-stu-id="70a57-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="70a57-139">U kunt bepalen dat de waarde moet worden gebruikt voor de `-ResourceId` parameter door de volgende vervangen [tekst] waar nodig, typt u de opdracht `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="70a57-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="70a57-140">De uitvoer van de ID van de opdracht ziet er ongeveer uit */subscriptions/ [abonnement Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span><span class="sxs-lookup"><span data-stu-id="70a57-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="70a57-141">Als u alleen gegevens wilt verzamelen uit logboek categorie toevoegen `-Categories [category]` aan het einde van de opdracht in het artikel, waarbij categorie is *NetworkSecurityGroupEvent* of *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="70a57-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="70a57-142">Als u niet de `-Categories` parameter gegevensverzameling is ingeschakeld voor zowel logboekbestand categorieën.</span><span class="sxs-lookup"><span data-stu-id="70a57-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="70a57-143">Logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="70a57-143">Logged data</span></span>

<span data-ttu-id="70a57-144">Gegevens in JSON-indeling is geschreven voor beide logboeken.</span><span class="sxs-lookup"><span data-stu-id="70a57-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="70a57-145">De specifieke gegevens die zijn geschreven voor elk Logboektype wordt vermeld in de volgende secties:</span><span class="sxs-lookup"><span data-stu-id="70a57-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="70a57-146">Gebeurtenislogboek</span><span class="sxs-lookup"><span data-stu-id="70a57-146">Event log</span></span>
<span data-ttu-id="70a57-147">Dit logboek bevat informatie over welke NSG regels worden toegepast op virtuele machines en cloud service rolinstanties, op basis van MAC-adres.</span><span class="sxs-lookup"><span data-stu-id="70a57-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="70a57-148">Het volgende voorbeeldgegevens worden geregistreerd voor elke gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="70a57-148">The following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="70a57-149">Regel teller logboek</span><span class="sxs-lookup"><span data-stu-id="70a57-149">Rule counter log</span></span>

<span data-ttu-id="70a57-150">Dit logboek bevat informatie over elke regel toegepast op resources.</span><span class="sxs-lookup"><span data-stu-id="70a57-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="70a57-151">Het volgende voorbeeldgegevens worden geregistreerd telkens wanneer die een regel wordt toegepast:</span><span class="sxs-lookup"><span data-stu-id="70a57-151">The following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="70a57-152">Weergeven en analyseren van Logboeken</span><span class="sxs-lookup"><span data-stu-id="70a57-152">View and analyze logs</span></span>

<span data-ttu-id="70a57-153">Lees voor meer informatie over het weergeven van de logboekgegevens van de activiteit, de [overzicht van de Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="70a57-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="70a57-154">Lees voor meer informatie over het weergeven van diagnostische logboekgegevens, de [overzicht van Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="70a57-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="70a57-155">Als u diagnostische gegevens naar Log Analytics verzenden, kunt u de [Netwerkbeveiligingsgroep Azure analytics](../log-analytics/log-analytics-azure-networking-analytics.md) oplossing voor verbeterde insights (preview).</span><span class="sxs-lookup"><span data-stu-id="70a57-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
