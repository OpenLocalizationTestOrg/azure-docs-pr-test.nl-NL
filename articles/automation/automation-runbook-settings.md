---
title: aaaRunbook instellingen | Microsoft Docs
description: Beschrijft Hallo configuratie-instellingen voor een runbook in Azure Automation en hoe ze met zowel Azure-beheerportal en Windows PowerShell Hallo toochange.
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="e6ff3-103">Runbook-instellingen</span><span class="sxs-lookup"><span data-stu-id="e6ff3-103">Runbook settings</span></span>
<span data-ttu-id="e6ff3-104">Elk runbook in Azure Automation heeft meerdere instellingen waarmee het toobe geïdentificeerd en toochange de logboekregistratie kan.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="e6ff3-105">Elk van deze instellingen wordt hieronder beschreven en gevolgd door procedures voor het toomodify ze.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="e6ff3-106">Instellingen</span><span class="sxs-lookup"><span data-stu-id="e6ff3-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="e6ff3-107">Naam en beschrijving</span><span class="sxs-lookup"><span data-stu-id="e6ff3-107">Name and description</span></span>
<span data-ttu-id="e6ff3-108">U kunt Hallo-naam van een runbook niet wijzigen nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="e6ff3-109">Hallo beschrijving is optioneel en kan up too512 tekens.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="e6ff3-110">Tags</span><span class="sxs-lookup"><span data-stu-id="e6ff3-110">Tags</span></span>
<span data-ttu-id="e6ff3-111">Labels kunt dat u tooassign verschillende woorden en woordgroepen toohelp identificatie van een runbook.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="e6ff3-112">Bijvoorbeeld, wanneer het indienen van een runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), u bepaalde labels tooidentify welke categorieën Hallo runbook zou moeten worden vermeld opgeven.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="e6ff3-113">U kunt meerdere labels voor een runbook opgeven door deze te scheiden met komma's.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="e6ff3-114">Logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="e6ff3-114">Logging</span></span>
<span data-ttu-id="e6ff3-115">Standaard worden uitgebreid en voortgang van de records niet toojob geschiedenis geschreven.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="e6ff3-116">U kunt instellingen voor een bepaald runbook toolog Hallo deze records te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="e6ff3-117">Zie voor meer informatie over deze records [Runbookuitvoer en -berichten](automation-runbook-output-and-messages.md).</span><span class="sxs-lookup"><span data-stu-id="e6ff3-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="e6ff3-118">Runbookinstellingen</span><span class="sxs-lookup"><span data-stu-id="e6ff3-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="e6ff3-119">Runbookinstellingen met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e6ff3-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="e6ff3-120">U kunt instellingen voor een runbook in hello Azure-portal wijzigen via Hallo **instellingen** blade voor Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="e6ff3-121">Selecteer in de Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een automation-account.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="e6ff3-122">Selecteer Hallo **Runbooks** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="e6ff3-123">Klik op de naam van een runbook hello en u de instellingenblade gerichte toohello voor Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="e6ff3-124">Hier kunt u opgeven of labels wijzigen, Hallo runbook beschrijving, logboekregistratie en tracering instellingen configureren en toegang tot support tools toohelp oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="e6ff3-125">Runbookinstellingen met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6ff3-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="e6ff3-126">U kunt Hallo [Set AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange Hallo-instellingen voor een runbook.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="e6ff3-127">Als u meerdere labels toospecify wilt, kunt u ofwel een matrix of een tekenreeks met door komma's gescheiden waarden toohello labels parameter opgeven.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="e6ff3-128">Kun je huidige labels Hallo Hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6ff3-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="e6ff3-129">Hallo volgende voorbeeldopdrachten laten zien hoe tooset Hallo eigenschappen voor een runbook.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="e6ff3-130">Dit voorbeeld voegt drie tags toohello bestaande tags en geeft aan dat uitgebreide records moeten worden vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="e6ff3-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="e6ff3-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6ff3-131">Next steps</span></span>
* <span data-ttu-id="e6ff3-132">hoe toocreate en ophalen uitvoer en foutberichten van runbooks, Zie toolearn [Runbookuitvoer en -berichten](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e6ff3-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="e6ff3-133">hoe een runbook dat is al ontwikkeld door Hallo community of andere bron- of toocreate uw eigen runbook tooadd zien toounderstand [een Runbook maken of importeren](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="e6ff3-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

