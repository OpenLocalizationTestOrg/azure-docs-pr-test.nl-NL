---
title: overzicht van service fabric-beveiliging aaaAzure | Microsoft Docs
description: Dit artikel bevat een overzicht van hello Azure service fabric-beveiliging.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: ec5355983c5d59f4e0c3b855965f03ac47f1a4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-overview"></a>Overzicht van Azure Service Fabric-beveiliging
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) is een platform voor gedistribueerde systemen waarmee u eenvoudig toopackage kunt implementeren en beheren van schaalbare en betrouwbare micro-services. Service Fabric adressen Hallo grote uitdagingen ontwikkelen en beheren van cloudtoepassingen. Ontwikkelaars en beheerders kunnen complexe infrastructuurproblemen voorkomen en zich concentreren op het implementeren van bedrijfsspecifieke, veeleisende werkbelastingen die schaalbaar, betrouwbaar en beheerbaar zijn.

In dit artikel beveiligingsoverzicht van Azure Service Fabric is gericht op Hallo gebieden te volgen:

-   Uw cluster beveiligen
-   Controle en diagnostische gegevens
-   Beveiligen met behulp van certificaten
-   Op rollen gebaseerde toegangsbeheer (RBAC)
-   Beveiligde cluster met behulp van Windows-beveiliging
-   Toepassingsbeveiliging configureren in Service Fabric
-   Veilige communicatie voor services van Azure Service Fabric-beveiliging

## <a name="securing-your-cluster"></a>Uw cluster beveiligen
Azure Service Fabric is een orchestrator van services in een cluster van machines, Clusters moet beveiligde tooprevent niet-geautoriseerde gebruikers verbinding maken met cluster tooyour, vooral wanneer er productieworkloads uitgevoerd. Hoewel het mogelijk toocreate een niet-beveiligde cluster, Hierdoor kunnen de anonieme gebruikers tooconnect tooit, als deze management eindpunten toohello beschrijft openbare Internet.

Deze sectie biedt een overzicht van Hallo security scenario's voor clusters die worden uitgevoerd op Azure of zelfstandige en verschillende technologieën tooimplement Hallo de scenario's. Hallo cluster security scenario's:

-   Knooppunt naar beveiliging
-   Beveiliging van de client-naar-knooppunt

### <a name="node-to-node-security"></a>Knooppunt naar beveiliging
Communicatie tussen Hallo virtuele machines of machines in Hallo cluster beveiligt. Dit zorgt ervoor dat alleen computers die geautoriseerd toojoin Hallo cluster zijn kunnen deelnemen die als host fungeert voor toepassingen en services in Hallo-cluster.

Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://msdn.microsoft.com/library/ff649801.aspx) of [Windows-beveiliging](https://msdn.microsoft.com/library/ff649396.aspx) voor Windows Server-machines.

**Beveiliging van een knooppunt naar certificate**

