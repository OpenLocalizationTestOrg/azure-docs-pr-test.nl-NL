---
title: Azure Storage met Azure Automation beheren
description: Meer informatie over hoe Azure Automation-service kan worden gebruikt voor het beheren van Azure Storage op grote schaal.
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 4649e42a628307e15f8b067503e4e8e13f16f1af
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="24808-103">Azure Storage met Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="24808-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="24808-104">Deze handleiding vindt u de Azure Automation-service en hoe deze kan worden gebruikt voor het vereenvoudigen van beheer van uw Azure Storage-blobs, tabellen en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="24808-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="24808-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="24808-105">What is Azure Automation?</span></span>
<span data-ttu-id="24808-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="24808-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="24808-107">Met Azure Automation, langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken kunnen worden geautomatiseerd om betrouwbaarheid en efficiëntie te verhogen en problemen sneller op de waarde voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="24808-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="24808-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar is om te voldoen aan de behoeften van uw wanneer uw organisatie groeit.</span><span class="sxs-lookup"><span data-stu-id="24808-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="24808-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="24808-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="24808-110">Lagere operationele overhead en vrijmaken IT / DevOps-personeel te concentreren op het werk dat zakelijke voegt waarde door uw cloud-beheertaken automatisch wordt uitgevoerd door Azure Automation te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="24808-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="24808-111">Hoe kan Azure Automation helpen Azure Storage beheren</span><span class="sxs-lookup"><span data-stu-id="24808-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="24808-112">Azure-opslag in Azure Automation kan worden beheerd met behulp van de PowerShell-cmdlets die beschikbaar zijn in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="24808-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="24808-113">Azure Automation heeft deze PowerShell-cmdlets Storage beschikbaar gebruiksklaar, zodat u alle van de blob, table en queue beheertaken in de service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="24808-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="24808-114">U kunt ook deze cmdlets in Azure Automation met de cmdlets voor andere Azure-services, complexe om taken te automatiseren via Azure-services en 3e systemen van derden koppelen.</span><span class="sxs-lookup"><span data-stu-id="24808-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="24808-115">De [galerie van Azure Automation-runbook](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) bevat een verscheidenheid aan product team en community runbooks om te beginnen met het automatiseren van beheer van Azure Storage, andere Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="24808-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="24808-116">Galerie-runbooks zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="24808-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="24808-117">Azure Storage-Blobs die bepaalde dagen oud met behulp van Automation-Service zijn verwijderen</span><span class="sxs-lookup"><span data-stu-id="24808-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="24808-118">Downloaden van een Blob naar Azure Storage</span><span class="sxs-lookup"><span data-stu-id="24808-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="24808-119">Back-up van alle schijven voor een enkele virtuele machine in Azure of voor alle VM's in een Cloud-Service</span><span class="sxs-lookup"><span data-stu-id="24808-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="24808-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24808-120">Next Steps</span></span>
<span data-ttu-id="24808-121">Nu dat u de basisprincipes van Azure Automation en hoe deze kan worden gebruikt voor het beheren van Azure Storage-blobs, tabellen en wachtrijen hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="24808-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="24808-122">Zie de zelfstudie Azure Automation [maken of importeren van een runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="24808-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

