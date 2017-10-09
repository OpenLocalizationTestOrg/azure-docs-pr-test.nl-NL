---
title: aaaSecure Service Fabric-cluster | Microsoft Docs
description: "Beschrijft Hallo security scenario's voor een Service Fabric-cluster en Hallo verschillende technologieën gebruikt tooimplement de scenario's."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Scenario's voor beveiliging van service Fabric-cluster
Een Service Fabric-cluster is een resource die u bezit. Clusters moet beveiligde tooprevent niet-geautoriseerde gebruikers verbinding maken met cluster tooyour, vooral wanneer er productieworkloads uitgevoerd. Hoewel het mogelijk toocreate een niet-beveiligde cluster, Hierdoor kunnen de anonieme gebruikers tooconnect tooit, als deze management eindpunten toohello beschrijft openbare Internet. 

Dit artikel biedt een overzicht van Hallo security scenario's voor clusters die worden uitgevoerd op Azure of zelfstandige en verschillende technologieën tooimplement Hallo de scenario's. Hallo cluster security scenario's:

* Knooppunt naar beveiliging
* Beveiliging van de client-naar-knooppunt
* Op rollen gebaseerde toegangsbeheer (RBAC)

## <a name="node-to-node-security"></a>Knooppunt naar beveiliging
Communicatie tussen Hallo virtuele machines of machines in Hallo cluster beveiligt. Dit zorgt ervoor dat alleen computers die geautoriseerd toojoin Hallo cluster zijn kunnen deelnemen die als host fungeert voor toepassingen en services in Hallo-cluster.

![Diagram van knooppunt naar communicatie][Node-to-Node]

Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://msdn.microsoft.com/library/ff649801.aspx) of [Windows-beveiliging](https://msdn.microsoft.com/library/ff649396.aspx) voor Windows Server-machines.

### <a name="node-to-node-certificate-security"></a>Beveiliging van een knooppunt naar certificate
Service Fabric maakt gebruik van X.509-servercertificaten die u als onderdeel van het Hallo-knooppunttype configuraties opgeeft wanneer u een cluster maakt. Een snel overzicht van wat deze certificaten zijn en hoe u kunt verkrijgen of ze maken wordt op Hallo einde van dit artikel aangeboden.

