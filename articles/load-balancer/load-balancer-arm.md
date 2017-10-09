---
title: Resource Manager-ondersteuning voor de Load Balancer aaaAzure | Microsoft Docs
description: Met behulp van powershell voor de Load Balancer met Azure Resource Manager. Met behulp van sjablonen voor de load balancer
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="88455-104">Ondersteuning van Azure Resource Manager gebruiken met Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="88455-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="88455-105">Azure Resource Manager is Hallo voorkeursbeheerpunten framework voor services in Azure.</span><span class="sxs-lookup"><span data-stu-id="88455-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="88455-106">Azure Load Balancer kunnen worden beheerd met Azure Resource Manager gebaseerde API's en hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="88455-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="88455-107">Concepten</span><span class="sxs-lookup"><span data-stu-id="88455-107">Concepts</span></span>

<span data-ttu-id="88455-108">Met Resource Manager Azure Load Balancer bevat Hallo onderliggende resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="88455-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="88455-109">Front-end-IP-configuratie: een Load balancer kan een of meer front-end IP-adressen, ook bekend als een virtueel IP-adressen (VIP's) bevatten.</span><span class="sxs-lookup"><span data-stu-id="88455-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="88455-110">Deze IP-adressen fungeren als inkomend voor Hallo-verkeer.</span><span class="sxs-lookup"><span data-stu-id="88455-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="88455-111">Back-end-adresgroep: dit zijn IP-adressen die zijn gekoppeld aan virtuele machine voor Hallo Network Interface Card (NIC) toowhich load worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="88455-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="88455-112">Taakverdeling regels: een regeleigenschap toegewezen een front-end opgegeven IP-adres en poort combinatie tooa set back-end-IP-adressen en combinatie van poort.</span><span class="sxs-lookup"><span data-stu-id="88455-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="88455-113">Een enkele load balancer kan meerdere regels voor taakverdeling bevatten.</span><span class="sxs-lookup"><span data-stu-id="88455-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="88455-114">Elke regel is een combinatie van een front-end IP en poort en back-end IP en poort die is gekoppeld aan virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="88455-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="88455-115">Tests – tests schakelt u tookeep bijhouden van Hallo status van de VM-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="88455-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="88455-116">Als u een health test mislukt, Hallo VM-instantie gaat buiten rotatie automatisch.</span><span class="sxs-lookup"><span data-stu-id="88455-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="88455-117">Binnenkomende NAT regels – NAT-regels definiëren Hallo binnenkomend verkeer via Hallo-front-end-IP en gedistribueerde toohello terug IP eindigen.</span><span class="sxs-lookup"><span data-stu-id="88455-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="88455-118">Snelstartsjablonen</span><span class="sxs-lookup"><span data-stu-id="88455-118">Quickstart templates</span></span>

<span data-ttu-id="88455-119">Azure Resource Manager kunt u tooprovision uw toepassingen met behulp van een declaratief sjabloon.</span><span class="sxs-lookup"><span data-stu-id="88455-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="88455-120">U kunt in één enkele sjabloon meerdere services plus de bijbehorende afhankelijkheden implementeren.</span><span class="sxs-lookup"><span data-stu-id="88455-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="88455-121">U hello gebruiken dezelfde sjabloon toorepeatedly uw toepassing tijdens elke fase van de levenscyclus van de toepassing hello implementeren.</span><span class="sxs-lookup"><span data-stu-id="88455-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="88455-122">Sjablonen kunnen definities voor virtuele Machines, virtuele netwerken, Beschikbaarheidssets, netwerkinterfaces (NIC's), Opslagaccounts, Load Balancers, Netwerkbeveiligingsgroepen en openbare IP-adressen bevatten.</span><span class="sxs-lookup"><span data-stu-id="88455-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="88455-123">U kunt alles wat die u nodig hebt voor een complexe toepassing maken met behulp van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="88455-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="88455-124">Hallo-sjabloonbestand kan worden gecontroleerd in content management-systeem voor versiebeheer en samenwerking.</span><span class="sxs-lookup"><span data-stu-id="88455-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="88455-125">Meer informatie over sjablonen</span><span class="sxs-lookup"><span data-stu-id="88455-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="88455-126">Meer informatie over netwerkbronnen</span><span class="sxs-lookup"><span data-stu-id="88455-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="88455-127">Met behulp van de Load Balancer van Azure-snelstartsjablonen vindt u in een [GitHub-opslagplaats](https://github.com/Azure/azure-quickstart-templates) die als host fungeert voor een set sjablonen community is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="88455-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="88455-128">Voorbeelden van sjablonen:</span><span class="sxs-lookup"><span data-stu-id="88455-128">Examples of templates:</span></span>

* [<span data-ttu-id="88455-129">2 virtuele machines in een Load Balancer en taakverdelingsregels</span><span class="sxs-lookup"><span data-stu-id="88455-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="88455-130">2 virtuele machines in een VNET met een interne Load Balancer en Load Balancer-regels</span><span class="sxs-lookup"><span data-stu-id="88455-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="88455-131">2 virtuele machines in een Load Balancer en NAT-regels configureren op Hallo LB</span><span class="sxs-lookup"><span data-stu-id="88455-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="88455-132">Azure Load Balancer met een PowerShell of CLI instellen</span><span class="sxs-lookup"><span data-stu-id="88455-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="88455-133">Aan de slag met Azure Resource Manager-cmdlets, opdrachtregel-hulpprogramma's en REST-API 's</span><span class="sxs-lookup"><span data-stu-id="88455-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="88455-134">[Azure-netwerken Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) gebruikte toocreate een Load Balancer kunt worden.</span><span class="sxs-lookup"><span data-stu-id="88455-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="88455-135">Hoe toocreate een load balancer met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88455-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="88455-136">Hello Azure CLI gebruiken met Azure Resource Management</span><span class="sxs-lookup"><span data-stu-id="88455-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="88455-137">De Load Balancer REST-API 's</span><span class="sxs-lookup"><span data-stu-id="88455-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="88455-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88455-138">Next steps</span></span>

<span data-ttu-id="88455-139">U kunt ook [maken van de load balancer van een Internetgericht](load-balancer-get-started-internet-arm-ps.md) en configureren van welk type [distributie modus](load-balancer-distribution-mode.md) voor een specifieke load balancer-netwerk het gedrag van verkeer.</span><span class="sxs-lookup"><span data-stu-id="88455-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="88455-140">Meer informatie over hoe toomanage [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="88455-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="88455-141">Dit is belangrijk wanneer uw toepassing tookeep verbindingen actief voor servers achter een load balancer moet.</span><span class="sxs-lookup"><span data-stu-id="88455-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
