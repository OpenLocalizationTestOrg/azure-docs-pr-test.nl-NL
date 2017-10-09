---
title: aaaSupported brontypen via Azure resourcestatus | Microsoft Docs
description: Ondersteunde resourcetypen via Azure resourcestatus
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Status van resourcetypen en controleert in Azure resourcestatus
Hieronder volgt een volledige lijst met alle Hallo controles uitgevoerd via een resourcestatus door resourcetypen.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Uitgevoerde controles|
|---|
|<ul><li>Alle Hallo Cache-knooppunten actief zijn en uitgevoerd?</li><li>Hallo Cache kan worden bereikt vanaf binnen Hallo datacenter?</li><li>Hallo die cache Hallo kunt u het maximum aantal verbindingen bereikt heeft?</li><li> Heeft het beschikbare geheugen uitgeput door Hallo-cache? </li><li>Hallo Cache korte tijd een groot aantal pagina's?</li><li>Cache is zwaar belast worden Hallo?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Uitgevoerde controles|
|---|
|<ul> <li>Een van de eindpunten Hallo is gestopt, verwijderd of niet juist geconfigureerd?</li><li>Is de aanvullende portal Hallo toegankelijk voor configuratiebewerkingen CDN?</li><li>Zijn er problemen met Hallo lopende levering van CDN-eindpunten?</li><li>Gebruikers Hallo-configuratie van hun bronnen CDN wijzigen?</li><li>Configuratiewijzigingen doorgeven snelheid Hallo verwacht?</li><li>Kunnen gebruikers Hallo CDN-configuratie met behulp van hello Azure-portal, PowerShell of Hallo API beheren?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Uitgevoerde controles|
|---|
|<ul><li>Hallo host-server actief is en wordt uitgevoerd?</li><li>Hallo host OS opstarten voltooid?</li><li>Hallo-container voor virtuele machine is ingericht en ingeschakeld?</li><li>Er is een netwerkverbinding tussen Hallo host en Hallo storage-account?</li><li>Opstarten van het Hallo van Hallo gastbesturingssysteem voltooid?</li><li>Is er lopende gepland onderhoud?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Uitgevoerde controles|
|---|
|<ul><li>Hallo-account kan worden bereikt vanaf binnen Hallo datacenter?</li><li>Is Hallo Resource Provider cognitieve Services beschikbaar?</li><li>Is cognitieve Service beschikbaar in de juiste regio Hallo Hallo?</li><li>Kan lezen bewerkingen worden uitgevoerd op opslagaccount Hallo Hallo resource metagegevens houden?</li><li>Hallo API-aanroep quotum is bereikt?</li><li>Is Hallo API-aanroep lezen-limiet bereikt?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.COMPUTE/virtualmachines
|Uitgevoerde controles|
|---|
|<ul><li>Hallo-server host deze virtuele machine omhoog en uitgevoerd?</li><li>Hallo host OS opstarten voltooid?</li><li>Hallo-container voor virtuele machine is ingericht en ingeschakeld?</li><li>Er is een netwerkverbinding tussen Hallo host en Hallo storage-account?</li><li>Opstarten van het Hallo van Hallo gastbesturingssysteem voltooid?</li><li>Is er lopende gepland onderhoud?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Uitgevoerde controles|
|---|
|<ul><li>Kunnen gebruikers verzenden taken tooData Lake Analytics in regio Hallo?</li><li>Basic-taken uitgevoerd en voltooid met succes in Hallo regio doen?</li><li>Kunnen lijst gebruikers catalogusitems in Hallo regio?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Uitgevoerde controles|
|---|
|<ul><li>Kunnen gebruikers gegevens tooData Lake Store in Hallo regio uploaden?</li><li>Kunnen gebruikers gegevens in Data Lake Store in Hallo regio downloaden?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Uitgevoerde controles|
|---|
|<ul><li>Er is een database of een verzameling aanvragen niet worden geleverd vanwege tooa DocumentDB-service niet beschikbaar zijn?</li><li>Er zijn aanvragen-document niet worden geleverd vanwege tooa DocumentDB-service niet beschikbaar zijn?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.Network/Connections
|Uitgevoerde controles|
|---|
|<ul><li>Is Hallo VPN-tunnel aangesloten?</li><li>Zijn er conflicten bij de configuratie in Hallo verbinding?</li><li>Vooraf gedeelde sleutels Hallo correct zijn geconfigureerd?</li><li>Hallo VPN-on-premises apparaat bereikbaar is?</li><li>Zijn er verschillen in Hallo IPSec/IKE-beveiligingsbeleid?</li><li>Is Hallo S2S VPN-verbinding juist is ingericht of in een foutstatus?</li><li>Is Hallo VNET-naar-VNET-verbinding juist is ingericht of in een foutstatus?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Uitgevoerde controles|
|---|
|<ul><li>Hallo VPN-gateway bereikbaar is via internet Hallo?</li><li>VPN-Gateway is in standby-modus worden Hallo?</li><li>Wordt Hallo VPN-service uitgevoerd op Hallo gateway?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Uitgevoerde controles|
|---|
|<ul><li> Kunnen de runtime-bewerkingen zoals registratie, installatie of verzenden worden uitgevoerd op Hallo naamruimte?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Uitgevoerde controles|
|---|
|<ul><li>Hallo hostbesturingssysteem actief is en wordt uitgevoerd?</li><li>Hallo workspaceCollection bereikbaar is via buiten Hallo datacenter?</li><li>Is Hallo PowerBI Resource Provider beschikbaar?</li><li>Is PowerBI-Service beschikbaar in de juiste regio Hallo Hallo?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Uitgevoerde controles|
|---|
|<ul><li>Kunnen de diagnostische gegevens bewerkingen worden uitgevoerd op Hallo cluster?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Uitgevoerde controles|
|---|
|<ul><li> Zijn er aanmeldingen toohello database?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Uitgevoerde controles|
|---|
|<ul><li>Zijn alle Hallo hosts waarbij Hallo taak wordt uitgevoerd en uitgevoerd?</li><li>Hallo-taak kan niet toostart is?</li><li>Zijn er lopende runtime upgrades?</li><li>Hallo-taak in een verwachte status (bijvoorbeeld uitgevoerd of gestopt door de klant)?</li><li>Hallo taak opgetreden uit geheugen uitzonderingen?</li><li>Zijn er lopende geplande compute updates?</li><li>Is Hallo uitvoeringsbeheer (dit plan) beschikbaar?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Uitgevoerde controles|
|---|
|<ul><li>Hallo host-server actief is en wordt uitgevoerd?</li><li>Internet Information Services wordt uitgevoerd</li><li>Is Hallo Load balancer wordt uitgevoerd?</li><li>Hallo Web Service-Plan kan worden bereikt vanaf binnen Hallo datacenter?</li><li>Is Hallo storage account hosting Hallo sites inhoud voor de serverFarm Hallo beschikbaar veldnamenrij?</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.Web/sites
|Uitgevoerde controles|
|---|
|<ul><li>Hallo host-server actief is en wordt uitgevoerd?</li><li>Is Internet Information server wordt uitgevoerd?</li><li>Is Hallo Load balancer wordt uitgevoerd?</li><li>Hallo Web-App kan worden bereikt vanaf binnen Hallo datacenter?</li><li>Hallo-opslagaccount als host fungeert voor Hallo site-inhoud beschikbaar?</li></ul>|

# <a name="next-steps"></a>Volgende stappen
-  Zie [inleiding tooAzure servicestatus](service-health-overview.md) en [inleiding tooAzure resourcestatus](resource-health-overview.md) toounderstand meer informatie hierover. 
-  [Veelgestelde vragen over Azure-resourcestatus](resource-health-faq.md)
- Waarschuwingen instellen, zodat u wordt gewaarschuwd van statusproblemen. Zie voor meer informatie [waarschuwingen configureren voor servicestatus](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 