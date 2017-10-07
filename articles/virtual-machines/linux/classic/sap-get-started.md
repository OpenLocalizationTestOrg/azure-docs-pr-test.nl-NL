---
title: aaaUsing SAP op Linux virtuele machines | Microsoft Docs
description: Meer informatie over het gebruik van SAP op virtuele Linux-machines in Microsoft Azure
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: a805cdecb515239057e185a92bf5c4d4e707f72f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="f6f81-103">Met behulp van SAP op Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="f6f81-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="f6f81-104">Cloudcomputing is een veelgebruikte term die meer belang binnen Hallo IT-sector van kleine bedrijven up toolarge en meertalige ondernemingen winnen wordt.</span><span class="sxs-lookup"><span data-stu-id="f6f81-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="f6f81-105">Microsoft Azure is Hallo Services Cloudplatform van Microsoft een breed scala aan nieuwe mogelijkheden biedt.</span><span class="sxs-lookup"><span data-stu-id="f6f81-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="f6f81-106">Klanten zijn nu kunnen toorapidly leveren en intrekken toepassingen als Cloud-Services, zodat ze niet beperkt tootechnical of budget beperkingen zijn.</span><span class="sxs-lookup"><span data-stu-id="f6f81-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="f6f81-107">In plaats van de tijd en geld investeren in hardware-infrastructuur, bedrijven kunnen zich concentreren op de toepassing hello, bedrijfsprocessen en de voordelen voor klanten en gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f6f81-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="f6f81-108">Met Microsoft Azure virtuele machines biedt Microsoft een uitgebreide infrastructuur als een Service (IaaS)-platform.</span><span class="sxs-lookup"><span data-stu-id="f6f81-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="f6f81-109">SAP NetWeaver-toepassingen worden ondersteund op virtuele Azure-machines (IaaS).</span><span class="sxs-lookup"><span data-stu-id="f6f81-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="f6f81-110">Hallo whitepapers hieronder wordt beschreven hoe tooplan en SAP NetWeaver implementeren op basis van toepassingen op Windows virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6f81-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="f6f81-111">U kunt ook SAP NetWeaver op basis van toepassingen implementeren op [Windows virtuele machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f6f81-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="f6f81-112">SAP NetWeaver op Azure SUSE Linux virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="f6f81-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="f6f81-113">titel: aaaTesting SAP NetWeaver op Microsoft Azure SUSE Linux VM's</span><span class="sxs-lookup"><span data-stu-id="f6f81-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="f6f81-114">Overzicht: Is er geen officiële SAP-ondersteuning voor het uitvoeren van de SAP NetWeaver op dit moment op Azure Linux VM's.</span><span class="sxs-lookup"><span data-stu-id="f6f81-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="f6f81-115">Niettemin wellicht klanten toodo sommige testen of overwegen toorun SAP-demo of opleiding systemen op Azure Linux VM's, zolang er is geen nodig contact op met ondersteuning van SAP.</span><span class="sxs-lookup"><span data-stu-id="f6f81-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="f6f81-116">Dit artikel instellen van Azure SUSE Linux VM's voor het uitvoeren van SAP kan helpen en biedt een aantal basic hints in volgorde tooavoid potentiële verrassingen.</span><span class="sxs-lookup"><span data-stu-id="f6f81-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="f6f81-117">Bijgewerkte: December 2015</span><span class="sxs-lookup"><span data-stu-id="f6f81-117">Updated: December 2015</span></span>

[<span data-ttu-id="f6f81-118">In dit artikel vindt u hier</span><span class="sxs-lookup"><span data-stu-id="f6f81-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

