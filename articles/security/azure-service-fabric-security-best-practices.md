---
title: aanbevolen beveiligingsprocedures aaaAzure Service Fabric | Microsoft Docs
description: Dit artikel bevat een set met aanbevolen procedures voor beveiliging van de Azure Service Fabric.
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
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Azure Service Fabric best practices voor beveiliging
Een toepassing in Azure implementeren is snel, eenvoudig en rendabele. Voordat u cloudtoepassing in productie nuttig toohave implementeert een best practice tooassist bij het evalueren van uw toepassing met een lijst met essentiële en aanbevolen best practices.

Azure Service Fabric is een platform voor gedistribueerde systemen waarmee u eenvoudig toopackage kunt, implementeren en beheren van schaalbare en betrouwbare microservices. Service Fabric ook een oplossing voor grote uitdagingen Hallo ontwikkelen en beheren van cloudtoepassingen. Ontwikkelaars en beheerders kunnen complexe infrastructuurproblemen voorkomen en zich concentreren op het implementeren van bedrijfsspecifieke, veeleisende werkbelastingen die schaalbaar, betrouwbaar en beheerbaar zijn. 

Voor elke beste kunnen worden uitgelegd:

-   Welke beste Hallo
-   Waarom u wilt dat tooenable die best practices
-   Wat zijn Hallo resultaat als u niet tooenable Hallo aanbevolen
-   Hoe meer u tooenable Hallo best practices

Momenteel hebben we de volgende aanbevolen beveiligingsprocedures voor Azure Service Fabric Hallo:

-   Sjabloon van Azure Resource Manager (arm) en Azure Service Fabric PowerShell-Module toocreate beveiligde cluster gebruiken
-   X.509-certificaten gebruiken
-   Beveiligingsbeleid configureren
-   Beveiligingsconfiguratie voor betrouwbare Actors
-   SSL configureren voor Azure Service Fabric
-   Isolatie/netwerkbeveiliging met Azure Service Fabric
-   Een sleutelkluis voor beveiliging instellen
-   Gebruikers tooroles toewijzen


## <a name="best-practices-for-securing-your-cluster"></a>Aanbevolen procedures voor het beveiligen van uw cluster

**Grote afbeelding**

Gebruik altijd een beveiligde cluster
-   Beveiliging van cluster-certificaten gebruiken
-   Clienttoegang (Admin en alleen-lezen) – gebruik AAD

Gebruik van geautomatiseerde implementaties
-   Scripts toogenerate gebruiken, en implementeert, geheimen overschakelen
-   Houd Hallo geheimen KV, AD gebruiken voor alle andere clienttoegang
-   Er is geen human hebt toothem toegang zonder verificatie.

Houd ook rekening met de volgende Hallo:
-   DMZ's met behulp van Netwerkbeveiligingsgroepen (nsg's) maken
-   Korte inleiding servers tooRDP in het cluster virtuele machines of toomanage uw cluster gebruiken

Clusters moet beveiligde tooprevent niet-geautoriseerde gebruikers verbinding maken met cluster tooyour, vooral wanneer er productieworkloads uitgevoerd. Hoewel het mogelijk toocreate een niet-beveiligde cluster, Hierdoor kunnen de anonieme gebruikers tooconnect tooit, als deze management eindpunten toohello beschrijft openbare Internet.

Technologieën gebruikt tooimplement de scenario's. Hallo [security scenario's](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) zijn:

-   Knooppunt naar beveiliging deze beveiligt communicatie tussen Hallo virtuele machines en computers in Hallo-cluster. Dit zorgt ervoor dat alleen computers die geautoriseerd toojoin Hallo cluster zijn kunnen deelnemen die als host fungeert voor toepassingen en services in Hallo-cluster.
Clusters die worden uitgevoerd op Azure of zelfstandige clusters met Windows gebruikt een [Certificaatbeveiliging](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) of [Windows-beveiliging](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) voor Windows Server-machines.
-   Client-naar-node beveiliging deze beveiligt communicatie tussen een Service Fabric-client en de afzonderlijke knooppunten in het Hallo-cluster.
-   Op rollen gebaseerde toegangsbeheer (RBAC) - u Hallo beheerder- en client gebruikersrollen gelijktijdig Hallo met maken van het cluster door afzonderlijke identiteiten (certificaten, AAD enz.) voor elk opgeven.
-   Aanbevelingen voor beveiliging-voor Azure-clusters, het wordt aanbevolen dat u AAD beveiliging tooauthenticate clients en certificaten voor knooppunt naar beveiliging.

