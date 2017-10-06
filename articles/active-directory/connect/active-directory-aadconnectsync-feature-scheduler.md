---
title: 'Azure AD Connect-synchronisatie: Scheduler | Microsoft Docs'
description: Dit onderwerp beschrijft de functie van de Hallo ingebouwde scheduler in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: c587039cc68d305862a07beff364894b6f74cd2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-scheduler"></a>Azure AD Connect-synchronisatie: Scheduler
Dit onderwerp wordt beschreven Hallo ingebouwde scheduler in Azure AD Connect-synchronisatie (ook synchronisatie-engine).

Deze functie is geïntroduceerd met build 1.1.105.0 (uitgebracht februari 2016).

## <a name="overview"></a>Overzicht
Azure AD Connect-synchronisatie synchroniseren veranderingen in uw lokale directory met behulp van een scheduler. Er zijn twee scheduler processen, één voor Wachtwoordsynchronisatie en één voor de synchronisatie en het onderhoud taken/het kenmerk object. Dit onderwerp worden de laatste Hallo.

In eerdere versies was Hallo planner voor objecten en kenmerken externe toohello synchronisatie-engine. Het Windows Taakplanner of een afzonderlijke Windows service tootrigger Hallo synchronisatieproces gebruikt. Hallo scheduler is met Hallo 1.1 releases ingebouwde toohello synchronisatie-engine en enige aanpassing staan. Hallo Synchronisatiefrequentie met nieuwe standaardwaarde is 30 minuten.

Hallo scheduler is verantwoordelijk voor twee taken:

* **Synchronisatiecyclus**. Hallo proces tooimport, synchroniseren en wijzigingen exporteren.
* **Onderhoudstaken**. Vernieuwen van sleutels en certificaten voor wachtwoord opnieuw instellen en Device Registration Service (DRS). Oude vermeldingen in Hallo operations logboek opschonen.

Hallo scheduler zelf altijd wordt uitgevoerd, maar deze kan worden geconfigureerd tooonly een of geen van deze taken uitvoeren. Bijvoorbeeld, als u uw eigen cyclus synchronisatieproces toohave moet, kunt u uitschakelen door deze taak in Hallo scheduler maar nog steeds uitgevoerd Hallo onderhoudstaak.

## <a name="scheduler-configuration"></a>Scheduler-configuratie
toosee uw huidige configuratieinstellingen, gaat u tooPowerShell en voer `Get-ADSyncScheduler`. U ziet dat lijkt op deze afbeelding:

