---
title: DNS-instellingen opgeven in een serviceconfiguratiebestand | Microsoft Docs
description: aangepaste DNS-instellingen voor virtueel netwerk met behulp van serviceconfiguratiebestand opgeven
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="2ab35-103">DNS-instellingen in een serviceconfiguratiebestand opgeven</span><span class="sxs-lookup"><span data-stu-id="2ab35-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="2ab35-104">DNS-elementen</span><span class="sxs-lookup"><span data-stu-id="2ab35-104">DNS elements</span></span>
<span data-ttu-id="2ab35-105">Een service-configuratiebestand mag bevatten een DnsServers-element met een lijst met IPv4-adressen voor de Domain Name System (DNS)-servers die door de service wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ab35-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="2ab35-106">Instellingen in het configuratiebestand van de service hebben voorrang boven de instellingen in het configuratiebestand van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="2ab35-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="2ab35-107">Zie voor meer informatie [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ab35-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="2ab35-108">**NetworkConfiguration-element**</span><span class="sxs-lookup"><span data-stu-id="2ab35-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="2ab35-109">De **naam** kenmerk in de **DnsServer** element alleen als een verwijzingsnaam wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2ab35-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="2ab35-110">Vertegenwoordigt niet de hostnaam voor de DNS-server.</span><span class="sxs-lookup"><span data-stu-id="2ab35-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="2ab35-111">Elke **DnsServer** kenmerkwaarde moet uniek zijn in het hele Microsoft Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2ab35-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="2ab35-112">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2ab35-112">See Also</span></span>
[<span data-ttu-id="2ab35-113">Het configuratieschema Azure-Service (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="2ab35-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="2ab35-114">Azure Virtual Network-configuratieschema</span><span class="sxs-lookup"><span data-stu-id="2ab35-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="2ab35-115">Een virtueel netwerk met behulp van de configuratiebestanden netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="2ab35-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="2ab35-116">Over de instellingen van het virtuele netwerk in de beheerportal</span><span class="sxs-lookup"><span data-stu-id="2ab35-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

