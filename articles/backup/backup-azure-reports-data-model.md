---
title: aaaData model voor Azure Backup
description: In dit artikel wordt gesproken over Power BI Gegevensdetails model voor Azure Backup-rapporten.
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Gegevensmodel voor Azure Backup-rapporten
Dit artikel wordt beschreven Hallo Power BI-gegevensmodel gebruikt voor het maken van Azure Backup-rapporten. Met deze gegevensmodel, kunt u bestaande rapporten op basis van de betreffende velden filteren en meer echter uw eigen rapporten maken met behulp van tabellen en velden in het Hallo-model. 

## <a name="creating-new-reports-in-power-bi"></a>Maken van nieuwe rapporten in Power BI
Power BI biedt die u kunt met aanpassingsfuncties [rapporten maken met het gegevensmodel Hallo](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/).

## <a name="using-azure-backup-data-model"></a>Met behulp van Azure Backup-gegevensmodel
U kunt Hallo na velden die zijn opgegeven als deel van de gegevens Hallo model toocreate rapporten en bestaande rapporten aanpassen.

### <a name="alert"></a>Waarschuwing
Deze tabel bevat basisvelden en aggregaties via verschillende gerelateerde waarschuwingsvelden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #AlertsCreatedInPeriod |Geheel getal |Aantal waarschuwingen dat is gemaakt in de geselecteerde tijdsperiode |
| % ActiveAlertsCreatedInPeriod |Percentage |Percentage van actieve waarschuwingen in de geselecteerde tijdsperiode |
| % CriticalAlertsCreatedInPeriod |Percentage |Percentage van kritieke waarschuwingen in de geselecteerde tijdsperiode |
| AlertOccurenceDate |Date |Datum waarop de waarschuwing is gemaakt |
| AlertSeverity |Tekst |Ernst van waarschuwing Hallo bijvoorbeeld kritiek |
| AlertStatus |Tekst |Status van de waarschuwing Hallo bijvoorbeeld actief |
| AlertType |Tekst |Type Hallo gegenereerde waarschuwing bijvoorbeeld back-up |
| AlertUniqueId |Tekst |Unieke Id van Hallo waarschuwing is gegenereerd |
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |Decimaal getal zijn |Gemiddelde tijd (in minuten) tooresolve waarschuwing voor geselecteerde tijdsperiode |
| EntityState |Tekst |Huidige status van de waarschuwing object Hallo bijvoorbeeld actief, verwijderd |

### <a name="backup-item"></a>Back-Item
Deze tabel bevat basisvelden en aggregaties gedurende verschillende back-item-gerelateerde velden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #BackupItems |Geheel getal |Aantal back-items |
| #UnprotectedBackupItems |Geheel getal |Aantal back-items voor beveiliging is gestopt of geconfigureerd voor back-ups maar back-ups niet gestart|
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| BackupItemFriendlyName |Tekst |Beschrijvende naam van back-item |
| BackupItemId |Tekst |Id van de back-item |
| BackupItemName |Tekst |Naam van back-item |
| BackupItemType |Tekst |Type back-item bijvoorbeeld VM FileFolder |
| EntityState |Tekst |Huidige status van Hallo back-upitems object bijvoorbeeld actief, verwijderd |
| LastBackupDateTime |Datum/tijd |Tijd van laatste back-up voor de geselecteerde back-item |
| LastBackupState |Tekst |Status van de laatste back-up voor de geselecteerde back-artikel bijvoorbeeld geslaagd, mislukt |
| LastSuccessfulBackupDateTime |Datum/tijd |Tijd van laatste geslaagde back-up voor de geselecteerde back-item |
| ProtectionState |Tekst |Huidige beveiligingsstatus van back-upitems Hallo bijvoorbeeld beveiligde, ProtectionStopped |

