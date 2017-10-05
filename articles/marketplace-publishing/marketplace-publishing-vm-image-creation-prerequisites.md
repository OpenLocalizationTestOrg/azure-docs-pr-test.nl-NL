---
title: Technische vereisten voor het maken van de installatiekopie van een virtuele machine voor Azure Marketplace | Microsoft Docs
description: Begrip van de vereisten voor het maken en implementeren van de installatiekopie van een virtuele machine naar de Azure Marketplace voor anderen om aan te schaffen.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="2ff09-103">Technische vereisten voor het maken van de installatiekopie van een virtuele machine voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="2ff09-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="2ff09-104">Het proces zorgvuldig door voordat u begint lees en begrijp waar en waarom elke stap wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2ff09-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="2ff09-105">Zo veel mogelijk, u moet voorbereiden van uw bedrijfsgegevens en andere gegevens, vereiste hulpprogramma's downloaden en/of technische onderdelen maken voordat u begint met een proces voor het maken van de aanbieding.</span><span class="sxs-lookup"><span data-stu-id="2ff09-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="2ff09-106">Deze items moeten worden van de hand van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2ff09-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="2ff09-107">Download de benodigde hulpprogramma's en toepassingen</span><span class="sxs-lookup"><span data-stu-id="2ff09-107">Download needed tools & applications</span></span>
<span data-ttu-id="2ff09-108">U hebt de volgende items gereed is voordat u begint met het proces:</span><span class="sxs-lookup"><span data-stu-id="2ff09-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="2ff09-109">Afhankelijk van het besturingssysteem die u ontwikkelt, installeert u de [Azure PowerShell-cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) of [Linux opdrachtregelinterface hulpprogramma](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) van de [Azure downloadt](https://azure.microsoft.com/downloads/) pagina.</span><span class="sxs-lookup"><span data-stu-id="2ff09-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="2ff09-110">Azure Opslagverkenner van CodePlex installeren.</span><span class="sxs-lookup"><span data-stu-id="2ff09-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="2ff09-111">Download en installeer het hulpprogramma certificeringsinstantie Test voor Azure gecertificeerd:</span><span class="sxs-lookup"><span data-stu-id="2ff09-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="2ff09-112">[http://go.Microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="2ff09-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="2ff09-113">U moet een Windows-computer het certificeringsinstantie-hulpprogramma uitvoert.</span><span class="sxs-lookup"><span data-stu-id="2ff09-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="2ff09-114">Als u een computer op basis van Windows niet hebt, kunt u het hulpprogramma voor het gebruik van een VM op basis van Windows in Azure uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2ff09-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="2ff09-115">Ondersteunde platforms</span><span class="sxs-lookup"><span data-stu-id="2ff09-115">Platforms supported</span></span>
<span data-ttu-id="2ff09-116">U kunt ontwikkelen op basis van een Azure-machines op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="2ff09-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="2ff09-117">Bepaalde elementen van het publicatieproces--zoals het maken van een Azure-compatibele virtuele harde schijf (VHD)--Gebruik verschillende hulpprogramma's en stappen, afhankelijk van welk besturingssysteem u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="2ff09-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="2ff09-118">Als u van Linux gebruikmaakt, raadpleegt u de sectie 'Een Azure-compatibele-VHD maken (op basis van Linux)' van de [virtuele machine installatiekopie publishing handleiding](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="2ff09-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="2ff09-119">Als u van Windows gebruikmaakt, raadpleegt u de sectie 'Een Azure-compatibele-VHD maken (op Windows gebaseerd)' van de [virtuele machine installatiekopie publishing handleiding](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="2ff09-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2ff09-120">U moet toegang tot een Windows-machine op:</span><span class="sxs-lookup"><span data-stu-id="2ff09-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="2ff09-121">Voer de validatie certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="2ff09-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="2ff09-122">Maken van de VHD gedeeld access signature-URL voor de verzending van het VHD-certificering.</span><span class="sxs-lookup"><span data-stu-id="2ff09-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="2ff09-123">Uw VHD ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="2ff09-123">Develop your VHD</span></span>
<span data-ttu-id="2ff09-124">U kunt Azure VHD's in de cloud of on-premises ontwikkelen:</span><span class="sxs-lookup"><span data-stu-id="2ff09-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="2ff09-125">Cloud-gebaseerde ontwikkeling betekent dat alle stappen van de ontwikkeling op afstand worden uitgevoerd op een VHD residente op Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff09-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="2ff09-126">Lokale ontwikkeling vereist downloaden van een VHD en ontwikkelen met behulp van on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="2ff09-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="2ff09-127">Hoewel dit mogelijk is raadzaam niet deze.</span><span class="sxs-lookup"><span data-stu-id="2ff09-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="2ff09-128">Houd er rekening mee dat ontwikkelen voor Windows of SQL lokale, moet u de relevante lokale licentiesleutels hebben.</span><span class="sxs-lookup"><span data-stu-id="2ff09-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="2ff09-129">U kan opnemen of installatie van SQL Server na het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2ff09-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="2ff09-130">Ook moet u uw aanbieding baseren op een goedgekeurde SQL-installatiekopie van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2ff09-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="2ff09-131">Als u lokale ontwikkelen besluit, moet u anders dan als u in de cloud ontwikkelt een aantal stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2ff09-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="2ff09-132">U kunt relevante informatie vinden in [maken van een installatiekopie van een lokale virtuele machine](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="2ff09-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
