---
title: aaaConfigure beveiligen van Azure Service Fabric clusterverbindingen | Microsoft Docs
description: Meer informatie over hoe toouse Visual Studio tooconfigure verbindingen die worden ondersteund door hello Azure Service Fabric-cluster beveiligen.
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Configureren van beveiligde verbindingen tooa Service Fabric-cluster vanuit Visual Studio
Meer informatie over hoe toouse Visual Studio toosecurely toegang krijgen tot een Azure Service Fabric-cluster met beleid voor toegangsbeheer geconfigureerd.

## <a name="cluster-connection-types"></a>Cluster-verbindingstypen
Twee soorten verbindingen worden ondersteund door hello Azure Service Fabric-cluster: **niet-beveiligde** verbindingen en **x509 op basis van certificaten** beveiligde verbindingen. (Voor Service Fabric-clusters on-premises gehoste **Windows** en **dSTS** verificaties worden ook ondersteund.) U hebt tooconfigure Hallo clustertype verbinding wanneer het Hallo-cluster wordt gemaakt. Zodra deze gemaakt, kan het verbindingstype Hallo kan niet worden gewijzigd.

Hallo-hulpprogramma's voor Visual Studio Service Fabric ondersteuning voor alle authenticatietypen voor verbindende tooa cluster voor publicatie. Zie [instellen van een Service Fabric-cluster van hello Azure-portal](service-fabric-cluster-creation-via-portal.md) voor instructies over het tooset een beveiligde Service Fabric-cluster.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Clusterverbindingen configureren in profielen publiceren
Als u een Service Fabric-project vanuit Visual Studio publiceert, gebruikt u Hallo **Service Fabric-toepassing publiceren** dialoogvenster vak toochoose een Azure Service Fabric-cluster. Onder **verbindingseindpunt**, selecteer een bestaand cluster in uw abonnement.

![Hallo ** publiceren Service Fabric toepassing ** in het dialoogvenster gebruikte tooconfigure een Service Fabric-verbinding is.][publishdialog]

Hallo **Service Fabric-toepassing publiceren** in het dialoogvenster automatisch gevalideerd Hallo cluster verbinding. Als u wordt gevraagd, meld u aan tooyour Azure-account. Als de validatie is geslaagd, betekent dit dat uw systeem Hallo juist certificaten tooconnect toohello cluster veilig geïnstalleerd of uw cluster is niet-beveiligde heeft. Mislukte gegevensvalidatie kunnen worden veroorzaakt door netwerkproblemen of omdat u niet hoeft uw systeem correct geconfigureerd tooconnect tooa beveiligde cluster.

![Hallo ** publiceren Service Fabric toepassing ** in het dialoogvenster valideert een bestaande correct geconfigureerd verbinding voor Service Fabric-cluster.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa beveiligde cluster
1. Zorg ervoor dat u toegang hebt tot een Hallo-clientcertificaten die Hallo bestemming cluster vertrouwensrelaties. Hallo-certificaat wordt gewoonlijk gedeeld als Personal Information Exchange (.pfx)-bestand. Zie [instellen van een Service Fabric-cluster van hello Azure-portal](service-fabric-cluster-creation-via-portal.md) voor hoe tooconfigure Hallo server toogrant tooa client access.
2. Hallo vertrouwd certificaat installeren. toodo, dubbelklik op Hallo pfx-bestand of Hallo PowerShell script importeren PfxCertificate tooimport Hallo certificaten gebruiken. Hallo-certificaat te installeren**Cert: \LocalMachine\My**. Het is OK tooaccept alle standaardinstellingen tijdens het Hallo-certificaat importeren.
3. Kies Hallo **publiceren...**  opdracht in het snelmenu Hallo Hallo project tooopen Hallo **Publish Azure Application** in het dialoogvenster en selecteer vervolgens Hallo doelcluster. Hallo hulpprogramma wordt automatisch opgelost Hallo verbinding en slaat Hallo beveiligde verbinding parameters in Hallo publiceren profiel.
4. Optioneel: U kunt Hallo bewerken profiel toospecify een beveiligde cluster verbinding publiceren.
   
   Omdat u Hallo publiceren profiel XML-bestand toospecify Hallo certificaatgegevens handmatig bewerkt, worden ervoor toonote Hallo naam van het certificaatarchief, slaat u de locatie en de vingerafdruk van het certificaat. U moet tooprovide deze waarden voor Hallo certificaatarchief naam en locatie is opgeslagen. Zie [hoe: ophalen Hallo vingerafdruk van een certificaat](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) voor meer informatie.
   
   U kunt Hallo *ClusterConnectionParameters* parameters toospecify Hallo PowerShell parameters toouse bij het verbinden van toohello Service Fabric-cluster. Geldige parameters zijn die worden geaccepteerd door Hallo Connect-ServiceFabricCluster cmdlet. Zie [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) voor een lijst met beschikbare parameters.
   
   Als u externe cluster tooa publiceren wilt, moet u toospecify Hallo juiste parameters voor die specifieke cluster. Hallo Hieronder volgt een voorbeeld van verbinding tooa niet-beveiligde cluster:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Hier volgt een voorbeeld voor verbindende tooan x509 op basis van certificaten beveiligde cluster:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Eventuele andere vereiste instellingen, zoals parameters voor het bijwerken en toepassing Parameter bestandslocatie, bewerken en vervolgens publiceert u de toepassing hello **Service Fabric-toepassing publiceren** dialoogvenster in Visual Studio.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over het openen van Service Fabric-clusters [uw cluster visualiseren met behulp van Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
