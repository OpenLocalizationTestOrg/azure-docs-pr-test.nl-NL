---
title: Service Fabric image store verbinding tekenreeks aaaAzure | Microsoft Docs
description: Hallo image store-verbindingsreeks begrijpen
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Hallo ImageStoreConnectionString instelling begrijpen

In sommige documentatie vermeld we kort Hallo bestaan van een parameter 'ImageStoreConnectionString' zonder het met een beschrijving van wat het betekent. En na het doorlopen van een artikel zoals [implementeren en verwijderen van toepassingen via PowerShell][10], het lijkt erop dat u hoeft kopiëren en plakken Hallo waarde wordt weergegeven in clustermanifest Hallo van Hallo doel cluster. Hallo-instelling moet dus worden geconfigureerd per cluster, maar bij het maken van een cluster via Hallo [Azure-portal][11], er is geen optie tooconfigure deze instelling en dat deze wordt altijd "fabric: Installatiekopieopslag'. Wat is Hallo doel van deze instelling vervolgens?

![Clustermanifest][img_cm]

Service Fabric gestart uit als een platform voor intern Microsoft-verbruik door veel verschillende teams, zodat sommige aspecten van deze zeer aanpasbare zijn-Hallo 'Image Store' een dergelijke aspect is. Hallo Image Store is in wezen een pluggable opslagplaats voor het opslaan van toepassingspakketten. Wanneer uw toepassing geïmplementeerde tooa knooppunt in Hallo-cluster is, wordt in dat knooppunt Hallo inhoud van het toepassingspakket downloadt van Hallo Image Store. Hallo ImageStoreConnectionString is een instelling van alle benodigde gegevens van de Hallo voor zowel de clients en de knooppunten toofind Hallo juiste Image Store voor een bepaald cluster.

Er zijn momenteel drie mogelijke soorten Image Store-providers en hun bijbehorende verbindingsreeksen zijn als volgt:

1. Image Store-Service: "fabric: Installatiekopieopslag'

2. Bestandssysteem: "file:[file system path]"

3. Azure Storage: ' xstore:DefaultEndpointsProtocol = https; AccountName = [...]; AccountKey = [...]; Container = [...] "

Hallo-providertype gebruikt in productie is Hallo Image Store-Service een stateful persistente systeemservice die u in Service Fabric Explorer kunt zien. 

![Image Store-Service][img_is]

Hosting Hallo Image Store in een systeemservice binnen Hallo cluster zelf wordt voorkomen dat externe afhankelijkheden voor Hallo pakket opslagplaats en geeft ons meer controle over Hallo plaats van opslag. Toekomstige verbeteringen rond Hallo Image Store zijn waarschijnlijk tootarget Hallo Image Store-provider eerst als dat niet exclusief. Hallo-verbindingsreeks voor Hallo Image Store-Service provider geen unieke informatie omdat Hallo-client al verbonden toohello doelcluster is. Hallo-client moet alleen tooknow dat protocollen die gericht is op Hallo system-service moeten worden gebruikt.

Hallo File System provider wordt gebruikt in plaats van Hallo Image Store-Service voor lokale 1-box-clusters tijdens ontwikkelcluster toobootstrap Hallo iets sneller. Hallo verschil is normaal gesproken een kleine, maar het is een nuttig optimalisatie voor de meeste mensen tijdens de ontwikkeling. De mogelijke toodeploy een lokale 1-box-cluster met Hallo andere providertypen opslag, maar meestal is er geen reden toodo dus omdat Hallo ontwikkelen en testen werkstroom blijft Hallo dezelfde ongeacht de provider. Dan dit gebruik bestaan Hallo bestandssysteem en Azure Storage providers alleen voor ondersteuning.

Dus Hallo ImageStoreConnectionString is geconfigureerd, wordt meestal NET gebruikt Hallo standaardinstelling. Bij het publiceren van tooAzure via [Visual Studio][12], Hallo-parameter is automatisch voor u ingesteld dienovereenkomstig. Hallo-verbindingsreeks is voor programmatische implementatie tooclusters gehost in Azure, altijd 'fabric: Installatiekopieopslag'. Hoewel bij twijfel kan de waarde altijd worden gecontroleerd door bij het ophalen van het clustermanifest Hallo door [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), of [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Zowel on-premises test en productieclusters moet altijd geconfigureerde toouse Hallo Image Store-Service provider ook.

### <a name="next-steps"></a>Volgende stappen
[Implementeren en verwijderen van toepassingen met behulp van PowerShell][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