tooconfigure hello zelfstandige cluster van Windows, Zie [instellingen configureren voor windows-cluster zelfstandige](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Gebruik Azure Resource Manager-sjablonen en Azure Service Fabric PowerShell-Module toocreate beveiligde cluster.
Een stapsgewijze handleiding helpt u bij het instellen van een beveiligde Azure Service Fabric-cluster in Azure met Azure Resource Manager is beschikbaar [hier](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Uw cluster hello Azure Resource Manager-sjabloon toocustomize gebruiken
-   Setup beheerd storage voor VM VHD 's

Hello Azure Resource Manager-sjabloon toodrive wijzigingen tooyour resourcegroep gebruiken
-   Eenvoudig Configuratiebeheer
-   Controleren

De clusterconfiguratie behandelen als Code
-   Bij het controleren van Hallo-configuraties die u kiest toodeploy grondig worden
-   Vermijd het gebruik van impliciete opdrachten tootweak uw resources rechtstreeks

Veel aspecten van Hallo [Service Fabric-toepassing lifecycle](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) kan worden geautomatiseerd. [Azure Service Fabric PowerShell-Module](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) automatiseert het algemene taken voor het implementeren, bijwerken, verwijderen en testen van Azure Service Fabric-toepassingen. Beheerd en HTTP-APIs voor app-beheer zijn ook beschikbaar.

## <a name="use-x509-certificates"></a>X.509-certificaten gebruiken
Clusters moeten altijd worden beveiligd met X.509-certificaten of Windows-beveiliging. Beveiliging alleen tijdens het maken van een cluster is geconfigureerd en is niet mogelijk tooenable beveiliging nadat Hallo-cluster is gemaakt.

Als u opgeeft een [cluster certificaat](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), Hallo-waarde van ClusterCredentialType tooX509 niet instellen. Als u een servercertificaat voor externe verbindingen opgeeft, stelt u Hallo ServerCredentialType tooX509.

-   Certificaten worden gebruikt in clusters met productieworkloads moeten worden gemaakt met een juist geconfigureerde service voor Windows Server-certificaat of verkregen van een erkende certificeringsinstantie (CA).
-   Gebruik nooit een tijdelijke en certificaten in productie die zijn gemaakt met de hulpprogramma's zoals MakeCert.exe testen.
-   U kunt een zelfondertekend certificaat gebruiken, maar u moet alleen doen voor testclusters en niet in de productieomgeving.

Als het Hallo-cluster is niet-beveiligd. Iedereen kan anoniem verbinding maken en beheerbewerkingen uitvoeren. Productieclusters moeten dus altijd worden beveiligd met X.509-certificaten of Windows-beveiliging.

hoe meer tooenable certificaten in service fabric-cluster ziet, toolearn [toevoegen of verwijderen van certificaten voor een service fabric-cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Beveiligingsbeleid configureren
Service Fabric kunt u ook beveiligde Hallo resources die worden gebruikt door toepassingen op moment van implementatie onder Hallo gebruikersaccounts--Hallo bijvoorbeeld, bestanden, mappen en certificaten. Hierdoor waarop toepassingen worden uitgevoerd, zelfs in een gedeelde gehoste omgeving veiliger van elkaar.

-   Gebruik van een gebruiker of groep voor Active Directory-domein: U kunt Hallo service onder Hallo referenties voor een Active Directory-gebruiker of groep account uitvoeren. Dit is van Active Directory on-premises binnen uw domein en is niet met Azure Active Directory (Azure AD). U kunt andere bronnen in Hallo-domein (bijvoorbeeld bestandsshares) die machtigingen hebben gekregen benaderen via een domeingebruiker of -groep.

-   Een beveiligingsbeleid voor toegang voor HTTP en HTTPS-eindpunten toewijzen: als u een RunAs-service voor beleid tooa toepassen en Hallo servicemanifest eindpunt resources met Hallo HTTP-protocol verklaart, moet u een SecurityAccessPolicy tooensure dat poorten toothese toegewezen opgeven eindpunten zijn correct-toegangscontrole vermeld voor Hallo RunAs-gebruikersaccount dat Hallo-service wordt uitgevoerd. Anders http.sys heeft geen toegang tot toohello service en voor het ophalen van de fouten met aanroepen van Hallo-client.
toolearn inschakelen meer beveiligingsbeleid in service fabric Zie [beveiligingsbeleid voor uw toepassing configureren](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Beveiligingsconfiguratie voor betrouwbare Actors
Service Fabric Reliable Actors is een implementatie van Hallo actor ontwerppatroon. Net als bij een ontwerppatroon software past Hallo besluit of toouse een specifiek patroon wordt gemaakt op basis van het al dan niet de probleem voor het ontwerpen van een software Hallo-patroon.

Algemene richtlijnen, moet u overwegen Hallo actor patroon toomodel uw probleem of scenario als:
-   De ruimte van uw probleem betrekking heeft op een groot aantal (duizendtallen of meer) van kleine, onafhankelijke en geïsoleerde eenheden van de status en logica.
-   U toowork met één thread-objecten die geen aanzienlijke interactie met externe onderdelen, waaronder status opvragen van een set die vereist is.
-   Uw actor-exemplaren niet aanroepfuncties met onvoorspelbare vertragingen worden geblokkeerd door uitgifte van i/o-bewerkingen.

In Service Fabric actoren zijn geïmplementeerd in Hallo Reliable Actors framework: een toepassing op basis van actor-patroon framework gebouwd boven [Service Fabric Reliable Services](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Elke betrouwbare Actor-service die u schrijft is daadwerkelijk een gepartitioneerde, stateful betrouwbare Service.
Elke actor is gedefinieerd als een exemplaar van een actortype, identieke toohello manier .NET-object is een exemplaar van een .NET-type. Bijvoorbeeld, kan er een actortype dat Hallo-functionaliteit van een rekenmachine implementeert en er zijn veel actoren van dat type die worden gedistribueerd op verschillende knooppunten in een cluster. Elke dergelijke actor wordt uniek geïdentificeerd door een actor-ID.

[Replicator beveiligingsconfiguraties](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) gebruikte toosecure Hallo-communicatiekanaal dat wordt gebruikt tijdens de replicatie zijn. Dit betekent dat services elkaars replicatieverkeer, om te garanderen dat Hallo-gegevens die maximaal beschikbaar is ook beveiligde kunnen niet zien. Standaard wordt een lege beveiligingsconfiguratiesectie voorkomen dat replicatiebeveiliging.
Configuraties voor replicator configureren Hallo replicator die verantwoordelijk is voor het maken van Hallo Actor State-Provider staat maximaal betrouwbare.

## <a name="configure-ssl-for-azure-service-fabric"></a>SSL configureren voor Azure Service Fabric

Server-verificatie: [worden geverifieerd](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) Hallo cluster management eindpunten tooa management-client, zodat hello Beheerclient weet het echte cluster toohello communiceert. Dit certificaat biedt ook een [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) voor Hallo HTTPS beheer-API en voor Service Fabric Explorer via HTTPS.
U moet een aangepaste domeinnaam voor uw cluster. Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, hello onderwerpnaam van het certificaat moet overeenkomen met Hallo aangepaste domeinnaam die u voor uw cluster gebruikt.

tooconfigure SSL voor een toepassing, moet u eerst tooget een SSL-certificaat dat is ondertekend door een certificeringsinstantie (CA), een vertrouwde derde die certificaten voor dit doel verleent. Als u nog geen een, moet u tooobtain van een bedrijf dat SSL-certificaten verkoopt.

Hallo-certificaat moet voldoen aan Hallo volgens de vereisten voor SSL-certificaten in Azure:
-   Hallo-certificaat moet een persoonlijke sleutel bevatten.
-   Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.
-   Hallo onderwerpnaam van het certificaat moet overeenkomen met Hallo domein gebruikt tooaccess Hallo-cloudservice. U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo cloudapp.net domein. U moet een aangepast domein naam toouse verkrijgen wanneer toegang krijgen tot uw service. Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, de onderwerpnaam van het Hallo-certificaat moet overeenkomen met Hallo aangepast domein naam die wordt gebruikt tooaccess uw toepassing. Bijvoorbeeld, als uw aangepaste domeinnaam contoso.com is u zou een certificaat aanvragen van uw Certificeringsinstantie voor **. contoso.com** of **www.contoso.com.**
-   Hallo-certificaat moet ten minste 2048-bits codering gebruiken.

HTTP is onveilig en onderwerp tooeavesdropping aanvallen omdat hello gegevens worden overgebracht van Hallo web browser toohello-webserver of tussen de andere eindpunten worden verzonden als leesbare tekst. Dit betekent dat aanvallers kunnen onderscheppen en gevoelige gegevens, zoals creditcardgegevens en account aanmeldingen bekijken. Wanneer gegevens worden verzonden of geboekt via een browser met gebruik van HTTPS, SSL zorgt ervoor dat dergelijke gegevens versleuteld en beveiligd tegen worden onderschept.

toolearn meer ziet, [SSL configureren voor azure-toepassing](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Isolatie/netwerkbeveiliging met Azure Service Fabric
Gebruik [Azure Resource Manager (ARM) sjabloon](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) als voorbeeld voor het instellen van een drie nodetype beveiligde cluster en toocontrol Hallo binnenkomend en uitgaand netwerkverkeer met behulp van Netwerkbeveiligingsgroepen.

Hallo sjabloon heeft een Netwerkbeveiligingsgroep voor elk Hallo virtuele machine scale set(VMSS) toocontrol Hallo binnenkomend en uitgaand verkeer Hallo VMSS. Standaard Hallo regels zijn ingesteld tooallow die alle Hallo verkeer dat vereist is door Hallo system services en Hallo toepassing poorten in Hallo-sjabloon. Bekijk deze regels en breng wijzigingen toofit toevoegen voor uw behoeften, waaronder nieuwe bestanden voor uw toepassingen.

Zie voor meer informatie [Azure Service Fabric: algemene scenario's voor netwerken](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Een sleutelkluis voor beveiliging instellen
Certificaten worden gebruikt in Service Fabric tooprovide verificatie en versleuteling toosecure verschillende aspecten van een cluster en de toepassingen.

Service Fabric gebruikt x.509-certificaten toosecure een cluster en beveiligingsfuncties van toepassing. U Sleutelkluis te gebruiken[certificaten beheren](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) voor Service Fabric-clusters in Azure. Wanneer een cluster wordt geïmplementeerd in Azure, worden de hello Azure-resourceprovider die verantwoordelijk is voor het maken van Service Fabric-clusters certificaten ophaalt uit Sleutelkluis en installeert ze op Hallo cluster virtuele machines.

relatie tussen Hallo [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), een service fabric-cluster en hello Azure-resourceprovider die gebruikmaakt van certificaten die zijn opgeslagen in een sleutelkluis bij het maken van een cluster.

**Een resourcegroep maken** Hallo eerste stap is het een resourcegroep specifiek voor uw sleutelkluis toocreate. Het is raadzaam dat u de sleutelkluis Hallo in een eigen resourcegroep geplaatst. Deze actie kunt u Hallo berekenings- en resourcegroepen, met inbegrip van Hallo resourcegroep die uw Service Fabric-cluster bevat zonder verlies van uw sleutels en geheimen verwijderen. Hallo-resourcegroep met de sleutelkluis moet Hallo dezelfde regio bevinden als het Hallo-cluster dat wordt gebruikt.

**Een sleutelkluis maken in de nieuwe resourcegroep Hallo** hello sleutelkluis moet zijn ingeschakeld voor implementatie tooallow Hallo compute resource provider tooget certificaten van deze en installeer deze op de virtuele machine-exemplaren.
hoe meer tooset van Azure sleutelkluis ziet, toolearn [aan de slag met Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Gebruikers rollen toewijzen
Nadat u Hallo toepassingen toorepresent uw cluster hebt gemaakt, uw gebruikers toewijzen toohello rollen die worden ondersteund door Service Fabric: alleen-lezen en de beheerder. U kunt Hallo rollen toewijzen met behulp van Hallo klassieke Azure-portal.

>[!Note]
> Zie voor meer informatie over functies in Service Fabric [toegangsbeheer op basis van rollen voor Service Fabric-clients](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Azure Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa zijn [Service Fabric-cluster](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): beheerder en gebruiker. Toegangsbeheer kunt Hallo beheerder toolimit toegang toocertain cluster clusterbewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken.

## <a name="next-steps"></a>Volgende stappen
- Instellen van uw Service Fabric [ontwikkelomgeving](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started).
- Meer informatie over [Service Fabric-ondersteuningsopties](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

