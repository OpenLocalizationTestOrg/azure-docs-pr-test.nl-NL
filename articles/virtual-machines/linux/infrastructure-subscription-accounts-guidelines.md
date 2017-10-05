---
title: Abonnement en -account voor virtuele Linux-machines in Azure | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor abonnementen en accounts in Azure.
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
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Azure-abonnement en accounts richtlijnen voor virtuele Linux-machines

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht benadering van beheer van abonnement en -account als uw omgeving en gebruikersgroep uitbreiden.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Richtlijnen voor de implementatie voor abonnementen en accounts
Beslissingen te nemen:

* Welke set van abonnementen en accounts komen u moet voor het hosten van uw IT-werkbelasting of infrastructuur?
* Hoe u omlaag in de hiërarchie aanpassen aan uw organisatie?

Taken:

* Definieer uw organisatiehiërarchie logische als u wilt beheren van een abonnement.
* Definiëren zodat deze overeenkomt met deze logische hiërarchie, de vereiste accounts en -abonnementen onder elke account.
* Maak de set-abonnementen en accounts met behulp van de naamconventie.

## <a name="subscriptions-and-accounts"></a>Abonnementen en accounts
Om te werken met Azure, moet u een of meer Azure-abonnementen. Resources, zoals virtuele machines (VM's) of virtuele netwerken bestaat in deze abonnementen.

* Enterprise-klanten hebben doorgaans een Enterprise-inschrijving, waardoor de bovenste-bron in de hiërarchie en is gekoppeld aan een of meer accounts.
* De bovenste resource is voor consumenten en klanten zonder een Enterprise-inschrijving, het account.
* Abonnementen worden gekoppeld aan accounts en kan er een of meer abonnementen per account. Azure records factureringsgegevens op het abonnementsniveau.

Vanwege de limiet van twee niveaus voor de relatie Account /-abonnement is het belangrijk dat de naamgevingsconventie van accounts en -abonnementen op de facturering behoeften uitlijnen. Bijvoorbeeld, als een globale bedrijf gebruikmaakt van Azure, kunnen ze ervoor kiezen om één account per regio en abonnementen beheerd hebben op het regioniveau:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Gebruik bijvoorbeeld de volgende structuur:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Als een regio wil hebben van meer dan één abonnement die is gekoppeld aan een bepaalde groep, moet een manier voor het coderen van de extra gegevens op het account of naam van het abonnement gebruikmaken van de naamconventie. Deze organisatie kan massaging factureringsgegevens om te genereren van de nieuwe niveaus van hiërarchie tijdens facturering rapporten:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

De organisatie kan eruitzien als in het volgende voorbeeld:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

We bieden gedetailleerde facturering via een downloadbaar bestand voor één account of voor alle accounts in een enterprise agreement.

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