![GetSyncScheduler](./media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

Als u ziet **Hallo synchronisatieopdracht of cmdlet is niet beschikbaar** wanneer u deze cmdlet uitvoert, klikt u vervolgens Hallo PowerShell-module is niet geladen. Dit probleem kan optreden als u Azure AD Connect op een domeincontroller of op een server met hogere niveaus van PowerShell beperking dan Hallo standaardinstellingen uitgevoerd. Als u deze fout ziet, voert u `Import-Module ADSync` toomake Hallo cmdlet die beschikbaar is.

* **AllowedSyncCycleInterval**. Hallo kortste tijdsinterval tussen synchronisatie cycli toegestaan door Azure AD. U vaker dan deze instelling kan niet worden gesynchroniseerd en nog steeds worden ondersteund.
* **CurrentlyEffectiveSyncCycleInterval**. Hallo planning momenteel van kracht. Deze heeft dezelfde als CustomizedSyncInterval waarde hello (indien ingesteld) als dit niet vaker dan AllowedSyncInterval. Als u een build voordat 1.1.281 gebruiken en u CustomizedSyncCycleInterval wijzigt, wordt deze wijziging van kracht na de volgende synchronisatiecyclus. Vanaf build 1.1.281 wordt Hallo wijziging direct van kracht.
* **CustomizedSyncCycleInterval**. Als u Hallo scheduler toorun op een andere frequentie dan Hallo standaard 30 minuten wilt, configureert u deze instelling. In vorige Hallo afbeelding, is Hallo scheduler ingesteld toorun elk uur in plaats daarvan. Als u deze instelling tooa waarde lager dan AllowedSyncInterval instelt, wordt deze laatste Hallo gebruikt.
* **NextSyncCyclePolicyType**. Delta of initiële. Hiermee wordt aangegeven of een volgende keer uitvoert Hallo alleen nog deltawijzigingen proces moet of hello volgende run als een volledige doen moet importeren en synchroniseren. Hallo laatstgenoemde zou ook opnieuw verwerken alle nieuwe of gewijzigde regels.
* **NextSyncCycleStartTimeInUTC**. Hallo scheduler begint zodra Hallo volgende synchronisatiecyclus.
* **PurgeRunHistoryInterval**. Hallo time-bewerking logboeken moeten blijven. Deze logboeken kunnen worden gecontroleerd in Hallo synchronisatie servicemanager. Standaard Hallo tookeep deze logboeken is 7 dagen.
* **SyncCycleEnabled**. Hiermee wordt aangegeven of Hallo scheduler Hallo import, synchronisatie en processen voor exporteren wordt uitgevoerd als onderdeel van de werking ervan.
* **MaintenanceEnabled**. Geeft als Hallo onderhoudsproces is ingeschakeld. Hallo certificaten/sleutels die worden bijgewerkt en schoont Hallo operations logboek.
* **StagingModeEnabled**. Toont als [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode) is ingeschakeld. Als deze instelling is ingeschakeld, wordt vervolgens het onderdrukt Hallo uitvoer wordt uitgevoerd, maar nog steeds import en synchronisatie uitvoeren.
* **SchedulerSuspended**. Ingesteld door Connect tijdens een upgrade tootemporarily blok Hallo scheduler wordt uitgevoerd.

U kunt sommige van deze instellingen met wijzigen `Set-ADSyncScheduler`. Hallo volgende parameters kan worden gewijzigd:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

In eerdere versies van Azure AD Connect **isStagingModeEnabled** is weergegeven in de Set ADSyncScheduler. Het is **niet-ondersteunde** tooset deze eigenschap. eigenschap Hallo **SchedulerSuspended** moet alleen worden gewijzigd door te verbinden. Het is **niet-ondersteunde** tooset dit met PowerShell rechtstreeks.

Hallo scheduler configuratie wordt opgeslagen in Azure AD. Als er een testserver is, elke wijziging in de primaire server Hallo ook van invloed op Hallo staging-server (met uitzondering van IsStagingModeEnabled).

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Syntaxis:`Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - dagen, uu - uren, mm - minuten en ss - seconden

Voorbeeld:`Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Wijzigingen Hallo scheduler toorun elke drie uur.

Voorbeeld:`Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Wijzigingen Hallo scheduler toorun dagelijks worden gewijzigd.

### <a name="disable-hello-scheduler"></a>Hallo scheduler uitschakelen  
Als u configuratiewijzigingen toomake nodig, wilt u toodisable Hallo scheduler. Bijvoorbeeld, wanneer u [configureert filtering](active-directory-aadconnectsync-configure-filtering.md) of [aanbrengen toosynchronization regels](active-directory-aadconnectsync-change-the-configuration.md).

toodisable hello scheduler, voer `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Hallo scheduler uitschakelen](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

Wanneer u uw wijzigingen hebt aangebracht, vergeet niet tooenable Hallo scheduler opnieuw met `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-hello-scheduler"></a>Hallo scheduler starten
Hallo scheduler wordt standaard elke 30 minuten uitgevoerd. In sommige gevallen wilt u misschien een synchronisatie tussen Hallo cyclus toorun cycli gepland of moet u een ander type toorun.

**Delta-synchronisatiecyclus**  
Een delta-synchronisatiecyclus bevat Hallo stappen te volgen:

* Delta-import op alle Connectors
* Deltasynchronisatie op alle Connectors
* Op alle Connectors exporteren

Kan het zijn dat u een urgente hebt wijzigen die onmiddellijk moet worden gesynchroniseerd en daarom moet u toomanually een cyclus uitgevoerd. Als u toomanually moet een cyclus vervolgens uitvoeren van PowerShell uitgevoerd `Start-ADSyncSyncCycle -PolicyType Delta`.

**Volledige synchronisatiecyclus**  
Als u een van de volgende configuratiewijzigingen Hallo hebt aangebracht, moet u toorun een volledige synchronisatiecyclus (ook Initiële):

* Meer objecten of -kenmerken toobe geïmporteerd uit een bronmap toegevoegd
* Wijzigingen aangebracht toohello synchronisatieregels
* Gewijzigd [filteren](active-directory-aadconnectsync-configure-filtering.md) zodat een verschillend aantal objecten opgenomen worden moet

Als u een van deze wijzigingen hebt aangebracht, moet u een volledige synchronisatie cyclus zodat Hallo synchronisatie-engine heeft Hallo kans tooreconsolidate Hallo-connectorspaces toorun. Een volledige synchronisatiecyclus bevat Hallo stappen te volgen:

* Volledige Import op alle Connectors
* Volledige synchronisatie van alle Connectors
* Op alle Connectors exporteren

tooinitiate een volledige synchronisatie-cyclus uitgevoerd `Start-ADSyncSyncCycle -PolicyType Initial` vanuit een PowerShell-prompt. Deze opdracht start een volledige synchronisatie-cyclus.

## <a name="stop-hello-scheduler"></a>Hallo scheduler stoppen
Als Hallo scheduler een synchronisatiecyclus momenteel wordt uitgevoerd, moet u mogelijk toostop deze. Als u Hallo-installatiewizard te starten en u beschikt over deze fout bijvoorbeeld:

![SyncCycleRunningError](./media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

Wanneer een synchronisatiecyclus wordt uitgevoerd, kunt u kunt geen configuratiewijzigingen aanbrengen. U kan wachten tot Hallo scheduler Hallo-proces is voltooid, maar u deze ook stoppen kunt zodat u onmiddellijk uw wijzigingen kunt aanbrengen. Hallo huidige cyclus wordt gestopt, is geen schadelijke en wijzigingen in behandeling worden verwerkt door de volgende keer uitvoert.

1. Begin door te vertellen Hallo scheduler toostop de huidige cyclus met PowerShell-cmdlet Hallo `Stop-ADSyncSyncCycle`.
2. Als u een build voordat 1.1.281 gebruiken, wordt gestopt Hallo scheduler niet Hallo huidige stopt Connector van de huidige taak. tooforce Hallo Connector toostop, nemen Hallo van de volgende activiteiten: ![StopAConnector](./media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Start **synchronisatieservice** vanuit het startmenu Hallo. Ga te**Connectors**, Hallo Connector met Hallo status markeren **met**, en selecteer **stoppen** van Hallo acties.

Hallo scheduler nog steeds actief is en wordt opnieuw gestart op de eerstvolgende gelegenheid installeren.

## <a name="custom-scheduler"></a>Aangepaste scheduler
Hallo-cmdlets beschreven in deze sectie zijn alleen beschikbaar in build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) en hoger.

Als de ingebouwde scheduler Hallo voldoet niet aan uw vereisten, kunt u Hallo Connectors met behulp van PowerShell plannen.

### <a name="invoke-adsyncrunprofile"></a>Aanroepen ADSyncRunProfile
Voor een verbindingslijn op deze manier kunt u een profiel starten:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

Hallo namen toouse voor [Connector namen](active-directory-aadconnectsync-service-manager-ui-connectors.md) en [groepnamen van profielen uitvoeren](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) vindt u in Hallo [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).

![Uitvoeringsprofiel aanroepen](./media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

Hallo `Invoke-ADSyncRunProfile` cmdlet synchroon is, dat wil zeggen, deze geen retourneert besturingselement totdat Hallo Connector Hallo-bewerking is voltooid is of met een fout.

Wanneer u uw Connectors plant, Hallo aanbeveling tooschedule wordt deze in volgorde Hallo:

1. (Volledige/Delta) Importeren uit een on-premises adreslijsten, zoals Active Directory
2. (Volledige/Delta) Importeren uit Azure AD
3. (Volledige/Delta) Synchronisatie van on-premises adreslijsten, zoals Active Directory
4. (Volledige/Delta) Synchronisatie van Azure AD
5. TooAzure AD exporteren
6. Exporteren van tooon-premises mappen, zoals Active Directory

Deze volgorde is hoe Hallo Connectors in Hallo ingebouwde scheduler wordt uitgevoerd.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
U kunt ook Hallo sync engine toosee bewaken als dit bezet is of niet-actief. Deze cmdlet retourneert een leeg resultaat als Hallo synchronisatie-engine niet actief is en niet een Connector wordt uitgevoerd. Als een Connector wordt uitgevoerd, retourneert het Hallo-naam van Hallo Connector.

```
Get-ADSyncConnectorRunStatus
```

![Uitvoeringsstatus van de connector](./media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
In vorige Hallo afbeelding, wordt de eerste regel Hallo is vanuit een status waarbij Hallo synchronisatie-engine niet actief is. de tweede regel Hallo uit wanneer hello Azure AD-Connector wordt uitgevoerd.

## <a name="scheduler-and-installation-wizard"></a>Wizard Scheduler en installatie
Als u Hallo-installatiewizard te starten, klikt u vervolgens Hallo scheduler tijdelijk onderbroken. Dit gedrag is omdat ervan wordt uitgegaan configuratiewijzigingen die u maakt en deze instellingen kunnen niet worden toegepast als de synchronisatie-engine Hallo actief wordt uitgevoerd. Om deze reden niet laten Hallo-installatiewizard openen omdat stopt Hallo synchronisatie-engine geen synchronisatie acties kan uitvoeren.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
