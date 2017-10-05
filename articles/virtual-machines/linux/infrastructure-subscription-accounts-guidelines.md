---
title: Abonnement en -account voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor abonnementen en accounts in Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="061b9-103">Azure-abonnement en accounts richtlijnen voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="061b9-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="061b9-104">Dit artikel is gericht op het inzicht benadering van beheer van abonnement en -account als uw omgeving en gebruikersgroep uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="061b9-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="061b9-105">Richtlijnen voor de implementatie voor abonnementen en accounts</span><span class="sxs-lookup"><span data-stu-id="061b9-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="061b9-106">Beslissingen te nemen:</span><span class="sxs-lookup"><span data-stu-id="061b9-106">Decisions:</span></span>

* <span data-ttu-id="061b9-107">Welke set van abonnementen en accounts komen u moet voor het hosten van uw IT-werkbelasting of infrastructuur?</span><span class="sxs-lookup"><span data-stu-id="061b9-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="061b9-108">Hoe u omlaag in de hiërarchie aanpassen aan uw organisatie?</span><span class="sxs-lookup"><span data-stu-id="061b9-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="061b9-109">Taken:</span><span class="sxs-lookup"><span data-stu-id="061b9-109">Tasks:</span></span>

* <span data-ttu-id="061b9-110">Definieer uw organisatiehiërarchie logische als u wilt beheren van een abonnement.</span><span class="sxs-lookup"><span data-stu-id="061b9-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="061b9-111">Definiëren zodat deze overeenkomt met deze logische hiërarchie, de vereiste accounts en -abonnementen onder elke account.</span><span class="sxs-lookup"><span data-stu-id="061b9-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="061b9-112">Maak de set-abonnementen en accounts met behulp van de naamconventie.</span><span class="sxs-lookup"><span data-stu-id="061b9-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="061b9-113">Abonnementen en accounts</span><span class="sxs-lookup"><span data-stu-id="061b9-113">Subscriptions and accounts</span></span>
<span data-ttu-id="061b9-114">Om te werken met Azure, moet u een of meer Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="061b9-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="061b9-115">Resources, zoals virtuele machines (VM's) of virtuele netwerken bestaat in deze abonnementen.</span><span class="sxs-lookup"><span data-stu-id="061b9-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="061b9-116">Enterprise-klanten hebben doorgaans een Enterprise-inschrijving, waardoor de bovenste-bron in de hiërarchie en is gekoppeld aan een of meer accounts.</span><span class="sxs-lookup"><span data-stu-id="061b9-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="061b9-117">De bovenste resource is voor consumenten en klanten zonder een Enterprise-inschrijving, het account.</span><span class="sxs-lookup"><span data-stu-id="061b9-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="061b9-118">Abonnementen worden gekoppeld aan accounts en kan er een of meer abonnementen per account.</span><span class="sxs-lookup"><span data-stu-id="061b9-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="061b9-119">Azure records factureringsgegevens op het abonnementsniveau.</span><span class="sxs-lookup"><span data-stu-id="061b9-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="061b9-120">Vanwege de limiet van twee niveaus voor de relatie Account /-abonnement is het belangrijk dat de naamgevingsconventie van accounts en -abonnementen op de facturering behoeften uitlijnen.</span><span class="sxs-lookup"><span data-stu-id="061b9-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="061b9-121">Bijvoorbeeld, als een globale bedrijf gebruikmaakt van Azure, kunnen ze ervoor kiezen om één account per regio en abonnementen beheerd hebben op het regioniveau:</span><span class="sxs-lookup"><span data-stu-id="061b9-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="061b9-122">Gebruik bijvoorbeeld de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="061b9-122">For instance, you might use the following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="061b9-123">Als een regio wil hebben van meer dan één abonnement die is gekoppeld aan een bepaalde groep, moet een manier voor het coderen van de extra gegevens op het account of naam van het abonnement gebruikmaken van de naamconventie.</span><span class="sxs-lookup"><span data-stu-id="061b9-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="061b9-124">Deze organisatie kan massaging factureringsgegevens om te genereren van de nieuwe niveaus van hiërarchie tijdens facturering rapporten:</span><span class="sxs-lookup"><span data-stu-id="061b9-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="061b9-125">De organisatie kan eruitzien als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="061b9-125">The organization could look like the following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="061b9-126">We bieden gedetailleerde facturering via een downloadbaar bestand voor één account of voor alle accounts in een enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="061b9-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="061b9-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="061b9-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

