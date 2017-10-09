---
title: vereisten voor het maken van de installatiekopie van een virtuele machine voor hello Azure Marketplace aaaTechnical | Microsoft Docs
description: Hallo-vereisten voor het maken en implementeren van een virtuele machine installatiekopie toohello Azure Marketplace voor anderen begrijpen toopurchase.
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
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="fdee9-103">Technische vereisten voor het maken van de installatiekopie van een virtuele machine voor hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="fdee9-103">Technical prerequisites for creating a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="fdee9-104">Hallo-proces zorgvuldig door voordat u begint lees en begrijp waar en waarom elke stap wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fdee9-104">Read hello process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="fdee9-105">Zo veel mogelijk, u moet uw bedrijfsgegevens en andere gegevens voorbereiden, vereiste hulpprogramma's downloaden en/of technische onderdelen maken voordat u begint met Hallo-proces voor het maken van aanbieding.</span><span class="sxs-lookup"><span data-stu-id="fdee9-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning hello offer creation process.</span></span> <span data-ttu-id="fdee9-106">Deze items moeten worden van de hand van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="fdee9-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="fdee9-107">Download de benodigde hulpprogramma's en toepassingen</span><span class="sxs-lookup"><span data-stu-id="fdee9-107">Download needed tools & applications</span></span>
<span data-ttu-id="fdee9-108">Moet u de volgende items gereed is voordat u begint met Hallo Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="fdee9-108">You should have hello following items ready before beginning hello process:</span></span>

* <span data-ttu-id="fdee9-109">Afhankelijk van het besturingssysteem die u ontwikkelt, installatie Hallo [Azure PowerShell-cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) of [Linux opdrachtregelinterface hulpprogramma](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) van Hallo [Azure downloadt](https://azure.microsoft.com/downloads/) pagina.</span><span class="sxs-lookup"><span data-stu-id="fdee9-109">Depending on which operating system you are targeting, install hello [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="fdee9-110">Azure Opslagverkenner van CodePlex installeren.</span><span class="sxs-lookup"><span data-stu-id="fdee9-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="fdee9-111">Download en installeer Hallo certificeringsinstantie Test hulpprogramma voor Azure gecertificeerd:</span><span class="sxs-lookup"><span data-stu-id="fdee9-111">Download and install hello Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="fdee9-112">[http://go.Microsoft.com/fwlink/?LinkId=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="fdee9-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="fdee9-113">U moet een computer met Windows toorun Hallo certificeringsinstantie hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="fdee9-113">You need a Windows-based computer toorun hello certification tool.</span></span> <span data-ttu-id="fdee9-114">Als u een computer op basis van Windows niet hebt, kunt u Hallo-hulpprogramma voor het gebruik van een VM op basis van Windows in Azure uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fdee9-114">If you do not have a Windows-based computer available, you can run hello tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="fdee9-115">Ondersteunde platforms</span><span class="sxs-lookup"><span data-stu-id="fdee9-115">Platforms supported</span></span>
<span data-ttu-id="fdee9-116">U kunt ontwikkelen op basis van een Azure-machines op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="fdee9-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="fdee9-117">Bepaalde elementen van Hallo publicatieproces--zoals het maken van een Azure-compatibele virtuele harde schijf (VHD)--Gebruik verschillende hulpprogramma's en stappen, afhankelijk van welk besturingssysteem u gebruikt:</span><span class="sxs-lookup"><span data-stu-id="fdee9-117">Some elements of hello publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="fdee9-118">Als u van Linux gebruikmaakt, raadpleeg dan toohello gedeelte 'Een Azure-compatibele-VHD maken (op basis van Linux)' Hallo [virtuele machine installatiekopie publishing handleiding](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="fdee9-118">If you are using Linux, refer toohello “Create an Azure-compatible VHD (Linux-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="fdee9-119">Als u van Windows gebruikmaakt, raadpleeg dan toohello gedeelte 'Een Azure-compatibele-VHD maken (op Windows gebaseerd)' Hallo [virtuele machine installatiekopie publishing handleiding](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="fdee9-119">If you are using Windows, refer toohello “Create an Azure-compatible VHD (Windows-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fdee9-120">U moet toegang tot tooa op basis van Windows machine:</span><span class="sxs-lookup"><span data-stu-id="fdee9-120">You need access tooa Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="fdee9-121">Hallo certificeringsinstantie validatiehulpprogramma uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fdee9-121">Run hello certification validation tool.</span></span>
> * <span data-ttu-id="fdee9-122">Hallo VHD gedeeld access signature-URL voor Hallo VHD certificeringsinstantie indienen maken.</span><span class="sxs-lookup"><span data-stu-id="fdee9-122">Create hello VHD shared access signature URL for hello VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="fdee9-123">Uw VHD ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="fdee9-123">Develop your VHD</span></span>
<span data-ttu-id="fdee9-124">U kunt Azure VHD's in Hallo cloud of on-premises ontwikkelen:</span><span class="sxs-lookup"><span data-stu-id="fdee9-124">You can develop Azure VHDs in hello cloud or on-premises:</span></span>

* <span data-ttu-id="fdee9-125">Cloud-gebaseerde ontwikkeling betekent dat alle stappen van de ontwikkeling op afstand worden uitgevoerd op een VHD residente op Azure.</span><span class="sxs-lookup"><span data-stu-id="fdee9-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="fdee9-126">Lokale ontwikkeling vereist downloaden van een VHD en ontwikkelen met behulp van on-premises infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="fdee9-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="fdee9-127">Hoewel dit mogelijk is raadzaam niet deze.</span><span class="sxs-lookup"><span data-stu-id="fdee9-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="fdee9-128">Houd er rekening mee dat ontwikkelen voor Windows of SQL lokale vereist dat u toohave Hallo relevante lokale licentiecodes te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fdee9-128">Note that developing for Windows or SQL on-premises requires you toohave hello relevant on-premises license keys.</span></span> <span data-ttu-id="fdee9-129">U kan opnemen of installatie van SQL Server na het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fdee9-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="fdee9-130">Ook moet u uw aanbieding baseren op de installatiekopie van een goedgekeurde SQL vanaf hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fdee9-130">You must also base your offer on an approved SQL image from hello Azure portal.</span></span> <span data-ttu-id="fdee9-131">Als u toodevelop lokale besluit, moet u een aantal stappen anders dan als u in Hallo cloud ontwikkelt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fdee9-131">If you decide toodevelop on-premises, you must perform some steps differently than if you were developing in hello cloud.</span></span> <span data-ttu-id="fdee9-132">U kunt relevante informatie vinden in [maken van een installatiekopie van een lokale virtuele machine](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="fdee9-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
