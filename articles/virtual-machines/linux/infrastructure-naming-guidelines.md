---
title: aaaAzure infrastructuur naamgevingsregels - Linux | Microsoft Docs
description: Meer informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor de naamgeving in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Azure-infrastructuur naamgevingsregels voor virtuele Linux-machines 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht in hoe tooapproach naamconventies voor uw verschillende Azure-resources toobuild een logische en gemakkelijk kan worden geïdentificeerd instellen van resources in uw hele omgeving.

## <a name="implementation-guidelines-for-naming-conventions"></a>Implementatie van richtlijnen voor naamgevingsregels
Beslissingen te nemen:

* Wat zijn uw naamgevingsregels voor Azure-resources?

Taken:

* Hallo-en achtervoegsel toouse tussen de consistentie van uw resources toomaintain definiëren.
* Definieer opslagaccount namen Hallo vereiste voor deze toobe globaal uniek zijn.
* Document Hallo naming convention toobe gebruikt en tooall partijen betrokken tooensure consistentie verdelen over implementaties.

## <a name="naming-conventions"></a>Naamgevingsregels
U moet beschikken over een goede naamgevingsconventie voordat u verder niets te maken in Azure. Een naamgevingsconventie zorgt ervoor dat alle Hallo resources een voorspelbare naam, waarmee de administratieve last van lagere Hallo die zijn gekoppeld aan deze resources beheren.

U kunt een specifieke set domeinnaamconventies die zijn gedefinieerd voor de hele organisatie of voor een specifieke Azure-abonnement of account toofollow. Hoewel het eenvoudig voor personen binnen organisaties tooestablish impliciete regels bij het werken met Azure-resources, moet u kunnen tooscale toobe voor teams die samenwerken in Azure.

Een reeks vooraf naamconventies overeenkomen. Er zijn enkele overwegingen met betrekking tot de naamconventies die meerdere waarmee wordt ingesteld van regels.

## <a name="affixes"></a>Brengt
Als u een naamgevingsconventie toodefine kijkt, is een beslissing of Hallo voorvoegsel is op:

* Hallo-naam (voorvoegsel) Hallo begint
* Hallo-einde van Hallo-naam (achtervoegsel)

Hier worden bijvoorbeeld twee verschillende namen voor een resourcegroep met Hallo `rg` brengt:

* Rg-WebApp (voorvoegsel)
* WebApp-Rg (achtervoegsel)

Achtervoegsel kunnen toodifferent aspecten die bepaalde resources Hallo Beschrijf verwijzen. Hallo ziet volgende tabel u enkele voorbeelden doorgaans worden gebruikt.

| Aspect | Voorbeelden | Opmerkingen |
|:--- |:--- |:--- |
| Omgeving |de prod-dev-, stg, |Afhankelijk van het Hallo-doel en de naam van elke omgeving. |
| Locatie |usw (VS-West), gebruiken (VS-Oost 2) |Afhankelijk van de regio Hallo Hallo datacenter of Hallo regio van Hallo-organisatie. |
| Azure onderdeel, service of product |Rg voor de resourcegroep VNet voor het virtuele netwerk |Afhankelijk van het Hallo-product voor welke Hallo-bron biedt ondersteuning voor. |
| Rol |DB, app, web |Afhankelijk van de rol Hallo van Hallo virtuele machine. |
| Exemplaar |01, 02, 03, enzovoort. |Voor bronnen die u meer dan één exemplaar hebt. Bijvoorbeeld, taakverdeling webservers in een cloudservice. |

Bij het maken van uw naamconventies, zorg ervoor dat ze duidelijk vermeld die brengt toouse voor elk type resource en in welke volgorde (voorvoegsel tegenover achtervoegsel).

## <a name="dates"></a>datums
Vaak is het belangrijk toodetermine Hallo datum van het maken van Hallo-naam van een bron. Het wordt aangeraden de Hallo JJJJMMDD datumnotatie. Het voordeel hiervan is niet alleen Hallo volledige datum geregistreerd, maar ook twee resources waarvan de namen verschillen op Hallo datum alfabetisch en in chronologische volgorde worden gesorteerd.

## <a name="naming-resources"></a>Naamgeving van resources
Elk type resource definiëren in Hallo naamgevingsconventie die moet hebben regels die bepalen hoe tooassign tooeach resource namen die is gemaakt. Deze regels gelden tooall typen resources, bijvoorbeeld:

* Abonnementen
* Accounts
* Opslagaccounts
* Virtuele netwerken
* Subnetten
* Beschikbaarheidssets
* Resourcegroepen
* Virtuele machines
* Eindpunten
* Netwerkbeveiligingsgroepen
* Rollen

tooensure die naam Hallo biedt voldoende informatie toodetermine toowhich resource verwijst, moet u beschrijvende namen.

## <a name="computer-names"></a>Computernamen
Wanneer u een virtuele machine (VM) maakt, wordt in Azure een VM-naam van up too64 tekens dat wordt gebruikt voor de resourcenaam Hallo vereist. Maakt gebruik van Azure Hallo dezelfde naam voor het Hallo-besturingssysteem is geïnstalleerd in Hallo VM. Echter, deze namen mogelijk niet altijd worden Hallo dezelfde.

Als een virtuele machine wordt gemaakt van een VHD-afbeeldingsbestand dat al een besturingssysteem bevat, Hallo de naam van de virtuele machine in Azure, kan afwijken van Hallo computernaam van de virtuele machine-besturingssysteem. Deze situatie kan een zekere mate van moeite tooVM management, dus u niet kunt beter kunt toevoegen. Wijs hello Azure VM resource Hallo dezelfde naam als de naam van de computer Hallo toohello besturingssysteem van die virtuele machine toe te wijzen.

U wordt aangeraden deze hello Azure VM-naam is hetzelfde als het onderliggende besturingssysteem computernaam Hallo Hallo.

## <a name="storage-account-names"></a>Namen van opslagaccounts
Deze sectie geldt niet te[Azure beheerd schijven](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), omdat u geen afzonderlijke storage-account maken. Storage-accounts hebben voor niet-beheerde schijven speciale regels die zijn voor hun namen. U kunt alleen kleine letters en cijfers. Zie voor meer informatie [een opslagaccount maken](../../storage/storage-create-storage-account.md#create-a-storage-account). Daarnaast moet Hallo opslagaccountnaam, met core.windows.net, een globaal geldig, unieke DNS-naam. Bijvoorbeeld, als Hallo storage-account mystorageaccount aangeroepen wordt, moeten hello volgende resulterende DNS-namen uniek zijn:

* mystorageaccount.BLOB.Core.Windows.NET
* mystorageaccount.Table.Core.Windows.NET
* mystorageaccount.Queue.Core.Windows.NET

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