### <a name="calendar"></a>Agenda
Deze tabel bevat informatie over velden met betrekking tot de agenda.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Date |Date |Datum geselecteerd voor het filteren van gegevens |
| DateKey |Tekst |Unieke sleutel voor elk item datum |
| DayDiff |Decimaal getal zijn |Verschil in dagen voor het filteren van gegevens, bijvoorbeeld, 0 geeft aan dat de gegevens van de huidige dag, -1 geeft aan dat de gegevens van de vorige één dag, 0 en 1 geven gegevens voor de huidige en vorige dag  |
| Maand |Tekst |Maand van Hallo jaar geselecteerd voor het filteren van gegevens, maand op de eerste dag begint en eindigt op 31e dag |
| MonthDate | Date |Datum in Hallo maand waarop maand eindigt, geselecteerd voor het filteren van gegevens |
| MonthDiff |Decimaal getal zijn |Verschil in maand voor het filteren van gegevens, bijvoorbeeld, 0 geeft aan dat gegevens van de huidige maand, -1 geeft aan dat gegevens van vorige maand, 0 en 1 geven gegevens voor de huidige en vorige maand |
| Week |Tekst |Week geselecteerd voor het filteren van gegevens, week op zondag begint en eindigt op zaterdag |
| WeekDate |Date |Datum in Hallo week waarop week eindigt, geselecteerd voor het filteren van gegevens |
| WeekDiff |Decimaal getal zijn |Verschil in de week voor het filteren van gegevens, bijvoorbeeld, 0 geeft aan dat gegevens van de huidige week, -1 geeft aan dat gegevens van de vorige week, 0 en 1 geven gegevens voor de huidige en vorige week |
| jaar |Tekst |Kalenderjaar geselecteerd voor het filteren van gegevens |
| YearDate |Date |Datum in Hallo jaar jaar wanneer eindigt, geselecteerd voor het filteren van gegevens |

### <a name="job"></a>Job
Deze tabel bevat basisvelden en aggregaties via verschillende velden met betrekking tot de taak.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #JobsCreatedInPeriod |Geheel getal |Aantal taken in de geselecteerde periode Hallo gemaakt |
| % FailuresForJobsCreatedInPeriod |Percentage |Percentage algemene taak fouten in de geselecteerde periode Hallo |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |Decimaal getal zijn |80e percentielwaarde van de gegevens worden overgebracht in MB voor **back-** taken die zijn gemaakt in de geselecteerde periode Hallo |
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |Decimaal getal zijn |Gemiddelde tijd in minuten voor **voltooide back-up** taken die zijn gemaakt in de geselecteerde tijdsperiode |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |Decimaal getal zijn |Gemiddelde tijd in minuten voor **terugzetten voltooid** taken die zijn gemaakt in de geselecteerde tijdsperiode |
| BackupStorageDestination |Tekst |Bestemming van back-upopslag bijvoorbeeld Cloud schijf  |
| EntityState |Tekst |Huidige status van het taakobject Hallo bijvoorbeeld actief, verwijderd |
| JobFailureCode |Tekst |Code string voor mislukt vanwege die taakfout hebben plaatsgevonden |
| JobOperation |Tekst |Bewerking voor die taak wordt uitgevoerd bijvoorbeeld back-up, herstel, Configureer back-up |
| JobStartDate |Date |Datum waarop de taak is gestart |
| JobStartTime |Time |Tijd wanneer de taak is gestart |
| JobStatus |Tekst |Status van Hallo voltooid taak bijvoorbeeld voltooid, is mislukt |
| JobUniqueId |Tekst |Unieke Id tooidentify Hallo taak |

