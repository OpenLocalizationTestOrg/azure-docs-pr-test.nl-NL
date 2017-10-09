---
title: aaaGet de slag met Azure DNS met hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate een DNS-zone en een record in Azure DNS. Dit is een stapsgewijze handleiding toocreate en beheren van uw eerste DNS-zone en een record met behulp van hello Azure-portal.
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 5cea01d840d794001cccac64defed8b329d948db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-hello-azure-portal"></a>Aan de slag met Azure DNS met hello Azure-portal

> [!div class="op_single_selector"]
> * [Azure Portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Dit artikel begeleidt u bij Hallo stappen toocreate, uw eerste DNS-zone en een record met behulp van hello Azure-portal. U kunt ook u deze stappen uitvoert met Azure PowerShell of Hallo platformoverschrijdende Azure CLI.

Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein. toostart die als host fungeert voor uw domein in Azure DNS, moet u een DNS-zone toocreate voor die domeinnaam. Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone. Ten slotte toopublish uw DNS-zone-toohello Internet, moet u tooconfigure Hallo-naamservers voor Hallo-domein. Elk van deze stappen wordt beschreven in Hallo stappen te volgen.

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

1. Meld u aan toohello Azure-portal
2. Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.

    ![DNS-zone](./media/dns-getstarted-portal/openzone650.png)

4. Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:


   | **Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|contoso.com|Hallo-naam van Hallo DNS-zone|
   |**Abonnement**|[Uw abonnement]|Selecteer een abonnement toocreate Hallo DNS-zone in.|
   |**Resourcegroep**|**Nieuwe maken:** contosoDNSRG|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.|
   |**Locatie**|VS - west||

> [!NOTE]
> Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone. Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.

## <a name="create-a-dns-record"></a>Een DNS-record maken

Hallo wordt volgende voorbeeld u begeleid Hallo-proces voor het maken van nieuwe "A" record. Zie voor andere typen records en records van bestaande toomodify [beheren DNS-records en recordsets met behulp van Azure-portal Hallo](dns-operations-recordsets-portal.md). 

1. Hello DNS-Zone is gemaakt in Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **contoso.com** DNS-zone in het Hallo-blade van alle resources. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **contoso.com** in Hallo **filteren op naam...** vak tooeasily toegang Hallo DNS-Zone.

1. Hallo boven aan het Hallo **DNS-zone** blade Selecteer **+ Recordset** tooopen hello **recordset toevoegen** blade.

1. Op Hallo **recordset toevoegen** blade Hallo na waarden invoeren en op **OK**. In dit voorbeeld maakt u een A-record.

   |**Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|www|Naam van de record Hallo|
   |**Type**|A| Type van de DNS-record toocreate, acceptabele waarden zijn A, AAAA, CNAME, MX, NS, SRV, TXT en PTR.  Voor meer informatie over recordtypen gaat u naar [Overview of DNS zones and records](dns-zones-records.md) (Overzicht van DNS-zones en -records)|
   |**TTL**|1|Time-to-live van Hallo DNS-aanvraag.|
   |**TTL-eenheid**|Uren|Maateenheid van de TTL-waarde.|
   |**IP-adres**|ipAddressValue| Deze waarde is Hallo IP-adres dat Hallo DNS-record wordt omgezet.|

## <a name="view-records"></a>Records weergeven

In het onderste gedeelte van Hallo DNS-zone blade Hallo ziet u Hallo-records voor Hallo DNS-zone. U ziet Hallo standaard DNS- en SOA-records, die in elke zone worden gemaakt, plus eventuele nieuwe records die u hebt gemaakt.

![zone](./media/dns-getstarted-portal/viewzone500.png)


## <a name="update-name-servers"></a>Naamservers bijwerken

Wanneer u zich ervan overtuigd dat uw DNS-zone en records hebben is ingesteld, moet u tooconfigure uw domeinnaam toouse hello Azure DNS-naamservers. Hierdoor kunnen andere gebruikers op Hallo Internet toofind de DNS-records.

Hallo-naamservers voor uw zone worden gegeven in hello Azure-portal:

![zone](./media/dns-getstarted-portal/viewzonens500.png)

Deze naamservers moeten worden geconfigureerd met Hallo domeinnaamregistrar (waarbij u hebt aangeschaft Hallo-domeinnaam). Uw registrar biedt Hallo optie tooset up Hallo naamservers voor Hallo-domein. Zie voor meer informatie [delegeren van uw domein tooAzure DNS-](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Alle resources verwijderen

toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stappen te volgen:

1. In de Azure-portal Hallo **Favorieten** deelvenster, klikt u op **alle resources**. Klik op Hallo **MyResourceGroup** resourcegroep in Hallo alle resources blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u **MyResourceGroup** in Hallo **filteren op naam...** vak tooeasily toegang Hallo resourcegroep.
1. In Hallo **MyResourceGroup** blade, klikt u op Hallo **verwijderen** knop.
1. Hallo portal, moet u tootype Hallo-naam van Hallo resource groep tooconfirm dat u wilt dat toodelete deze. Klik op **verwijderen**, Type *MyResourceGroup* hello Resourcegroepnaam, vervolgens klikt u op **verwijderen**. Een resourcegroep verwijdert, worden alle bronnen binnen de resourcegroep hello, dus altijd zeker tooconfirm Hallo inhoud van een resourcegroep voordat u het verwijdert. Hallo portal Hiermee verwijdert u alle resources binnen de resourcegroep Hallo vervolgens Hallo resourcegroep zelf verwijdert. Dit proces duurt enkele minuten.


## <a name="next-steps"></a>Volgende stappen

Zie toolearn meer informatie over Azure DNS [Azure DNS-overzicht](dns-overview.md).

Zie toolearn meer informatie over het beheren van DNS-records in Azure DNS [beheren DNS-records en recordsets met behulp van Azure-portal Hallo](dns-operations-recordsets-portal.md).