Service Fabric maakt gebruik van X.509-servercertificaten die u als onderdeel van het Hallo-knooppunttype configuraties opgeeft wanneer u een cluster maakt. Een snel overzicht van wat deze certificaten zijn en [hoe kunt u verkrijgen of maken ze is opgegeven in dit artikel](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Certificaatbeveiliging is geconfigureerd tijdens het Hallo-cluster maken via hello Azure-portal, Azure Resource Manager-sjablonen of een zelfstandige JSON-sjabloon. U kunt een primaire certificaat en een optionele secundaire certificaat dat wordt gebruikt voor het certificaat rollovers opgeven. Hallo primaire en secundaire certificaten die u opgeeft moet anders zijn dan Hallo Beheerclient en alleen-lezen clientcertificaten u opgeeft voor [clientknooppunt beveiliging](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Beveiliging van de client-naar-knooppunt
Client toonode beveiliging is geconfigureerd met behulp van de identiteit van de Client. tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow welke client-id's die kunnen worden vertrouwd. Dit kan op twee verschillende manieren doen:

-   Geef Hallo groep Domeingebruikers die verbinding kunnen maken of
-   Geef Hallo knooppunt domeingebruikers die verbinding kunnen maken.

Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn:

-   Beheerder
-   Gebruiker

Toegangsbeheer biedt Hallo mogelijkheid voor Hallo beheerder toolimit toegang toocertain clustertypen van bewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken voor een cluster. Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.

**De beveiliging van client-naar-node certificate**

De beveiliging van client-naar-node certificate is tijdens het maken van Hallo-cluster via hello Azure-portal Resource Manager-sjablonen of een zelfstandige JSON-sjabloon door op te geven van een clientcertificaat voor de beheerder en/of een clientcertificaat voor de gebruiker geconfigureerd. Hallo beheerder client- en clientcertificaten die u opgeeft moet anders dan Hallo primaire en secundaire certificaten die u voor knooppunt naar beveiliging opgeeft.

Clients die verbinding maken met Hallo beheerder certificaat toohello-cluster hebben volledige toegang toomanagement mogelijkheden. Clients die verbinding maken toohello cluster Hallo alleen-lezengebruiker-clientcertificaat hebben alleen leestoegang toomanagement mogelijkheden. In een ander woord die deze certificaten worden gebruikt voor hello wordt rollen gebaseerd toegangsbeheer (RBAC).

Voor Azure Lees [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) toolearn hoe tooconfigure beveiliging in een cluster van het certificaat.

**Beveiliging van de client naar het knooppunt Azure Active Directory (AAD) in Azure**

Clusters die worden uitgevoerd op Azure kunnen ook veilige toegang toohello eindpunten voor beheer met behulp van Azure Active Directory (AAD). Zie [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) voor informatie over hoe toocreate nodig AAD artefacten hello, hoe toopopulate ze tijdens cluster maken en hoe tooconnect toothose daarna clusters.

AAD kan organisaties (bekend als tenants) toomanage gebruiker toegang tooapplications, die zijn onderverdeeld in toepassingen met een aanmelding webgebaseerde gebruikersinterface en toepassingen met een native Clientervaring.

Een Service Fabric-cluster biedt verschillende vermelding punten tooits beheerfunctionaliteit, met inbegrip van Hallo web gebaseerde Service Fabric Explorer en Visual Studio. Als gevolg hiervan, maakt u twee AAD toepassingen toocontrol toegang toohello cluster, een webtoepassing en een systeemeigen toepassing.
Voor Azure clusters, wordt het aanbevolen AAD beveiliging tooauthenticate clients en -certificaten te voor een knooppunt naar beveiliging gebruiken.

Voor zelfstandige WindowsServer-clusters, wordt het aanbevolen Windows-beveiliging met een groep beheerde account (GMA) te gebruiken als u Windows Server 2012 R2 en Active Directory. Anders nog steeds gebruiken Windows-beveiliging met Windows-accounts.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Controle en diagnostische gegevens voor Azure Service Fabric
[Controle en diagnostische gegevens](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) kritieke toodeveloping, testen en implementeren van toepassingen en services in elke omgeving zijn. Service Fabric-oplossingen werken het beste wanneer u plannen en implementeren van controle en diagnostische gegevens waarmee Zorg ervoor toepassingen dat en services werkt zoals verwacht in een lokale ontwikkelingsomgeving of in de productieomgeving.

Vanuit het beveiligingsoogpunt van Hallo belangrijkste doelstellingen van controle en diagnostische gegevens zijn naar:

-   Detecteren en onderzoeken van problemen met hardware- en -infrastructuur die mogelijk vanwege tooa beveiligingsgebeurtenis.
-   Problemen met software en de app waarmee de indicator van inbreuk (IoC) kunnen detecteren.
-   Resource begrijpen verbruik toohelp onbedoelde DOS-aanval te voorkomen.

Hallo totale werkstroom van de bewaking en diagnostische gegevens bestaat uit drie stappen:

-   **Genereren van gebeurtenis:** dit gebeurtenissen (Logboeken, traceringen, aangepaste gebeurtenissen) omvat op Hallo-infrastructuur (cluster) en toepassing / service-niveau. Lees meer over [infrastructuur niveau gebeurtenissen](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) en [niveau toepassingsgebeurtenissen](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) toounderstand wat is opgegeven en hoe tooadd instrumentation verder.
-   **Aggregatie van gebeurtenis:** gegenereerde gebeurtenissen moeten toobe worden verzameld en geaggregeerd voordat ze kunnen worden weergegeven. Doorgaans aangeraden [Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (meer lijken op basis van tooagent logboekverzameling) of [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (in-process logboekgegevens verzameld).
-   **Analyse:** gebeurtenissen moeten toobe gevisualiseerde en toegankelijk zijn in sommige-indeling, tooallow voor analyse en weergave zo nodig. Er zijn verschillende geweldige platforms die aanwezig zijn in de markt Hallo wanneer deze toohello analyse en visualisatie van controle en diagnostische gegevens wordt. Hallo twee die wij adviseren zijn [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) en [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) vanwege tootheir betere integratie met Service Fabric.

U kunt ook [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) toomonitor veel van hello Azure-resources waarop een Service Fabric-cluster is gebouwd.

Een watchdog is een afzonderlijke service die u kunt health bekijken en laden tussen services en het rapport status voor alles in Hallo health modelhiërarchie. Dit kan helpen voorkomen dat er fouten die niet kunnen worden gedetecteerd op basis van Hallo-weergave van een service. Watchdogs zijn ook een goede plaats toohost code waarmee corrigerende acties zonder tussenkomst van de gebruiker (bijvoorbeeld het opschonen van logboekbestanden in de opslag op bepaalde tijdsintervallen) wordt uitgevoerd. U vindt een steekproef watchdog service-implementatie [hier](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Beveiligen met behulp van certificaten
Met behulp van certificaten, wordt aangegeven hoe toosecure Hallo communicatie tussen Hallo verschillende knooppunten van uw zelfstandige Windows-cluster, evenals hoe tooauthenticate clients die verbinding maken toothis cluster x.509-certificaten gebruiken. Dit zorgt ervoor dat alleen gemachtigde gebruikers toegang cluster hello tot hebben, geïmplementeerde toepassingen Hallo en beheertaken uitvoeren. Certificaatbeveiliging moet worden ingeschakeld op Hallo cluster als Hallo cluster wordt gemaakt.

### <a name="x509-certificates-and-service-fabric"></a>X.509-certificaten en Service Fabric
Digitale x.509-certificaten zijn vaak gebruikte tooauthenticate clients en servers en tooencrypt en digitaal ondertekenen van berichten.

Hallo bevat volgende tabel Hallo-certificaten die u nodig van uw cluster-instellingen hebt:

|Certificaat informatie instelling |Beschrijving|
|-------------------------------|-----------|
|ClusterCertificate|    Dit certificaat is vereist toosecure Hallo communicatie tussen knooppunten Hallo op een cluster. U kunt twee verschillende certificaten, een primaire en een secundaire voor een upgrade.|
|ServerCertificate| Dit certificaat wordt toohello client weergegeven als er wordt geprobeerd tooconnect toothis cluster. U kunt twee verschillende servercertificaten, een primaire en een secundaire voor een upgrade.|
|ClientCertificateThumbprints|  Dit is een set van certificaten die u tooinstall op Hallo geverifieerde clients wilt.|
|ClientCertificateCommonNames|  Hallo algemene naam van de eerste clientcertificaat Hallo voor Hallo CertificateCommonName instellen. Hallo CertificateIssuerThumbprint is Hallo vingerafdruk voor Hallo verlener van dit certificaat.|
|ReverseProxyCertificate|   Dit is een optioneel certificaat dat kan worden opgegeven als u wilt dat toosecure uw [Reverse Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Voor meer informatie over het beveiligen van certificaten, [Klik hier](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Op rollen gebaseerde toegangsbeheer (RBAC)
Toegangsbeheer kunt Hallo beheerder toolimit toegang toocertain cluster clusterbewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken. Twee verschillende access controletypen worden ondersteund voor clients die verbinding maken tooa cluster: beheerdersrol en gebruikersrol.

Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.

U opgeven Hallo beheerder- en client gebruikersrollen gelijktijdig Hallo met cluster maken door afzonderlijke identiteiten (certificaten, AAD enz.) voor elk. Zie voor meer informatie over instellingen voor toegangsbeheer standaard Hallo en hoe toochange standaardinstellingen Hallo [toegangsbeheer voor Service Fabric-clients op basis van rollen](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Beveiligde zelfstandige cluster met behulp van Windows-beveiliging
tooprevent onbevoegde toegang tooa Service Fabric-cluster, moet u Hallo-cluster beveiligen. Beveiliging is vooral belangrijk bij Hallo cluster productieworkloads wordt uitgevoerd. Hierin wordt beschreven hoe tooconfigure knooppunt naar beveiliging en op client-naar-knooppunt met behulp van Windows-beveiliging in ClusterConfig.JSON bestand Hallo.

**Windows-beveiliging met behulp van gMSA configureren**

Knooppunt toonode beveiliging wordt geconfigureerd door in te stellen [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) wanneer het service fabric moet toorun onder gMSA. In de volgorde toobuild vertrouwensrelaties tussen knooppunten, moeten ze worden aangebracht op de hoogte van elkaar.

Client toonode beveiliging is geconfigureerd met behulp van ClientIdentities. In de volgorde tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow configureren welke client-id's die kunnen worden vertrouwd.

**Windows-beveiliging met behulp van een machine-beheergroep configureren**

Knooppunt toonode beveiliging wordt geconfigureerd via de instelling met de ClusterIdentity als u wilt dat toouse een Machinegroep binnen een Active Directory-domein. Zie voor meer informatie [maken van een Machine-groep in Active Directory](https://msdn.microsoft.com/library/aa545347).

Beveiliging van de client naar het knooppunt is geconfigureerd met behulp van ClientIdentities. tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow Hallo client, identiteiten die Hallo cluster vertrouwen kunnen configureren. U kunt een vertrouwensrelatie in twee verschillende manieren:

-   Geef Hallo groep Domeingebruikers die verbinding kunnen maken.
-   Geef Hallo knooppunt domeingebruikers die verbinding kunnen maken.

## <a name="configure-application-security-in-service-fabric"></a>Toepassingsbeveiliging configureren in Service Fabric
### <a name="managing-secrets-in-service-fabric-applications"></a>Het beheren van geheimen in Service Fabric-toepassingen
Deze methode helpt bij het beheren van geheimen in een Service Fabric-toepassing. Geheimen mag gevoelige informatie, zoals de storage-verbindingsreeksen, wachtwoorden of andere waarden die niet moeten worden behandeld als tekst zonder opmaak.

Deze benadering wordt [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) toomanage sleutels en geheimen. Met behulp van geheimen in een toepassing is echter cloud platform networkdirect tooallow toepassingen toobe geïmplementeerd tooa cluster overal worden gehost. Er zijn vier hoofdstappen in deze overdracht:

-   Verkrijgen van een certificaat voor het uitwisselen van gegevens.
-   Hallo-certificaat installeren in uw cluster.
-   Versleutelen geheime waarden bij het implementeren van een toepassing met Hallo-certificaat en injecteren van een service Settings.xml-configuratiebestand.
-   Alleen versleutelde waarden buiten Settings.xml door te ontsleutelen met Hallo hetzelfde uitwisselen certificaat.

>[!Note]
>Meer informatie over [geheimen in Service Fabric-toepassingen beheren](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Beveiligingsbeleid configureren voor uw toepassing
Met behulp van Azure Service Fabric-beveiliging, kunt u beveiligde toepassingen die worden uitgevoerd in de cluster Hallo onder verschillende gebruikersaccounts. Service Fabric-beveiliging kunt u ook beveiligde Hallo resources die worden gebruikt door toepassingen op moment van implementatie onder Hallo gebruikersaccounts--Hallo bijvoorbeeld, bestanden, mappen en certificaten. Hierdoor waarop toepassingen worden uitgevoerd, zelfs in een gedeelde gehoste omgeving veiliger van elkaar.
Hallo stappen omvatten:

-   Hallo-beleid voor een toegangspunt voor service-instellingen configureren.
-   PowerShell-opdrachten starten vanuit een setup-toegangspunt.
-   Console-omleiding gebruiken voor lokale foutopsporing.
-   Configureer een beleid voor servicepakketten code.
-   Wijs een beveiligingsbeleid voor toegang voor HTTP en HTTPS-eindpunten.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Veilige communicatie voor services in Azure Service Fabric-beveiliging
Beveiliging is een van de belangrijkste aspecten Hallo van communicatie. toepassingsframework voor Hallo Reliable Services biedt enkele vooraf gedefinieerde communicatie stacks en hulpprogramma's die gebruikt tooimprove beveiliging worden kunnen.

-   [Beveiligen van een service wanneer u remoting service](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Beveiligen van een service wanneer u een WCF-communicatie-stack](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Volgende stappen
- Raadpleeg voor algemene informatie over de clusterbeveiliging van de [een cluster maken in Azure Resource Manager-sjabloon met](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) en [Azure-portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Lees de informatie over [Service Fabric-clusterbeveiliging](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