### <a name="policy"></a>Beleid
Deze tabel bevat basisvelden en aggregaties via verschillende beleid gerelateerde velden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #Policies |Geheel getal |Aantal back-upbeleid dat in Hallo systeem bestaan |
| #PoliciesInUse |Geheel getal |Aantal beleidsregels die momenteel wordt gebruikt voor back-ups configureren |
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| BackupDaysOfTheWeek |Tekst |Hallo weekdagen wanneer back-ups zijn gepland |
| BackupFrequency |Tekst |Frequentie waarmee back-ups worden uitgevoerd, bijvoorbeeld dagelijks, wekelijks |
| BackupTimes |Tekst |Datum en tijd wanneer de back-ups zijn gepland |
| DailyRetentionDuration |Geheel getal |Duur van de totale bewaartermijn in dagen voor geconfigureerde back-ups |
| DailyRetentionTimes |Tekst |Datum en tijd wanneer de dagelijkse bewaarperiode is geconfigureerd |
| EntityState |Tekst |Huidige status van groepsbeleidsobject Hallo bijvoorbeeld actief, verwijderd |
| MonthlyRetentionDaysOfTheMonth |Tekst |Hallo maand geselecteerd voor het bewaren van maandelijkse datums |
| MonthlyRetentionDaysOfTheWeek |Tekst |Dagen van week Hallo geselecteerd voor het maandelijkse bewaren |
| MonthlyRetentionDuration |Decimaal getal zijn |Duur van de totale bewaarperiode in maanden voor geconfigureerde back-ups |
| MonthlyRetentionFormat |Tekst |Typ van configuratie voor het bewaren van maandelijkse bijvoorbeeld dagelijks voor dag wekelijks is gebaseerd op basis van week |
| MonthlyRetentionTimes |Tekst |Datum en tijd wanneer maandelijkse bewaarperiode is geconfigureerd |
| MonthlyRetentionWeeksOfTheMonth |Tekst |Weken van Hallo maand wanneer maandelijkse bewaartermijn is geconfigureerd, bijvoorbeeld First, Last, enzovoort. |
| PolicyName |Tekst |Naam van het Hallo-beleid is gedefinieerd |
| PolicyUniqueId |Tekst |De unieke Id tooidentify Hallo-beleid |
| RetentionType |Tekst |Type bewaarbeleid bijvoorbeeld, dagelijks, wekelijks, maandelijks, jaarlijks |
| WeeklyRetentionDaysOfTheWeek |Tekst |Dagen van week Hallo geselecteerd voor het bewaren van wekelijks |
| WeeklyRetentionDuration |Decimaal getal zijn |Totale duur van de wekelijkse bewaren weken voor geconfigureerde back-ups |
| WeeklyRetentionTimes |Tekst |Datum en tijd wanneer de wekelijkse bewaarperiode is geconfigureerd |
| YearlyRetentionDaysOfTheMonth |Tekst |Hallo maand geselecteerd voor het bewaren van jaarlijkse datums |
| YearlyRetentionDaysOfTheWeek |Tekst |Dagen van week Hallo geselecteerd voor het bewaren van jaarlijkse |
| YearlyRetentionDuration |Decimaal getal zijn |Duur van de totale bewaartermijn in jaren voor geconfigureerde back-ups |
| YearlyRetentionFormat |Tekst |Typ van configuratie voor het bewaren van jaarlijkse bijvoorbeeld dagelijks voor dag wekelijks is gebaseerd op basis van week |
| YearlyRetentionMonthsOfTheYear |Tekst |Maanden van Hallo jaar geselecteerd voor het bewaren van jaarlijkse |
| YearlyRetentionTimes |Tekst |Datum en tijd wanneer jaarlijks bewaarbeleid is geconfigureerd |
| YearlyRetentionWeeksOfTheMonth |Tekst |Weken van Hallo maand wanneer de jaarlijkse bewaartermijn is geconfigureerd, bijvoorbeeld First, Last, enzovoort. |

