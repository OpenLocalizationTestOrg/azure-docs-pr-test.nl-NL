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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>DNS-instellingen opgeven in een configuratiebestand voor het virtuele netwerk
Een configuratiebestand netwerk bestaat uit twee elementen waarmee u instellingen voor toospecify Domain Name System (DNS kunt): **DnsServers** en **DnsServerRef**. U kunt een lijst met DNS-servers toevoegen door te geven van de IP-adressen en namen toohello verwijzen naar **DnsServers** element. U kunt een **DnsServerRef** element toospecify welke DNS-serveringangen uit Hallo DnsServers element worden gebruikt voor andere netwerksites binnen het virtuele netwerk.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

In dit artikel bevat informatie over Hallo klassieke implementatiemodel.

Hallo netwerk configuratiebestand kan Hallo volgende elementen bevatten. Hallo titel van elk element is gekoppelde tooa pagina met aanvullende informatie over Hallo element waarde-instellingen.

> [!IMPORTANT]
> Zie voor meer informatie over hoe tooconfigure netwerk configuratiebestand Hallo [configureren van een virtueel netwerk via een netwerk-configuratiebestand](virtual-networks-using-network-configuration-file.md). Zie voor meer informatie over elk element in het configuratiebestand voor Hallo netwerk [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[DNS-Element](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Hallo **naam** kenmerk in Hallo **DnsServer** element alleen als een verwijzing wordt gebruikt voor Hallo **DnsServerRef** element. Dit vormt geen hostnaam Hallo voor Hallo DNS-server. Elke **DnsServer** kenmerkwaarde uniek zijn binnen de gehele Microsoft Azure-abonnement Hallo
> 
> 

[Virtueel netwerk Sites Element](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> In volgorde toospecify deze instelling voor Hallo virtuele netwerksites element, het eerder moet zijn gedefinieerd in Hallo DNS-element. Hallo DnsServerRef *naam* in Hallo virtuele netwerksites element tooa naam-waarde opgegeven in Hallo DNS-element voor DNS-server moet verwijzen *naam*.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Hallo begrijpen [Azure Virtual Network-configuratieschema](http://go.microsoft.com/fwlink/?LinkId=248093).
* Hallo begrijpen [Azure Service configuratieschema](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Configureren van een virtueel netwerk met behulp van de configuratiebestanden netwerk](virtual-networks-using-network-configuration-file.md).

