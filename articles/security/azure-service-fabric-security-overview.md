---
title: Overzicht van Azure service fabric-beveiliging | Microsoft Docs
description: Dit artikel bevat een overzicht van de Azure service fabric-beveiliging.
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
ms.openlocfilehash: 4cbd2791649c6d2dd005521cedb44c17aa874073
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-service-fabric-security-overview"></a>Overzicht van Azure Service Fabric-beveiliging
[Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) is een platform voor gedistribueerde systemen waarmee u gemakkelijk verpakken, implementeren en beheren van schaalbare en betrouwbare micro-services. Service Fabric adressen aanzienlijke uitdagingen bij het ontwikkelen en beheren van cloudtoepassingen. Ontwikkelaars en beheerders kunnen complexe infrastructuurproblemen voorkomen en zich concentreren op het implementeren van bedrijfsspecifieke, veeleisende werkbelastingen die schaalbaar, betrouwbaar en beheerbaar zijn.

In dit artikel beveiligingsoverzicht van Azure Service Fabric is gericht op de volgende gebieden:

-   Uw cluster beveiligen
-   Controle en diagnostische gegevens
-   Beveiligen met behulp van certificaten
-   Op rollen gebaseerde toegangsbeheer (RBAC)
-   Beveiligde cluster met behulp van Windows-beveiliging
-   Toepassingsbeveiliging configureren in Service Fabric
-   Veilige communicatie voor services van Azure Service Fabric-beveiliging

## <a name="securing-your-cluster"></a>Uw cluster beveiligen
Azure Service Fabric is een orchestrator van services in een cluster van machines, Clusters moeten worden beveiligd om te voorkomen dat onbevoegde gebruikers verbinding maken met uw cluster, vooral wanneer er productieworkloads uitgevoerd. Hoewel het mogelijk om een niet-beveiligde cluster te maken, kan hierdoor dus anonieme gebruikers verbinding kunnen maken, als eindpunten voor beheer met het openbare Internet zichtbaar.

Deze sectie biedt een overzicht van de beveiliging scenario's voor clusters die worden uitgevoerd op Azure of zelfstandige en de verschillende technologieën gebruikt voor het implementeren van de scenario's. De cluster security scenario's:

-   Knooppunt naar beveiliging
-   Beveiliging van de client-naar-knooppunt

### <a name="node-to-node-security"></a>Knooppunt naar beveiliging
Communicatie tussen de virtuele machines of machines in het cluster beveiligt. Dit zorgt ervoor dat alleen de computers die zijn gemachtigd om lid van het cluster te kunnen deelnemen die als host fungeert voor toepassingen en services in het cluster.

Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://msdn.microsoft.com/library/ff649801.aspx) of [Windows-beveiliging](https://msdn.microsoft.com/library/ff649396.aspx) voor Windows Server-machines.

**Beveiliging van een knooppunt naar certificate**

Service Fabric maakt gebruik van X.509-servercertificaten die u als onderdeel van de configuraties van het type knooppunt opgeeft wanneer u een cluster maakt. Een snel overzicht van wat deze certificaten zijn en [hoe kunt u verkrijgen of maken ze is opgegeven in dit artikel](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/working-with-certificates).

Certificaatbeveiliging is geconfigureerd tijdens het maken van het cluster via de Azure-portal, Azure Resource Manager-sjablonen of een zelfstandige JSON-sjabloon. U kunt een primaire certificaat en een optionele secundaire certificaat dat wordt gebruikt voor het certificaat rollovers opgeven. De primaire en secundaire certificaten die u opgeeft moet anders zijn dan de Beheerclient en alleen-lezen clientcertificaten u opgeeft voor [clientknooppunt beveiliging](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security).

### <a name="client-to-node-security"></a>Beveiliging van de client-naar-knooppunt
Client voor de beveiliging van knooppunt is geconfigureerd met behulp van de Client identiteiten. Als u wilt een vertrouwensrelatie tussen een client en het cluster, moet u het cluster om te weten welke client identiteiten die kunnen worden vertrouwd. Dit kan op twee verschillende manieren doen:

-   Geef de groep Domeingebruikers die verbinding kunnen maken of
-   Geef de domein-knooppunt gebruikers die verbinding kunnen maken.

Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die zijn verbonden met een Service Fabric-cluster:

-   Beheerder
-   Gebruiker

