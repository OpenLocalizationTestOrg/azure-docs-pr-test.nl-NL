---
title: Een Service Fabric-cluster beveiligen | Microsoft Docs
description: "Beschrijft de security scenario's voor Service Fabric-cluster en de verschillende technologieën gebruikt voor het implementeren van de scenario's."
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
ms.openlocfilehash: 5afbe575a8affc37b8f902c0988585a83921e3d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Scenario's voor beveiliging van service Fabric-cluster
Een Service Fabric-cluster is een resource die u bezit. Clusters moeten worden beveiligd om te voorkomen dat onbevoegde gebruikers verbinding maken met uw cluster, vooral wanneer er productieworkloads uitgevoerd. Hoewel het mogelijk om een niet-beveiligde cluster te maken, kan hierdoor dus anonieme gebruikers verbinding kunnen maken, als eindpunten voor beheer met het openbare Internet zichtbaar. 

Dit artikel bevat een overzicht van scenario's voor de beveiliging voor clusters die worden uitgevoerd op Azure of zelfstandige en de verschillende technologieën gebruikt voor het implementeren van de scenario's. De cluster security scenario's:

* Knooppunt naar beveiliging
* Beveiliging van de client-naar-knooppunt
* Op rollen gebaseerde toegangsbeheer (RBAC)

## <a name="node-to-node-security"></a>Knooppunt naar beveiliging
Communicatie tussen de virtuele machines of machines in het cluster beveiligt. Dit zorgt ervoor dat alleen de computers die zijn gemachtigd om lid van het cluster te kunnen deelnemen die als host fungeert voor toepassingen en services in het cluster.

![Diagram van knooppunt naar communicatie][Node-to-Node]

Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://msdn.microsoft.com/library/ff649801.aspx) of [Windows-beveiliging](https://msdn.microsoft.com/library/ff649396.aspx) voor Windows Server-machines.

### <a name="node-to-node-certificate-security"></a>Beveiliging van een knooppunt naar certificate
Service Fabric maakt gebruik van X.509-servercertificaten die u als onderdeel van de configuraties van het type knooppunt opgeeft wanneer u een cluster maakt. Een snel overzicht van wat deze certificaten zijn en hoe u kunt verkrijgen of ze maken is aan het einde van dit artikel opgegeven.

