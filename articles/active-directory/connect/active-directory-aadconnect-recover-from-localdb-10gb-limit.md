---
title: 'Azure AD Connect: Hoe toorecover van 10GB LocalDB beperken probleem | Microsoft Docs'
description: Dit onderwerp wordt beschreven hoe toorecover Azure AD Connect-synchronisatie Service zodra het LocalDB 10GB probleem beperken.
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect: Hoe toorecover van 10 GB-limiet LocalDB
Azure AD Connect vereist een SQL Server-database toostore identity-gegevens. Hallo-standaard die SQL Server 2012 Express LocalDB met Azure AD Connect geïnstalleerd of uw eigen volledig SQL gebruiken. Voor SQL Server Express geldt een limiet van 10 GB. Wanneer u LocalDB gebruikt en deze limiet is bereikt, kan de Azure AD Connect-synchronisatieservice niet langer starten of goed synchroniseren. In dit artikel biedt herstelstappen Hallo.

## <a name="symptoms"></a>Symptomen
Er zijn twee algemene symptomen:

* Azure AD Connect-synchronisatieservice **wordt uitgevoerd** maar mislukt toosynchronize met *'gestopt-database-schijf-volledig'* fout.

* Azure AD Connect-synchronisatieservice **niet kan toostart is**. Wanneer u toostart Hallo service probeert, mislukt met de gebeurtenis 6323 en foutbericht *"Hallo-server een fout opgetreden omdat SQL Server geen schijfruimte meer heeft."*

