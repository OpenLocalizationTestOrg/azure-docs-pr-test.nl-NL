---
title: aaaManage Azure Storage met Azure Automation
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure Storage op grote schaal kan worden.
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
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="48358-103">Azure Storage met Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="48358-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="48358-104">Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikt toosimplify beheer van uw Azure Storage-blobs, tabellen en wachtrijen kan zijn.</span><span class="sxs-lookup"><span data-stu-id="48358-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="48358-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="48358-105">What is Azure Automation?</span></span>
<span data-ttu-id="48358-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="48358-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="48358-107">Met behulp van Azure Automation, herhaalde langlopende, handmatige, foutgevoelige en regelmatig taken worden geautomatiseerd tooincrease betrouwbaarheid en efficiëntie en tijd toovalue voor uw organisatie te verminderen.</span><span class="sxs-lookup"><span data-stu-id="48358-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="48358-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar toomeet wanneer uw organisatie groeit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="48358-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="48358-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="48358-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="48358-110">Lagere operationele overhead en vrijmaken IT / DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="48358-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="48358-111">Hoe kan Azure Automation helpen Azure Storage beheren</span><span class="sxs-lookup"><span data-stu-id="48358-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="48358-112">Azure-opslag in Azure Automation kan worden beheerd met Hallo PowerShell-cmdlets die beschikbaar zijn in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="48358-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="48358-113">Azure Automation heeft deze opslag PowerShell-cmdlets beschikbaar out of box hello, zodat u al uw blob, table en queue beheertaken in Hallo service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="48358-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="48358-114">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="48358-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="48358-115">Hallo [galerie van Azure Automation-runbook](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) bevat een verscheidenheid aan product team en community runbooks tooget gestart met het automatiseren van beheer van Azure Storage, andere Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="48358-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="48358-116">Galerie-runbooks zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="48358-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="48358-117">Azure Storage-Blobs die bepaalde dagen oud met behulp van Automation-Service zijn verwijderen</span><span class="sxs-lookup"><span data-stu-id="48358-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="48358-118">Downloaden van een Blob naar Azure Storage</span><span class="sxs-lookup"><span data-stu-id="48358-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="48358-119">Back-up van alle schijven voor een enkele virtuele machine in Azure of voor alle VM's in een Cloud-Service</span><span class="sxs-lookup"><span data-stu-id="48358-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="48358-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48358-120">Next Steps</span></span>
<span data-ttu-id="48358-121">Nu u Hallo basisbeginselen van Azure Automation en hoe het kan gebruikte toomanage Azure Storage-blobs, tabellen en wachtrijen hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="48358-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="48358-122">Zie hello Azure Automation-zelfstudie [maken of importeren van een runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="48358-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

