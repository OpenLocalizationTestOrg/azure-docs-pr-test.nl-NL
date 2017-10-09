---
title: overzicht van de load balancer gerichte aaaInternet | Microsoft Docs
description: Overzicht voor Internet gerichte load balancer en de bijbehorende functies. Hoe werkt een load balancer voor virtuele machines en cloudservices met Azure.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="f8858-104">Internet gerichte load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="f8858-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="f8858-105">Azure load balancer wijst Hallo openbare IP-adres en poort nummer van binnenkomende verkeer toohello persoonlijke IP-adres en poort van Hallo virtuele machine en omgekeerd voor Hallo antwoord verkeer van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f8858-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="f8858-106">Regels voor taakverdeling kunnen u specifieke typen toodistribute van verkeer tussen meerdere virtuele machines of services.</span><span class="sxs-lookup"><span data-stu-id="f8858-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="f8858-107">Bijvoorbeeld, kunt u Hallo belasting van de aanvraag webverkeer spreiden meerdere webservers of web-rollen.</span><span class="sxs-lookup"><span data-stu-id="f8858-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="f8858-108">Voor een cloudservice die exemplaren van webrollen of werkrollen bevat, kunt u een openbaar eindpunt in hello (.csdef) servicedefinitiebestand definiëren.</span><span class="sxs-lookup"><span data-stu-id="f8858-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="f8858-109">Hallo *servicedefinition.csdef* bestand bevat de eindpuntconfiguratie Hallo en wanneer er meerdere rolexemplaren voor een implementatie van web- of worker-rol, Hallo load balancer worden ingesteld voor het.</span><span class="sxs-lookup"><span data-stu-id="f8858-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="f8858-110">Hallo manier tooadd exemplaren tooyour cloudimplementatie verandert Hallo-exemplaren op Hallo serviceconfiguratiebestand (.csfg).</span><span class="sxs-lookup"><span data-stu-id="f8858-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="f8858-111">Hallo volgende afbeelding ziet u een eindpunt met gelijke taakverdeling voor internetverkeer die wordt gedeeld door drie virtuele machines voor Hallo openbare en persoonlijke TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="f8858-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="f8858-112">Deze drie virtuele machines zijn in een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="f8858-112">These three virtual machines are in a load-balanced set.</span></span>

![openbare load balancer-voorbeeld](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="f8858-114">Afbeelding 1 - eindpunt voor internetverkeer Netwerktaakverdeling</span><span class="sxs-lookup"><span data-stu-id="f8858-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="f8858-115">Wanneer Internet-clients webpagina-aanvragen toohello openbaar IP-adres van de cloudservice Hallo op TCP-poort 80 verzenden, distribueert hello Azure Load Balancer Hallo aanvragen tussen Hallo drie virtuele machines in Hallo taakverdeling set.</span><span class="sxs-lookup"><span data-stu-id="f8858-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="f8858-116">Zie voor meer informatie over load balancer algoritmen Hallo [overzichtspagina van load balancer](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="f8858-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="f8858-117">Azure Load Balancer distribueert standaard netwerkverkeer wordt evenredig verdeeld over meerdere exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f8858-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="f8858-118">U kunt ook de affiniteit van de sessie configureren voor meer informatie Zie [load balancer-distributie modus](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="f8858-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8858-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8858-119">Next steps</span></span>

<span data-ttu-id="f8858-120">Meer informatie over [interne load balancer](load-balancer-internal-overview.md) toobetter begrijpen welke load balancer is beter geschikt zijn voor uw implementatie van de cloud.</span><span class="sxs-lookup"><span data-stu-id="f8858-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="f8858-121">U kunt ook [maken van de load balancer van een Internetgericht](load-balancer-get-started-internet-arm-ps.md) en configureren van welk type [distributie modus](load-balancer-distribution-mode.md) voor een specifieke load balancer-netwerk het gedrag van verkeer.</span><span class="sxs-lookup"><span data-stu-id="f8858-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="f8858-122">Als uw toepassing tookeep verbindingen voor servers achter een load balancer actief is moet, kunt u meer begrip over [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="f8858-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="f8858-123">Dit helpt toolearn over niet-actieve Verbindingsgedrag wanneer u van Azure Load Balancer gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="f8858-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
