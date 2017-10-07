---
title: aaaLog Analytics gegevensmodel voor Azure Backup
description: In dit artikel wordt gesproken over logboekanalyse Gegevensdetails model voor Azure backup-gegevens.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>Log Analytics-gegevensmodel voor Azure backup-gegevens
Dit artikel wordt beschreven Hallo-gegevensmodel dat is gebruikt voor het pushen reporting gegevens tooLog Analytics. Met dit gegevensmodel, kunt u aangepaste query's, dashboards maken en gebruiken in OMS. 

## <a name="using-azure-backup-data-model"></a>Met behulp van Azure Backup-gegevensmodel
U kunt Hallo velden die deel uitmaken van Hallo data model toocreate visuele elementen, aangepaste query's en dashboard volgens uw vereisten te volgen.

### <a name="alert"></a>Waarschuwing
Deze tabel bevat informatie over verwante waarschuwingsvelden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| AlertUniqueId_s |Tekst |Unieke Id van Hallo waarschuwing is gegenereerd |
| AlertType_s |Tekst |Type Hallo gegenereerde waarschuwing, bijvoorbeeld: back-up |
| AlertStatus_s |Tekst |Status van Hallo waarschuwing, bijvoorbeeld, actief |
| AlertOccurenceDateTime_s |Datum/tijd |Datum en tijd waarop de waarschuwing is gemaakt |
| AlertSeverity_s |Tekst |Ernst van Hallo waarschuwing, bijvoorbeeld: kritiek |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| BackupItemUniqueId_s |Tekst |Unieke Id van Hallo back-upitems toowhich die te deel uitmaakt van deze waarschuwing|
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo waarschuwing object, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich te deel uitmaakt van deze waarschuwing|
| OperationName |Tekst |Dit veld wordt de naam van de huidige bewerking Hallo - waarschuwing |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| ProtectedServerUniqueId_s |Tekst |Unieke Id van Hallo beveiligd toowhich die te deel uitmaakt van deze waarschuwing|
| VaultUniqueId_s |Tekst |Unieke Id van Hallo beveiligd toowhich die te deel uitmaakt van deze waarschuwing|
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="backupitem"></a>BackupItem
Deze tabel bevat informatie over back-item-gerelateerde velden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |  
| BackupItemUniqueId_s |Tekst |Unieke Id van de back-upitems Hallo |
| BackupItemId_s |Tekst |Id van de back-item |
| BackupItemName_s |Tekst |Naam van back-item |
| BackupItemFriendlyName_s |Tekst |Beschrijvende naam van back-item |
| BackupItemType_s |Tekst |Type back-item, bijvoorbeeld VM FileFolder |
| ProtectedServerName_s |Tekst |Naam van de beveiligde server toowhich back-item behoort te|
| ProtectionState_s |Tekst |Huidige beveiligingsstatus van Hallo back-item, bijvoorbeeld beveiligde, ProtectionStopped |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo back-object, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich te deel uitmaakt van deze back-item|
| OperationName |Tekst |Dit veld vertegenwoordigt naam van de huidige bewerking Hallo - BackupItem |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="backupitemassociation"></a>BackupItemAssociation
Deze tabel bevat informatie over back-upitems koppelingen met verschillende entiteiten.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |  
| BackupItemUniqueId_s |Tekst |Unieke Id van de back-upitems Hallo |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo back-koppelingsobject item, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich te deel uitmaakt van deze back-item|
| OperationName |Tekst |Dit veld vertegenwoordigt naam van de huidige bewerking Hallo - BackupItemAssociation |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| PolicyUniqueId_g |Tekst |De unieke Id tooidentify Hallo-beleid van back-up item is te gekoppeld|
| ProtectedServerUniqueId_s |Tekst |Unieke Id van Hallo beveiligde server toowhich die te deel uitmaakt van deze back-item|
| VaultUniqueId_s |Tekst |Unieke Id van Hallo kluis toowhich die te deel uitmaakt van deze back-item|
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="job"></a>Job
Deze tabel bevat informatie over velden met betrekking tot de taak.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| BackupItemUniqueId_s |Tekst |Unieke Id van Hallo back-upitems toowhich die te deel uitmaakt van deze taak|
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo taakobject, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich te deel uitmaakt van deze taak|
| OperationName |Tekst |Dit veld wordt de naam van de huidige bewerking Hallo - taak |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| ProtectedServerUniqueId_s |Tekst |Unieke Id van Hallo beveiligd toowhich die te deel uitmaakt van deze taak|
| VaultUniqueId_s |Tekst |Unieke Id van Hallo beveiligd toowhich die te deel uitmaakt van deze taak|
| JobOperation_s |Tekst |Bewerking voor die taak wordt uitgevoerd bijvoorbeeld back-up, herstel, Configureer back-up |
| JobStatus_s |Tekst |Status van Hallo taak, bijvoorbeeld voltooid, kan niet voltooid |
| JobFailureCode_s |Tekst |Code string voor mislukt vanwege die taakfout hebben plaatsgevonden |
| JobStartDateTime_s |Datum/tijd |Datum en tijd wanneer taak gestart die wordt uitgevoerd |
| BackupStorageDestination_s |Tekst |Bestemming van back-upopslag, bijvoorbeeld Cloud, schijf  |
| JobDurationInSecs_s | Aantal |Totaal aantal taak duur in seconden |
| DataTransferredInMB_s | Aantal |Gegevens die voor deze taak worden overgebracht in MB|
| JobUniqueId_g |Tekst |Unieke Id tooidentify Hallo taak |
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="policy"></a>Beleid
Deze tabel bevat informatie over beleid gerelateerde velden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo beleidsobject, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich dit beleid te behoort|
| OperationName |Tekst |Dit veld wordt de naam van de huidige bewerking Hallo - beleid |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| PolicyUniqueId_g |Tekst |De unieke Id tooidentify Hallo-beleid |
| PolicyName_s |Tekst |Naam van het Hallo-beleid is gedefinieerd |
| BackupFrequency_s |Tekst |Frequentie waarmee de back-ups worden uitgevoerd, bijvoorbeeld dagelijks, wekelijks |
| BackupTimes_s |Tekst |Datum en tijd wanneer de back-ups zijn gepland |
| BackupDaysOfTheWeek_s |Tekst |Hallo weekdagen wanneer back-ups zijn gepland |
| RetentionDuration_s |Geheel getal |Duur van de bewaarperiode voor geconfigureerde back-ups |
| DailyRetentionDuration_s |Geheel getal |Duur van de totale bewaartermijn in dagen voor geconfigureerde back-ups |
| DailyRetentionTimes_s |Tekst |Datum en tijd wanneer de dagelijkse bewaarperiode is geconfigureerd |
| WeeklyRetentionDuration_s |Decimaal getal zijn |Totale duur van de wekelijkse bewaren weken voor geconfigureerde back-ups |
| WeeklyRetentionTimes_s |Tekst |Datum en tijd wanneer de wekelijkse bewaarperiode is geconfigureerd |
| WeeklyRetentionDaysOfTheWeek_s |Tekst |Dagen van week Hallo geselecteerd voor het bewaren van wekelijks |
| MonthlyRetentionDuration_s |Decimaal getal zijn |Duur van de totale bewaarperiode in maanden voor geconfigureerde back-ups |
| MonthlyRetentionTimes_s |Tekst |Datum en tijd wanneer maandelijkse bewaarperiode is geconfigureerd |
| MonthlyRetentionFormat_s |Tekst |Configuratie voor het maandelijkse bewaren, bijvoorbeeld dagelijks voor de dag gebaseerd wekelijks voor de week op basis van type |
| MonthlyRetentionDaysOfTheWeek_s |Tekst |Dagen van week Hallo geselecteerd voor het maandelijkse bewaren |
| MonthlyRetentionWeeksOfTheMonth_s |Tekst |Weken van Hallo maand wanneer maandelijkse bewaarperiode is geconfigureerd, bijvoorbeeld de eerste, laatste enzovoort. |
| YearlyRetentionDuration_s |Decimaal getal zijn |Duur van de totale bewaartermijn in jaren voor geconfigureerde back-ups |
| YearlyRetentionTimes_s |Tekst |Datum en tijd wanneer jaarlijks bewaarbeleid is geconfigureerd |
| YearlyRetentionMonthsOfTheYear_s |Tekst |Maanden van Hallo jaar geselecteerd voor het bewaren van jaarlijkse |
| YearlyRetentionFormat_s |Tekst |Configuratie voor jaarlijkse bewaren, bijvoorbeeld dagelijks voor de dag gebaseerd wekelijks voor de week op basis van type |
| YearlyRetentionDaysOfTheMonth_s |Tekst |Hallo maand geselecteerd voor het bewaren van jaarlijkse datums |
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="policyassociation"></a>PolicyAssociation
Deze tabel bevat informatie over beleid koppelingen met verschillende entiteiten.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo beleidsobject, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up bijvoorbeeld IaaSVM, FileFolder toowhich dit beleid te behoort|
| OperationName |Tekst |Dit veld vertegenwoordigt naam van de huidige bewerking Hallo - PolicyAssociation |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| PolicyUniqueId_g |Tekst |De unieke Id tooidentify Hallo-beleid |
| VaultUniqueId_s |Tekst |Unieke Id van Hallo kluis toowhich die dit beleid te behoort|
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="protectedserver"></a>ProtectedServer
Deze tabel bevat informatie over beveiligde velden met betrekking tot de server.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| ProtectedServerName_s |Tekst |Naam van de beveiligde server |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo beveiligde server-object, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up bijvoorbeeld IaaSVM, FileFolder toowhich deze beveiligde server te behoort|
| OperationName |Tekst |Dit veld vertegenwoordigt naam van de huidige bewerking Hallo - ProtectedServer |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| ProtectedServerUniqueId_s |Tekst |Unieke Id van Hallo beveiligde server |
| RegisteredContainerId_s |Tekst |Id van de container die is geregistreerd voor back-up |
| ProtectedServerType_s |Tekst |Type van de beveiligde server een back-up bijvoorbeeld Windows |
| ProtectedServerFriendlyName_s |Tekst |Beschrijvende naam van de beveiligde server |
| AzureBackupAgentVersion_s |Tekst |Versienummer van Agent back-up-versie |
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
Deze tabel bevat informatie over de beveiligde server koppelingen met andere entiteiten.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo beveiligde server koppeling-object, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich deze beveiligde server te behoort|
| OperationName |Tekst |Dit veld vertegenwoordigt naam van de huidige bewerking Hallo - ProtectedServerAssociation |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| ProtectedServerUniqueId_s |Tekst |Unieke Id van Hallo beveiligde server |
| VaultUniqueId_s |Tekst |Unieke Id van Hallo kluis toowhich die deze beveiligde server te behoort|
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="storage"></a>Storage
Deze tabel bevat informatie over velden met betrekking tot opslag.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| CloudStorageInBytes_s |Decimaal getal zijn |Back-cloudopslag die wordt gebruikt door de back-ups, berekend op basis van de laatste waarde |
| ProtectedInstances_s |Decimaal getal zijn |Het aantal beveiligde exemplaren dat wordt gebruikt voor het berekenen van de frontend-opslag in facturering, berekend op basis van de laatste waarde |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo opslagobject, bijvoorbeeld Active, verwijderd |
| BackupManagementType_s |Tekst |Providertype voor het uitvoeren van back-up, bijvoorbeeld IaaSVM FileFolder toowhich deze opslag te behoort|
| OperationName |Tekst |Dit veld wordt de naam van de huidige bewerking Hallo - opslag |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| ProtectedServerUniqueId_s |Tekst |Unieke Id van Hallo beveiligde server waarvoor de opslag wordt berekend |
| VaultUniqueId_s |Tekst |Unieke Id van de kluis Hallo voor opslag wordt berekend |
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld representse type Hallo resource waarvoor gegevens worden verzameld - kluizen |

