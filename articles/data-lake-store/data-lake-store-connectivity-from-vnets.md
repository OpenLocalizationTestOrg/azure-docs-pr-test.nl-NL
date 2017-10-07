---
title: aaaConnect tooAzure Data Lake Store uit VNETs | Microsoft Docs
description: Verbinding maken met tooAzure Data Lake Store uit Azure VNETs
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Toegang tot Azure Data Lake Store van VM's binnen een Azure VNET
Azure Data Lake Store is een PaaS-service die wordt uitgevoerd op het openbare Internet IP-adressen. Een server die u kunt verbinding maken met het openbare Internet kunnen toohello doorgaans verbinding ook tooAzure Data Lake Store-eindpunten. Standaard alle VM's die in Azure VNETs toegang heeft tot Internet Hallo en daarmee toegang tot Azure Data Lake Store. Het is echter mogelijk tooconfigure virtuele machines in een VNET toonot toohello toegang tot Internet hebben. Voor deze VM's is toegang tot tooAzure Data Lake Store beperkt ook. Openbare toegang tot Internet blokkeren voor virtuele machines in Azure VNETs kan worden gedaan met behulp van een Hallo benadering te volgen.

* Door het configureren van Netwerkbeveiligingsgroep groepen (NSG)
* Door gebruiker gedefinieerde Routes (UDR) configureren
* Door het uitwisselen van routes via BGP (dynamische routering standaardprotocol) wanneer u ExpressRoute gebruikt dat blok toegang tot Internet toohello

In dit artikel leert u hoe tooenable toohello Azure Data Lake Store toegang van Azure VM's die zijn beperkt tooaccess resources met behulp van een van drie methoden Hallo die hierboven worden genoemd.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Connectiviteit tooAzure Data Lake Store van VM's met beperkte connectiviteit inschakelen
tooaccess Azure Data Lake opslaan van dergelijke virtuele machines, moet u ze configureren tooaccess Hallo IP-adres waar hello Azure Data Lake Store-account beschikbaar is. U kunt Hallo IP-adressen voor uw Data Lake Store-accounts identificeren door Hallo DNS-namen van uw accounts op te lossen (`<account>.azuredatalakestore.net`). Hiervoor kunt u hulpprogramma's zoals **nslookup**. Open een opdrachtprompt op de computer en Voer Hallo volgende opdracht uit.

    nslookup mydatastore.azuredatalakestore.net

Hallo uitvoer lijkt op Hallo volgende. Hallo waarde ten opzichte van **adres** eigenschap Hallo IP-adres is gekoppeld aan uw Data Lake Store-account is.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>Verbinding van VM's met behulp van de NSG beperkt inschakelen
Wanneer een NSG-regel wordt gebruikt tooblock toegang krijgen tot toohello Internet, kunt u een andere NSG waarmee toegang toohello Data Lake Store IP-adres maken. Meer informatie over het NSG-regels is beschikbaar op [wat is er een Netwerkbeveiligingsgroep?](../virtual-network/virtual-networks-nsg.md). Voor instructies over hoe toocreate nsg's zien [hoe toomanage nsg's met behulp van Azure-portal Hallo](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>Verbinding van VM's met behulp van UDR of ExpressRoute beperkt inschakelen
Wanneer routes, udr's of uitgewisseld BGP routes, zijn de gebruikte tooblock toegang toohello Internet, moet een speciale route toobe geconfigureerd zodat virtuele machines in deze subnetten toegang Data Lake Store-eindpunten tot hebben. Zie voor meer informatie [wat de gebruiker gedefinieerde Routes zijn?](../virtual-network/virtual-networks-udr-overview.md). Zie voor instructies over het maken van udr's [maken udr's in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>Verbinding van VM's met behulp van ExpressRoute beperkt inschakelen
Wanneer een ExpressRoute-circuit is geconfigureerd, kunnen Hallo lokale servers toegang tot Data Lake Store via openbare peering. Meer informatie over het configureren van ExpressRoute voor openbare peering is beschikbaar op [Veelgestelde vragen over ExpressRoute](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
* [De beveiliging van gegevens die zijn opgeslagen in Azure Data Lake Store](data-lake-store-security-overview.md)

