---
title: aaaLearn over opties voor ondersteuning van Azure Service Fabric | Microsoft Docs
description: Azure Service Fabric-cluster-versies ondersteund en koppelingen toofile ondersteuningstickets
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Opties voor Azure Service Fabric-ondersteuning

toodeliver hello juiste ondersteuning voor uw Service Fabric-clusters dat u uw werk toepassing worden uitgevoerd op laadt, we hebben ingesteld om verschillende opties voor u. Afhankelijk van Hallo niveau van ondersteuning nodig en Hallo ernst van Hallo-probleem, u toopick juiste Hallo-opties. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Productie of problemen met live site rapporteren of vraag ondersteuning voor Azure

Open een serviceticket voor professionele ondersteuning voor het melden van problemen met live-site op het Service Fabric-cluster dat is geïmplementeerd in Azure, [in Azure portal](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) of [Microsoft support-portal](http://support.microsoft.com/oas/default.aspx?prid=16146).

Meer informatie over:
 
- [Professional-ondersteuning van Microsoft voor Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Microsoft premier support](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Productie of problemen met live site rapporteren of vraag ondersteuning voor betaalde voor zelfstandige die service Fabric-clusters

Voor lokale reporting problemen live-site op het Service Fabric-cluster worden geïmplementeerd, of op andere clouds, opent u een ticket voor professionele ondersteuning op [Microsoft ondersteuning portal](http://support.microsoft.com/oas/default.aspx?prid=16146).

Meer informatie over:

- [Professional-ondersteuning van Microsoft voor on-premises](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Microsoft premier support](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Rapport Azure Service Fabric-problemen 
We hebben ingesteld om een GitHub-opslagplaats voor het melden van Service Fabric-problemen.  We zijn ook actief bewaking Hallo forums te volgen.

### <a name="github-repo"></a>GitHub-repo- 
Problemen met de Azure Service Fabric een rapport over [problemen van een Service Fabric git-opslagplaats](https://github.com/Azure/service-fabric-issues). Deze opslagplaats is bedoeld voor rapportage en tracering van problemen met Azure Service Fabric en voor het maken van kleine functieaanvragen. **Gebruik geen problemen met deze tooreport live-site**.

### <a name="stackoverflow-and-msdn-forums"></a>StackOverflow en MSDN-forums

Hallo [Service Fabric-code op StackOverflow] [ stackoverflow] en Hallo [Service Fabric-forum op MSDN] [ msdn-forum] worden gebruikt voor vragen over beste hoe Hallo platform werkt en hoe u bepaalde taken ermee kunt uitvoeren.

### <a name="azure-feedback-forum"></a>Forum met Feedback van Azure

Hallo [Forum met Feedback van Azure voor Service Fabric] [ uservoice-forum] Hallo beste plaats voor het indienen van grote functie ideeën die u hebt voor het product Hallo bekijken we de meest populaire aanvragen Hallo deel uitmaken van onze gemiddeld toolong-term planning. We raden u toorally ondersteuning voor uw suggesties binnen Hallo-community.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Ondersteunde versies van de Service Fabric.

Zorg ervoor dat het cluster een ondersteunde versie van Service Fabric altijd wordt uitgevoerd. Als en dat we Hallo-release van een nieuwe versie van Service Fabric aankondigen, is voor einde van de ondersteuningsperiode Hallo vorige versie gemarkeerd na een minimum van 60 dagen na die datum. Hallo nieuwe releases worden aangekondigd [op Hallo Service Fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric/).

Raadpleeg de volgende documenten voor meer informatie over het toohello tookeep uw een ondersteunde versie van Service Fabric-cluster.

- [Upgrade van Service Fabric-versie op een Azure-cluster](service-fabric-cluster-upgrade.md)
- [Upgrade van Service Fabric-versie op een zelfstandige windows server-cluster](service-fabric-cluster-upgrade-windows-server.md)
 
Hier volgen Hallo-lijst van Hallo Service Fabric-versies die worden ondersteund en de einddatum van de ondersteuning.

| **Service Fabric-runtime-cluster** | **Compatibel SDK / NuGet-pakket versies** | **Einde van ondersteuning datum** |
| --- | --- | --- |
| Alle cluster eerdere versies-too5.3.121 |Kleiner dan of gelijk zijn tooversion 2.3 |20 januari 2017 |
| 5.3.* |Kleiner dan of gelijk zijn tooversion 2.3 |24 februari 2017 |
| 5.4.* |Kleiner dan of gelijk zijn tooversion 2.4 |Kan 10,2017     |
| 5.5.* |Kleiner dan of gelijk zijn tooversion 2,5 |Augustus 10,2017    |
| 5.6.* |Kleiner dan of gelijk zijn tooversion 2.6 |Oktober 13,2017    |
| 5.7.* |Kleiner dan of gelijk zijn tooversion 2.7 |Huidige versie en dus geen einddatum

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Service Fabric-Preview versies - wordt niet ondersteund voor gebruik in productieomgevingen.
Van tijd tootime brengen we versies die we feedback willen, belangrijke functies die worden uitgebracht als voorbeelden hebben. Deze preview-versies mag alleen worden gebruikt voor testdoeleinden. Uw productiecluster moet altijd een ondersteunde, stabiele, Service Fabric-versie worden uitgevoerd. Een preview-versie begint altijd met een primaire en secundaire versienummer van 255. Als u een Service Fabric versie 255.255.5703.949 ziet, is deze releaseversie bijvoorbeeld alleen toobe gebruikt in testclusters en is Preview-versie. Deze preview-versies worden ook vermeld in Hallo [Service Fabric-teamblog](https://blogs.msdn.microsoft.com/azureservicefabric) en details hebt op Hallo van functies.

Er is geen ondersteuningsoptie betaalde voor deze preview-versies. Gebruik een van Hallo-opties die worden vermeld onder [rapport Azure Service Fabric problemen](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) tooask vragen of feedback geven.

## <a name="next-steps"></a>Volgende stappen

- [Upgrade van service fabric-versie op een Azure-cluster](service-fabric-cluster-upgrade.md)
- [Upgrade van Service Fabric-versie op een zelfstandige windows server-cluster](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
