---
title: aaaCreate een internetgerichte load balancer - Azure classic-portal | Microsoft Docs
description: Meer informatie over hoe een Internet gerichte load balancer aan classic deployment model met toocreate Hallo klassieke Azure-portal
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="9967d-103">Maken van een Internetgericht load balancer (klassiek) Hallo klassieke Azure-portal aan de slag</span><span class="sxs-lookup"><span data-stu-id="9967d-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9967d-104">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9967d-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="9967d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9967d-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="9967d-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9967d-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="9967d-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="9967d-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="9967d-108">Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="9967d-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="9967d-109">Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken.</span><span class="sxs-lookup"><span data-stu-id="9967d-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="9967d-110">U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel.</span><span class="sxs-lookup"><span data-stu-id="9967d-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="9967d-111">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="9967d-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="9967d-112">U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9967d-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="9967d-113">Een internetgerichte load balancer voor virtuele machines instellen</span><span class="sxs-lookup"><span data-stu-id="9967d-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="9967d-114">In de volgorde tooload saldo netwerkverkeer van Hallo Internet over Hallo virtuele machines van een cloudservice, moet u een set met gelijke taakverdeling maken.</span><span class="sxs-lookup"><span data-stu-id="9967d-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="9967d-115">Deze procedure wordt ervan uitgegaan dat u al Hallo virtuele machines hebt gemaakt en dat ze alle zijn binnen Hallo dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="9967d-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="9967d-116">**tooconfigure een set met gelijke taakverdeling voor virtuele machines**</span><span class="sxs-lookup"><span data-stu-id="9967d-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="9967d-117">Klik in de klassieke Azure-portal hello, **virtuele Machines**, en klik vervolgens op Hallo-naam van een virtuele machine in Hallo taakverdeling set.</span><span class="sxs-lookup"><span data-stu-id="9967d-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="9967d-118">Klik op **Eindpunten** en vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9967d-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="9967d-119">Op Hallo **toevoegen van een virtuele machine van de endpoint tooa** pagina, klikt u op Hallo pijl-rechts.</span><span class="sxs-lookup"><span data-stu-id="9967d-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="9967d-120">Op Hallo **Geef details op Hallo van Hallo eindpunt** pagina:</span><span class="sxs-lookup"><span data-stu-id="9967d-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="9967d-121">In **naam**, typ een naam voor het Hallo-eindpunt of selecteer Hallo naam in Hallo lijst met vooraf gedefinieerde eindpunten voor algemene protocollen.</span><span class="sxs-lookup"><span data-stu-id="9967d-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="9967d-122">In **Protocol**, selecteer Hallo-protocol is vereist voor het Hallo-type van het eindpunt, TCP of UDP, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="9967d-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="9967d-123">In **poort van de openbare en particuliere poort**, typt u Hallo poortnummers die u wilt dat Hallo toouse van de virtuele machine, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="9967d-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="9967d-124">U kunt Hallo particuliere poort en firewallregels op Hallo virtuele machine tooredirect verkeer op een manier die geschikt is voor uw toepassing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9967d-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="9967d-125">Hallo particuliere poort kan hetzelfde als de openbare poort Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9967d-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="9967d-126">U kan bijvoorbeeld poort 80 tooboth Hallo openbare en particuliere poort toewijzen voor een eindpunt voor internetverkeer (HTTP).</span><span class="sxs-lookup"><span data-stu-id="9967d-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="9967d-127">Selecteer **een set met gelijke taakverdeling maken**, en klik vervolgens op pijl-rechts Hallo.</span><span class="sxs-lookup"><span data-stu-id="9967d-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="9967d-128">Op Hallo **Hallo taakverdeling set configureren** pagina, typ een naam voor Hallo Netwerktaakverdeling instellen en vervolgens Hallo waarden voor het gedrag van de test Hallo Azure Load Balancer worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="9967d-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="9967d-129">Hallo Load Balancer gebruikt tests toodetermine indien Hallo virtuele machines in Hallo taakverdeling set beschikbaar tooreceive inkomend verkeer zijn.</span><span class="sxs-lookup"><span data-stu-id="9967d-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="9967d-130">Klik op Hallo vinkje toocreate Hallo taakverdeling eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9967d-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="9967d-131">U ziet **Ja** in Hallo **taakverdeling setnaam** kolom Hallo **eindpunten** pagina voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9967d-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="9967d-132">Klik in de portal Hallo op **virtuele Machines**, klikt u op naam van een extra virtuele machine in Hallo taakverdeling set hello, klik op **eindpunten**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9967d-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="9967d-133">Op Hallo **toevoegen van een virtuele machine van de endpoint tooa** pagina, klikt u op **eindpunt tooan bestaande taakverdeling set toevoegen**, selecteert u de naam Hallo van Hallo taakverdeling set en klik op Hallo pijl-rechts.</span><span class="sxs-lookup"><span data-stu-id="9967d-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="9967d-134">Op Hallo **Geef details op Hallo van Hallo eindpunt** pagina en klik vervolgens op het vinkje Hallo Typ een naam voor het Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="9967d-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="9967d-135">Herhaal stap 8-10 voor Hallo aanvullende virtuele machines in Hallo taakverdeling set.</span><span class="sxs-lookup"><span data-stu-id="9967d-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9967d-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9967d-136">Next steps</span></span>

[<span data-ttu-id="9967d-137">Aan de slag met het configureren van een interne load balancer</span><span class="sxs-lookup"><span data-stu-id="9967d-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="9967d-138">Een distributiemodus voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="9967d-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9967d-139">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="9967d-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
