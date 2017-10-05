---
title: Beheren van Azure Sleutelkluis met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe Azure Automation-service kan worden gebruikt voor het beheren van Azure Sleutelkluis.
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
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="4d9ff-103">Het beheren van Azure Sleutelkluis met behulp van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4d9ff-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="4d9ff-104">Deze handleiding vindt u de Azure Automation-service en hoe deze kan worden gebruikt voor het vereenvoudigen van beheer van uw sleutels en geheimen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4d9ff-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="4d9ff-105">What is Azure Automation?</span></span>
<span data-ttu-id="4d9ff-106">[Azure Automation](../automation/automation-intro.md) is een Azure-service voor het vereenvoudigen van beheer door automatisering van bedrijfsprocessen en configuratie van de gewenste status.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="4d9ff-107">Met behulp van Azure Automation, handmatige, kunnen herhaald, langlopende, foutgevoelige taken worden geautomatiseerd om betrouwbaarheid, efficiëntie en tijd voor de waarde voor uw organisatie te verhogen.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="4d9ff-108">Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar is om te voldoen aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="4d9ff-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4d9ff-110">Operationele overhead verminderen en vrijmaken IT en DevOps-personeel te concentreren op het werk dat zakelijke meerwaarde door uw cloud-beheertaken automatisch wordt uitgevoerd door Azure Automation te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="4d9ff-111">Hoe kan Azure Automation helpen beheren van Azure Sleutelkluis?</span><span class="sxs-lookup"><span data-stu-id="4d9ff-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="4d9ff-112">Sleutelkluis in Azure Automation kunnen worden beheerd met behulp van de [AzureRM Sleutelkluis-cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) en [Azure Classic Sleutelkluis-cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d9ff-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="4d9ff-113">De Azure-module voor het beheren van klassieke Sleutelkluis is beschikbaar automatisch in Azure Automation en u kunt importeren de [AzureRM KeyVault-module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) in Azure Automation, zodat u veel van de Sleutelkluis-beheertaken kunt uitvoeren in de service.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="4d9ff-114">U kunt ook deze cmdlets in Azure Automation met de cmdlets voor andere Azure-services, complexe om taken te automatiseren via Azure-services en 3e systemen van derden koppelen.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4d9ff-115">Met de Azure Sleutelkluis-cmdlets kunt u deze taken onder andere uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4d9ff-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="4d9ff-116">Maken en configureren van een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="4d9ff-116">Create and configure a key vault</span></span>
* <span data-ttu-id="4d9ff-117">Maken of importeren van een sleutel</span><span class="sxs-lookup"><span data-stu-id="4d9ff-117">Create or import a key</span></span>
* <span data-ttu-id="4d9ff-118">Maken of bijwerken van een geheim</span><span class="sxs-lookup"><span data-stu-id="4d9ff-118">Create or update a secret</span></span>
* <span data-ttu-id="4d9ff-119">Kenmerken van een sleutel bijwerken</span><span class="sxs-lookup"><span data-stu-id="4d9ff-119">Update attributes of a key</span></span>
* <span data-ttu-id="4d9ff-120">Een sleutel of geheim ophalen</span><span class="sxs-lookup"><span data-stu-id="4d9ff-120">Get a key or secret</span></span>
* <span data-ttu-id="4d9ff-121">Een sleutel of geheim verwijderen</span><span class="sxs-lookup"><span data-stu-id="4d9ff-121">Delete a key or secret</span></span>

<span data-ttu-id="4d9ff-122">Hier volgen enkele voorbeelden van Sleutelkluis beheren met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4d9ff-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="4d9ff-123">Azure Sleutelkluis - stap voor stap</span><span class="sxs-lookup"><span data-stu-id="4d9ff-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="4d9ff-124">Installeren en configureren van een Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="4d9ff-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="4d9ff-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d9ff-125">Next steps</span></span>
<span data-ttu-id="4d9ff-126">Nu u de basisprincipes van Azure Automation en hoe deze kan worden gebruikt voor het beheren van Azure Sleutelkluis hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4d9ff-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="4d9ff-127">Zie de Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="4d9ff-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="4d9ff-128">Zie de [Azure Key Vault PowerShell-scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="4d9ff-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

