---
title: aaaOffice 365 oplossing in de Operations Management Suite (OMS) | Microsoft Docs
description: Dit artikel bevat informatie over configuratie en gebruik van Hallo Office 365-oplossing in OMS.  Het bevat een gedetailleerde beschrijving van Hallo Office 365-records gemaakt in logboekanalyse.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Office 365-oplossing in de Operations Management Suite (OMS)

![Office 365-logo](media/oms-solution-office-365/icon.png)

Hallo Office 365-oplossing voor Operations Management Suite (OMS) kunt u toomonitor uw Office 365-omgeving in logboekanalyse.  

- Controleren van gebruikersactiviteiten op uw gebruikspatronen van Office 365-accounts tooanalyze evenals trends voor gebruikersgedrag. U kunt bijvoorbeeld specifieke gebruiksscenario's, zoals bestanden die worden gedeeld buiten uw organisatie of de meest populaire SharePoint-sites Hallo uitpakken.
- Monitor configuratiewijzigingen van beheerder activiteiten tootrack of hoge bevoegdheid bewerkingen.
- Detecteren en onderzoeken van ongewenste gebruikersgedrag die behoeften van uw organisatie kan worden aangepast.
- Controle en naleving demonstreren. U kunt bijvoorbeeld toegang bestandsbewerkingen op vertrouwelijke bestanden, waarmee u kunnen met het Hallo-controle en naleving proces bewaken.
- Uitvoeren van operationele problemen oplossen met behulp van OMS zoeken boven op Office 365-activiteitsgegevens van uw organisatie.

## <a name="prerequisites"></a>Vereisten
Hallo volgende is vereist voorafgaande toothis oplossing wordt geïnstalleerd en geconfigureerd.

