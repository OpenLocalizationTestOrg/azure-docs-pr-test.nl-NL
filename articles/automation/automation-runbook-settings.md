---
title: Runbookinstellingen | Microsoft Docs
description: Beschrijft de configuratie-instellingen voor een runbook in Azure Automation en het wijzigen van deze met de Azure Management Portal en de Windows PowerShell.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="c78bc-103">Runbook-instellingen</span><span class="sxs-lookup"><span data-stu-id="c78bc-103">Runbook settings</span></span>
<span data-ttu-id="c78bc-104">Elk runbook in Azure Automation heeft meerdere instellingen waarmee het kan worden geïdentificeerd en de logboekregistratie kan wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c78bc-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="c78bc-105">Elk van deze instellingen wordt hieronder beschreven en gevolgd door procedures voor het wijzigen van deze.</span><span class="sxs-lookup"><span data-stu-id="c78bc-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="c78bc-106">Instellingen</span><span class="sxs-lookup"><span data-stu-id="c78bc-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="c78bc-107">Naam en beschrijving</span><span class="sxs-lookup"><span data-stu-id="c78bc-107">Name and description</span></span>
<span data-ttu-id="c78bc-108">U kunt de naam van een runbook niet wijzigen nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c78bc-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="c78bc-109">De beschrijving is optioneel en mag maximaal 512 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="c78bc-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="c78bc-110">Tags</span><span class="sxs-lookup"><span data-stu-id="c78bc-110">Tags</span></span>
<span data-ttu-id="c78bc-111">Labels kunt u verschillende woorden en woordgroepen om vast te stellen van een runbook toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c78bc-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="c78bc-112">Bijvoorbeeld, wanneer het indienen van een runbook de [PowerShell Gallery](https://www.powershellgallery.com/), u bepaalde labels om te identificeren welke categorieën die het runbook moet worden weergegeven in opgeven.</span><span class="sxs-lookup"><span data-stu-id="c78bc-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="c78bc-113">U kunt meerdere labels voor een runbook opgeven door deze te scheiden met komma's.</span><span class="sxs-lookup"><span data-stu-id="c78bc-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="c78bc-114">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="c78bc-114">Logging</span></span>
<span data-ttu-id="c78bc-115">Standaard worden uitgebreid en voortgang van de records niet naar Taakgeschiedenis geschreven.</span><span class="sxs-lookup"><span data-stu-id="c78bc-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="c78bc-116">U kunt de instellingen voor een bepaald runbook voor logboekregistratie van deze records te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c78bc-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="c78bc-117">Zie voor meer informatie over deze records [Runbookuitvoer en -berichten](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="c78bc-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="c78bc-118">Runbookinstellingen</span><span class="sxs-lookup"><span data-stu-id="c78bc-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="c78bc-119">Runbookinstellingen met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c78bc-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="c78bc-120">Kunt u instellingen voor een runbook in de Azure portal van de **instellingen** blade voor het runbook.</span><span class="sxs-lookup"><span data-stu-id="c78bc-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="c78bc-121">Selecteer in de Azure-portal **Automation** en klik vervolgens op de naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="c78bc-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="c78bc-122">Selecteer de **Runbooks** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c78bc-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="c78bc-123">Klik op de naam van een runbook en wordt u omgeleid naar de instellingenblade voor het runbook.</span><span class="sxs-lookup"><span data-stu-id="c78bc-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="c78bc-124">Hier kunt u opgeven of labels, de beschrijving van de runbook wijzigen, logboekregistratie en traceringsinstellingen configureren en toegang tot ondersteuning voor hulpprogramma's om u te helpen bij het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c78bc-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="c78bc-125">Runbookinstellingen met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c78bc-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="c78bc-126">U kunt de [Set AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet om de instellingen voor een runbook wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c78bc-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="c78bc-127">Als u meerdere labels opgeven wilt, kunt u ofwel een matrix of een tekenreeks met door komma's gescheiden waarden naar de Tags-parameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="c78bc-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="c78bc-128">U kunt de huidige labels met krijgen de [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="c78bc-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="c78bc-129">De volgende voorbeeldopdrachten laten zien hoe de eigenschappen voor een runbook instellen.</span><span class="sxs-lookup"><span data-stu-id="c78bc-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="c78bc-130">Dit voorbeeld worden drie tags toegevoegd aan de bestaande labels en geeft aan dat uitgebreide records moeten worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="c78bc-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="c78bc-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c78bc-131">Next steps</span></span>
* <span data-ttu-id="c78bc-132">Zie voor meer informatie over het maken en ophalen van de uitvoer en foutberichten van runbooks, [Runbookuitvoer en -berichten](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="c78bc-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="c78bc-133">Om te begrijpen hoe een runbook dat al is ontwikkeld door de community of een andere bron toevoegen of maken van uw eigen Zie runbook [een Runbook maken of importeren](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="c78bc-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