## <a name="short-term-recovery-steps"></a>Korte termijn herstelstappen
Deze sectie bevat Hallo stappen tooreclaim DB ruimte nodig voor Azure AD Connect-synchronisatieservice tooresume bewerking. Hallo stappen omvatten:
1. [Hallo-synchronisatieservice status bepalen](#determine-the-synchronization-service-status)
2. [Hallo database verkleinen](#shrink-the-database)
3. [Uitvoeren van de gegevens van geschiedenis verwijderen](#delete-run-history-data)
4. [Geef een kortere bewaarperiode voor gegevens van de geschiedenis uitvoeren](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Hallo-synchronisatieservice status bepalen
Bepaal eerst of er nog steeds Hallo Synchronization Service wordt uitgevoerd of niet:

1. Aanmelden tooyour Azure AD Connect-server als beheerder.

2. Ga te**Service Control Manager**.

3. Controleer de status van Hallo **Microsoft Azure AD Sync**.


4. Als deze wordt uitgevoerd, geen stoppen of Hallo-service opnieuw starten. Overslaan [verkleinen Hallo database](#shrink-the-database) stap en ga te[verwijderen uitvoeren geschiedenisgegevens](#delete-run-history-data) stap.

5. Als deze niet wordt uitgevoerd, probeert u toostart Hallo-service. Als het Hallo-service is gestart, gaat u verder [verkleinen Hallo database](#shrink-the-database) stap en ga te[verwijderen uitvoeren geschiedenisgegevens](#delete-run-history-data) stap. Ga anders verder met [verkleinen Hallo database](#shrink-the-database) stap.

### <a name="shrink-hello-database"></a>Hallo database verkleinen
Hallo verkleinen bewerking toofree up voldoende DB ruimte toostart Hallo Synchronization Service gebruiken. Het vrijgemaakt DB-ruimte door het verwijderen van spaties in Hallo-database. Deze stap is best-effort als is er geen garantie dat u altijd ruimte kunt herstellen. toolearn meer informatie over de verkleiningsbewerking, Lees dit artikel [verkleinen van een database](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Deze stap overslaan als u Hallo synchronisatieservice toorun krijgt. Het is tooshrink Hallo SQL-database niet aanbevolen omdat dit ertoe toopoor upprestaties vanwege tooincreased fragmentatie leiden kan.

Hallo-naam van het Hallo-database gemaakt voor Azure AD Connect is **ADSync**. een verkleiningsbewerking tooperform, u moet zich aanmelden als Hallo sysadmin of de DBO van Hallo-database. Tijdens de installatie van Azure AD Connect Hallo na accounts sysadmin-rechten krijgen:
* Lokale beheerders
* Hallo-gebruikersaccount dat gebruikt toorun Azure AD Connect-installatie is.
* Hallo Sync-serviceaccount die wordt gebruikt als Hallo context van Azure AD Connect-synchronisatieservice besturingssysteem.
* Hallo lokale groep ADSyncAdmins die is gemaakt tijdens de installatie.

1. Maak een back-up van database door te kopiëren Hallo **ADSync.mdf** en **ADSync_log.ldf** bestanden onder `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa veilige locatie.

2. Start een nieuwe PowerShell-sessie.

3. Navigeer toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Start **sqlcmd** hulpprogramma met Hallo opdracht `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, met behulp van Hallo referentie van een sysadmin of Hallo database DBO.

5. tooshrink Hallo-database, op Hallo sqlcmd-opdrachtprompt (1 >), voer `DBCC Shrinkdatabase(ADSync,1);`, gevolgd door `GO` in de volgende regel Hallo.

6. Als het Hallo-bewerking is voltooid, probeer het opnieuw toostart Hallo-synchronisatieservice. Als u Hallo-synchronisatieservice starten kunt, gaat u verder te[verwijderen uitvoeren geschiedenisgegevens](#delete-run-history-data) stap. Als dat niet het geval is, moet u contact op met ondersteuning.

### <a name="delete-run-history-data"></a>Uitvoeren van de gegevens van geschiedenis verwijderen
Standaard behoudt Azure AD Connect up tooseven dagen van de uitvoeringsgeschiedenis gegevens. In deze stap verwijderen we Hallo geschiedenis tooreclaim DB gegevensruimte uitvoeren zodat Azure AD Connect-synchronisatieservice synchroniseren opnieuw kunt starten.

1.  Start **Synchronization Service Manager** door te gaan tooSTART → Synchronization-Service.

2.  Ga toohello **Operations** tabblad.

3.  Onder **acties**, selecteer **wissen wordt uitgevoerd**...

4.  U kunt kiezen **wissen van alle sessies** of **wissen wordt uitgevoerd voordat er... <date>**  optie. Het wordt aanbevolen dat u start door het wissen van gegevens van geschiedenis die ouder dan twee dagen zijn worden uitgevoerd. Als u toorun in DB grootte probleem doorgaat, en kies vervolgens Hallo **wissen van alle sessies** optie.

### <a name="shorten-retention-period-for-run-history-data"></a>Geef een kortere bewaarperiode voor gegevens van de geschiedenis uitvoeren
Deze stap is de kans op tooreduce Hallo na meerdere synchronisatiecycli die worden uitgevoerd in Hallo limiet van 10 GB probleem.

1. Open een nieuw PowerShell-sessie.

2. Voer `Get-ADSyncScheduler` en noteer Hallo PurgeRunHistoryInterval eigenschap, waarmee de huidige bewaarperiode Hallo.

3. Voer `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` tooset Hallo bewaren periode tootwo dagen. Pas de bewaarperiode Hallo naar gelang van toepassing.

## <a name="long-term-solution--migrate-toofull-sql"></a>Op lange termijn oplossing: migreren toofull SQL
In het algemeen Hallo probleem indicatief 10 GB-databasegrootte is niet meer voldoende voor Azure AD Connect toosynchronize is uw lokale Active Directory tooAzure AD. Het is raadzaam dat u overschakelt naar toousing Hallo volledige versie van SQL server. U vervangen niet rechtstreeks Hallo LocalDB van een bestaande implementatie van Azure AD Connect door Hallo Hallo volledige versie van SQL database. In plaats daarvan moet u een nieuwe Azure AD Connect-server met volledige versie van SQL Hallo implementeren. Het is raadzaam dat u een swing migratie uitvoeren waarbij Hallo nieuwe Azure AD Connect-server (met SQL database) wordt geïmplementeerd als een testserver, volgende toohello bestaande Azure AD Connect-server (met LocalDB). 
* Voor instructies over hoe tooconfigure externe SQL met Azure AD Connect verwijzen tooarticle [aangepaste installatie van Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Raadpleeg voor instructies voor migratie voor een upgrade voor Azure AD Connect swing tooarticle [Azure AD Connect: upgraden van een vorige versie-toohello recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