Certificaatbeveiliging is geconfigureerd tijdens het maken van het cluster via de Azure-portal, Azure Resource Manager-sjablonen of een zelfstandige JSON-sjabloon. U kunt een primaire certificaat en een optionele secundaire certificaat dat wordt gebruikt voor het certificaat rollovers opgeven. De primaire en secundaire certificaten die u opgeeft moet anders zijn dan de Beheerclient en alleen-lezen clientcertificaten u opgeeft voor [clientknooppunt beveiliging](#client-to-node-security).

Voor Azure Lees [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](service-fabric-cluster-creation-via-arm.md) voor informatie over het Certificaatbeveiliging configureren in een cluster.

Lees voor zelfstandige Windows Server [een zelfstandige cluster op Windows met behulp van X.509-certificaten beveiligen](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>Knooppunt naar windows-beveiliging
Lees voor zelfstandige Windows Server [beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>Beveiliging van de client-naar-knooppunt
Clients geverifieerd en communicatie tussen een client en de afzonderlijke knooppunten in het cluster beveiligt. Dit type beveiliging verifieert en communicatie met de client, die zorgt dat alleen geautoriseerde gebruikers toegang heeft tot het cluster en de toepassingen die zijn geïmplementeerd op het cluster beveiligt. Clients via hun Windows-beveiliging referenties of hun beveiligingsreferenties certificaat uniek geïdentificeerd.

![Diagram van communicatie van client-naar-knooppunt][Client-to-Node]

Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://msdn.microsoft.com/library/ff649801.aspx) of [Windows-beveiliging](https://msdn.microsoft.com/library/ff649396.aspx).

### <a name="client-to-node-certificate-security"></a>De beveiliging van client-naar-node certificate
 De beveiliging van client-naar-node certificate is tijdens het maken van het cluster via de Azure-portal Resource Manager-sjablonen of een zelfstandige JSON-sjabloon door op te geven van een clientcertificaat voor de beheerder en/of een clientcertificaat voor de gebruiker geconfigureerd.  De client en de gebruiker beheerclientcertificaten u opgeeft moet anders zijn dan de primaire en secundaire certificaten die u opgeeft voor [knooppunt naar beveiliging](#node-to-node-security) als een best practice. Standaard worden de clustercertificaten voor knooppunt naar beveiliging toegevoegd aan de lijst met toegestane client Admin certificaten.

Clients die verbinding maken met het cluster via de admin-certificaat hebben volledige toegang tot de beheerfuncties.  Clients die verbinding maken met het cluster via het clientcertificaat voor alleen-lezengebruiker alleen leestoegang hebben tot beheermogelijkheden. Met andere woorden worden deze certificaten gebruikt voor de rol basissen toegangsbeheer (RBAC) verderop in dit artikel wordt beschreven.

Voor Azure Lees [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](service-fabric-cluster-creation-via-arm.md) voor informatie over het Certificaatbeveiliging configureren in een cluster.

Lees voor zelfstandige Windows Server [een zelfstandige cluster op Windows met behulp van X.509-certificaten beveiligen](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Beveiliging van de client naar het knooppunt Azure Active Directory (AAD) in Azure
Clusters die worden uitgevoerd op Azure kunnen ook beveiligde toegang tot de eindpunten voor beheer met behulp van Azure Active Directory (AAD). Zie [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](service-fabric-cluster-creation-via-arm.md) voor meer informatie over het maken van de benodigde AAD-artefacten, hoe deze in te vullen tijdens het maken en daarna verbinding maken met deze clusters.

## <a name="security-recommendations"></a>Aanbevelingen voor beveiliging
Voor Azure clusters, wordt het aanbevolen gebruik van AAD-beveiliging voor verificatie van clients en certificaten voor knooppunt naar beveiliging.

Clusters wordt aangeraden Windows-beveiliging te gebruiken met een groep beheerde accounts (GMA) zelfstandig Windows Server hebt u Windows Server 2012 R2 en Active Directory. Anders nog steeds gebruiken Windows-beveiliging met Windows-accounts.

## <a name="role-based-access-control-rbac"></a>Op rollen gebaseerd toegangsbeheer (RBAC)
Toegangsbeheer kan de Clusterbeheerder om te beperken van toegang tot bepaalde clusterbewerkingen voor verschillende groepen gebruikers, zodat het cluster beter te beveiligen. Twee verschillende access controletypen worden ondersteund voor clients die verbinding maken met een cluster: beheerdersrol en gebruikersrol.

Beheerders hebben volledige toegang tot de beheerfuncties (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang tot beheermogelijkheden (bijvoorbeeld querymogelijkheden) en de mogelijkheid om op te lossen, toepassingen en services.

U opgeven de functies van de client beheerder en gebruiker op het moment van cluster maken door afzonderlijke identiteiten (certificaten, AAD enz.) voor elk. Zie voor meer informatie over de standaardinstellingen voor het beheer van toegang en het wijzigen van de standaardinstellingen [toegangsbeheer voor Service Fabric-clients op basis van rollen](service-fabric-cluster-security-roles.md).

## <a name="x509-certificates-and-service-fabric"></a>X.509-certificaten en Service Fabric
Digitale x.509-certificaten worden meestal gebruikt voor verificatie van clients en servers en voor het versleutelen en digitaal ondertekenen van berichten. Voor meer informatie over deze certificaten, gaat u naar [werken met certificaten](http://msdn.microsoft.com/library/ms731899.aspx).

Een aantal belangrijke zaken te overwegen:

* Certificaten worden gebruikt in clusters met productieworkloads moeten worden gemaakt met behulp van een juist geconfigureerde service voor Windows Server-certificaat of verkregen van een goedgekeurde [certificeringsinstantie (CA)](https://en.wikipedia.org/wiki/Certificate_authority).
* Gebruik nooit een tijdelijke en certificaten in productie die zijn gemaakt met de hulpprogramma's zoals MakeCert.exe testen.
* U kunt een zelfondertekend certificaat gebruiken, maar u moet alleen doen voor testclusters en niet in de productieomgeving.

### <a name="server-x509-certificates"></a>X.509-certificaten van server
Servercertificaten zijn de belangrijkste taak van een server (knooppunt) om clients te verifiëren of verificatie van een server (knooppunt) naar een server (knooppunt). Een van de eerste controles wanneer een client of het knooppunt verifieert een knooppunt is de waarde van de algemene naam in het veld Onderwerp controleren. Deze algemene naam of een van de certificaten van alternatieve onderwerpnamen moet aanwezig zijn in de lijst met algemene namen.

Het volgende artikel beschrijft het genereren van certificaten met alternatieve namen voor onderwerp (SAN): [een alternatieve onderwerpnaam toevoegen aan een beveiligde LDAP-certificaat](http://support.microsoft.com/kb/931351).

Het veld onderwerp verschillende waarden kan bevatten, elk voorafgegaan door een initialisatie om aan te geven het waardetype. De initialisatie is meestal 'CN' voor algemene naam; bijvoorbeeld "CN = www.contoso.com '. Het is ook mogelijk dat het onderwerpveld leeg is. Als de optionele alternatieve onderwerpnaam-veld is ingevuld, moet deze bevatten zowel de algemene naam van het certificaat als één vermelding per alternatieve onderwerpnaam. Deze worden ingevoerd als DNS-naam waarden.

De waarde van het veld beoogde doeleinden van het certificaat moet een geschikte waarde, zoals 'serververificatie' of 'clientverificatie' bevatten.

### <a name="client-x509-certificates"></a>Client X.509-certificaten
Clientcertificaten zijn doorgaans niet uitgegeven door een certificeringsinstantie van derden. In plaats daarvan bevat het persoonlijke archief van de huidige gebruikerslocatie doorgaans clientcertificaten daar geplaatst door een basisinstantie met een doel van 'clientverificatie'. De client kan zo'n certificaat gebruiken als wederzijdse verificatie vereist is.

> [!NOTE]
> Alle beheerbewerkingen op een Service Fabric-cluster vereist servercertificaat. Clientcertificaten kunnen niet worden gebruikt voor beheer.
> 
> 

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->


## <a name="next-steps"></a>Volgende stappen
Dit artikel bevat conceptuele informatie over de clusterbeveiliging van het. Vervolgens


1.  [een cluster in Azure met behulp van een Resource Manager-sjabloon maken](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure-portal](service-fabric-cluster-creation-via-portal.md).

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
