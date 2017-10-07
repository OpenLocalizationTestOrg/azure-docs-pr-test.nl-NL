---
title: aaaOverview van Azure DNS | Microsoft Docs
description: Overzicht van DNS-hosting-service op Microsoft Azure. Host uw domein in Microsoft Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="e2c93-104">Azure DNS-overzicht</span><span class="sxs-lookup"><span data-stu-id="e2c93-104">Azure DNS overview</span></span>

<span data-ttu-id="e2c93-105">Hallo Domain Name System en DNS, is verantwoordelijk voor het omzetten van (of het oplossen van) een website of service name tooits IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e2c93-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="e2c93-106">Azure DNS is een hosting service voor DNS-domeinen omzetten van namen met behulp van Microsoft Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="e2c93-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="e2c93-107">U kunt uw DNS beheren door het hosten van uw Azure-domeinen records met dezelfde referenties, API's, hulpprogramma's en facturering Hallo als uw andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="e2c93-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![DNS-overzicht](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="e2c93-109">Functies</span><span class="sxs-lookup"><span data-stu-id="e2c93-109">Features</span></span>

* <span data-ttu-id="e2c93-110">**Betrouwbaarheid en prestaties** -DNS-domeinen in Azure DNS worden gehost op Azure wereldwijd netwerk van DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="e2c93-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="e2c93-111">We gebruiken Anycast networking zodat elke DNS-query wordt beantwoord door Hallo dichtstbijzijnde beschikbare DNS-server.</span><span class="sxs-lookup"><span data-stu-id="e2c93-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="e2c93-112">Dit biedt zowel snelle prestaties en hoge beschikbaarheid voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="e2c93-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="e2c93-113">**Naadloze integratie** -hello Azure DNS-service kan gebruikte toomanage DNS-records voor uw Azure-services en gebruikte tooprovide DNS voor uw externe resources ook kan worden.</span><span class="sxs-lookup"><span data-stu-id="e2c93-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="e2c93-114">Azure DNS is geïntegreerd in hello Azure-portal en maakt gebruik van dezelfde referenties, facturering en support-contract Hallo als uw andere Azure-services.</span><span class="sxs-lookup"><span data-stu-id="e2c93-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="e2c93-115">**Beveiliging** -hello Azure DNS-service is gebaseerd op Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e2c93-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="e2c93-116">Als zodanig voordelen van Resource Manager-functies zoals rollen gebaseerd toegangsbeheer controlelogboeken en resource vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="e2c93-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="e2c93-117">Uw domeinen en records kunnen worden beheerd via hello Azure-portal, Azure PowerShell-cmdlets en Hallo platformoverschrijdende Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e2c93-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="e2c93-118">Toepassingen waarbij automatisch DNS-beheer kunnen integreren met de service via Hallo Hallo REST-API en SDK's.</span><span class="sxs-lookup"><span data-stu-id="e2c93-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="e2c93-119">Azure DNS ondersteunt momenteel geen kopen van domeinnamen.</span><span class="sxs-lookup"><span data-stu-id="e2c93-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="e2c93-120">Als u wilt dat toopurchase domeinen, moet u toouse een domeinnaamregistrar van derden.</span><span class="sxs-lookup"><span data-stu-id="e2c93-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="e2c93-121">Hallo registrar brengt doorgaans een kleine jaarlijkse rekening.</span><span class="sxs-lookup"><span data-stu-id="e2c93-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="e2c93-122">Hallo-domeinen kunnen vervolgens worden gehost in Azure DNS voor het beheer van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="e2c93-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="e2c93-123">Zie [delegeren van een domein tooAzure DNS-](dns-domain-delegation.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2c93-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="e2c93-124">Prijzen</span><span class="sxs-lookup"><span data-stu-id="e2c93-124">Pricing</span></span>

<span data-ttu-id="e2c93-125">DNS-facturering is gebaseerd op Hallo aantal DNS-zones die worden gehost in Azure en door Hallo aantal DNS-query's.</span><span class="sxs-lookup"><span data-stu-id="e2c93-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="e2c93-126">meer informatie over prijzen bezoek toolearn [prijzen van Azure DNS-](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="e2c93-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="e2c93-127">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="e2c93-127">FAQ</span></span>

<span data-ttu-id="e2c93-128">Zie voor veelgestelde vragen over Azure DNS Hallo [DNS-Veelgestelde vragen over Azure](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="e2c93-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c93-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2c93-129">Next steps</span></span>

<span data-ttu-id="e2c93-130">Meer informatie over DNS-zones en records in via: [DNS-zones en registreert overzicht](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="e2c93-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="e2c93-131">Meer informatie over hoe te[maken van een DNS-zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e2c93-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="e2c93-132">Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure.</span><span class="sxs-lookup"><span data-stu-id="e2c93-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