- Organisatie Office 365-abonnement.
- Referenties voor een gebruikersaccount dat een globale beheerder.
- controlegegevens tooreceive, moet u [controle configureren](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) in uw Office 365-abonnement.  Houd er rekening mee dat [Postvakcontrole](https://technet.microsoft.com/library/dn879651.aspx) wordt afzonderlijk geconfigureerd.  U kunt nog steeds Hallo oplossing installeren en andere gegevens verzamelen als controle is niet geconfigureerd.
 


## <a name="management-packs"></a>Management packs
Deze oplossing wordt niet geïnstalleerd voor alle management packs in de verbonden beheergroepen.
  

## <a name="configuration"></a>Configuratie
Eenmaal u [Hallo Office 365-oplossing tooyour abonnement toevoegen](../log-analytics/log-analytics-add-solutions.md), hebt u tooconnect het tooyour Office 365-abonnement.

1. Hallo waarschuwingenbeheer oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [oplossingen toevoegen](../log-analytics/log-analytics-add-solutions.md).
2. Ga te**instellingen** in Hallo OMS-portal.
3. Onder **verbonden bronnen**, selecteer **Office 365**.
4. Klik op **verbinding maken met Office 365**.<br>![Processtappen verbinden Office 365](media/oms-solution-office-365/configure.png)
5. Meld u aan tooOffice 365 met een account dat een globale beheerder voor uw abonnement. 
6. Hallo-abonnement wordt vermeld met de Hallo werkbelastingen die Hallo oplossing bewaakt.<br>![Processtappen verbinden Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Gegevensverzameling
### <a name="supported-agents"></a>Ondersteunde agents
Hallo Office 365-oplossing niet ophalen van gegevens uit een van de Hallo [OMS agents](../log-analytics/log-analytics-data-sources.md).  Het ophalen van gegevens rechtstreeks vanuit Office 365.

### <a name="collection-frequency"></a>Verzamelingsfrequentie
Office 365 verzendt een [webhook melding](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) met gedetailleerde gegevens tooLog Analytics telkens wanneer een record wordt gemaakt.

## <a name="using-hello-solution"></a>Met behulp van Hallo-oplossing
Wanneer u Hallo Office 365-oplossing tooyour OMS-werkruimte toevoegt, Hallo **Office 365** tegel tooyour OMS dashboard worden toegevoegd. Deze tegel wordt een aantal en de grafische weergave van Hallo aantal computers in uw omgeving en de updatenaleving ervan weergegeven.<br><br>
![Tegel samenvatting van Office 365](media/oms-solution-office-365/tile.png)  

Klik op Hallo **Office 365** tegel tooopen hello **Office 365** dashboard.

![Office 365-Dashboard](media/oms-solution-office-365/dashboard.png)  

Hallo dashboard bevat Hallo kolommen in de volgende tabel Hallo. Elke kolom bevat Hallo top tien waarschuwingen per aantal die overeenkomt met dat van de kolom criteria voor Hallo bereik en tijdbereik opgegeven. U kunt een zoekopdracht logboek waarmee de volledige lijst Hallo door te klikken op Zie alle onderaan Hallo Hallo kolom of door te klikken op de kolomkop Hallo uitvoeren.

| Kolom | Beschrijving |
|:--|:--|
| Bewerkingen | Bevat informatie over Hallo actieve gebruikers van uw abonnementen op alle gecontroleerde Office 365. U zult ook kunnen toosee Hallo aantal activiteiten dat gedurende een bepaalde periode gebeuren.
| Exchange | U kunt Hallo uitsplitsing van Exchange Server-activiteiten zoals de machtiging voor toevoegen of Set-postvak. |
| SharePoint | Toont de belangrijkste activiteiten Hallo dat gebruikers op de SharePoint-documenten uitvoeren. Wanneer u inzoomen op deze tegel zoekpagina Hallo Hallo worden details weergegeven van deze activiteiten, zoals Hallo doeldocument en Hallo-locatie van deze activiteit. Bijvoorbeeld, voor een gebeurtenis bestand geopend, kunt u zich kunt toosee Hallo document dat wordt geopend, de bijbehorende accountnaam en het IP-adres. |
| Azure Active Directory | Bovenste gebruikersactiviteiten, zoals gebruiker-wachtwoord opnieuw instellen en aanmeldingspogingen bevat. Wanneer u inzoomen, kunt u zich kunt toosee Hallo details van deze activiteiten zoals Hallo resultaatstatus. Dit is vooral handig als u wilt dat toomonitor verdachte activiteiten op uw Azure Active Directory. |




## <a name="log-analytics-records"></a>Log Analytics-records

Alle records die zijn gemaakt in de werkruimte voor logboekanalyse Hallo door Hallo Office 365-oplossing een **Type** van **OfficeActivity**.  Hallo **OfficeWorkload** eigenschap bepaalt welke Office 365-servicerecord Hallo verwijst te Exchange, AzureActiveDirectory, SharePoint of OneDrive.  Hallo **RecordType** -eigenschap geeft op Hallo type bewerking.  Hallo eigenschappen varieert voor elk bewerkingstype en worden weergegeven in onderstaande Hallo tabellen.

### <a name="common-properties"></a>Algemene eigenschappen
Hallo volgende eigenschappen zijn algemene tooall Office 365-records.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type | *OfficeActivity* |
| client-IP | Hallo IP-adres van Hallo-apparaat dat is gebruikt bij het Hallo-activiteit is geregistreerd. Hallo IP-adres wordt weergegeven in de notatie voor een IPv4- of IPv6-adres. |
| OfficeWorkload | Office 365-service die Hallo record verwijst.<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| Bewerking | Hallo-naam van de gebruiker of beheerder activiteit Hallo.  |
| OrganizationId | Hallo GUID voor Office 365-tenant van uw organisatie. Deze waarde wordt altijd worden Hallo dezelfde voor uw organisatie, ongeacht Hallo Office 365-service waarin het optreedt. |
| recordType | Type van een bewerking uitgevoerd. |
| ResultStatus | Hiermee wordt aangegeven of Hallo actie (opgegeven in hello eigenschap Operation) gelukt is. Mogelijke waarden zijn geslaagd, PartiallySucceded of mislukt. Exchange-admin-activiteit Hallo-waarde is True of False. |
| Gebruikers-id | Hallo UPN (User Principal Name) van Hallo-gebruiker die Hallo actie dat heeft geresulteerd in Hallo record aan te melden; heeft uitgevoerd bijvoorbeeld: my_name@my_domain_name. Houd er rekening mee dat records voor de activiteit uitgevoerd door systeemaccounts (zoals SHAREPOINT\system of NTAUTHORITY\SYSTEM) ook opgenomen worden. | 
| UserKey | Een alternatieve ID voor de gebruiker Hallo aangegeven in Hallo eigenschap UserId.  Deze eigenschap wordt bijvoorbeeld gevuld met de Hallo passport unieke ID (PUID) voor gebeurtenissen die worden uitgevoerd door gebruikers in SharePoint, OneDrive voor bedrijven en Exchange. Deze eigenschap kan ook dezelfde waarde als Hallo eigenschap UserID voor gebeurtenissen in andere services en evenementen uitgevoerd door systeemaccounts Hallo opgeven|
| UserType | Hallo-type van de gebruiker die het Hallo-bewerking uitgevoerd.<br><br>Beheerder<br>Toepassing<br>DcAdmin<br>Reguliere<br>Gereserveerd<br>ServicePrincipal<br>Systeem |


### <a name="azure-active-directory-base"></a>Azure Active Directory-basis
Hallo volgende eigenschappen zijn algemene tooall Azure Active Directory-records.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| recordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | Hallo-type van Azure AD-gebeurtenis. |
| extendedProperties | Hallo uitgebreide eigenschappen van gebeurtenis hello Azure AD. |


### <a name="azure-active-directory-account-logon"></a>Aanmelding bij Azure Active Directory-Account
Deze records worden gemaakt wanneer een gebruiker in Active Directory probeert toolog op.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| recordType     | AzureActiveDirectoryAccountLogon |
| Toepassing | Hallo-toepassing die gebeurtenis Hallo account aanmelden, zoals Office 15. |
| Client | Meer informatie over client hello apparaat, een besturingssysteem van het apparaat en browser van een apparaat dat is gebruikt voor Hallo van Hallo account aanmelding gebeurtenis. |
| loginStatus | Deze eigenschap is rechtstreeks uit OrgIdLogon.LoginStatus. Hallo-toewijzing van verschillende interessante aanmeldingsfouten kan worden uitgevoerd door waarschuwingen algoritmen. |
| UserDomain | Hello Tenant identiteit informatie (TII). | 


### <a name="azure-active-directory"></a>Azure Active Directory
Deze records worden gemaakt wanneer een wijziging of toevoegingen tooAzure Active Directory-objecten worden gemaakt.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| recordType     | AzureActiveDirectory |
| AADTarget | Hallo-gebruiker die Hallo actie (aangeduid door Hallo eigenschap Operation) is uitgevoerd op. |
| Actor | Hallo-gebruiker of service-principal die Hallo actie is uitgevoerd. |
| ActorContextId | GUID van Hallo organisatie die actor Hallo Hallo behoort. |
| ActorIpAddress | Hallo actor van IP-adres in de notatie voor IPV4 of IPV6-adres. |
| InterSystemsId | Hallo GUID die Hallo acties houden over onderdelen in Hallo Office 365-service. |
| IntraSystemId |   Hallo GUID die wordt gegenereerd door de Azure Active Directory tootrack Hallo actie. |
| SupportTicketId | Hallo klantondersteuning ticket-ID voor de actie in situaties "act-op-andere gebruikers-of" Hallo. |
| TargetContextId | GUID van het Hallo-organisatie die de gebruiker in de doelgroep Hallo Hallo behoort. |


### <a name="data-center-security"></a>Data Center-beveiliging
Deze records worden gemaakt van controlegegevens Center gegevensbeveiliging.  

| Eigenschap | Beschrijving |
|:--- |:--- |
| EffectiveOrganization | Hallo-naam van het Hallo-tenant die uitbreiding van bevoegdheden/cmdlet Hallo is gericht op. |
| ElevationApprovedTime | Hallo tijdstempel voor wanneer Hallo verhoging is goedgekeurd. |
| ElevationApprover | Hallo-naam van een Microsoft-manager. |
| ElevationDuration | Hallo duur voor welke Hallo uitbreiding van bevoegdheden actief was. |
| ElevationRequestId |  Een unieke id voor Hallo uitbreiding van bevoegdheden aanvraag. |
| ElevationRole | Hallo rol Hallo verhoging is aangevraagd voor. |
| ElevationTime | Hallo begintijd van Hallo uitbreiding van bevoegdheden. |
| Start_Time | Hallo begintijd van de uitvoering van Hallo-cmdlets. |


### <a name="exchange-admin"></a>Exchange-beheerder
Deze records worden gemaakt wanneer er wijzigingen zijn aangebracht tooExchange configuratie.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | Exchange |
| recordType     | ExchangeAdmin |
| ExternalAccess |  Hiermee geeft u op of Hallo cmdlet is uitgevoerd door een gebruiker in uw organisatie, door medewerkers van Microsoft-datacenter of in een datacenter-serviceaccount of door een gedelegeerde beheerder. Hallo waarde False wordt aangegeven dat die Hallo-cmdlet is uitgevoerd door iemand die in uw organisatie. Hallo waarde True geeft aan dat Hallo-cmdlet is uitgevoerd door datacenter personeel, een datacenter-serviceaccount of een gedelegeerde beheerder. |
| ModifiedObjectResolvedName |  Dit is Hallo gebruiker beschrijvende naam van Hallo-object dat door de cmdlet Hallo is gewijzigd. Dit is alleen geregistreerd als Hallo cmdlet Hallo-object wijzigt. |
| Organisatienaam | de naam van de Hallo van Hallo-tenant. |
| OriginatingServer | Hallo-naam van Hallo-server uit welke Hallo cmdlet is uitgevoerd. |
| Parameters | Hallo-naam en waarde voor alle parameters die zijn gebruikt met Hallo cmdlet die wordt geïdentificeerd in Hallo Operations-eigenschap. |


### <a name="exchange-mailbox"></a>Exchange-postvak
Deze records worden gemaakt wanneer wijzigingen of toevoegingen tooExchange postvakken worden gemaakt.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | Exchange |
| recordType     | ExchangeItem |
| ClientInfoString | Informatie over Hallo e-mailclient die gebruikt tooperform Hallo bewerking, zoals een browserversie, de Outlook-versie en de informatie van mobiele apparaten is. |
| Client_IPAddress | Hallo IP-adres van Hallo-apparaat dat is gebruikt bij het Hallo-bewerking is vastgelegd. Hallo IP-adres wordt weergegeven in de notatie voor een IPv4- of IPv6-adres. |
| ClientMachineName | de computernaam die als host fungeert voor de Outlook-client Hallo Hallo. |
| ClientProcessName | Hallo e-mailclient die gebruikte tooaccess Hallo postvak is. |
| ClientVersion | Hallo-versie van het e-mailclient Hallo. |
| InternalLogonType | Gereserveerd voor intern gebruik. |
| Logon_Type | Geeft Hallo type gebruiker die Hallo Postvak geopend en uitgevoerd Hallo-bewerking die is vastgelegd. |
| LogonUserDisplayName |    Hallo gebruiksvriendelijke naam van gebruiker Hallo Hallo bewerking uitgevoerd. |
| LogonUserSid | Hallo-SID van gebruiker Hallo die Hallo bewerking uitgevoerd. |
| MailboxGuid | Hallo Exchange-GUID van Hallo postvak dat is geopend. |
| MailboxOwnerMasterAccountSid | Postvak eigenaarsaccount hoofdaccount SID. |
| MailboxOwnerSid | SID van de eigenaar van het Postvak Hallo Hallo. |
| MailboxOwnerUPN | Hallo e-mailadres van Hallo eigenaar Hallo postvak dat is geopend. |


### <a name="exchange-mailbox-audit"></a>Exchange-postvak Audit
Deze records worden gemaakt wanneer u een vermelding postvak wordt gemaakt.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | Exchange |
| recordType     | ExchangeItem |
| Item | Hiermee geeft u Hallo item bij welke Hallo bewerking is uitgevoerd | 
| SendAsUserMailboxGuid | Hallo Exchange-GUID van Hallo postvak dat is geopend toosend e-mail als. |
| SendAsUserSmtp | SMTP-adres van Hallo gebruiker wordt geïmiteerd. |
| SendonBehalfOfUserMailboxGuid | Hallo Exchange-GUID van Hallo postvak dat is geopend toosend mail namens. |
| SendOnBehalfOfUserSmtp | SMTP-adres van de gebruiker Hallo op namens wie Hallo e-mailbericht wordt verzonden. |


### <a name="exchange-mailbox-audit-group"></a>Exchange-postvak Audit-groep
Deze records worden gemaakt wanneer wijzigingen of toevoegingen tooExchange groepen worden gemaakt.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Informatie over elk item in het Hallo-groep. |
| CrossMailboxOperations | Hiermee wordt aangegeven als Hallo bewerking meer dan één postvak betrokken. |
| DestMailboxId | Alleen ingesteld als Hallo CrossMailboxOperations parameter ingesteld op True is. Hiermee geeft u Hallo doelpostvak GUID. |
| DestMailboxOwnerMasterAccountSid | Alleen ingesteld als Hallo CrossMailboxOperations parameter ingesteld op True is. Hiermee geeft u Hallo SID voor Hallo hoofdaccount SID van de eigenaar van het Postvak Hallo doel. |
| DestMailboxOwnerSid | Alleen ingesteld als Hallo CrossMailboxOperations parameter ingesteld op True is. Hiermee geeft u Hallo SID van Hallo doelpostvak. |
| DestMailboxOwnerUPN | Alleen ingesteld als Hallo CrossMailboxOperations parameter ingesteld op True is. Hiermee geeft u Hallo UPN van de eigenaar Hallo van Hallo doelpostvak. |
| DestFolder | Hallo doelmap voor bewerkingen, zoals verplaatsen. |
| Map | Hallo-map is waarin een groep items zich bevindt. |
| Mappen |     Informatie over Hallo bronmappen die zijn betrokken bij een bewerking. Als bijvoorbeeld mappen zijn geselecteerd en vervolgens verwijderd. |


### <a name="sharepoint-base"></a>SharePoint-basis
Deze eigenschappen zijn algemene tooall SharePoint records.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | Geeft aan dat een gebeurtenis is opgetreden in SharePoint. Mogelijke waarden zijn SharePoint of ObjectModel. |
| itemType | Hallo type object dat is geopend of gewijzigd. Zie Hallo ItemType tabel voor meer informatie over Hallo soorten objecten. |
| MachineDomainInfo | Informatie over apparaat synchronisatiebewerkingen. Deze informatie wordt gerapporteerd als het aanwezig is in het Hallo-aanvraag. |
| MachineId |   Informatie over apparaat synchronisatiebewerkingen. Deze informatie wordt gerapporteerd als het aanwezig is in het Hallo-aanvraag. |
| Site_ | Hallo GUID van Hallo site waar Hallo-bestand of map toegankelijk is voor Hallo gebruiker zich bevindt. |
| Source_Name | Hallo-entiteit die geactiveerd Hallo gecontroleerd bewerking. Mogelijke waarden zijn SharePoint of ObjectModel. |
| UserAgent | Informatie over de client of de browser van Hallo gebruiker. Deze informatie wordt verstrekt door Hallo-client of de browser. |


### <a name="sharepoint-schema"></a>SharePoint-Schema
Deze records worden gemaakt wanneer u configuratiewijzigingen worden aangebracht tooSharePoint.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | Optionele tekenreeks voor aangepaste gebeurtenissen. |
| Event_Data |  De nettolading voor aangepaste gebeurtenissen is optioneel. |
| ModifiedProperties | Hallo-eigenschap is opgenomen voor admin-gebeurtenissen, zoals een gebruiker toe te voegen als lid van een site of een groep siteverzamelingen-beheerder. Hallo-eigenschap bevat de naam van de Hallo van Hallo-eigenschap die is aangepast (bijvoorbeeld Hallo beheerder van de Site-groep), nieuwe waarde van Hallo gewijzigd eigenschap (dergelijke Hallo-gebruiker die als een beheerder van de site is toegevoegd) en de vorige waarde Hallo Hallo gewijzigd object Hallo. |


### <a name="sharepoint-file-operations"></a>SharePoint-bestandsbewerkingen
Deze records worden gemaakt in het antwoord toofile bewerkingen in SharePoint.

| Eigenschap | Beschrijving |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | bestandsextensie Hallo van een bestand dat wordt verplaatst of gekopieerd. Deze eigenschap wordt alleen weergegeven voor FileCopied en FileMoved gebeurtenissen. |
| DestinationFileName | Hallo-naam van Hallo-bestand wordt gekopieerd of verplaatst. Deze eigenschap wordt alleen weergegeven voor FileCopied en FileMoved gebeurtenissen. |
| DestinationRelativeUrl | Hallo-URL van de doelmap Hallo waar een bestand wordt gekopieerd of verplaatst. Hallo combinatie van waarden voor parameters SiteURL, DestinationRelativeURL en DestinationFileName Hallo is Hallo dezelfde is als Hallo-waarde voor de eigenschap ObjectID hello, die Hallo volledige padnaam voor Hallo-bestand dat is gekopieerd. Deze eigenschap wordt alleen weergegeven voor FileCopied en FileMoved gebeurtenissen. |
| SharingType | Hallo-type van de machtigingen die zijn toegewezen gebruiker toohello die Hallo resource is gedeeld met delen. Deze gebruiker wordt geïdentificeerd door Hallo UserSharedWith parameter. |
| Site_Url | Hallo-URL van Hallo site waar Hallo-bestand of map toegankelijk is voor Hallo gebruiker zich bevindt. |
| SourceFileExtension | bestandsextensie Hallo van Hallo-bestand dat door de gebruiker Hallo is geopend. Deze eigenschap is leeg als Hallo-object dat is geopend, een map is. |
| Bronbestandsnaam |  Hallo-naam van het Hallo-bestand of map door de gebruiker Hallo geopend. |
| SourceRelativeUrl | Hallo-URL van Hallo-map die toegankelijk is voor de gebruiker Hallo Hallo-bestand bevat. Hallo combinatie van waarden voor de parameters SiteURL, SourceRelativeURL en bronbestandsnaam Hallo Hallo is hetzelfde als het Hallo-waarde voor Hallo ObjectID eigenschap, die de volledige padnaam Hallo voor Hallo-bestand gebruikt door de gebruiker Hallo Hallo. |
| UserSharedWith |  Hallo-gebruiker die met een bron is gedeeld. |




## <a name="sample-log-searches"></a>Voorbeeldzoekopdrachten in logboeken
Hallo volgende tabel biedt een voorbeeld-logboek zoekt bijwerkrecords die door deze oplossing worden verzameld.

| Query’s uitvoeren | Beschrijving |
| --- | --- |
|Telling van alle Hallo-bewerkingen voor uw Office 365-abonnement |"Type = OfficeActivity | meten count() voor bewerking ' |
|Informatie over het gebruik van SharePoint-sites|"Type = OfficeActivity OfficeWorkload = sharepoint | meting count() als SiteUrl tellen | Aantal asc sorteren '|
|Toegang bestandsbewerkingen door gebruikerstype|"Type = OfficeActivity OfficeWorkload sharepoint bewerking = FileAccessed = | meten count() door UserType'|
|Zoeken met specifieke trefwoorden|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Externe acties van de monitor op Exchange|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Problemen oplossen

Als uw Office 365-oplossing is geen gegevens verzameld zoals verwacht, Controleer de status op Hallo OMS-portal op **instellingen** -> **verbonden bronnen** -> **Office 365** . Hallo volgende tabel beschrijft elke status.

| Status | Beschrijving |
|:--|:--|
| Actief | Hallo Office 365-abonnement actief is en Hallo werkbelasting is met succes verbonden tooyour OMS-werkruimte. |
| In behandeling | Hallo Office 365-abonnement actief is, maar Hallo werkbelasting is nog niet tooyour OMS-werkruimte is verbonden. Hallo zijn eerste keer dat u verbinding maakt met Hallo Office 365-abonnement, met alle Hallo werkbelastingen op deze status totdat ze zijn verbonden. Wacht 24 uur totdat alle Hallo werkbelastingen tooswitch tooActive. |
| Inactieve | Hallo Office 365-abonnement is in een inactieve status heeft. Controleer op de pagina van uw Office 365-beheerder voor meer informatie. Nadat u uw Office 365-abonnement hebt geactiveerd, wordt het ontkoppelen van OMS-werkruimte en koppelt u deze opnieuw toostart ontvangen van gegevens. |



## <a name="next-steps"></a>Volgende stappen
* Logboek van zoekopdrachten in gebruiken [logboekanalyse](../log-analytics/log-analytics-log-searches.md) tooview gedetailleerde gegevens bijwerken.
* [Maak uw eigen dashboards](../log-analytics/log-analytics-dashboards.md) toodisplay uw favoriete zoekopdrachten voor Office 365.
* [Waarschuwingen maken](../log-analytics/log-analytics-alerts.md) toobe proactief een melding van belangrijke Office 365-activiteiten.  
