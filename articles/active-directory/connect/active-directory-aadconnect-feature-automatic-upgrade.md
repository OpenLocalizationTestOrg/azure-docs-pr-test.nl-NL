---
title: 'Azure AD Connect: Automatische upgrade | Microsoft Docs'
description: Dit onderwerp beschrijft Hallo ingebouwde automatische upgradefunctie in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b395e8f-fa3c-4e55-be54-392dd303c472
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 70d15eb3adf7758d8a43d278157daa504e059a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-automatic-upgrade"></a>Azure AD Connect: automatische upgrade
Deze functie is geïntroduceerd met build 1.1.105.0 (uitgebracht februari 2016).

## <a name="overview"></a>Overzicht
Zorg dat uw Azure AD Connect-installatie is altijd toodate is nooit zo eenvoudig Hello **Automatische upgrade** functie. Deze functie is standaard ingeschakeld voor snelle installatie en upgrade van DirSync. Wanneer een nieuwe versie wordt uitgebracht, wordt de installatie automatisch bijgewerkt.

Automatische upgrade is standaard ingeschakeld voor de volgende Hallo:

* Snelle installatie instellingen en DirSync-upgrades.
* Met behulp van SQL Express LocalDB, dit is wat snelle instellingen altijd gebruiken. DirSync met SQL Express ook LocalDB gebruiken.
* Hallo AD-account is Hallo standaard MSOL_ account gemaakt door snelle instellingen en DirSync.
* Minder dan 100.000 objecten in de metaverse Hallo hebben.

huidige status van de automatische upgrade Hallo kan worden weergegeven met de PowerShell-cmdlet Hallo `Get-ADSyncAutoUpgrade`. Hallo volgende statussen heeft:

| Status | Opmerking |
| --- | --- |
| Ingeschakeld |Automatische upgrade is ingeschakeld. |
| Onderbroken |Stel door alleen Hallo-systeem. Hallo-systeem is niet meer in aanmerking komende tooreceive automatische upgrades. |
| Uitgeschakeld |Automatische upgrade is uitgeschakeld. |

U kunt schakelen tussen **ingeschakeld** en **uitgeschakelde** met `Set-ADSyncAutoUpgrade`. Alleen Hallo system mogen Hallo status instellen **onderbroken**.

Automatische upgrade maakt gebruik van Azure AD Connect Health voor upgrade Hallo-infrastructuur. Zorg ervoor dat u Hallo URL's hebt geopend in uw proxyserver voor voor automatische upgrade toowork, **Azure AD Connect Health** zoals beschreven in [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Als hello **Synchronization Service Manager** gebruikersinterface op Hallo-server wordt uitgevoerd en vervolgens hello upgrade wordt onderbroken totdat Hallo UI is gesloten.

## <a name="troubleshooting"></a>Problemen oplossen
Als de Connect-installatie niet automatisch bijgewerkt wanneer wordt zoals verwacht, volgt u deze stappen toofind uit wat is mogelijk onjuist.

Eerst moet u niet verwachten Hallo Automatische upgrade toobe geprobeerd Hallo eerste dag die een nieuwe versie wordt uitgebracht. Er is een opzettelijke aanvraaggrootte voordat u een upgrade wordt uitgevoerd, zodat normaal als de installatie onmiddellijk wordt niet bijgewerkt.

Als u denkt iets niet goed is dat, klikt u vervolgens voert u eerst `Get-ADSyncAutoUpgrade` tooensure Automatische upgrade is ingeschakeld.

Controleer vervolgens of dat u Hallo vereist URL's in uw proxy of firewall hebt geopend. Is het automatisch bijwerken met behulp van Azure AD Connect Health zoals beschreven in Hallo [overzicht](#overview). Als u een proxy gebruikt, te controleren of Health is geconfigureerde toouse een [proxyserver](../connect-health/active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy). Ook testen Hallo [Health connectiviteit](../connect-health/active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service) tooAzure AD.

Hallo connectiviteit tooAzure AD geverifieerd, is het tijd toolook in gebeurtenislogboeken meer Hallo. Start Logboeken Hallo en bekijkt hello **toepassing** eventlog. Een filter eventlog voor Hallo-bron toevoegen **Azure AD Connect Upgrade** en Hallo gebeurtenis-id-bereik **300 399**.  
![Eventlog-filter voor de automatische upgrade](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogfilter.png)  

