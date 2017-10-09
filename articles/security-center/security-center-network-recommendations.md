---
title: aaaProtecting uw netwerk in Azure Security Center | Microsoft Docs
description: Dit document gaat in Azure Security Center aanbevelingen die u helpen beveiligen van uw Azure-netwerk en blijven in overeenstemming met het beveiligingsbeleid.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="38c6c-103">Beveiligen van uw netwerk in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="38c6c-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="38c6c-104">Azure Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="38c6c-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="38c6c-105">Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, maakt deze aanbevelingen die u helpt bij Hallo Hallo nodig-besturingselementen configureren.</span><span class="sxs-lookup"><span data-stu-id="38c6c-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="38c6c-106">Aanbevelingen tooAzure brontypen die van toepassing: virtuele machines (VM's), netwerken, SQL en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="38c6c-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="38c6c-107">In dit artikel biedt de aanbevelingen die van toepassing zijn tooyour netwerk.</span><span class="sxs-lookup"><span data-stu-id="38c6c-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="38c6c-108">Netwerkcentrum aanbevelingen om de volgende generatie firewalls, Netwerkbeveiligingsgroepen en regels voor binnenkomend verkeer op configureren.</span><span class="sxs-lookup"><span data-stu-id="38c6c-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="38c6c-109">Gebruik Hallo onderstaande tabel als een verwijzing toohelp erkent u Hallo beschikbaar netwerk aanbevelingen en elke eigenschap als u deze toe te passen.</span><span class="sxs-lookup"><span data-stu-id="38c6c-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="38c6c-110">Aanbevelingen voor de beschikbare netwerken</span><span class="sxs-lookup"><span data-stu-id="38c6c-110">Available network recommendations</span></span>
| <span data-ttu-id="38c6c-111">Aanbeveling</span><span class="sxs-lookup"><span data-stu-id="38c6c-111">Recommendation</span></span> | <span data-ttu-id="38c6c-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="38c6c-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="38c6c-113">Een firewall van de volgende generatie toevoegen</span><span class="sxs-lookup"><span data-stu-id="38c6c-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="38c6c-114">Raadt aan dat u, een volgende generatie Firewall (NGFW) van een Microsoft-partner tooincrease uw beveiligingsinstellingen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="38c6c-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="38c6c-115">Verkeer alleen via NGFW sturen</span><span class="sxs-lookup"><span data-stu-id="38c6c-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="38c6c-116">Raadt aan dat u configureert (NSG) netwerkbeveiligingsgroepen die binnenkomend verkeer tooyour VM via uw NGFW afdwingen.</span><span class="sxs-lookup"><span data-stu-id="38c6c-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="38c6c-117">Netwerkbeveiligingsgroepen op subnetten of virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="38c6c-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="38c6c-118">Raadt het nsg's op subnetten of VM's in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="38c6c-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="38c6c-119">Toegang tot en met een Internetgericht eindpunt beperken</span><span class="sxs-lookup"><span data-stu-id="38c6c-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="38c6c-120">Raadt aan dat u regels voor binnenkomend verkeer voor het nsg's configureren.</span><span class="sxs-lookup"><span data-stu-id="38c6c-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="38c6c-121">Zie ook</span><span class="sxs-lookup"><span data-stu-id="38c6c-121">See also</span></span>
<span data-ttu-id="38c6c-122">toolearn meer informatie over de aanbevelingen die van toepassing zijn tooother Azure brontypen, Zie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="38c6c-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="38c6c-123">Beveiligen van uw virtuele machines in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="38c6c-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="38c6c-124">Beveiligen van uw toepassingen in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="38c6c-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="38c6c-125">Beveiligen van uw Azure SQL-service in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="38c6c-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="38c6c-126">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="38c6c-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="38c6c-127">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="38c6c-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="38c6c-128">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="38c6c-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="38c6c-129">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="38c6c-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
