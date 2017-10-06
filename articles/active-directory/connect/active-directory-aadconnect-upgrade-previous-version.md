---
title: 'Azure AD Connect: Upgraden van een vorige versie | Microsoft Docs'
description: Hallo verschillende methoden tooupgrade toohello meest recente versie van Azure Active Directory Connect, met inbegrip van een in-place upgrade en een migratie swing uitgelegd.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect: Upgraden van een vorige versie-toohello recente
Dit onderwerp beschrijft Hallo verschillende methoden waarmee u tooupgrade uw meest recente versie van Azure Active Directory (Azure AD) verbinding maken met de installatie toohello kunt. We adviseren dat u zelf de meest recente Hallo releases van Azure AD Connect. U ook Hallo stappen gebruiken in Hallo [migratie bewegen](#swing-migration) sectie wanneer u een aanzienlijke configuratie wijzigen.

Als u tooupgrade van DirSync wilt, Zie [een upgrade uitvoert van Azure AD-synchronisatiehulpprogramma (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) in plaats daarvan.

Er zijn enkele verschillende strategieën waarmee u tooupgrade Azure AD Connect kunt.

| Methode | Beschrijving |
| --- | --- |
| [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) |Dit is de eenvoudigste methode Hallo voor klanten met een snelle installatie. |
| [In-place upgrade](#in-place-upgrade) |Als u één server hebt, kunt u Hallo installatie in-place upgraden op Hallo van dezelfde server. |
| [Migratie bewegen](#swing-migration) |U kunt met twee servers voorbereiden op een van de servers Hallo met Hallo nieuwe release of de configuratie en actieve server Hallo wijzigen wanneer u klaar bent. |

Zie voor machtigingen informatie Hallo [machtigingen die vereist zijn voor een upgrade](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Nadat u uw nieuwe Azure AD Connect-server toostart synchroniseren wijzigingen tooAzure AD hebt ingeschakeld, moet u niet terugdraaien toousing DirSync of Azure AD Sync. Downgraden van Azure AD Connect toolegacy clients, met inbegrip van DirSync en Azure AD Sync, wordt niet ondersteund en tooissues zoals gegevensverlies kan leiden in Azure AD.

## <a name="in-place-upgrade"></a>In-place upgrade
Een in-place upgrade werkt voor het verplaatsen van Azure AD Sync of Azure AD Connect. Werkt niet voor het verplaatsen van DirSync of voor een oplossing met Forefront Identity Manager (FIM) + Azure AD-Connector.

Deze methode verdient de voorkeur wanneer u één server en minder dan ongeveer 100.000 objecten. Er zijn wijzigingen in de toohello out of box sync regels, een volledige import en een volledige synchronisatie uitgevoerd als na de upgrade Hallo. Deze methode zorgt ervoor dat de nieuwe configuratie Hallo toegepaste tooall bestaande objecten in Hallo-systeem. Dit kan enkele uren, afhankelijk van het aantal objecten die in het bereik van de synchronisatie-engine Hallo Hallo duren. Hallo normale delta synchronisatie scheduler (die wordt standaard gesynchroniseerd elke 30 minuten) is onderbroken, maar Wachtwoordsynchronisatie blijft. U kunt overwegen Hallo in-place upgrade tijdens een weekend doen. Als er geen wijzigingen toohello out-of-box-configuratie met Hallo nieuwe Azure AD Connect release, vervolgens een normale delta-import/synchronisatie wordt gestart in plaats daarvan.  
![In-place upgrade](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Als u wijzigingen toohello out-of-box-synchronisatieregels hebt gemaakt, zijn wordt deze regels ingesteld terug toohello standaardconfiguratie bij een upgrade. toomake ervoor dat uw configuratie wordt gehouden tussen upgrades, zorg ervoor dat u wijzigingen aanbrengt, zoals ze zijn beschreven in [aanbevolen procedures voor het wijzigen van de standaardconfiguratie Hallo](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Tijdens een upgrade ter plekke, kunnen er wijzigingen die zijn geïntroduceerd waarvoor specifieke synchronisatie activiteiten (met inbegrip van de stap van de volledige Import en volledige synchronisatie) toobe uitgevoerd nadat de upgrade is voltooid. toodefer dergelijke activiteiten, Raadpleeg toosection [hoe toodefer volledige synchronisatie na de upgrade](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Swingmigratie
Als u de implementatie van een complexe of veel objecten hebt, kan het niet praktisch toodo een in-place upgrade op Hallo live systeem zijn. Voor sommige klanten dit proces kan meerdere dagen--duren en gedurende deze tijd geen wijzigingen zijn verwerkt. U kunt deze methode ook gebruiken wanneer u van plan toomake substantieel zijn gewijzigd tooyour configuratie bent en tootry gewenste ze uit voordat u ze toohello cloud bent gepusht.

Hallo aanbevolen methode voor deze scenario's is toouse een swing-migratie. U moet (ten minste) twee servers--één actieve server en één server met tijdelijke bestanden. Hallo actieve server (weergegeven met ononderbroken blauwe lijnen in de volgende afbeelding Hallo) is verantwoordelijk voor Hallo active productie laden. Hallo testserver (weergegeven met onderbroken paarse lijnen) is voorbereid met Hallo nieuwe release of de configuratie. Wanneer deze volledig klaar is, wordt deze server actief gemaakt. Hallo vorige active server, die nu heeft hello oude versie of de configuratie die zijn geïnstalleerd, wordt in Hallo staging-server en wordt bijgewerkt.

Hallo twee servers kunnen verschillende versies gebruiken. Bijvoorbeeld Hallo actieve server dat u van plan toodecommission bent Azure AD Sync kunt gebruiken en nieuwe testserver hello Azure AD Connect kunt gebruiken. Als u swing migratie toodevelop Hallo een nieuwe configuratie, het een goed idee toohave Hallo dezelfde versies op twee servers.  
![Tijdelijke server](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Bepaalde klanten graag toohave drie of vier servers voor dit scenario. Wanneer Hallo testserver is geüpgraded, hebt u niet een back-upserver voor [herstel na noodgevallen](active-directory-aadconnectsync-operations.md#disaster-recovery). Met drie of vier servers, kunt u één set van primaire/stand-by-servers met de nieuwe versie hello, die zorgt ervoor dat er altijd een testserver die gereed tootake via voorbereiden.

Deze stappen werken ook toomove van Azure AD Sync of een oplossing met FIM + Azure AD-Connector. Deze stappen werken niet voor DirSync, maar dezelfde migratie deze methode (ook wel parallelle implementatie) met de stappen voor DirSync Hallo is in [Upgrade Azure Active Directory-synchronisatie (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Een migratie swing tooupgrade gebruiken
1. Als u Azure AD Connect op servers en plan tooonly maken een configuratiewijziging hebt gebruikt, zorg ervoor dat uw actieve server- en staging-server zowel met behulp van dezelfde versie Hallo. Waardoor het gemakkelijker toocompare verschillen later. Als u een van Azure AD Sync upgrade uitvoert, hebben deze servers verschillende versies. Als u een van een oudere versie van Azure AD Connect upgrade uitvoert, is het een goed idee toostart met Hallo twee servers die dezelfde versie met behulp van hello, maar dit is niet vereist.
2. Als u een aangepaste configuratie hebt aangebracht en uw testserver beschikt niet over deze stappen Hallo onder [verplaatsen van een aangepaste configuratie van Hallo actieve server toohello testserver](#move-custom-configuration-from-active-to-staging-server).
3. Als u een van een oudere versie van Azure AD Connect upgrade uitvoert upgraden Hallo staging-server toohello meest recente versie. Als u, Azure AD Sync verplaatsen wilt, installeert u Azure AD Connect op uw server met tijdelijke bestanden.
4. Hallo sync engine uitvoeren volledige import en een volledige synchronisatie op de testserver kunt.
5. Controleer dat de nieuwe configuratie Hallo niet leiden tot onverwachte wijzigingen met behulp van de stappen onder 'Verifiëren' hello in [controleren Hallo configuratie van een server](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Als er iets niet als verwachte, de juiste, Hallo import en synchronisatie uitvoeren, gegevens en controleren Hallo totdat er goed uitziet, door Hallo stappen te volgen.
6. Hallo staging-server toobe Hallo actieve server overschakelen. Dit is Hallo laatste stap 'Switch active server' in [controleren Hallo configuratie van een server](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Als u een Azure AD Connect upgrade uitvoert, Hallo-server die wordt nu in staging-modus toohello meest recente versie bijwerken. Volg dezelfde stappen als voorheen tooget Hallo gegevens en configuratie bijgewerkt Hallo. Als u Azure AD Sync bijgewerkt, kunt u nu uitschakelen en de oude server buiten gebruik stellen.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Een aangepaste configuratie van Hallo actieve server toohello staging-server verplaatsen
Als u wijzigingen toohello active configuratieserver hebt gemaakt, moet u toomake zeker die dezelfde Hallo wijzigingen zijn toegepast toohello staging-server. toohelp dit verplaatsen, kunt u Hallo [documentatie voor Azure AD Connect-configuratie](https://github.com/Microsoft/AADConnectConfigDocumenter).

U kunt verplaatsen Hallo aangepaste synchronisatie regels die u hebt gemaakt met behulp van PowerShell. U moet de andere Hallo wijzigingen toepassen dezelfde manier op systemen, en u Hallo wijzigingen kan niet worden gemigreerd. Hallo [configuratie documentatie](https://github.com/Microsoft/AADConnectConfigDocumenter) kunt u vergelijken Hallo twee systemen toomake zeker van te zijn dat ze identiek zijn. Hallo hulpprogramma kan ook helpen bij de automatisering van Hallo stappen in deze sectie.

U moet tooconfigure Hallo volgende dingen Hallo dezelfde manier op beide servers:

* Verbinding toohello dezelfde forests
* Elk domein en OE filteren
* Hallo dezelfde optionele functies, zoals Wachtwoordsynchronisatie en wachtwoord terugschrijven

**Aangepaste synchronisatieregels verplaatsen**  
toomove aangepaste synchronisatieregels, Hallo te volgen:

1. Open **synchronisatie regeleditor** op uw actieve server.
2. Selecteer een aangepaste regel. Klik op **exporteren**. Hiermee wordt een Kladblok-venster. Hallo tijdelijke bestand opslaan met een PS1-uitbreiding. Hierdoor kunt u een PowerShell-script. Hallo PS1-bestand toohello staging-server kopiëren.  
   ![Exporteren van de synchronisatie-regel](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Hallo Connector GUID verschilt op Hallo staging-server en deze moeten wijzigen. tooget hello GUID, start **synchronisatie regeleditor**, selecteer een van de Hallo out-of-box-regels die verwijzen naar Hallo dezelfde verbonden systeem en klik op **exporteren**. Hallo GUID in uw PS1-bestand vervangen door Hallo GUID van Hallo staging-server.
4. Voer Hallo PS1-bestand in een PowerShell-prompt. Hiermee maakt u de aangepaste synchronisatieregel Hallo op Hallo staging-server.
5. Herhaal dit voor alle aangepaste regels.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>Hoe toodefer volledige synchronisatie na de upgrade
Tijdens een upgrade ter plekke, kunnen er wijzigingen die zijn geïntroduceerd waarvoor specifieke synchronisatie activiteiten (met inbegrip van de stap van de volledige Import en volledige synchronisatie) toobe uitgevoerd. Bijvoorbeeld connector schemawijzigingen vereisen **volledige import** stap en out-of-box synchronisatie regel wordt gewijzigd, moeten **volledige synchronisatie** stap toobe uitgevoerd op de betrokken connectors. Tijdens de upgrade, Azure AD Connect bepaalt welke synchronisatiebewerkingen zijn vereist en registreert deze als *overschrijft*. Hallo volgende synchronisatiecyclus, Hallo synchronisatie scheduler deze overschrijvingen opneemt en deze worden uitgevoerd. Zodra een onderdrukking met succes wordt uitgevoerd, wordt deze verwijderd.

Mogelijk zijn er situaties waarin u niet dat deze overschrijvingen tootake plaats onmiddellijk na de upgrade wilt. Bijvoorbeeld, u talrijke gesynchroniseerde objecten hebt en wilt u deze stappen synchronisatie toooccur na kantooruren. tooremove deze onderdrukt:

1. Tijdens de upgrade, **schakelt** Hallo optie **Hallo synchronisatieproces starten wanneer de configuratie is voltooid**. Dit wordt uitgeschakeld Hallo synchronisatie scheduler en voorkomt dat synchronisatiecyclus die hebben plaatsgevonden automatisch voordat Hallo onderdrukkingen worden verwijderd.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Nadat de upgrade is voltooid, voert u Hallo cmdlet toofind uit welke onderdrukkingen zijn toegevoegd na:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > Hallo overschrijvingen zijn specifiek voor een connector. In Hallo volgende voorbeeld, stap van de volledige Import en volledige synchronisatie zijn toegevoegd tooboth Hallo on-premises AD-Connector en Azure AD-Connector.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Noteer Hallo bestaande onderdrukkingen die zijn toegevoegd.
   
4. Hallo tooremove onderdrukt voor zowel volledige import en een volledige synchronisatie op een willekeurige connector Hallo volgende cmdlet uitvoeren:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   tooremove hello onderdrukkingen op alle connectors uitvoeren Hallo volgende PowerShell-script:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. tooresume hello scheduler, Hallo volgende cmdlet uitvoeren:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Houd er rekening mee tooexecute Hallo vereist synchronisatie stappen zo snel mogelijk. U kunt handmatig uitvoeren van deze stappen Hallo Synchronization Service Manager of Hallo onderdrukkingen terug met Hallo Set ADSyncSchedulerConnectorOverride cmdlet toevoegen.

Hallo tooadd onderdrukt voor zowel volledige import en een volledige synchronisatie op een willekeurige connector Hallo volgende cmdlet uitvoeren:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).
