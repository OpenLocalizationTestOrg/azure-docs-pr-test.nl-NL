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
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>DNS-instellingen in een serviceconfiguratiebestand opgeven
## <a name="dns-elements"></a>DNS-elementen
Een service-configuratiebestand mag bevatten een DnsServers-element met een lijst met IPv4-adressen voor Hallo Domain Name System (DNS)-servers die Hallo-service wordt gebruikt. Instellingen in het serviceconfiguratiebestand hello, hebben voorrang boven de instellingen in het configuratiebestand Hallo-netwerk. Zie voor meer informatie [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**NetworkConfiguration-element**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Hallo **naam** kenmerk in Hallo **DnsServer** element alleen als een verwijzingsnaam wordt gebruikt. Dit vormt geen hostnaam Hallo voor Hallo DNS-server. Elke **DnsServer** kenmerkwaarde uniek zijn binnen de gehele Microsoft Azure-abonnement Hallo.
> 
> 

## <a name="see-also"></a>Zie ook
[Het configuratieschema Azure-Service (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Azure Virtual Network-configuratieschema](http://go.microsoft.com/fwlink/?LinkId=248093)

[Een virtueel netwerk met behulp van de configuratiebestanden netwerk configureren](http://go.microsoft.com/fwlink/?LinkId=248094)

[Over Virtual Network-instellingen in het Hallo-beheerportal](http://go.microsoft.com/fwlink/?LinkId=248092)