Certificaatbeveiliging is geconfigureerd tijdens het Hallo-cluster maken via hello Azure-portal, Azure Resource Manager-sjablonen of een zelfstandige JSON-sjabloon. U kunt een primaire certificaat en een optionele secundaire certificaat dat wordt gebruikt voor het certificaat rollovers opgeven. Hallo primaire en secundaire certificaten die u opgeeft moet anders zijn dan Hallo Beheerclient en alleen-lezen clientcertificaten u opgeeft voor [clientknooppunt beveiliging](#client-to-node-security).

Voor Azure Lees [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](service-fabric-cluster-creation-via-arm.md) toolearn hoe tooconfigure beveiliging in een cluster van het certificaat.

Lees voor zelfstandige Windows Server [een zelfstandige cluster op Windows met behulp van X.509-certificaten beveiligen](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Knooppunt naar windows-beveiliging
Lees voor zelfstandige Windows Server [beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Beveiliging van de client-naar-knooppunt
Clients geverifieerd en communicatie tussen een client en de afzonderlijke knooppunten in het Hallo-cluster beveiligt. Dit type beveiliging verifieert en communicatie met de client, die zorgt dat alleen geautoriseerde gebruikers toegang heeft tot Hallo-cluster en Hallo-toepassingen die zijn geïmplementeerd op Hallo cluster beveiligt. Clients via hun Windows-beveiliging referenties of hun beveiligingsreferenties certificaat uniek geïdentificeerd.

![Diagram van communicatie van client-naar-knooppunt][Client-to-Node]

Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://msdn.microsoft.com/library/ff649801.aspx) of [Windows-beveiliging](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>De beveiliging van client-naar-node certificate
 De beveiliging van client-naar-node certificate is tijdens het maken van Hallo-cluster via hello Azure-portal, Resource Manager-sjablonen of een zelfstandige JSON-sjabloon door op te geven van een clientcertificaat voor de beheerder en/of een clientcertificaat voor de gebruiker geconfigureerd.  Hallo-client en de gebruiker beheerclientcertificaten u opgeeft moet anders zijn dan Hallo primaire en secundaire certificaten die u opgeeft voor [knooppunt naar beveiliging](#node-to-node-security) als een best practice. Standaard worden Hallo clustercertificaten voor knooppunt naar beveiliging toohello toegestaan client Admin certificaten lijst toegevoegd.

Clients die verbinding maken met Hallo beheerder certificaat toohello-cluster hebben volledige toegang toomanagement mogelijkheden.  Clients die verbinding maken toohello cluster Hallo alleen-lezengebruiker-clientcertificaat hebben alleen leestoegang toomanagement mogelijkheden. Met andere woorden worden deze certificaten gebruikt voor Hallo rollen basissen toegangsbeheer (RBAC) verderop in dit artikel wordt beschreven.

Voor Azure Lees [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](service-fabric-cluster-creation-via-arm.md) toolearn hoe tooconfigure beveiliging in een cluster van het certificaat.

Lees voor zelfstandige Windows Server [een zelfstandige cluster op Windows met behulp van X.509-certificaten beveiligen](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Beveiliging van de client naar het knooppunt Azure Active Directory (AAD) in Azure
Clusters die worden uitgevoerd op Azure kunnen ook veilige toegang toohello eindpunten voor beheer met behulp van Azure Active Directory (AAD). Zie [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](service-fabric-cluster-creation-via-arm.md) voor informatie over hoe toocreate nodig AAD artefacten hello, hoe toopopulate ze tijdens cluster maken en hoe tooconnect toothose daarna clusters.

## <a name="security-recommendations"></a>Aanbevelingen voor beveiliging
Voor Azure clusters, wordt het aanbevolen AAD beveiliging tooauthenticate clients en -certificaten te voor een knooppunt naar beveiliging gebruiken.

Clusters wordt aangeraden Windows-beveiliging te gebruiken met een groep beheerde accounts (GMA) zelfstandig Windows Server hebt u Windows Server 2012 R2 en Active Directory. Anders nog steeds gebruiken Windows-beveiliging met Windows-accounts.

## <a name="role-based-access-control-rbac"></a>Op rollen gebaseerd toegangsbeheer (RBAC)
Toegangsbeheer kunt Hallo beheerder toolimit toegang toocertain cluster clusterbewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken. Twee verschillende access controletypen worden ondersteund voor clients die verbinding maken tooa cluster: beheerdersrol en gebruikersrol.

Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.

U opgeven Hallo beheerder- en client gebruikersrollen gelijktijdig Hallo met cluster maken door afzonderlijke identiteiten (certificaten, AAD enz.) voor elk. Zie voor meer informatie over instellingen voor toegangsbeheer standaard Hallo en hoe toochange standaardinstellingen Hallo [toegangsbeheer voor Service Fabric-clients op basis van rollen](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>X.509-certificaten en Service Fabric
Digitale x.509-certificaten zijn vaak gebruikte tooauthenticate clients en servers en tooencrypt en digitaal ondertekenen van berichten. Voor meer informatie over deze certificaten gaat te[werken met certificaten](http://msdn.microsoft.com/library/ms731899.aspx).

Een aantal belangrijke zaken tooconsider:

* Certificaten worden gebruikt in clusters met productieworkloads moeten worden gemaakt met behulp van een juist geconfigureerde service voor Windows Server-certificaat of verkregen van een goedgekeurde [certificeringsinstantie (CA)](https://en.wikipedia.org/wiki/Certificate_authority).
* Gebruik nooit een tijdelijke en certificaten in productie die zijn gemaakt met de hulpprogramma's zoals MakeCert.exe testen.
* U kunt een zelfondertekend certificaat gebruiken, maar u moet alleen doen voor testclusters en niet in de productieomgeving.

### <a name="server-x509-certificates"></a>X.509-certificaten van server
Servercertificaten hebt Hallo primaire taak van een server (knooppunt) tooclients verifiëren of verificatie van een server (knooppunt) tooa server (knooppunt). Een van de eerste controles Hallo wanneer een client of het knooppunt verifieert een knooppunt is toocheck Hallo waarde van de algemene naam in het veld onderwerp Hallo Hallo. Deze algemene naam of een van de alternatieve onderwerpnamen Hallo-certificaten moet aanwezig zijn in de lijst met algemene namen Hallo zijn.

Hallo volgende artikel wordt beschreven hoe toogenerate met alternatieve namen voor onderwerp (SAN)-certificaten: [hoe de LDAP-certificaat voor het beveiligen van een alternatieve naam voor onderwerp tooa tooadd](http://support.microsoft.com/kb/931351).

het veld onderwerp Hallo verschillende waarden kan bevatten, elk voorafgegaan door een waardetype initialisatie tooindicate Hallo. Meest voorkomende is Hallo initialisatie 'CN' voor de algemene naam; bijvoorbeeld "CN = www.contoso.com '. Het is ook mogelijk dat Hallo onderwerp veld toobe leeg. Als Hallo optioneel alternatieve onderwerpnaam veld is ingevuld, moet deze algemene naam van certificaat Hallo Hallo en één vermelding per alternatieve onderwerpnaam bevatten. Deze worden ingevoerd als DNS-naam waarden.

Hallo-waarde van veld van de Hallo beoogde doeleinden van Hallo certificaat moet een geschikte waarde, zoals 'serververificatie' of 'clientverificatie' bevatten.

### <a name="client-x509-certificates"></a>Client X.509-certificaten
Clientcertificaten zijn doorgaans niet uitgegeven door een certificeringsinstantie van derden. In plaats daarvan bevat hello archief Persoonlijk van huidige gebruikerslocatie Hallo meestal clientcertificaten daar geplaatst door een basisinstantie met een doel van 'clientverificatie'. Hallo-client kunt zo'n certificaat gebruiken wanneer wederzijdse verificatie vereist is.

> [!NOTE]
> Alle beheerbewerkingen op een Service Fabric-cluster vereist servercertificaat. Clientcertificaten kunnen niet worden gebruikt voor beheer.
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>Volgende stappen
Dit artikel bevat conceptuele informatie over de clusterbeveiliging van het. Vervolgens


1.  [een cluster in Azure met behulp van een Resource Manager-sjabloon maken](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure-portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