U ziet nu Hallo-gebeurtenislogboeken die zijn gekoppeld aan het Hallo-status voor automatische upgrade.  
![Eventlog-filter voor de automatische upgrade](./media/active-directory-aadconnect-feature-automatic-upgrade/eventlogresult.png)  

Hallo resultaatcode heeft een voorvoegsel en met een overzicht van Hallo staat.

| Het voorvoegsel van de resultaat | Beschrijving |
| --- | --- |
| Geslaagd |Hallo-installatie is bijgewerkt. |
| UpgradeAborted |Een tijdelijke situatie Hallo upgrade gestopt. Deze opnieuw uit te voeren en Hallo verwachting is dat later lukt. |
| UpgradeNotSupported |Hallo systeem heeft een configuratie die blokkeert Hallo systeem automatisch wordt bijgewerkt. Er is geprobeerd toosee als Hallo status wordt gewijzigd, maar Hallo verwachting is dat Hallo systeem handmatig moet worden bijgewerkt. |

Hier volgt een lijst met de meest voorkomende Hallo-berichten u vindt. Deze lijst bevat niet alle, maar het resultaat Hallo-bericht moet wissen met welk probleem Hallo is.

| Resultaat bericht | Beschrijving |
| --- | --- |
| **UpgradeAborted** | |
| UpgradeAbortedCouldNotSetUpgradeMarker |Kan niet toohello register schrijven. |
| UpgradeAbortedInsufficientDatabasePermissions |Hallo ingebouwde groep administrators heeft geen machtigingen toohello database. Handmatig bijwerken toohello meest recente versie van Azure AD Connect tooaddress dit probleem. |
| UpgradeAbortedInsufficientDiskSpace |Er is onvoldoende ruimte schijf toosupport een upgrade. |
| UpgradeAbortedSecurityGroupsNotPresent |Kan niet zoeken en los alle beveiligingsgroepen die worden gebruikt door Hallo synchronisatie-engine. |
| UpgradeAbortedServiceCanNotBeStarted |Hallo NT-Service **Microsoft Azure AD Sync** toostart is mislukt. |
| UpgradeAbortedServiceCanNotBeStopped |Hallo NT-Service **Microsoft Azure AD Sync** toostop is mislukt. |
| UpgradeAbortedServiceIsNotRunning |Hallo NT-Service **Microsoft Azure AD Sync** wordt niet uitgevoerd. |
| UpgradeAbortedSyncCycleDisabled |de optie SyncCycle in Hallo Hallo [scheduler](active-directory-aadconnectsync-feature-scheduler.md) is uitgeschakeld. |
| UpgradeAbortedSyncExeInUse |Hallo [service Synchronisatiebeheer UI](active-directory-aadconnectsync-service-manager-ui.md) is geopend op Hallo-server. |
| UpgradeAbortedSyncOrConfigurationInProgress |Hallo-installatiewizard wordt uitgevoerd of een synchronisatie buiten Hallo scheduler is gepland. |
| **UpgradeNotSupported** | |
| UpgradeNotSupportedCustomizedSyncRules |U kunt uw eigen aangepaste regels toohello configuratie hebt toegevoegd. |
| UpgradeNotSupportedDeviceWritebackEnabled |U hebt ingeschakeld Hallo [apparaat terugschrijven](active-directory-aadconnect-feature-device-writeback.md) functie. |
| UpgradeNotSupportedGroupWritebackEnabled |U hebt ingeschakeld Hallo [Write-back van groep](active-directory-aadconnect-feature-preview.md#group-writeback) functie. |
| UpgradeNotSupportedInvalidPersistedState |Hallo-installatie is niet een snelle instellingen of een upgrade van DirSync. |
| UpgradeNotSupportedMetaverseSizeExceeeded |U hebt meer dan 100.000 objecten in Hallo metaverse. |
| UpgradeNotSupportedMultiForestSetup |U verbinding maakt toomore dan één forest. Snelle installatie verbinding alleen tooone forest. |
| UpgradeNotSupportedNonLocalDbInstall |U maakt geen gebruik van een SQL Server Express LocalDB-database. |
| UpgradeNotSupportedNonMsolAccount |Hallo [AD Connector-account](active-directory-aadconnect-accounts-permissions.md#active-directory-account) is niet-standaardaccount MSOL_ Hallo meer. |
| UpgradeNotSupportedStagingModeEnabled |Hallo server toobe is ingesteld in [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode). |
| UpgradeNotSupportedUserWritebackEnabled |U hebt ingeschakeld Hallo [Write-back van gebruiker](active-directory-aadconnect-feature-preview.md#user-writeback) functie. |

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
