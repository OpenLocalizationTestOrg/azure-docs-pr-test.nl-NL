---
title: Overzicht van de load balancer Internetgericht | Microsoft Docs
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
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="76247-104">Internet gerichte load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="76247-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="76247-105">Azure load balancer wijst het openbare IP-adres en poort aantal binnenkomend verkeer naar het particuliere IP-adres en poort nummer van de virtuele machine en omgekeerd voor het verkeer van het antwoord van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="76247-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="76247-106">Regels voor taakverdeling kunnen u bepaalde soorten verkeer tussen meerdere virtuele machines of services distribueren.</span><span class="sxs-lookup"><span data-stu-id="76247-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="76247-107">Bijvoorbeeld, kunt u het laden van de aanvraag webverkeer spreiden meerdere webservers of web-rollen.</span><span class="sxs-lookup"><span data-stu-id="76247-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="76247-108">Voor een cloudservice die exemplaren van webrollen of werkrollen bevat, kunt u een openbaar eindpunt definiëren in het servicedefinitiebestand (.csdef).</span><span class="sxs-lookup"><span data-stu-id="76247-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="76247-109">De *servicedefinition.csdef* bestand bevat de eindpuntconfiguratie en wanneer er meerdere rolexemplaren voor een implementatie van web- of worker-rol, de load balancer worden ingesteld voor het.</span><span class="sxs-lookup"><span data-stu-id="76247-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="76247-110">Het aantal exemplaren op het serviceconfiguratiebestand (.csfg) is het wijzigen van de manier waarop exemplaren toevoegen aan uw implementatie van de cloud.</span><span class="sxs-lookup"><span data-stu-id="76247-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="76247-111">De volgende afbeelding ziet een eindpunt met gelijke taakverdeling voor internetverkeer die wordt gedeeld door drie virtuele machines voor de openbare en persoonlijke TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="76247-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="76247-112">Deze drie virtuele machines zijn in een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="76247-112">These three virtual machines are in a load-balanced set.</span></span>

![openbare load balancer-voorbeeld](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="76247-114">Afbeelding 1 - eindpunt voor internetverkeer Netwerktaakverdeling</span><span class="sxs-lookup"><span data-stu-id="76247-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="76247-115">Wanneer Internet-clients webpagina-aanvragen naar het openbare IP-adres van de cloudservice op TCP-poort 80 verzenden, distribueert de Azure Load Balancer de aanvragen tussen de drie virtuele machines in de set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="76247-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="76247-116">Zie voor meer informatie over de algoritmen voor load balancer, het [overzichtspagina van load balancer](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="76247-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="76247-117">Azure Load Balancer distribueert standaard netwerkverkeer wordt evenredig verdeeld over meerdere exemplaren van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="76247-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="76247-118">U kunt ook de affiniteit van de sessie configureren voor meer informatie Zie [load balancer-distributie modus](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="76247-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="76247-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76247-119">Next steps</span></span>

<span data-ttu-id="76247-120">Meer informatie over [interne load balancer](load-balancer-internal-overview.md) om beter te begrijpen welke load balancer is beter geschikt zijn voor uw implementatie van de cloud.</span><span class="sxs-lookup"><span data-stu-id="76247-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="76247-121">U kunt ook [maken van de load balancer van een Internetgericht](load-balancer-get-started-internet-arm-ps.md) en configureren van welk type [distributie modus](load-balancer-distribution-mode.md) voor een specifieke load balancer-netwerk het gedrag van verkeer.</span><span class="sxs-lookup"><span data-stu-id="76247-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="76247-122">Als uw toepassing verbindingen actief moet houden voor servers achter een load balancer, krijgt u meer inzicht in [niet-actieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="76247-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="76247-123">Op deze manier krijgt u meer informatie over het gedrag van niet-actieve verbindingen wanneer u Azure Load Balancer gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76247-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
