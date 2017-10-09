---
title: aaaSubscription en accounts voor Windows-machines in Azure | Microsoft Docs
description: Informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor abonnementen en accounts in Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="3935e-103">Azure-abonnement en accounts richtlijnen voor het Windows-VM 's</span><span class="sxs-lookup"><span data-stu-id="3935e-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="3935e-104">Dit artikel is gericht op het inzicht in hoe tooapproach-abonnement en account beheer als uw omgeving en de gebruikersgroep groeit.</span><span class="sxs-lookup"><span data-stu-id="3935e-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="3935e-105">Richtlijnen voor de implementatie voor abonnementen en accounts</span><span class="sxs-lookup"><span data-stu-id="3935e-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="3935e-106">Beslissingen te nemen:</span><span class="sxs-lookup"><span data-stu-id="3935e-106">Decisions:</span></span>

* <span data-ttu-id="3935e-107">Welke set van abonnementen en accounts moet u toohost infrastructuur of uw IT-werkbelasting?</span><span class="sxs-lookup"><span data-stu-id="3935e-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="3935e-108">Hoe toobreak omlaag Hallo hiërarchie toofit uw organisatie?</span><span class="sxs-lookup"><span data-stu-id="3935e-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="3935e-109">Taken:</span><span class="sxs-lookup"><span data-stu-id="3935e-109">Tasks:</span></span>

* <span data-ttu-id="3935e-110">Definieer uw organisatiehiërarchie logische als u graag toomanage op abonnementsniveau.</span><span class="sxs-lookup"><span data-stu-id="3935e-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="3935e-111">toomatch deze logische hiërarchie definiëren Hallo-accounts die zijn vereist en abonnementen onder elke account.</span><span class="sxs-lookup"><span data-stu-id="3935e-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="3935e-112">Hallo set abonnementen en accounts met behulp van de naamconventie maken.</span><span class="sxs-lookup"><span data-stu-id="3935e-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="3935e-113">Abonnementen en accounts</span><span class="sxs-lookup"><span data-stu-id="3935e-113">Subscriptions and accounts</span></span>
<span data-ttu-id="3935e-114">toowork met Azure, moet u een of meer Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="3935e-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="3935e-115">Resources, zoals virtuele machines (VM's) of virtuele netwerken bestaat in deze abonnementen.</span><span class="sxs-lookup"><span data-stu-id="3935e-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="3935e-116">Enterprise-klanten hebben doorgaans een Enterprise-inschrijving die Hallo bovenste-bron in Hallo hiërarchie en is gekoppeld tooone of meer accounts.</span><span class="sxs-lookup"><span data-stu-id="3935e-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="3935e-117">Voor consumenten en klanten zonder een Enterprise-inschrijving is Hallo bovenste resource Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="3935e-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="3935e-118">Abonnementen worden gekoppeld tooaccounts en kan er een of meer abonnementen per account.</span><span class="sxs-lookup"><span data-stu-id="3935e-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="3935e-119">Azure records factureringsgegevens op Hallo abonnementsniveau.</span><span class="sxs-lookup"><span data-stu-id="3935e-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="3935e-120">Vervaldatum toohello limiet van twee hiërarchieniveaus op Hallo Account /-abonnement relatie is het belangrijk tooalign Hallo naamgevingsconventie accounts en -abonnementen toohello die behoeften facturering.</span><span class="sxs-lookup"><span data-stu-id="3935e-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="3935e-121">Bijvoorbeeld als een globale bedrijf gebruikmaakt van Azure, ze mogelijk toohave één account per regio kiezen en abonnementen hebt beheerd op Hallo van regioniveau:</span><span class="sxs-lookup"><span data-stu-id="3935e-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="3935e-122">Gebruik bijvoorbeeld Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="3935e-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="3935e-123">Als een regio toohave meer dan één abonnement gekoppeld tooa bepaalde groep beslist, een tooencode manier moet gebruikmaken van de naamconventie Hallo Hallo extra gegevens op Hallo-account of de naam van de Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3935e-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="3935e-124">Deze organisatie kunt facturering gegevens toogenerate Hallo nieuwe niveaus van hiërarchie massaging tijdens facturering rapporten:</span><span class="sxs-lookup"><span data-stu-id="3935e-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="3935e-125">Hallo-organisatie kan eruitzien als Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="3935e-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="3935e-126">We bieden gedetailleerde facturering via een downloadbaar bestand voor één account of voor alle accounts in een enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="3935e-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3935e-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3935e-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

