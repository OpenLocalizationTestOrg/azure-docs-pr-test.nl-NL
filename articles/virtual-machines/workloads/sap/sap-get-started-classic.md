---
title: SAP op Linux virtuele machines gebruiken | Microsoft Docs
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
ms.openlocfilehash: 66eb53f99ce4b30ec283243deb3649c9ca897a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="5de81-103">Met behulp van SAP op Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="5de81-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="5de81-104">Cloud computing is een veelgebruikte term die in de IT-sector steeds belangrijker wordt, zowel voor kleine bedrijven als voor grote ondernemingen en multinationals.</span><span class="sxs-lookup"><span data-stu-id="5de81-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="5de81-105">Microsoft Azure is het cloudserviceplatform van Microsoft dat een groot aantal nieuwe mogelijkheden biedt.</span><span class="sxs-lookup"><span data-stu-id="5de81-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="5de81-106">Klanten kunnen toepassingen nu snel als cloudservices inrichten en de inrichting weer ongedaan maken, zodat technische of financiële beperkingen geen rol spelen.</span><span class="sxs-lookup"><span data-stu-id="5de81-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="5de81-107">In plaats van tijd en geld te investeren in de hardware-infrastructuur kunnen bedrijven zich nu richten op de toepassing, bedrijfsprocessen en de voordelen voor klanten en gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5de81-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="5de81-108">Met Microsoft Azure virtuele machines biedt Microsoft een uitgebreide infrastructuur als een Service (IaaS)-platform.</span><span class="sxs-lookup"><span data-stu-id="5de81-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="5de81-109">SAP NetWeaver-toepassingen worden ondersteund op virtuele Azure-machines (IaaS).</span><span class="sxs-lookup"><span data-stu-id="5de81-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="5de81-110">De whitepapers die hieronder wordt beschreven hoe plannen en implementeren van toepassingen voor SAP NetWeaver gebaseerd op Windows virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="5de81-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="5de81-111">U kunt ook SAP NetWeaver op basis van toepassingen implementeren op [Windows virtuele machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5de81-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="5de81-112">SAP NetWeaver op Azure SUSE Linux virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="5de81-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="5de81-113">Titel: SAP NetWeaver op Microsoft Azure SUSE Linux VM's testen</span><span class="sxs-lookup"><span data-stu-id="5de81-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="5de81-114">Overzicht: Is er geen officiële SAP-ondersteuning voor het uitvoeren van de SAP NetWeaver op dit moment op Azure Linux VM's.</span><span class="sxs-lookup"><span data-stu-id="5de81-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="5de81-115">Niettemin klanten zou willen sommige testen of overwegen of uit te voeren SAP-demo training systemen op Azure Linux VM's, zolang er is geen nodig contact op met ondersteuning van SAP.</span><span class="sxs-lookup"><span data-stu-id="5de81-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="5de81-116">Dit artikel kunt instellen van Azure SUSE Linux VM's voor het uitvoeren van SAP en biedt een aantal basic hints om te voorkomen dat potentiële verrassingen.</span><span class="sxs-lookup"><span data-stu-id="5de81-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="5de81-117">Bijgewerkte: December 2015</span><span class="sxs-lookup"><span data-stu-id="5de81-117">Updated: December 2015</span></span>

[<span data-ttu-id="5de81-118">In dit artikel vindt u hier</span><span class="sxs-lookup"><span data-stu-id="5de81-118">This article can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

