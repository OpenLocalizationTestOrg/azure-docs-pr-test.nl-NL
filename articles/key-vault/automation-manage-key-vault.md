---
title: aaaManage Azure Key Vault met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure Key Vault kan zijn.
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="d80b0-103">Het beheren van Azure Sleutelkluis met behulp van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="d80b0-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="d80b0-104">Deze handleiding vindt u toohello Azure Automation-service en hoe het kan gebruikte toosimplify beheer van uw sleutels en geheimen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="d80b0-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="d80b0-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="d80b0-105">What is Azure Automation?</span></span>
<span data-ttu-id="d80b0-106">[Azure Automation](../automation/automation-intro.md) is een Azure-service voor het vereenvoudigen van beheer door automatisering van bedrijfsprocessen en configuratie van de gewenste status.</span><span class="sxs-lookup"><span data-stu-id="d80b0-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="d80b0-107">Met behulp van Azure Automation, kunnen handmatige, herhaalde langlopende en foutgevoelige-taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="d80b0-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="d80b0-108">Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="d80b0-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="d80b0-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="d80b0-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="d80b0-110">Operationele overhead verminderen en vrijmaken IT en DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d80b0-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="d80b0-111">Hoe kan Azure Automation helpen beheren van Azure Sleutelkluis?</span><span class="sxs-lookup"><span data-stu-id="d80b0-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="d80b0-112">Sleutelkluis in Azure Automation kunnen worden beheerd met behulp van Hallo [AzureRM Sleutelkluis-cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) en [Azure Classic Sleutelkluis-cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="d80b0-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="d80b0-113">Hallo Azure-module voor het beheren van klassieke Sleutelkluis beschikbaar automatisch in Azure Automation is en u kunt importeren Hallo [AzureRM KeyVault-module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) in Azure Automation, zodat u veel van uw Sleutelkluis-beheer kan uitvoeren taken in het Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="d80b0-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="d80b0-114">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="d80b0-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="d80b0-115">Met hello Azure Sleutelkluis-cmdlets kunt u deze taken onder andere uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d80b0-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="d80b0-116">Maken en configureren van een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="d80b0-116">Create and configure a key vault</span></span>
* <span data-ttu-id="d80b0-117">Maken of importeren van een sleutel</span><span class="sxs-lookup"><span data-stu-id="d80b0-117">Create or import a key</span></span>
* <span data-ttu-id="d80b0-118">Maken of bijwerken van een geheim</span><span class="sxs-lookup"><span data-stu-id="d80b0-118">Create or update a secret</span></span>
* <span data-ttu-id="d80b0-119">Kenmerken van een sleutel bijwerken</span><span class="sxs-lookup"><span data-stu-id="d80b0-119">Update attributes of a key</span></span>
* <span data-ttu-id="d80b0-120">Een sleutel of geheim ophalen</span><span class="sxs-lookup"><span data-stu-id="d80b0-120">Get a key or secret</span></span>
* <span data-ttu-id="d80b0-121">Een sleutel of geheim verwijderen</span><span class="sxs-lookup"><span data-stu-id="d80b0-121">Delete a key or secret</span></span>

<span data-ttu-id="d80b0-122">Hier volgen enkele voorbeelden van het gebruik van PowerShell toomanage Sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="d80b0-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="d80b0-123">Azure Sleutelkluis - stap voor stap</span><span class="sxs-lookup"><span data-stu-id="d80b0-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="d80b0-124">Installeren en configureren van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="d80b0-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="d80b0-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d80b0-125">Next steps</span></span>
<span data-ttu-id="d80b0-126">Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure Sleutelkluis hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d80b0-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="d80b0-127">Zie hello Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="d80b0-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="d80b0-128">Zie Hallo [Azure Key Vault PowerShell-scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="d80b0-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

