---
title: -Microsoft Threat Modeling Tool - aaaAuthorization Azure | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>Beveiliging Frame: Autorisatie | Oplossingen 
| Product/Service | Artikel |
| --------------- | ------- |
| **Een grens machine vertrouwensrelatie** | <ul><li>[Zorg ervoor dat de juiste ACL's geconfigureerde toorestrict niet-geautoriseerde toegang toodata op Hallo apparaat zijn](#acl-restricted-access)</li><li>[Zorg ervoor dat gevoelige gebruikersspecifieke toepassingsinhoud wordt opgeslagen in gebruikersprofiel directory](#sensitive-directory)</li><li>[Zorg ervoor dat Hallo geïmplementeerde toepassingen worden uitgevoerd met de minimaal benodigde bevoegdheden](#deployed-privileges)</li></ul> |
| **Webtoepassing** | <ul><li>[Sequentiële volgorde afdwingen bij het verwerken van zakelijke logica stromen](#sequential-logic)</li><li>[Snelheidsbeperking mechanisme tooprevent opsomming implementeren](#rate-enumeration)</li><li>[Zorg ervoor dat de juiste autorisatie geïmplementeerd is en principe van minimale bevoegdheden wordt gevolgd.](#principle-least-privilege)</li><li>[Zakelijke logica en resource toegang autorisatiebeslissingen moeten niet zijn gebaseerd op parameters van de binnenkomende aanvraag](#logic-request-parameters)</li><li>[Zorg ervoor dat de inhoud en resources zijn niet inventariseerbare of toegankelijk via de geforceerde bladeren](#enumerable-browsing)</li></ul> |
| **Database** | <ul><li>[Zorg ervoor dat minst bevoegde accounts gebruikte tooconnect tooDatabase server](#privileged-server)</li><li>[Rij Level Security-RLS tooprevent tenants toegang tot elkaars gegevens implementeren](#rls-tenants)</li><li>[De rol sysadmin mag alleen geldige nodig gebruikers hebben.](#sysadmin-users)</li></ul> |
| **IoT-Cloudgateway** | <ul><li>[TooCloud Gateway verbinding maken met de minste bevoegdheden tokens](#cloud-least-privileged)</li></ul> |
| **Azure Event Hub** | <ul><li>[Een verzenden alleen-lezen machtigingen SAS-sleutel gebruiken voor het genereren van apparaattokens](#sendonly-sas)</li><li>[Gebruik geen toegangstokens die directe toegang toohello Event Hub opgeven](#access-tokens-hub)</li><li>[Verbinding maken met tooEvent Hub met SAS-codes dat Hallo minimale machtigingen vereist](#sas-minimum-permissions)</li></ul> |
| **Azure Documentdb** | <ul><li>[Gebruik resource tokens tooconnect tooDocumentDB indien mogelijk](#resource-docdb)</li></ul> |
| **Vertrouwensgrenzen van Azure** | <ul><li>[Inschakelen van fijnmazig access management tooAzure abonnement met RBAC](#grained-rbac)</li></ul> |
| **Service Fabric-Vertrouwensgrenzen** | <ul><li>[Beperken van de client toegang toocluster bewerkingen met RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[Veld beveiligingsniveau en beveiliging modellering uitgevoerd indien vereist](#modeling-field)</li></ul> |
| **Dynamics CRM-Portal** | <ul><li>[Beveiliging modellering van portal accounts Houd in gedachten dat beveiligingsmodel Hallo voor Hallo portal wijkt af van de rest van CRM Hallo uitvoeren](#portal-security)</li></ul> |
| **Azure Storage** | <ul><li>[Fijnmazig toestemming van een bereik van entiteiten in de Azure-tabelopslag](#permission-entities)</li><li>[Op rollen gebaseerde toegangsbeheer (RBAC) tooAzure storage-account met Azure Resource Manager inschakelen](#rbac-azure-manager)</li></ul> |
| **Mobiele clients** | <ul><li>[Impliciete jailbreakdetectie of detectie basismappen implementeren](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[Van zwakke klassenverwijzing in WCF](#weak-class-wcf)</li><li>[WCF-implementeren Authorization control](#wcf-authz)</li></ul> |
| **Web-API** | <ul><li>[Juiste autorisatiemechanismen in ASP.NET Web API implementeren](#authz-aspnet)</li></ul> |
| **IoT-apparaat** | <ul><li>[Autorisatie controles uitvoeren in Hallo-apparaat als deze ondersteuning biedt voor verschillende acties die verschillende machtigingsniveaus vereisen](#device-permission)</li></ul> |
| **Veld IoT Gateway** | <ul><li>[Autorisatie controles uitvoeren in Hallo Veldgateway als deze ondersteuning biedt voor verschillende acties die verschillende machtigingsniveaus vereisen](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>Zorg ervoor dat de juiste ACL's geconfigureerde toorestrict niet-geautoriseerde toegang toodata op Hallo apparaat zijn

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat de juiste ACL's geconfigureerde toorestrict niet-geautoriseerde toegang toodata op Hallo apparaat zijn|

## <a id="sensitive-directory"></a>Zorg ervoor dat gevoelige gebruikersspecifieke toepassingsinhoud wordt opgeslagen in gebruikersprofiel directory

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat gevoelige gebruikersspecifieke toepassingsinhoud wordt opgeslagen in gebruikersprofiel directory. Dit is tooprevent meerdere gebruikers Hallo machine toegang tot elkaars gegevens.|

## <a id="deployed-privileges"></a>Zorg ervoor dat Hallo geïmplementeerde toepassingen worden uitgevoerd met de minimaal benodigde bevoegdheden

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Een grens machine vertrouwensrelatie | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat de toepassing hello geïmplementeerd met minimale bevoegdheden wordt uitgevoerd. |

## <a id="sequential-logic"></a>Sequentiële volgorde afdwingen bij het verwerken van zakelijke logica stromen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | In volgorde tooverify die deze fase via is uitgevoerd door een legitieme gebruiker u wilt tooenforce Hallo toepassing tooonly zakelijke logica processtromen in opeenvolgende volgorde, met alle stappen in de realistische menselijke tijd wordt verwerkt en niet verwerken volgorde, wordt overgeslagen stappen, verwerkt de stappen van een andere gebruiker of transacties te snel verzonden.|

## <a id="rate-enumeration"></a>Snelheidsbeperking mechanisme tooprevent opsomming implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Zorg ervoor dat gevoelige id willekeurige's. Controle van de CAPTCHA op anonieme's implementeren. Zorg ervoor dat fout en uitzondering niet specifieke gegevens bekendmaken moeten|

## <a id="principle-least-privilege"></a>Zorg ervoor dat de juiste autorisatie geïmplementeerd is en principe van minimale bevoegdheden wordt gevolgd.

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Hallo principe betekent dat een gebruikersaccount geeft alleen de bevoegdheden die de essentiële toothat gebruikers werkuren. Bijvoorbeeld, een back-gebruiker geen tooinstall software nodig: daarom Hallo back-gebruiker beschikt over rechten alleen toorun back-ups en back-up-gerelateerde toepassingen. Andere bevoegdheden, zoals het installeren van nieuwe software, worden geblokkeerd. Hallo geldt ook tooa pc-gebruiker die meestal werkt in een normaal gebruikersaccount en opent een account met machtigingen, een wachtwoord beveiligd (dat wil zeggen, een superuser) alleen wanneer Hallo situatie absoluut vraagt. </p><p>Dit principe kan ook worden toegepast tooyour-webtoepassingen. In plaats van alleen afhankelijk van de op rollen gebaseerde verificatiemethoden met behulp van sessies, in plaats daarvan willen we tooassign bevoegdheden toousers door middel van een systeem met verificatie op basis van de Database. We sessies in volgorde tooidentify nog steeds gebruiken als Hallo gebruiker is aangemeld correct nu alleen in plaats van die gebruiker met een specifieke rol die we toe te wijzen met bevoegdheden tooverify welke acties hij bevoorrechte tooperform op Hallo systeem toewijzen. Een groot pro van deze methode is ook, wanneer een gebruiker toobe minder bevoegdheden die uw wijzigingen worden toegepast op Hallo snel heeft omdat Hallo toewijzen is niet afhankelijk Hallo-sessie die anders tooexpire eerst had toegewezen.</p>|

## <a id="logic-request-parameters"></a>Zakelijke logica en resource toegang autorisatiebeslissingen moeten niet zijn gebaseerd op parameters van de binnenkomende aanvraag

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Wanneer u controleert of een gebruiker met beperkte toegang tooreview is verwerkt bepaalde gegevens, Hallo toegang beperkingen moet serverzijde. Hallo userID moet worden opgeslagen in een sessievariabele aanmelden en moet de gebruikte tooretrieve gebruikersgegevens uit de database Hallo |

### <a name="example"></a>Voorbeeld
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
Nu kan een aanvaller mogelijk niet knoeien en Hallo toepassing bewerking niet wijzigen omdat het Hallo-id voor het ophalen van gegevens Hallo verwerkt serverzijde.

## <a id="enumerable-browsing"></a>Zorg ervoor dat de inhoud en resources zijn niet inventariseerbare of toegankelijk via de geforceerde bladeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Webtoepassing | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Gevoelige statisch en configuratie-bestanden moeten niet worden opgeslagen in Hallo Webroot. Voor de inhoud niet vereist toobe openbare inhoud op de juiste toegang besturingselementen moeten worden toegepast of de verwijdering van Hallo zelf.</p><p>Ook wordt geforceerde bladeren meestal gecombineerd met Brute kracht technieken toogather informatie door te proberen tooaccess zoveel URL's als mogelijke tooenumerate mappen en bestanden op een server. Aanvallers kunnen controleren voor alle variaties van vaak bestaande bestanden. Een zoekbewerking wachtwoord zou bijvoorbeeld bestanden met inbegrip van psswd.txt, password.htm password.dat en andere variaties omvatten.</p><p>toomitigate dit mogelijkheden voor de detectie van beveiligingsaanvallen probeert moeten worden opgenomen.</p>|

## <a id="privileged-server"></a>Zorg ervoor dat minst bevoegde accounts gebruikte tooconnect tooDatabase server

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [SQL-Database machtigingen hiërarchie](https://msdn.microsoft.com/library/ms191465), [securables voor SQL-database](https://msdn.microsoft.com/library/ms190401) |
| **Stappen** | Minst bevoegde accounts moet gebruikte tooconnect toohello database. Aanmelding van de toepassing moet worden beperkt in Hallo-database en moet alleen geselecteerde opgeslagen procedures worden uitgevoerd. Aanmelding van de toepassing moet hebben geen directe tabeltoegang. |

## <a id="rls-tenants"></a>Rij Level Security-RLS tooprevent tenants toegang tot elkaars gegevens implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | SQL Azure, OnPrem |
| **Kenmerken**              | SQL-versie - V12, SQL-versie - MsSQL2016 |
| **Verwijzingen**              | [SQL Server-beveiliging voor rijniveau (RLS)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **Stappen** | <p>Beveiliging op rijniveau kunt klanten toocontrol toegang toorows in een databasetabel op basis van kenmerken Hallo van Hallo gebruiker (bijv, groep lidmaatschap of -uitvoering context) van een query uit te voeren.</p><p>Rij-Level Security (RLS) vereenvoudigt het Hallo-ontwerp en de codering van beveiliging in uw toepassing. RLS kunt u tooimplement beperkingen voor gegevenstoegang rij. Bijvoorbeeld ervoor te zorgen dat werknemers toegang krijgen tot alleen die rijen met gegevens die relevante tootheir afdeling zijn of een bedrijf van de klant gegevens toegang tooonly Hallo gegevens relevante tootheir beperken.</p><p>Hallo toegang beperking logica is gevonden in de databaselaag Hallo in plaats van opslag van Hallo-gegevens in een andere toepassingslaag. elke keer dat de toegang tot die gegevens van elke categorie wordt uitgevoerd, past Hallo databasesysteem Hallo toegangsbeperkingen. Hierdoor Hallo beveiligingssysteem betrouwbaarder en robuuste doordat Hallo surface area van Hallo beveiligingssysteem.</p><p>|

Houd er rekening mee dat RLS als een out-of-the-box databasefunctie is van toepassing alleen tooSQL Server vanaf 2016 en Azure SQL-database. Als Hallo out-of-the-box-RLS functie is niet geïmplementeerd, er moet voor worden gezorgd dat de gegevenstoegang beperkt met behulp van weergaven en Procedures is

## <a id="sysadmin-users"></a>De rol sysadmin mag alleen geldige nodig gebruikers hebben.

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Database | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [SQL-Database machtigingen hiërarchie](https://msdn.microsoft.com/library/ms191465), [securables voor SQL-database](https://msdn.microsoft.com/library/ms190401) |
| **Stappen** | Leden van de vaste serverrol SysAdmin Hallo moeten zeer beperkt en nooit accounts die worden gebruikt door toepassingen bevatten.  Bekijk Hallo lijst met gebruikers in rol Hallo en verwijder alle overbodige accounts|

## <a id="cloud-least-privileged"></a>TooCloud Gateway verbinding maken met de minste bevoegdheden tokens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-Cloudgateway | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Keuze van de gateway - Azure IoT Hub |
| **Verwijzingen**              | [Toegangsbeheer IOT-Hub](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **Stappen** | Minimale bevoegdheden machtigingen toovarious onderdelen die verbinding maken met tooCloud Gateway (IoT Hub) bieden. Typisch voorbeeld is: apparaat/inrichting component registryread schrijftijd gebruikt, gebeurtenis-Processor (ASA) maakt gebruik van Service verbinding maken. Afzonderlijke apparaten verbinding maken met de referenties van het apparaat|

## <a id="sendonly-sas"></a>Een verzenden alleen-lezen machtigingen SAS-sleutel gebruiken voor het genereren van apparaattokens

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Event Hub | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie en beveiliging model overzicht van Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Stappen** | Een SAS-sleutel is gebruikte toogenerate afzonderlijk apparaattokens. Een SAS-sleutel verzenden alleen-lezen machtigingen tijdens het genereren van het Hallo-apparaattoken gebruiken voor een opgegeven uitgever|

## <a id="access-tokens-hub"></a>Gebruik geen toegangstokens die directe toegang toohello Event Hub opgeven

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Event Hub | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie en beveiliging model overzicht van Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Stappen** | Een token dat directe toegang toohello event hub verleent mogen niet worden toegekend toohello apparaat. Met behulp van een minstens een token voor Hallo-apparaat dat toegang alleen tooa publisher te zou identificeren en deze afgekeurde als gevonden toobe een rogue of aangetast apparaat.|

## <a id="sas-minimum-permissions"></a>Verbinding maken met tooEvent Hub met SAS-codes dat Hallo minimale machtigingen vereist

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Event Hub | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Verificatie en beveiliging model overzicht van Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Stappen** | Minimale bevoegdheden machtigingen toovarious backend-toepassingen die verbinding toohello Event Hub maken bieden. Afzonderlijke SAS-sleutels voor elke back-endtoepassing genereren en leveren alleen Hallo vereist machtigingen - toothem verzenden, ontvangen of beheren.|

## <a id="resource-docdb"></a>Gebruik resource tokens tooconnect tooCosmos DB indien mogelijk

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Documentdb | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Een resource-token is gekoppeld aan een resource van de machtiging DocumentDB en opnamen Hallo relatie tussen Hallo gebruiker van een database en het Hallo-machtiging die de gebruiker heeft voor een specifieke bron DocumentDB-toepassing (bijvoorbeeld verzameling en het document). Gebruik altijd een resource token tooaccess hello DocumentDB als Hallo-client niet kan vertrouwd worden met de verwerking van sleutels in master of alleen-lezen - als een eindgebruikerstoepassing zoals een mobiele of bureaubladtoepassingen client. Gebruik hoofdsleutel of alleen-lezen sleutels van de back-end-toepassingen die deze sleutels veilig kunnen opslaan.|

## <a id="grained-rbac"></a>Inschakelen van fijnmazig access management tooAzure abonnement met RBAC

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Vertrouwensgrenzen van Azure | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **Stappen** | Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over geavanceerd toegangsbeheer voor Azure. Met RBAC kunt verleent u alleen Hallo hoeveelheid toegang die gebruikers nodig tooperform hun werk hebben.|

## <a id="cluster-rbac"></a>Beperken van de client toegang toocluster bewerkingen met RBAC

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Service Fabric-Vertrouwensgrenzen | 
| **SDL-fase**               | Implementatie |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | Omgeving - Azure |
| **Verwijzingen**              | [Toegangsbeheer op basis van rollen voor Service Fabric-clients](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **Stappen** | <p>Azure Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn: beheerder en gebruiker. Toegangsbeheer kunt Hallo beheerder toolimit toegang toocertain cluster clusterbewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken.</p><p>Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.</p><p>U opgeven Hallo twee client rollen (administrator en client) gelijktijdig Hallo met maken van het cluster door afzonderlijke certificaten voor elk.</p>|

## <a id="modeling-field"></a>Veld beveiligingsniveau en beveiliging modellering uitgevoerd indien vereist

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Veld beveiligingsniveau en beveiliging modellering uitgevoerd indien vereist|

## <a id="portal-security"></a>Beveiliging modellering van portal accounts Houd in gedachten dat beveiligingsmodel Hallo voor Hallo portal wijkt af van de rest van CRM Hallo uitvoeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Dynamics CRM-Portal | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Beveiliging modellering van portal accounts Houd in gedachten dat beveiligingsmodel Hallo voor Hallo portal wijkt af van de rest van CRM Hallo uitvoeren|

## <a id="permission-entities"></a>Fijnmazig toestemming van een bereik van entiteiten in de Azure-tabelopslag

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | StorageType - tabel |
| **Verwijzingen**              | [Hoe toodelegate toegang krijgen tot tooobjects in uw Azure storage-account via SAS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **Stappen** | In bepaalde zakelijke scenario's zijn Azure Table Storage vereist toostore gevoelige gegevens die caters toodifferent partijen. Bijvoorbeeld gevoelige gegevens die betrekking hebben toodifferent landen. In dergelijke gevallen kan SAS handtekeningen worden samengesteld door te geven Hallo partitie en rij sleutelbereiken, zodat een gebruiker toegang heeft tot gegevens specifieke tooa bepaald land.| 

## <a id="rbac-azure-manager"></a>Op rollen gebaseerde toegangsbeheer (RBAC) tooAzure storage-account met Azure Resource Manager inschakelen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Azure Storage | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [Hoe toosecure uw storage-account met op rollen gebaseerde toegangsbeheer (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **Stappen** | <p>Als u een nieuw opslagaccount maakt, selecteert u een van de klassieke weergave of Azure Resource Manager-implementatiemodel. Hallo klassieke model van het maken van resources in Azure kunt alleen ofwel volledig, ofwel toegang toohello abonnement en op zijn beurt Hallo storage-account.</p><p>Met hello Azure Resource Manager-model plaatst u Hallo storage-account in een resource group en beheer toegang toohello management vlak van het specifieke storage-account met Azure Active Directory. Bijvoorbeeld, kunt u specifieke gebruikers geven Hallo mogelijkheid tooaccess Hallo toegangscodes voor opslag, terwijl andere gebruikers informatie over Hallo storage-account weergeven kunnen, maar heeft geen toegang de opslagaccountsleutels Hallo tot.</p>|

## <a id="rooting-detection"></a>Impliciete jailbreakdetectie of detectie basismappen implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Mobiele clients | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Toepassing moet een eigen configuratie- en gebruikersbestanden gegevens in de aanvraag als telefoon is geroot of heeft een jailbreak beveiligt. Basismappen/geroot op te splitsen impliceert onbevoegde toegang, welke normale gebruikers niet op hun eigen telefoons. Daarom moet toepassing impliciete detectielogica hebben voor opstarten van de toepassing, toodetect als Hallo telefoon is geroot.</p><p>Hallo detectielogica voor smartcardlezers kan eenvoudig toegang krijgen tot bestanden die normaal gesproken alleen basis-gebruiker toegang, bijvoorbeeld heeft:</p><ul><li>/System/App/SuperUser.APK</li><li>/ sbin/su</li><li>/System/bin/su</li><li>/System/xbin/su</li><li>/Data/Local/xbin/su</li><li>/Data/local/bin/su</li><li>/System/SD/xbin/su</li><li>/System/bin/failsafe/su</li><li>/Data/Local/su</li></ul><p>Als de toepassing hello toegang heeft tot deze bestanden, geeft aan dat de toepassing hello als hoofdgebruiker wordt uitgevoerd.</p>|

## <a id="weak-class-wcf"></a>Van zwakke klassenverwijzing in WCF

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, NET Framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | <p>Hallo wordt een verwijzing zwakke klasse, dat een aanvaller kan tooexecute niet-geautoriseerde code gebruikt. Hallo programma verwijst naar een gebruiker gedefinieerde klasse die is niet uniek geïdentificeerd. Wanneer deze licht geïdentificeerde klasse, Hallo CLR type loader zoekt Hallo klasse in de volgende locaties in Hallo Hallo wordt geladen in .NET opgegeven volgorde:</p><ol><li>Assembly van het type Hallo Hallo bekend is, Hallo loader zoekopdrachten Hallo van het configuratiebestand omleiding locaties, GAC, Hallo huidige assembly met configuratie-informatie als basismap van de toepassing hello</li><li>Als de assembly Hallo onbekend is, Hallo Hallo loader zoekopdrachten huidige assembly van mscorlib en Hallo locatie geretourneerd door Hallo TypeResolve gebeurtenis-handler</li><li>Deze zoekvolgorde CLR kan worden gewijzigd met hooks zoals Hallo mechanisme voor het doorsturen van het Type en Hallo AppDomain.TypeResolve gebeurtenis</li></ol><p>Wanneer een hacker Hallo CLR-zoekvolgorde door het maken van een andere klasse Hallo dezelfde naam en die Hallo CLR eerst laadt plaatsen in een alternatieve locatie, Hallo CLR wordt per ongeluk Hallo aanvaller opgegeven code uitvoeren</p>|

### <a name="example"></a>Voorbeeld
Hallo `<behaviorExtensions/>` element van Hallo WCF-configuratiebestand onderstaande Hiermee geeft u WCF-tooadd een aangepaste gedrag klasse tooa bepaalde WCF-extensie.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
Met behulp van de FQDN-namen (sterk) unieke wijze identificeert een en verhoogt bovendien beveiliging van uw systeem. Volledig gekwalificeerde assembly-namen gebruiken bij het registreren van typen in Hallo machine.config en app.config-bestanden.

### <a name="example"></a>Voorbeeld
Hallo `<behaviorExtensions/>` element van Hallo WCF-configuratiebestand onderstaande Hiermee geeft u WCF tooadd aangepaste gedrag sterk verwezen klasse tooa bepaalde WCF-extensie.
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF-implementeren Authorization control

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | WCF | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, NET Framework 3 |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Stappen** | <p>Deze service wordt niet gebruikt voor een besturingselement voor autorisatie. Wanneer een client een bepaalde WCF-service wordt aangeroepen, biedt WCF verschillende autorisatie-schema's die controleren dat die Hallo aanroeper heeft een machtiging tooexecute Hallo servicemethode op Hallo-server. Als autorisatie besturingselementen zijn niet ingeschakeld voor de WCF-services, kunt een geverifieerde gebruiker uitbreiding van bevoegdheden te bereiken.</p>|

### <a name="example"></a>Voorbeeld
Hallo na configuratie wordt WCF toonot selectievakje Hallo autorisatieniveau van Hallo client wanneer Hallo-service wordt uitgevoerd:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Gebruik een service autorisatie schema tooverify die de aanroeper van methode Hallo Hallo is dus geautoriseerde toodo. WCF beschikt over twee modi en kunt u Hallo definitie van een aangepaste autorisatie-schema. Hallo UseWindowsGroups modus Windows-rollen en gebruikers en Hallo UseAspNetRoles modus gebruikt een provider van een ASP.NET-functie, zoals SQL Server, tooauthenticate.

### <a name="example"></a>Voorbeeld
Hallo wordt volgende configuratie WCF toomake ervoor dat Hallo client maakt deel uit van de groep Administrators Hallo voordat Hallo toevoegen-service wordt uitgevoerd:
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
Hallo-service wordt vervolgens gedeclareerd als Hallo volgende:
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>Juiste autorisatiemechanismen in ASP.NET Web API implementeren

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Web-API | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemeen, MVC5 |
| **Kenmerken**              | N.V.T. identiteitsprovider Provider - ADFS, Identity - Azure AD |
| **Verwijzingen**              | [Verificatie en autorisatie in ASP.NET Web-API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **Stappen** | <p>Gegevens over de serverfunctie voor gebruikers van de toepassing hello kan worden afgeleid van Azure AD of AD FS-claims als Hallo toepassing afhankelijk van deze als id-provider is of Hallo toepassing zelf kan het opgegeven. In al deze gevallen moet Hallo aangepaste autorisatie-uitvoering Hallo rol gebruikersgegevens valideren.</p><p>Gegevens over de serverfunctie voor gebruikers van de toepassing hello kan worden afgeleid van Azure AD of AD FS-claims als Hallo toepassing afhankelijk van deze als id-provider is of Hallo toepassing zelf kan het opgegeven. In al deze gevallen moet Hallo aangepaste autorisatie-uitvoering Hallo rol gebruikersgegevens valideren.</p>

### <a name="example"></a>Voorbeeld
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
Alle domeincontrollers Hallo en actiemethoden die tooprotected moet moeten gedecoreerd worden met hierboven kenmerk.
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>Autorisatie controles uitvoeren in Hallo-apparaat als deze ondersteuning biedt voor verschillende acties die verschillende machtigingsniveaus vereisen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | IoT-apparaat | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | <p>Hallo apparaat dienen Hallo aanroeper toocheck toe te staan als Hallo aanroeper Hallo vereist machtigingen tooperform Hallo actie aangevraagd heeft. Voor bijvoorbeeld kunt spreek Hallo apparaat is een Smart Lock deur die kan worden gecontroleerd vanuit Hallo cloud, plus het functies zoals het op afstand vergrendelen van klep Hallo biedt.</p><p>Hallo Smart Lock van klep biedt ontgrendelen functionaliteit, alleen wanneer iemand is fysiek wordt geleverd in de buurt Hallo deur met een kaart. In dit geval moet Hallo-implementatie van de externe opdracht Hallo en besturingselement worden gedaan zodanig dat geen een functionaliteit toounlock Hallo deur biedt omdat Hallo cloudgateway niet geautoriseerde toosend deur Hallo toounlock van een opdracht.</p>|

## <a id="field-permission"></a>Autorisatie controles uitvoeren in Hallo Veldgateway als deze ondersteuning biedt voor verschillende acties die verschillende machtigingsniveaus vereisen

| Titel                   | Details      |
| ----------------------- | ------------ |
| **Onderdeel**               | Veld IoT Gateway | 
| **SDL-fase**               | Ontwikkelen |  
| **Van toepassing technologieën** | Algemene |
| **Kenmerken**              | N.v.t.  |
| **Verwijzingen**              | N.v.t.  |
| **Stappen** | Hallo Veldgateway dienen Hallo aanroeper toocheck toe te staan als Hallo aanroeper Hallo vereist machtigingen tooperform Hallo actie aangevraagd heeft. Voor bijvoorbeeld moet er andere machtigingen voor een gebruiker met beheerdersrechten gebruikt interface/API tooconfigure een veld gateway v/s-apparaten die verbinding maken tooit.|
