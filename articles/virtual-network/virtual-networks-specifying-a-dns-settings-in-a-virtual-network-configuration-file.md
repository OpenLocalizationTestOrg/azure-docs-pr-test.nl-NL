---
title: DNS-instellingen in een virtueel netwerk configuratiebestand aaaSpecifying | Microsoft Docs
description: Hoe DNS-serverinstellingen toochange in een virtueel netwerk met behulp van de configuratie van een virtueel netwerk in het klassieke implementatiemodel Hallo bestand
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="4b3a7-103">DNS-instellingen opgeven in een configuratiebestand voor het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="4b3a7-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="4b3a7-104">Een configuratiebestand netwerk bestaat uit twee elementen waarmee u instellingen voor toospecify Domain Name System (DNS kunt): **DnsServers** en **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="4b3a7-105">U kunt een lijst met DNS-servers toevoegen door te geven van de IP-adressen en namen toohello verwijzen naar **DnsServers** element.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="4b3a7-106">U kunt een **DnsServerRef** element toospecify welke DNS-serveringangen uit Hallo DnsServers element worden gebruikt voor andere netwerksites binnen het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4b3a7-107">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="4b3a7-108">Hallo netwerk configuratiebestand kan Hallo volgende elementen bevatten.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="4b3a7-109">Hallo titel van elk element is gekoppelde tooa pagina met aanvullende informatie over Hallo element waarde-instellingen.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b3a7-110">Zie voor meer informatie over hoe tooconfigure netwerk configuratiebestand Hallo [configureren van een virtueel netwerk via een netwerk-configuratiebestand](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="4b3a7-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="4b3a7-111">Zie voor meer informatie over elk element in het configuratiebestand voor Hallo netwerk [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b3a7-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="4b3a7-112">DNS-Element</span><span class="sxs-lookup"><span data-stu-id="4b3a7-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="4b3a7-113">Hallo **naam** kenmerk in Hallo **DnsServer** element alleen als een verwijzing wordt gebruikt voor Hallo **DnsServerRef** element.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="4b3a7-114">Dit vormt geen hostnaam Hallo voor Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="4b3a7-115">Elke **DnsServer** kenmerkwaarde uniek zijn binnen de gehele Microsoft Azure-abonnement Hallo</span><span class="sxs-lookup"><span data-stu-id="4b3a7-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="4b3a7-116">Virtueel netwerk Sites Element</span><span class="sxs-lookup"><span data-stu-id="4b3a7-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="4b3a7-117">In volgorde toospecify deze instelling voor Hallo virtuele netwerksites element, het eerder moet zijn gedefinieerd in Hallo DNS-element.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="4b3a7-118">Hallo DnsServerRef *naam* in Hallo virtuele netwerksites element tooa naam-waarde opgegeven in Hallo DNS-element voor DNS-server moet verwijzen *naam*.</span><span class="sxs-lookup"><span data-stu-id="4b3a7-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4b3a7-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b3a7-119">Next steps</span></span>
* <span data-ttu-id="4b3a7-120">Hallo begrijpen [Azure Virtual Network-configuratieschema](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="4b3a7-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="4b3a7-121">Hallo begrijpen [Azure Service configuratieschema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="4b3a7-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="4b3a7-122">[Configureren van een virtueel netwerk met behulp van de configuratiebestanden netwerk](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="4b3a7-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

