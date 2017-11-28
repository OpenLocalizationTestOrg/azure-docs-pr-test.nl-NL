---
title: DNS-instellingen in een serviceconfiguratiebestand aaaSpecifying | Microsoft Docs
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
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="1328b-103">DNS-instellingen in een serviceconfiguratiebestand opgeven</span><span class="sxs-lookup"><span data-stu-id="1328b-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="1328b-104">DNS-elementen</span><span class="sxs-lookup"><span data-stu-id="1328b-104">DNS elements</span></span>
<span data-ttu-id="1328b-105">Een service-configuratiebestand mag bevatten een DnsServers-element met een lijst met IPv4-adressen voor Hallo Domain Name System (DNS)-servers die Hallo-service wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1328b-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="1328b-106">Instellingen in het serviceconfiguratiebestand hello, hebben voorrang boven de instellingen in het configuratiebestand Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="1328b-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="1328b-107">Zie voor meer informatie [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="1328b-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="1328b-108">**NetworkConfiguration-element**</span><span class="sxs-lookup"><span data-stu-id="1328b-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="1328b-109">Hallo **naam** kenmerk in Hallo **DnsServer** element alleen als een verwijzingsnaam wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1328b-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="1328b-110">Dit vormt geen hostnaam Hallo voor Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="1328b-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="1328b-111">Elke **DnsServer** kenmerkwaarde uniek zijn binnen de gehele Microsoft Azure-abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="1328b-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="1328b-112">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1328b-112">See Also</span></span>
[<span data-ttu-id="1328b-113">Het configuratieschema Azure-Service (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="1328b-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="1328b-114">Azure Virtual Network-configuratieschema</span><span class="sxs-lookup"><span data-stu-id="1328b-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="1328b-115">Een virtueel netwerk met behulp van de configuratiebestanden netwerk configureren</span><span class="sxs-lookup"><span data-stu-id="1328b-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="1328b-116">Over Virtual Network-instellingen in het Hallo-beheerportal</span><span class="sxs-lookup"><span data-stu-id="1328b-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

