---
title: aaaManage DNS-record sets en records met Azure DNS | Microsoft Docs
description: Azure DNS biedt Hallo mogelijkheid toomanage DNS-record wordt ingesteld en registreert bij het hosten van uw domein.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a>DNS-records en recordsets beheren met behulp van hello Azure-portal

> [!div class="op_single_selector"]
> * [Azure Portal](dns-operations-recordsets-portal.md)
> * [Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-recordsets-cli.md)
> * [PowerShell](dns-operations-recordsets.md)

Dit artikel laat zien hoe Hallo toomanage recordsets en records voor uw DNS-zone met behulp van Azure-portal.

Het is belangrijk toounderstand Hallo verschil tussen de DNS-recordsets en afzonderlijke DNS-records. Een recordset is een verzameling van records in een zone die Hallo dezelfde naam en zijn Hallo hetzelfde type hebben. Zie voor meer informatie [maken DNS-recordsets en records met behulp van Azure-portal Hallo](dns-getstarted-create-recordset-portal.md).

## <a name="create-a-new-record-set-and-record"></a>Een nieuwe recordset en record maken

een record in hello Azure-portal toocreate Zie [maken DNS-records met behulp van Azure-portal Hallo](dns-getstarted-create-recordset-portal.md).

## <a name="view-a-record-set"></a>Een recordset weergeven

1. Ga in de Azure-portal hello, toohello **DNS-zone** blade.
2. Hallo-Recordset zoekt en selecteert u deze. Hiermee opent u de eigenschappen van Hallo Recordset.

    ![Zoeken naar een Recordset](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a>Voeg een nieuwe record tooa-Recordset

U kunt toevoegen, too20 records tooany Recordset. Een recordset mag niet twee identieke records. Lege recordsets (met nul records) kunnen worden gemaakt, maar worden niet weergegeven op Hallo Azure DNS-naamservers. Recordsets van het type CNAME kunnen maximaal één record bevatten.

1. Op Hallo **eigenschappen van de recordset** blade voor uw DNS-zone, klikt u op Hallo-record dat u tooadd een record wilt ingesteld.

    ![Selecteer een Recordset](./media/dns-operations-recordsets-portal/selectset500.png)

2. Geef Hallo Recordset eigenschappen Hallo velden.

    ![Een record toevoegen](./media/dns-operations-recordsets-portal/addrecord500.png)

3. Klik op **opslaan** op Hallo Hallo blade toosave bovenaan uw instellingen. Sluit de blade Hallo.
4. In de hoek hello ziet u dat Hallo-record wordt opgeslagen.

    ![Recordset opslaan](./media/dns-operations-recordsets-portal/saving150.png)

Nadat het Hallo-record is opgeslagen, waarden op Hallo Hallo **DNS-zone** blade Hallo nieuwe record wordt weergegeven.

## <a name="update-a-record"></a>Een record bijwerken

Hallo-velden die u kunt bijwerken wanneer u een record in een bestaande recordset bijwerkt, zijn afhankelijk van Hallo type record waarmee u werkt.

1. Op Hallo **eigenschappen van de recordset** blade voor uw recordset en zoeken naar Hallo record.
2. Hallo record wijzigen. Wanneer u een record wijzigt, kunt u de beschikbare instellingen voor de record Hallo Hallo kunt wijzigen. Hallo in Hallo voorbeeld te volgen, **IP-adres** veld is geselecteerd en Hallo IP-adres wordt Hallo proces wordt gewijzigd.

    ![Een record wijzigen](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. Klik op **opslaan** op Hallo Hallo blade toosave bovenaan uw instellingen. In de rechterbovenhoek Hallo ziet u Hallo melding dat Hallo-record is opgeslagen.

    ![Recordset opgeslagen](./media/dns-operations-recordsets-portal/saved150.png)

Nadat het Hallo-record is opgeslagen, Hallo waarden voor Hallo record moet worden ingesteld op Hallo **DNS-zone** blade Hallo bijgewerkt record bevatten.

## <a name="remove-a-record-from-a-record-set"></a>Een record verwijderen uit een Recordset

U kunt hello Azure portal tooremove records uit een recordset. Houd er rekening mee dat Hallo laatste record van een recordset niet Hallo Recordset verwijderen worden.

1. Op Hallo **eigenschappen van de recordset** blade voor uw recordset en zoeken naar Hallo record.
2. Klik op Hallo-record dat u wilt dat tooremove. Selecteer vervolgens **verwijderen**.

    ![Een record verwijderen](./media/dns-operations-recordsets-portal/removerecord500.png)

3. Klik op **opslaan** op Hallo Hallo blade toosave bovenaan uw instellingen.
4. Nadat het Hallo-record is verwijderd, de waarden voor de record Hallo op Hallo Hallo **DNS-zone** blade nieuwe Hallo verwijderen.

## <a name="delete"></a>Een recordset verwijderen

1. Op Hallo **eigenschappen van de recordset** blade voor uw recordset en klikt u op **verwijderen**.

    ![Een recordset verwijderen](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. Er verschijnt een bericht waarin wordt gevraagd als u wilt dat toodelete Hallo-Recordset.
3. Controleer of Hallo naam komt overeen met Hallo record ingesteld dat u toodelete wilt en klik vervolgens op **Ja**.
4. Op Hallo **DNS-zone** blade controleren Hallo recordset is niet meer zichtbaar.

## <a name="work-with-ns-and-soa-records"></a>Werken met NS en SOA-records

NS en SOA-records die automatisch worden gemaakt, worden anders worden beheerd vanuit andere recordtypen.

### <a name="modify-soa-records"></a>SOA-records wijzigen

U kunt toevoegen of verwijderen van records uit Hallo automatisch gemaakt SOA-record is ingesteld in het toppunt Hallo zone (naam = ' @ '). Echter kunt u een van de parameters Hallo binnen Hallo SOA-record (met uitzondering van de "Host") en de TTL van de recordset Hallo.

### <a name="modify-ns-records-at-hello-zone-apex"></a>NS-records in het toppunt zone Hallo wijzigen

Hallo NS-recordset in het toppunt Hallo zone wordt automatisch gemaakt met elke DNS-zone. Het bevat Hallo-namen van hello Azure DNS-naam servers toegewezen toohello zone.

U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen. U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset. U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers.

Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt. Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gewijzigd zonder beperking.

### <a name="delete-soa-or-ns-record-sets"></a>SOA- of NS recordsets verwijderen

U kunt geen Hallo SOA- en NS-recordsets in het toppunt Hallo zone verwijderen (naam = ' @ ') die automatisch worden gemaakt wanneer het Hallo-zone wordt gemaakt. Ze worden automatisch verwijderd wanneer u Hallo zone verwijdert.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over Azure DNS Hallo [Azure DNS-overzicht](dns-overview.md).
* Zie voor meer informatie over het automatiseren van DNS [maken van DNS-zones en -recordsets met .NET SDK Hallo](dns-sdk.md).
* Zie voor meer informatie over de reverse DNS-records [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).
