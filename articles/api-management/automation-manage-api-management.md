---
title: Azure API Management met behulp van Azure Automation beheren
description: Meer informatie over hoe Azure Automation-service kan worden gebruikt voor het beheren van Azure API Management.
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 73a1135482b88ea7c228bc8b228d47c57b2e70a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="5691d-103">Azure API Management met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="5691d-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="5691d-104">Deze handleiding vindt u de Azure Automation-service en hoe deze kan worden gebruikt voor het vereenvoudigen van beheer van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="5691d-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="5691d-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="5691d-105">What is Azure Automation?</span></span>
<span data-ttu-id="5691d-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="5691d-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="5691d-107">Met behulp van Azure Automation, handmatige, kunnen herhaald, langlopende, foutgevoelige taken worden geautomatiseerd om betrouwbaarheid, efficiëntie en tijd voor de waarde voor uw organisatie te verhogen.</span><span class="sxs-lookup"><span data-stu-id="5691d-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="5691d-108">Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar is om te voldoen aan uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="5691d-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="5691d-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="5691d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="5691d-110">Operationele overhead verminderen en vrijmaken IT en DevOps-personeel te concentreren op het werk dat zakelijke meerwaarde door uw cloud-beheertaken automatisch wordt uitgevoerd door Azure Automation te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="5691d-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="5691d-111">Hoe kan Azure Automation helpen beheren van Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="5691d-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="5691d-112">API Management in Azure Automation kunnen worden beheerd met behulp van de [Windows PowerShell-cmdlets voor Azure API Management-API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="5691d-112">API Management can be managed in Azure Automation by using the [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="5691d-113">U kunt PowerShell workflow-scripts om uit te voeren veel van uw API Management-taken met de cmdlets schrijven in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="5691d-113">Within Azure Automation you can write PowerShell workflow scripts to perform many of your API Management tasks using the cmdlets.</span></span> <span data-ttu-id="5691d-114">U kunt ook deze cmdlets in Azure Automation met de cmdlets voor andere Azure-services, complexe om taken te automatiseren via Azure-services en 3e systemen van derden koppelen.</span><span class="sxs-lookup"><span data-stu-id="5691d-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="5691d-115">Hier volgen enkele voorbeelden van het gebruik van API Management met Automation:</span><span class="sxs-lookup"><span data-stu-id="5691d-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="5691d-116">Azure API Management-PowerShell gebruiken voor back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="5691d-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="5691d-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5691d-117">Next Steps</span></span>
<span data-ttu-id="5691d-118">Nu u de basisprincipes van Azure Automation en hoe deze kan worden gebruikt voor het beheren van Azure API Management hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5691d-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure API Management, follow these links to learn more.</span></span>

* <span data-ttu-id="5691d-119">Zie de Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="5691d-119">See the Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

