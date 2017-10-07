---
title: aaaManage DNS-zones in Azure DNS - Azure-portal | Microsoft Docs
description: U kunt DNS-zones met hello Azure-portal beheren. Dit artikel wordt beschreven hoe tooupdate, verwijderen en DNS-zones maken op Azure DNS
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a>Hoe toomanage DNS-Zones in hello Azure-portal

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Dit artikel laat zien hoe toomanage uw DNS-zones met behulp van hello Azure-portal. U kunt ook de DNS-zones met behulp van de platformoverschrijdende Hallo beheren [Azure CLI](dns-operations-dnszones-cli.md) of hello Azure [PowerShell](dns-operations-dnszones.md).

## <a name="create-a-dns-zone"></a>Een DNS-zone maken

1. Meld u aan toohello Azure-portal
2. Klik op Hallo Hub-menu en klik op **Nieuw > netwerken >** en klik vervolgens op **DNS-zone** tooopen Hallo maken DNS-zone blade.

    ![DNS-zone](./media/dns-operations-dnszones-portal/openzone650.png)

4. Op Hallo **maken DNS-zone** blade Voer Hallo volgende waarden en klik vervolgens op **maken**:


   | **Instelling** | **Waarde** | **Details** |
   |---|---|---|
   |**Naam**|contoso.com|Hallo-naam van Hallo DNS-zone|
   |**Abonnement**|[Uw abonnement]|Selecteer een abonnement toocreate Hallo DNS-zone in.|
   |**Resourcegroep**|**Nieuwe maken:** contosoDNSRG|Maak een resourcegroep. de naam van resourcegroep Hallo moet uniek zijn binnen het Hallo-abonnement die u hebt geselecteerd. meer informatie over resourcegroepen lezen Hallo toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overzichtsartikel.|
   |**Locatie**|VS - west||

> [!NOTE]
> Hallo resourcegroep toohello locatie van resourcegroep Hallo verwijst, en heeft geen invloed op Hallo DNS-zone. Hallo DNS-zone locatie is altijd 'global' en niet wordt weergegeven.

## <a name="list-dns-zones"></a>Lijst met DNS-zones

In Azure-portal Hallo, te navigeren**meer services** > **Networking** > **DNS-zones**. Elke DNS-zone, is het eigen resource, zoals het aantal recordsets en naamservers kunnen worden bekeken in deze weergave. Hallo kolom **NAAMSERVERS** is niet in de standaardweergave hello, tooadd Klik **kolommen**, selecteer **naamservers** en klik op **gedaan**.

![aanbieding DNS-zones](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a>Een DNS-zone verwijderen

Navigeer tooa DNS-zone in het Hallo-portal. Op Hallo **DNS-zone** blade, klikt u op **zone verwijderen**. U bent na vragen aan gebruiker tooconfirm u toodelete Hallo DNS-zone zijn productiviteitsniveau. Een DNS-zone verwijderen, verwijdert tevens alle Hallo-records die zijn opgenomen in het Hallo-zone.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toowork met uw DNS-Zone en records in via [aan de slag met Azure DNS hello Azure-portal met](dns-getstarted-portal.md).
