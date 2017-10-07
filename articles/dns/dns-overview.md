---
title: aaaOverview van Azure DNS | Microsoft Docs
description: Overzicht van DNS-hosting-service op Microsoft Azure. Host uw domein in Microsoft Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Azure DNS-overzicht

Hallo Domain Name System en DNS, is verantwoordelijk voor het omzetten van (of het oplossen van) een website of service name tooits IP-adres. Azure DNS is een hosting service voor DNS-domeinen omzetten van namen met behulp van Microsoft Azure-infrastructuur. U kunt uw DNS beheren door het hosten van uw Azure-domeinen records met dezelfde referenties, API's, hulpprogramma's en facturering Hallo als uw andere Azure-services.

![DNS-overzicht](./media/dns-overview/scenario.png)

## <a name="features"></a>Functies

* **Betrouwbaarheid en prestaties** -DNS-domeinen in Azure DNS worden gehost op Azure wereldwijd netwerk van DNS-naamservers. We gebruiken Anycast networking zodat elke DNS-query wordt beantwoord door Hallo dichtstbijzijnde beschikbare DNS-server. Dit biedt zowel snelle prestaties en hoge beschikbaarheid voor uw domein.

* **Naadloze integratie** -hello Azure DNS-service kan gebruikte toomanage DNS-records voor uw Azure-services en gebruikte tooprovide DNS voor uw externe resources ook kan worden. Azure DNS is geïntegreerd in hello Azure-portal en maakt gebruik van dezelfde referenties, facturering en support-contract Hallo als uw andere Azure-services.

* **Beveiliging** -hello Azure DNS-service is gebaseerd op Azure Resource Manager. Als zodanig voordelen van Resource Manager-functies zoals rollen gebaseerd toegangsbeheer controlelogboeken en resource vergrendelen. Uw domeinen en records kunnen worden beheerd via hello Azure-portal, Azure PowerShell-cmdlets en Hallo platformoverschrijdende Azure CLI. Toepassingen waarbij automatisch DNS-beheer kunnen integreren met de service via Hallo Hallo REST-API en SDK's.

Azure DNS ondersteunt momenteel geen kopen van domeinnamen. Als u wilt dat toopurchase domeinen, moet u toouse een domeinnaamregistrar van derden. Hallo registrar brengt doorgaans een kleine jaarlijkse rekening. Hallo-domeinen kunnen vervolgens worden gehost in Azure DNS voor het beheer van DNS-records. Zie [delegeren van een domein tooAzure DNS-](dns-domain-delegation.md) voor meer informatie.

## <a name="pricing"></a>Prijzen

DNS-facturering is gebaseerd op Hallo aantal DNS-zones die worden gehost in Azure en door Hallo aantal DNS-query's. meer informatie over prijzen bezoek toolearn [prijzen van Azure DNS-](https://azure.microsoft.com/pricing/details/dns/).

## <a name="faq"></a>Veelgestelde vragen

Zie voor veelgestelde vragen over Azure DNS Hallo [DNS-Veelgestelde vragen over Azure](dns-faq.md).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over DNS-zones en records in via: [DNS-zones en registreert overzicht](dns-zones-records.md).

Meer informatie over hoe te[maken van een DNS-zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.

Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure.

