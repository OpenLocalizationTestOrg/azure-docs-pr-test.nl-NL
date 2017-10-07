---
title: aaaSubscription voor virtuele Linux-machines in Azure | Microsoft Docs
description: Informatie over Hallo belangrijke ontwerp- en implementatiestappen richtlijnen voor abonnementen en accounts in Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Azure-abonnement en accounts richtlijnen voor virtuele Linux-machines

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht in hoe tooapproach-abonnement en account beheer als uw omgeving en de gebruikersgroep groeit.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Richtlijnen voor de implementatie voor abonnementen en accounts
Beslissingen te nemen:

* Welke set van abonnementen en accounts moet u toohost infrastructuur of uw IT-werkbelasting?
* Hoe toobreak omlaag Hallo hiërarchie toofit uw organisatie?

Taken:

* Definieer uw organisatiehiërarchie logische als u graag toomanage op abonnementsniveau.
* toomatch deze logische hiërarchie definiëren Hallo-accounts die zijn vereist en abonnementen onder elke account.
* Hallo set abonnementen en accounts met behulp van de naamconventie maken.

## <a name="subscriptions-and-accounts"></a>Abonnementen en accounts
toowork met Azure, moet u een of meer Azure-abonnementen. Resources, zoals virtuele machines (VM's) of virtuele netwerken bestaat in deze abonnementen.

* Enterprise-klanten hebben doorgaans een Enterprise-inschrijving die Hallo bovenste-bron in Hallo hiërarchie en is gekoppeld tooone of meer accounts.
* Voor consumenten en klanten zonder een Enterprise-inschrijving is Hallo bovenste resource Hallo-account.
* Abonnementen worden gekoppeld tooaccounts en kan er een of meer abonnementen per account. Azure records factureringsgegevens op Hallo abonnementsniveau.

Vervaldatum toohello limiet van twee hiërarchieniveaus op Hallo Account /-abonnement relatie is het belangrijk tooalign Hallo naamgevingsconventie accounts en -abonnementen toohello die behoeften facturering. Bijvoorbeeld als een globale bedrijf gebruikmaakt van Azure, ze mogelijk toohave één account per regio kiezen en abonnementen hebt beheerd op Hallo van regioniveau:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Gebruik bijvoorbeeld Hallo structuur te volgen:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Als een regio toohave meer dan één abonnement gekoppeld tooa bepaalde groep beslist, een tooencode manier moet gebruikmaken van de naamconventie Hallo Hallo extra gegevens op Hallo-account of de naam van de Hallo-abonnement. Deze organisatie kunt facturering gegevens toogenerate Hallo nieuwe niveaus van hiërarchie massaging tijdens facturering rapporten:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

Hallo-organisatie kan eruitzien als Hallo voorbeeld te volgen:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

We bieden gedetailleerde facturering via een downloadbaar bestand voor één account of voor alle accounts in een enterprise agreement.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