Toegangsbeheer biedt de mogelijkheid voor de Clusterbeheerder om te beperken van toegang tot bepaalde soorten clusterbewerkingen voor verschillende groepen gebruikers, zodat het cluster beter te beveiligen. Beheerders hebben volledige toegang tot de beheerfuncties (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang tot beheermogelijkheden (bijvoorbeeld querymogelijkheden) en de mogelijkheid om op te lossen, toepassingen en services.

**De beveiliging van client-naar-node certificate**

De beveiliging van client-naar-node certificate is tijdens het maken van het cluster via de Azure-portal Resource Manager-sjablonen of een zelfstandige JSON-sjabloon door op te geven van een clientcertificaat voor de beheerder en/of een clientcertificaat voor de gebruiker geconfigureerd. De client en de gebruiker beheerclientcertificaten die u opgeeft moet verschillen van de primaire en secundaire certificaten die u voor knooppunt naar beveiliging opgeeft.

Clients die verbinding maken met het cluster via de admin-certificaat hebben volledige toegang tot de beheerfuncties. Clients die verbinding maken met het cluster via het clientcertificaat voor alleen-lezengebruiker alleen leestoegang hebben tot beheermogelijkheden. In een ander woord die deze certificaten worden gebruikt voor de rol gebaseerd toegangsbeheer (RBAC).

Voor Azure Lees [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) voor informatie over het Certificaatbeveiliging configureren in een cluster.

**Beveiliging van de client naar het knooppunt Azure Active Directory (AAD) in Azure**

Clusters die worden uitgevoerd op Azure kunnen ook beveiligde toegang tot de eindpunten voor beheer met behulp van Azure Active Directory (AAD). Zie [een cluster met behulp van een Azure Resource Manager-sjabloon instellen](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) voor meer informatie over het maken van de benodigde AAD-artefacten, hoe deze in te vullen tijdens het maken en daarna verbinding maken met deze clusters.

AAD kan organisaties (bekend als tenants) voor het beheren van de gebruikerstoegang tot toepassingen die zijn onderverdeeld in toepassingen met een aanmelding webgebaseerde gebruikersinterface en toepassingen met een native Clientervaring.

Een Service Fabric-cluster biedt verschillende toegangspunten naar de beheerfunctionaliteit, met inbegrip van het web gebaseerde Service Fabric Explorer en Visual Studio. Als gevolg hiervan, maakt u twee AAD toepassingen toegang tot het cluster, een webtoepassing en een systeemeigen toepassing.
Voor Azure clusters, wordt het aanbevolen gebruik van AAD-beveiliging voor verificatie van clients en certificaten voor knooppunt naar beveiliging.

Voor zelfstandige WindowsServer-clusters, wordt het aanbevolen Windows-beveiliging met een groep beheerde account (GMA) te gebruiken als u Windows Server 2012 R2 en Active Directory. Anders nog steeds gebruiken Windows-beveiliging met Windows-accounts.

## <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Controle en diagnostische gegevens voor Azure Service Fabric
[Controle en diagnostische gegevens](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-overview) cruciaal zijn voor het ontwikkelen, testen en implementeren van toepassingen en services in elke omgeving. Service Fabric-oplossingen werken het beste wanneer u plannen en implementeren van controle en diagnostische gegevens waarmee Zorg ervoor toepassingen dat en services werkt zoals verwacht in een lokale ontwikkelingsomgeving of in de productieomgeving.

Vanuit het beveiligingsoogpunt van zijn de belangrijkste doelstellingen van controle en diagnostische gegevens naar:

-   Detecteren en onderzoeken van hardware- en infrastructuur voor problemen die veroorzaakt door een beveiligingsgebeurtenis worden kunnen.
-   Problemen met software en de app waarmee de indicator van inbreuk (IoC) kunnen detecteren.
-   Begrijpen brongebruik om te voorkomen dat onbedoeld DOS-aanval.

De algemene werkstroom van controle en diagnostische gegevens bestaat uit drie stappen:

-   **Genereren van gebeurtenis:** hierbij gebeurtenissen (Logboeken, traceringen, aangepaste gebeurtenissen) op de infrastructuur (cluster) en de toepassing / service-niveau. Lees meer over [infrastructuur niveau gebeurtenissen](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-infra) en [niveau toepassingsgebeurtenissen](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-generation-app) om te begrijpen wat is opgegeven en het toevoegen van meer instrumentation.
-   **Aggregatie van gebeurtenis:** gegenereerde gebeurtenissen moeten worden verzameld en geaggregeerd voordat ze kunnen worden weergegeven. Doorgaans aangeraden [Azure Diagnostics](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-wad) (meer vergelijkbaar met logboekverzameling op basis van een agent) of [EventFlow](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow) (in-process logboekgegevens verzameld).
-   **Analyse:** gebeurtenissen moeten worden gevisualiseerde en toegankelijk zijn in sommige indeling, toestaan voor analyse en indien nodig wordt weergegeven. Er zijn verschillende geweldige platforms die aanwezig zijn in de markt als het gaat om de analyse- en visualisatie van controle en diagnostische gegevens. De twee die wij adviseren [OMS](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-oms) en [Application Insights](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-event-analysis-appinsights) vanwege hun betere integratie met Service Fabric.

U kunt ook [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) voor het bewaken van veel van de Azure-resources waarop een Service Fabric-cluster is gebouwd.

Een watchdog is een afzonderlijke service die u kunt health bekijken en laden tussen services en het rapport status voor alles in de hiërarchie van de health-model. Dit kan helpen voorkomen dat er fouten die niet kunnen worden gedetecteerd op basis van de weergave van een service. Watchdogs zijn ook een goede plaats naar host-code die corrigerende acties zonder tussenkomst van de gebruiker (bijvoorbeeld het opschonen van logboekbestanden in de opslag op bepaalde tijdsintervallen) uitvoert. U vindt een steekproef watchdog service-implementatie [hier](https://azure.microsoft.com/resources/samples/service-fabric-watchdog-service/).

## <a name="secure-using-certificates"></a>Beveiligen met behulp van certificaten
Met behulp van certificaten, krijgt het beveiligen van de communicatie tussen de verschillende knooppunten van uw zelfstandige Windows-cluster ook hoe voor verificatie van clients die verbinding maken met dit cluster met behulp van X.509-certificaten. Dit zorgt ervoor dat alleen geautoriseerde gebruikers kunnen toegang het cluster, geïmplementeerde toepassingen tot en beheertaken uitvoeren. Certificaatbeveiliging moet worden ingeschakeld op het cluster als het cluster is gemaakt.

### <a name="x509-certificates-and-service-fabric"></a>X.509-certificaten en Service Fabric
Digitale x.509-certificaten worden meestal gebruikt voor verificatie van clients en servers en voor het versleutelen en digitaal ondertekenen van berichten.

De volgende tabel vindt u de certificaten die u nodig van uw cluster-instellingen hebt:

|Certificaat informatie instelling |Beschrijving|
|-------------------------------|-----------|
|ClusterCertificate|    Dit certificaat is vereist om de communicatie tussen de knooppunten op een cluster te beveiligen. U kunt twee verschillende certificaten, een primaire en een secundaire voor een upgrade.|
|ServerCertificate| Dit certificaat wordt geverifieerd op de client als er wordt geprobeerd verbinding maken met dit cluster. U kunt twee verschillende servercertificaten, een primaire en een secundaire voor een upgrade.|
|ClientCertificateThumbprints|  Dit is een set van certificaten die u wilt installeren op de geverifieerde clients.|
|ClientCertificateCommonNames|  De algemene naam van het certificaat van de eerste client ingesteld voor de CertificateCommonName. De CertificateIssuerThumbprint is de vingerafdruk voor de verlener van dit certificaat.|
|ReverseProxyCertificate|   Dit is een optioneel certificaat dat kan worden opgegeven als u wilt beveiligen uw [Reverse Proxy](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy).|

Voor meer informatie over het beveiligen van certificaten, [Klik hier](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security).

## <a name="role-based-access-control-rbac"></a>Op rollen gebaseerde toegangsbeheer (RBAC)
Toegangsbeheer kan de Clusterbeheerder om te beperken van toegang tot bepaalde clusterbewerkingen voor verschillende groepen gebruikers, zodat het cluster beter te beveiligen. Twee verschillende access controletypen worden ondersteund voor clients die verbinding maken met een cluster: beheerdersrol en gebruikersrol.

Beheerders hebben volledige toegang tot de beheerfuncties (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang tot beheermogelijkheden (bijvoorbeeld querymogelijkheden) en de mogelijkheid om op te lossen, toepassingen en services.

U opgeven de functies van de client beheerder en gebruiker op het moment van cluster maken door afzonderlijke identiteiten (certificaten, AAD enz.) voor elk. Zie voor meer informatie over de standaardinstellingen voor het beheer van toegang en het wijzigen van de standaardinstellingen [toegangsbeheer voor Service Fabric-clients op basis van rollen](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

## <a name="secure-standalone-cluster-using-windows-security"></a>Beveiligde zelfstandige cluster met behulp van Windows-beveiliging
Om te voorkomen dat onbevoegde toegang tot een Service Fabric-cluster, moet u het cluster te beveiligen. Beveiliging is vooral belangrijk bij het cluster wordt uitgevoerd voor productie-workloads. Wordt beschreven hoe u de beveiliging van client-naar-knooppunt en knooppunt naar configureren met behulp van Windows-beveiliging in het bestand ClusterConfig.JSON.

**Windows-beveiliging met behulp van gMSA configureren**

Knooppunt voor de beveiliging van knooppunt is geconfigureerd door in te stellen [ClustergMSAIdentity](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-windows-security) wanneer het service fabric moet worden uitgevoerd onder gMSA. Om te kunnen maken van vertrouwensrelaties tussen knooppunten, moeten ze worden aangebracht op de hoogte van elkaar.

Client voor de beveiliging van knooppunt is geconfigureerd met behulp van ClientIdentities. Om een vertrouwensrelatie tussen een client en het cluster, moet u het cluster om te weten welke client identiteiten die kunnen worden vertrouwd.

**Windows-beveiliging met behulp van een machine-beheergroep configureren**

Knooppunt voor de beveiliging van knooppunt is geconfigureerd door de instelling met de ClusterIdentity als u wilt gebruiken van een Machinegroep binnen een Active Directory-domein. Zie voor meer informatie [maken van een Machine-groep in Active Directory](https://msdn.microsoft.com/library/aa545347).

Beveiliging van de client naar het knooppunt is geconfigureerd met behulp van ClientIdentities. Als u wilt een vertrouwensrelatie tussen een client en het cluster, moet u het cluster om te weten van de client-identiteiten die kan worden vertrouwd door het cluster configureren. U kunt een vertrouwensrelatie in twee verschillende manieren:

-   Geef de groep Domeingebruikers die verbinding kunnen maken.
-   Geef de domein-knooppunt gebruikers die verbinding kunnen maken.

## <a name="configure-application-security-in-service-fabric"></a>Toepassingsbeveiliging configureren in Service Fabric
### <a name="managing-secrets-in-service-fabric-applications"></a>Het beheren van geheimen in Service Fabric-toepassingen
Deze methode helpt bij het beheren van geheimen in een Service Fabric-toepassing. Geheimen mag gevoelige informatie, zoals de storage-verbindingsreeksen, wachtwoorden of andere waarden die niet moeten worden behandeld als tekst zonder opmaak.

Deze benadering wordt [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) voor het beheren van sleutels en geheimen. Met behulp van geheimen in een toepassing is echter cloud platform-networkdirect naar toepassingen kunnen worden geïmplementeerd naar een cluster overal worden gehost. Er zijn vier hoofdstappen in deze overdracht:

-   Verkrijgen van een certificaat voor het uitwisselen van gegevens.
-   Installeer het certificaat in het cluster.
-   Versleutelen geheime waarden bij het implementeren van een toepassing met het certificaat en een service Settings.xml configuratiebestand injecteren.
-   Versleutelde waarden buiten Settings.xml lezen door te ontsleutelen met hetzelfde certificaat uitwisselen.

>[!Note]
>Meer informatie over [geheimen in Service Fabric-toepassingen beheren](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).

### <a name="configure-security-policies-for-your-application"></a>Beveiligingsbeleid configureren voor uw toepassing
Met behulp van Azure Service Fabric-beveiliging, kunt u beveiligde toepassingen die worden uitgevoerd in het cluster onder verschillende gebruikersaccounts. Service Fabric-beveiliging kunt u ook de resources die worden gebruikt door toepassingen op het moment van implementatie onder de gebruikersaccounts--bijvoorbeeld, bestanden, mappen en certificaten beveiligen. Hierdoor waarop toepassingen worden uitgevoerd, zelfs in een gedeelde gehoste omgeving veiliger van elkaar.
De stappen omvatten:

-   Configureer het beleid voor een toegangspunt voor service-instelling.
-   PowerShell-opdrachten starten vanuit een setup-toegangspunt.
-   Console-omleiding gebruiken voor lokale foutopsporing.
-   Configureer een beleid voor servicepakketten code.
-   Wijs een beveiligingsbeleid voor toegang voor HTTP en HTTPS-eindpunten.

## <a name="secure-communication-for-services-in-azure-service-fabric-security"></a>Veilige communicatie voor services in Azure Service Fabric-beveiliging
Beveiliging is een van de belangrijkste aspecten van de communicatie. Het framework Reliable Services biedt enkele vooraf gedefinieerde communicatie stacks en hulpprogramma's die kunnen worden gebruikt om beveiliging te verbeteren.

-   [Beveiligen van een service wanneer u remoting service](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication).
-   [Beveiligen van een service wanneer u een WCF-communicatie-stack](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-secure-communication#help-secure-a-service-when-youre-using-a-wcf-based-communication-stack).

## <a name="next-steps"></a>Volgende stappen
- Raadpleeg voor algemene informatie over de clusterbeveiliging van de [een cluster maken in Azure Resource Manager-sjabloon met](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) en [Azure-portal](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal).
- Lees de informatie over [Service Fabric-clusterbeveiliging](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security).