### <a name="protected-server"></a>Beveiligde Server
Deze tabel bevat basisvelden en aggregaties via verschillende beveiligde server-gerelateerde velden.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #ProtectedServers |Geheel getal |Het aantal beveiligde servers |
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| AzureBackupAgentOSType |Tekst |Type besturingssysteem van Azure Backup Agent |
| AzureBackupAgentOSVersion |Tekst |OS-versie van Azure Backup Agent |
| AzureBackupAgentUpdateDate |Tekst |Datum waarop de Agent Backup-Agent is bijgewerkt |
| AzureBackupAgentVersion |Tekst |Versienummer van Agent back-up-versie |
| BackupManagementType |Tekst |Providertype voor het uitvoeren van back-up bijvoorbeeld IaaSVM FileFolder |
| EntityState |Tekst |Huidige status van de beveiligde server-object Hallo bijvoorbeeld actief, verwijderd |
| ProtectedServerFriendlyName |Tekst |Beschrijvende naam van de beveiligde server |
| ProtectedServerName |Tekst |Naam van de beveiligde server |
| ProtectedServerType |Tekst |Type van de beveiligde server een back-up bijvoorbeeld IaaSVMContainer |
| ProtectedServerName |Tekst |Naam van de beveiligde server toowhich back-item behoort |
| RegisteredContainerId |Tekst |Id van de container die is geregistreerd voor back-up |

### <a name="storage"></a>Storage
Deze tabel bevat basisvelden en aggregaties via verschillende velden met betrekking tot opslag.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #ProtectedInstances |Decimaal getal zijn |Het aantal beveiligde exemplaren dat wordt gebruikt voor het berekenen van frontend-opslag in facturering, berekend op basis van de laatste waarde in de geselecteerde tijd |
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| CloudStorageInMB |Decimaal getal zijn |Back-cloudopslag die wordt gebruikt door de back-ups, berekend op basis van de laatste waarde in de geselecteerde tijd |
| EntityState |Tekst |Huidige status van Hallo object bijvoorbeeld actief, verwijderd |
| LastUpdatedDate |Date |Datum waarop de geselecteerde rij voor het laatst is bijgewerkt |

### <a name="time"></a>Time
Deze tabel bevat informatie over velden met betrekking tot de tijd.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Uur |Time |Uur van Hallo dag, bijvoorbeeld 1:00:00 PM |
| HourNumber |Decimaal getal zijn |Het aantal uren in Hallo dag, bijvoorbeeld 13,00 |
| Minuut |Decimaal getal zijn |Minuut van Hallo uur |
| PeriodOfTheDay |Tekst |Periode tijdsperiode Hallo dag, bijvoorbeeld 12-3 uur |
| Time |Time |Tijd van de dag Hallo bijvoorbeeld 12:00:01 uur |
| TimeKey |Tekst |Sleutelwaarde toorepresent tijd |

### <a name="vault"></a>Kluis
Deze tabel bevat basisvelden en aggregaties via verschillende velden met betrekking tot de kluis.

| Veld | Gegevenstype | Beschrijving |
| --- | --- | --- |
| #Vaults |Geheel getal |Het aantal kluizen |
| AsOnDateTime |Datum/tijd |Meest recente te vernieuwen voor de geselecteerde rij Hallo |
| AzureDataCenter |Tekst |Datacenter waar kluis zich bevindt |
| EntityState |Tekst |Huidige status van Hallo kluis object bijvoorbeeld actief, verwijderd |
| StorageReplicationType |Tekst |Type opslagreplicatie voor Hallo kluis bijvoorbeeld GeoRedundant |
| SubscriptionId |Tekst |Abonnement-Id van Hallo klant geselecteerd voor het genereren van rapporten |
| VaultName |Tekst |Naam van de kluis Hallo |
| VaultTags |Tekst |Labels toohello kluis die is gekoppeld |

## <a name="next-steps"></a>Volgende stappen
Zodra u hello gegevensmodel bekijkt voor het maken van Azure Backup-rapporten, Raadpleeg de volgende artikelen voor meer informatie over het maken en weergeven van rapporten in Power BI Hallo.

* [Maken van rapporten in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [Filteren van rapporten in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
