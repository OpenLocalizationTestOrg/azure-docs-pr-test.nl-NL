---
title: problemen met de beschikbaarheid aaaApplication en de service voor veelgestelde vragen over Microsoft Azure Cloud Services | Microsoft Docs
description: Dit artikel worden Hallo Veelgestelde vragen over de toepassing en servicebeschikbaarheid voor Microsoft Azure Cloud Services.
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Toepassings- en problemen met de servicebeschikbaarheid voor Azure Cloud Services: veelgestelde vragen (FAQ's)

Dit artikel bevat veelgestelde vragen over de toepassing en problemen met de servicebeschikbaarheid voor [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). U kunt ook contact opnemen met Hallo [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>Mijn rol is gerecycled. Is er een update voor mijn cloudservice uitgerold?
Min of meer versies maand, Microsoft een nieuwe versie van de Gast OS voor PaaS VM's van Windows Azure. Het Gastbesturingssysteem is slechts één update in Hallo pijplijn. Een release kan worden beïnvloed door veel andere factoren. Bovendien Azure wordt uitgevoerd op honderden of duizenden computers. Daarom is het onmogelijk toopredict Hallo exacte datum en tijd waarop de rollen opnieuw wordt opgestart. We Hallo Gast OS bijwerken van RSS-Feed bijwerken met Hallo meest recente informatie die we hebben, maar u moet rekening houden met die tijd toobe geschatte waarde gerapporteerd. We zijn dit is problematisch voor klanten en werkt aan een plan toolimit of nauwkeurig keer opnieuw wordt opgestart.

Zie voor meer informatie over recente updates voor gast OS [Azure Gast OS releases en SDK compatibiliteit matrix](cloud-services-guestos-update-matrix.md).

Zie voor nuttige informatie bij opnieuw opstarten en aanwijzers tootechnical details van updates voor gast en Host-OS Hallo MSDN blogbericht [rol exemplaar opnieuw wordt opgestart vanwege tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Waarom Hallo eerste aanvraag toomy cloudservice nadat het Hallo-service niet actief is geweest voor enige tijd duurt langer dan normaal?
Wanneer Hallo webserver de eerste aanvraag hello ontvangt, eerst gecompileerd Hallo code en vervolgens Hallo-aanvraag wordt verwerkt. Dat is waarom eerste aanvraag duurt langer dan Hallo Hallo anderen. Standaard opgehaald Hallo groep van toepassingen afgesloten in geval van een gebruiker inactiviteit. Hallo groep van toepassingen wordt ook recycle standaard elke 1,740 minuten (29 uur).

Internet Information Services (IIS)-toepassingen kunnen worden periodiek gerecycled tooavoid onstabiel statussen die tooapplication crashes, loopt vast of geheugenlekken leiden kunnen.

Hallo documenten te volgen helpt u begrijpen en dit probleem te verhelpen:
* [Trage initiële laden is hersteld voor IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [IIS 7.5 toepassing eerste webaanvraag na-toepassingen recyclen erg traag](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

Als u toochange Hallo standaardgedrag van IIS wilt, moet u toouse starten van de taken, omdat het als u handmatig wijzigingen toohello Webrol exemplaren toepast, Hallo wijzigingen uiteindelijk worden gewist.

Zie voor meer informatie [hoe tooconfigure en voer opstarten taken voor een cloudservice](cloud-services-startup-tasks.md).