### <a name="vault"></a>Kluis
Deze tabel bevat informatie over velden met betrekking tot de kluis.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| EventName_s |Tekst |Dit veld naam van deze gebeurtenis vertegenwoordigt, is altijd AzureBackupCentralReport |
| SchemaVersion_s |Tekst |Dit veld geeft de huidige versie van het Hallo-schema, is het **V1** |
| State_s |Tekst |Huidige status van Hallo kluis object, bijvoorbeeld Active, verwijderd |
| OperationName |Tekst |Dit veld wordt de naam van de huidige bewerking Hallo - kluis |
| Category |Tekst |Dit veld wordt de categorie van diagnostische gegevens tooLog Analytics gepusht, is het AzureBackupReport |
| Resource |Tekst |Dit is Hallo resource waarvoor gegevens worden verzameld, ziet u de naam van de Recovery Services-kluis |
| VaultUniqueId_s |Tekst |Unieke Id van de kluis Hallo |
| VaultName_s |Tekst |Naam van de kluis Hallo |
| AzureDataCenter_s |Tekst |Datacenter waar kluis zich bevindt |
| StorageReplicationType_s |Tekst |Type opslagreplicatie voor Hallo kluis, bijvoorbeeld GeoRedundant |
| SourceSystem |Tekst |Bronsysteem van huidige gegevens Hallo - Azure |
| ResourceId |Tekst |Dit veld geeft resource-id waarvoor gegevens worden verzameld, wordt een melding weergegeven Recovery Services-kluis resource-id |
| SubscriptionId |Tekst |Dit veld wordt de abonnement-id van het Hallo-resource (RS kluis) waarvoor gegevens worden verzameld |
| ResourceGroup |Tekst |Dit veld wordt de brongroep van bron hello (RS kluis) waarvoor gegevens worden verzameld |
| ResourceProvider |Tekst |Dit veld wordt Hallo resourceprovider waarvoor gegevens worden verzameld - Microsoft.RecoveryServices |
| ResourceType |Tekst |Dit veld wordt het type Hallo resource waarvoor gegevens worden verzameld - kluizen |

## <a name="next-steps"></a>Volgende stappen
Wanneer u hello gegevensmodel bekijkt voor het maken van Azure Backup-rapporten, kunt u beginnen [dashboard maken](../log-analytics/log-analytics-dashboards.md) in Log Analytics en OMS.
