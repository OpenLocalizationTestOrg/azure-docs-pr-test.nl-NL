---
title: 'Azure AD Connect: upgraden van DirSync | Microsoft Docs'
description: Meer informatie over hoe tooupgrade van DirSync tooAzure AD Connect. In dit artikel beschrijft Hallo stappen voor het upgraden van DirSync tooAzure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: upgraden van DirSync
Azure AD Connect is Hallo opvolgende tooDirSync. Hallo manieren voor het upgraden van DirSync in dit onderwerp vindt u. Deze stappen werken niet voor een upgrade van een andere versie van Azure AD Connect of Azure AD Sync.

Zorg voordat u begint met de installatie van Azure AD Connect te[Azure AD Connect downloadt](http://go.microsoft.com/fwlink/?LinkId=615771) en volledige Hallo vereiste stappen in [Azure AD Connect: Hardware en vereisten](active-directory-aadconnect-prerequisites.md). In het bijzonder gewenste tooread over de volgende hello, aangezien deze gebieden verschillende van DirSync zijn:

* Hallo vereiste versie van .net- en PowerShell. Nieuwere versies zijn vereist toobe op Hallo server dan wat DirSync nodig is.
* Hallo proxyserverconfiguratie. Als u een proxy server tooreach Hallo internet, moet deze instelling worden geconfigureerd voordat u een upgrade. DirSync gebruikt altijd Hallo proxyserver geconfigureerd voor Hallo gebruiker te installeren, maar de instellingen voor de Azure AD Connect maakt gebruik van de computer in plaats daarvan.
* Hallo-URL's vereist toobe open Hallo proxyserver. Hallo-vereisten zijn voor basisscenario's, de scenario's ook ondersteund door DirSync, Hallo dezelfde. Als u toouse Hallo nieuwe functies opgenomen met Azure AD Connect wilt, kunnen enkele nieuwe URL's moeten worden geopend.

> [!NOTE]
> Wanneer u uw nieuwe Azure AD Connect-server toostart synchroniseren wijzigingen tooAzure AD hebt ingeschakeld, moet u niet terugdraaien toousing DirSync of Azure AD Sync. Downgraden van Azure AD Connect toolegacy clients zoals DirSync en Azure AD Sync wordt niet ondersteund en tooissues zoals gegevensverlies kan leiden in Azure AD.

Als u de upgrade niet vanaf DirSync wilt uitvoeren, zie dan [verwante documentatie](#related-documentation) voor andere scenario's.

## <a name="upgrade-from-dirsync"></a>Upgraden van DirSync
Er zijn verschillende opties voor Hallo upgrade, afhankelijk van uw huidige DirSync-implementatie. Als Hallo tijd voor de upgrade is minder dan drie uur verwachte, is de aanbeveling Hallo toodo een in-place upgrade. Als Hallo tijd voor de upgrade is meer dan drie uur verwacht, is de aanbeveling Hallo toodo een parallelle implementatie op een andere server. Schatting dat als u meer dan 50.000 objecten hebt duurt langer dan drie uur toodo Hallo upgrade.

| Scenario |
| --- | --- |
| [In-place upgrade](#in-place-upgrade) |
| [Parallelle implementatie](#parallel-deployment) |

> [!NOTE]
> Wanneer u van plan bent tooupgrade van DirSync tooAzure AD Connect, komen niet zelf DirSync verwijderen vóór de upgrade Hallo. Azure AD Connect leest en Hallo-configuratie migreren van DirSync en verwijderen na het inspecteren Hallo-server.

**In-place upgrade**  
Hallo verwacht tijd toocomplete Hallo upgrade wordt weergegeven door het Hallo-wizard. Deze schatting is gebaseerd op Hallo veronderstelling dat het duurt drie uur toocomplete een upgrade voor een database met 50.000 objecten (gebruikers, contactpersonen en groepen voordat). Als het aantal objecten in de database Hallo minder dan 50.000 is, raadt Azure AD Connect een in-place upgrade. Als u toocontinue besluit, de huidige instellingen automatisch toegepast tijdens de upgrade en de server automatisch hervat actieve synchronisatie.

Als u toodo een configuratiemigratie wilt en een parallelle implementatie, kunt u Hallo in-place upgrade aanbeveling negeren. U kunt bijvoorbeeld Hallo kans toorefresh Hallo hardware en besturingssystemen uitvoeren. Zie voor meer informatie, Hallo [parallelle implementatie](#parallel-deployment) sectie.

**Parallelle implementatie**  
Als u meer dan 50.000 objecten hebt, wordt een parallelle implementatie aanbevolen. Deze implementatie voorkomt dat uw gebruikers last krijgen van een vertraagde service. Hello Azure AD Connect-installatie probeert tooestimate Hallo uitvaltijd voor Hallo upgrade, maar als u DirSync in Hallo verleden hebt geüpgraded, uw eigen ervaring waarschijnlijk toobe Hallo handleiding met aanbevolen is.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Ondersteunde DirSync configuraties toobe bijgewerkt
Hallo volgende configuratiewijzigingen worden ondersteund met bijgewerkte DirSync:

* Domein- en OE-filters
* Alternatief id (UPN)
* Wachtwoordsynchronisatie en Exchange hybrid uitwisselen
* Uw forest/domein- en Azure AD-instellingen
* Filteren op basis van gebruikerskenmerken

Hallo na wijziging kan niet worden bijgewerkt. Als u deze configuratie hebt, wordt Hallo upgrade geblokkeerd:

* Niet-ondersteunde DirSync-wijzigingen: bijvoorbeeld verwijderde kenmerken en het gebruik van een aangepaste extensie-DLL

![Upgrade geblokkeerd](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

In deze gevallen Hallo aanbeveling is tooinstall een nieuwe Azure AD Connect-server in [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode) en controleer of Hallo oude DirSync en nieuwe Azure AD Connect-configuratie. Pas eventuele wijzigingen aan met behulp van aangepaste configuratie, zoals beschreven in [Aangepaste configuratie Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md).

Hallo-wachtwoorden gebruikt door DirSync voor serviceaccounts Hallo kunnen niet worden opgehaald en worden niet gemigreerd. Deze wachtwoorden worden opnieuw ingesteld tijdens de upgrade Hallo.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>De stappen op hoog niveau voor het upgraden van DirSync tooAzure AD Connect
1. Welkom tooAzure AD Connect
2. Analyse van de huidige DirSync-configuratie
3. Azure AD globaal beheerderswachtwoord ophalen
4. Referenties voor een enterprise-beheerdersaccount (alleen gebruikt tijdens de installatie van Azure AD Connect Hallo) verzamelen
5. Installatie van Azure AD Connect
   * DirSync verwijderen (of tijdelijk uitschakelen)
   * Azure AD Connect installeren
   * Optioneel beginnen met synchroniseren

Extra stappen zijn vereist wanneer:

* U momenteel de volledige SQL Server gebruikt (lokaal of extern)
* U meer dan 50.000 objecten gereed hebt voor synchronisatie

## <a name="in-place-upgrade"></a>In-place upgrade
1. Start hello Azure AD Connect-installatieprogramma (MSI).
2. Bekijk en ik ga hiermee akkoord toolicense gebruiksrechtovereenkomst en privacyverklaring.  
   ![Welkom tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Klik op volgende toobegin analyse van uw bestaande DirSync-installatie.  
   ![Analyse van de huidige Directory Sync-installatie](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Als de Hallo analyse is voltooid, ziet u Hallo aanbevelingen voor het tooproceed.  
   * Als u SQL Server Express gebruiken en minder dan 50.000 objecten hebt, wordt Hallo volgende scherm weergegeven:  
     ![Analyse voltooid, gereed tooupgrade van DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Als u een volledige SQL Server voor DirSync gebruikt, ziet u in plaats daarvan deze pagina:  
     ![Analyse voltooid, gereed tooupgrade van DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     Hallo-informatie met betrekking tot Hallo bestaande SQL Server-databaseserver wordt gebruikt door DirSync wordt weergegeven. Maak, indien nodig, de juiste aanpassingen. Klik op **volgende** toocontinue Hallo-installatie.
   * Als u meer dan 50.000 objecten hebt, ziet u dit scherm:  
     ![Analyse voltooid, gereed tooupgrade van DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed met een in-place upgrade, klikt u op Hallo selectievakje volgende toothis bericht: **gaan met de upgrade van DirSync op deze computer.**
     toodo een [parallelle implementatie](#parallel-deployment) in plaats daarvan u Hallo DirSync-configuratie-instellingen exporteren en Hallo configuratie toohello nieuwe server te verplaatsen.
5. Hallo wachtwoord opgeven voor Hallo account waarmee u momenteel tooconnect tooAzure AD. Dit moet Hallo account momenteel wordt gebruikt door DirSync.  
   ![Voer uw Azure AD-referenties in](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Als u een foutbericht krijgt en problemen met de connectiviteit heeft, raadpleeg dan [Connectiviteitsproblemen oplossen](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Geef een enterprise-beheerdersaccount op voor Active Directory.  
   ![Voer uw ADDS-referenties in](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. U bent nu klaar tooconfigure. Wanneer u op **Upgrade** klikt, wordt DirSync verwijderd en Azure AD Connect geconfigureerd. De synchronisatie wordt gestart.  
   ![Gereed tooconfigure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Nadat het Hallo-installatie is voltooid, afmelden en aanmelden opnieuw tooWindows vóór u Synchronization Service Manager of Synchronization Rule Editor gaat gebruiken of toomake andere configuratiewijzigingen gaat.

## <a name="parallel-deployment"></a>Parallelle implementatie
### <a name="export-hello-dirsync-configuration"></a>Hallo DirSync-configuratie exporteren
**Parallelle implementatie met meer dan 50.000 objecten**

Als u meer dan 50.000 objecten hebt, Hallo raadt de Azure AD Connect-installatie een parallelle implementatie.

Er wordt een scherm vergelijkbare toohello volgende weergegeven:  
![Analyse voltooid](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Als u wilt dat tooproceed met parallelle implementatie, moet u tooperform Hallo stappen te volgen:

* Klik op Hallo **-instellingen exporteren** knop. Wanneer u Azure AD Connect op een afzonderlijke server installeert, worden deze instellingen worden gemigreerd van uw huidige DirSync tooyour nieuwe Azure AD Connect-installatie.

Wanneer uw instellingen zijn geëxporteerd, kunt u hello Azure AD Connect-wizard op Hallo DirSync-server afsluiten. Ga door met de volgende stap hello te[Azure AD Connect installeert op een afzonderlijke server](#installation-of-azure-ad-connect-on-separate-server)

**Parallelle implementatie met minder dan 50.000 objecten**

Als u minder dan 50.000 objecten hebt maar nog steeds toodo een parallelle implementatie wilt, klikt u vervolgens Hallo te volgen:

1. Hello Azure AD Connect-installatieprogramma (MSI) worden uitgevoerd.
2. Wanneer er Hallo **Welkom tooAzure AD Connect** scherm afsluiten Hallo-installatiewizard door te klikken op 'X' hello in Hallo rechtsboven Hallo-venster.
3. Open een opdrachtprompt.
4. Installeer vanuit Hallo locatie waar Azure AD Connect (standaard: C:\Program Files\Microsoft Azure Active Directory Connect) Hallo volgende opdracht uitvoeren: `AzureADConnect.exe /ForceExport`.
5. Klik op Hallo **-instellingen exporteren** knop. Wanneer u Azure AD Connect op een afzonderlijke server installeert, worden deze instellingen worden gemigreerd van uw huidige DirSync tooyour nieuwe Azure AD Connect-installatie.

![Analyse voltooid](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Wanneer uw instellingen zijn geëxporteerd, kunt u hello Azure AD Connect-wizard op Hallo DirSync-server afsluiten. Ga door met de volgende stap hello te[Azure AD Connect installeert op een afzonderlijke server](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Azure AD Connect op een afzonderlijke server installeren
Wanneer u Azure AD Connect op een nieuwe server installeert, is Hallo veronderstelling dat u wilt dat tooperform een schone installatie van Azure AD Connect. Omdat u wilt dat toouse Hallo DirSync-configuratie, moet u er een aantal extra stappen tootake zijn:

1. Hello Azure AD Connect-installatieprogramma (MSI) worden uitgevoerd.
2. Wanneer er Hallo **Welkom tooAzure AD Connect** scherm afsluiten Hallo-installatiewizard door te klikken op 'X' hello in Hallo rechtsboven Hallo-venster.
3. Open een opdrachtprompt.
4. Installeer vanuit Hallo locatie waar Azure AD Connect (standaard: C:\Program Files\Microsoft Azure Active Directory Connect) Hallo volgende opdracht uitvoeren: `AzureADConnect.exe /migrate`.
   Hello Azure AD Connect-installatiewizard wordt gestart en geeft u Hello scherm te volgen:  
   ![Voer uw Azure AD-referenties in](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Selecteer Hallo settings-bestand dat geëxporteerd vanuit uw DirSync-installatie.
6. Configureer de geavanceerde opties, inclusief:
   * Een aangepaste installatielocatie voor Azure AD Connect.
   * Een bestaand exemplaar van SQL Server (standaard: Azure AD Connect installeert SQL Server 2012 Express). Gebruik geen Hallo hetzelfde database-exemplaar als uw DirSync-server.
   * Een serviceaccount gebruikt tooconnect tooSQL Server (als de SQL Server-database zich extern wordt deze account een domeinaccount van de service moet).
     Deze opties zijn te zien op dit scherm:  
     ![Voer uw Azure AD-referenties in](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Klik op **Volgende**.
8. Op Hallo **gereed tooconfigure** pagina, laat u Hallo **Hallo synchronisatieproces gestart zodra Hallo-configuratie is voltooid** gecontroleerd. Hallo-server is nu [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode) zodat de wijzigingen zijn niet geëxporteerde tooAzure AD.
9. Klik op **Install**.
10. Nadat het Hallo-installatie is voltooid, afmelden en aanmelden opnieuw tooWindows vóór u Synchronization Service Manager of Synchronization Rule Editor gaat gebruiken of toomake andere configuratiewijzigingen gaat.

> [!NOTE]
> Synchronisatie tussen Windows Server Active Directory en Azure Active Directory, maar er zijn geen wijzigingen geëxporteerde tooAzure AD. Slechts één synchronisatieprogramma tegelijk kan actief wijzigingen exporteren. Deze status wordt de [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode) genoemd.

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Controleren of Azure AD Connect gereed toobegin synchronisatie
tooverify die Azure AD Connect gereed tootake via van DirSync, moet u tooopen **Synchronization Service Manager** in de groep Hallo **Azure AD Connect** vanuit het startmenu Hallo.

Ga in de toepassing hello, toohello **Operations** tabblad. Op dit tabblad Bevestig dat Hallo volgende bewerkingen zijn voltooid:

* Importeren op Hallo AD-Connector
* Importeren op Hallo Azure AD-Connector
* Volledige synchronisatie van Hallo AD-Connector
* Volledige synchronisatie van hello Azure AD-Connector

![Importeren en synchroniseren zijn voltooid](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Bekijk Hallo resultaat van deze bewerkingen en zorg ervoor dat er geen fouten zijn.

Als u wilt dat toosee en inspecteren Hallo-wijzigingen die over toobe geëxporteerd tooAzure AD zijn, leest u hoe tooverify configuratie onder Hallo [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode). Voer de vereiste wijzigingen door in de configuratie zodat alles klopt.

U bent klaar tooswitch van DirSync tooAzure AD wanneer u deze stappen hebt uitgevoerd en zijn tevreden Hallo resultaat.

### <a name="uninstall-dirsync-old-server"></a>DirSync verwijderen (oude server)
* Zoek in **Programma's en onderdelen**  naar **Windows Azure Active Directory-synchronisatie**
* **Windows Azure Active Directory-synchronisatie** verwijderen
* Hallo verwijdering mogelijk toocomplete van too15 minuten duren.

Als u liever later toouninstall DirSync, kunt u ook tijdelijk Hallo server afsluiten of Hallo service uitschakelen. Als er iets mis gaat deze methode kunt u toore-Schakel deze. Het wordt echter niet verwacht dat die Hallo stap mislukt zodat dit niet nodig.

Met DirSync verwijderd of uitgeschakeld, is er geen actieve server tooAzure AD exporteren. Hallo volgende stap tooenable Azure AD Connect moet worden voltooid voordat de wijzigingen in uw lokale Active Directory blijven toobe gesynchroniseerd tooAzure AD.

### <a name="enable-azure-ad-connect-new-server"></a>Azure AD Connect inschakelen (nieuwe server)
Na de installatie wordt opnieuw openen van Azure AD connect kunt u de aanvullende configuratiewijzigingen toomake. Start **Azure AD Connect** vanuit Hallo startmenu of vanuit de snelkoppeling Hallo op Hallo bureaublad. Zorg ervoor dat u niet toorun Hallo installatie MSI opnieuw proberen.

Hier ziet u de volgende Hallo:  
![Extra taken](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Selecteer **Faseringsmodus configureren**.
* Schakel fasering door unchecking hello **faseringsmodus ingeschakeld** selectievakje.

![Voer uw Azure AD-referenties in](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Klik op Hallo **volgende** knop
* Klik op de bevestigingspagina voor het Hallo Hallo **installeren** knop.

Azure AD Connect is nu uw actieve server en u moet back toousing uw bestaande DirSync-server niet wijzigen.

## <a name="next-steps"></a>Volgende stappen
Nu u Azure AD Connect geïnstalleerd hebt kunt u [Hallo installatie verifiëren en licenties toewijzen](active-directory-aadconnect-whats-next.md).

Meer informatie over deze nieuwe functies, Hallo-installatie zijn ingeschakeld: [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [onopzettelijk verwijderen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), en [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Meer informatie over deze veelvoorkomende onderwerpen: [scheduler en hoe tootrigger synchronisatie](active-directory-aadconnectsync-feature-scheduler.md).

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
