---
title: een object dat niet tooAzure AD synchroniseert aaaTroubleshoot | Microsoft-Docs
description: Waarom een object niet tooAzure AD synchroniseren.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Een object dat niet tooAzure AD synchroniseert oplossen

Als een object niet als verwachte tooAzure AD synchroniseren is, kan het zijn diverse redenen. Als u een e-mailbericht fout van Azure AD hebt ontvangen of u Zie Hallo-fout in Azure AD Connect Health, Lees [exportfouten oplossen](active-directory-aadconnect-troubleshoot-sync-errors.md) in plaats daarvan. Maar als u een probleem waarbij Hallo-object niet in Azure AD is oplossen wilt, in dit onderwerp wordt voor u. Hierin wordt beschreven hoe toofind fouten in de component van de lokale hello Azure AD Connect synchroniseren.

toofind hello fouten, gaat u toolook op een aantal verschillende plaatsen in Hallo volgorde:

1. Hallo [bewerkingslogboeken](#operations) voor het zoeken naar fouten die zijn geïdentificeerd door de synchronisatie-engine Hallo tijdens het importeren en synchroniseren.
2. Hallo [connectorruimte](#connector-space-object-properties) voor het vinden van ontbrekende objecten en synchronisatiefouten.
3. Hallo [metaverse](#metaverse-object-properties) voor het vinden van problemen met gegevens.

Start [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) voordat u deze stappen begint.

## <a name="operations"></a>Bewerkingen
Hallo operations tabblad in Hallo Synchronization Service Manager is waar u de probleemoplossing moet beginnen. Hallo operations tabblad toont Hallo resultaten van de meest recente Hallo-bewerkingen.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

het bovenste gedeelte Hallo worden alle wordt uitgevoerd in chronische weergegeven. Standaard Hallo operations logboek bevat gegevens over de Hallo afgelopen zeven dagen, maar deze instelling kan worden gewijzigd met de Hallo [scheduler](active-directory-aadconnectsync-feature-scheduler.md). U wilt toolook voor alle uitvoeren die een status geslaagd niet weergegeven. U kunt Hallo sorteren door te klikken op Hallo headers wijzigen.

Hallo **Status** kolom Hallo meest belangrijke informatie en toont Hallo ernstigste probleem voor een run. Hier volgt een korte samenvatting van de meest voorkomende statussen Hallo in volgorde van prioriteit tooinvestigate (waarbij * enkele mogelijke fout tekenreeksen geven).

| Status | Opmerking |
| --- | --- |
| Stop-* |Hallo uitvoeren kan niet worden voltooid. Bijvoorbeeld, als hello extern systeem niet actief is en kan geen verbinding worden gemaakt. |
| gestopt fout limiet |Er zijn meer dan 5000 fouten. Hallo uitvoeren is automatisch gestopt vanwege het grote aantal fouten toohello. |
| voltooide -\*-fouten |Hallo voltooide uitgevoerd, maar er zijn fouten (minder dan 5000) die moeten worden onderzocht. |
| voltooide -\*-waarschuwingen |Hallo uitvoeren voltooid, maar sommige gegevens is niet in staat Hallo verwacht. Als u fouten hebt, klikt u vervolgens dit bericht is meestal slechts een symptoom zijn. Totdat u fouten hebt opgelost, moet u de waarschuwingen niet onderzoeken. |
| voltooid |Geen problemen. |

Wanneer u een rij selecteert, updates Hallo onder tooshow Hallo details van die worden uitgevoerd. Hallo onder toohello ver linksboven, hebt u mogelijk een lijst met de melding **stap #**. Deze lijst wordt alleen weergegeven als er meerdere domeinen in uw forest waar elk domein wordt vertegenwoordigd door een stap. Hallo-domeinnaam vindt u onder de kop Hallo **partitie**. Onder **Synchronisatiestatistieken**, vindt u meer informatie over Hallo aantal wijzigingen dat is verwerkt. U kunt klikken op Hallo koppelingen tooget een lijst met objecten Hallo gewijzigd. Als u objecten met fouten hebt, deze fouten worden weergegeven onder **synchronisatiefouten**.

### <a name="troubleshoot-errors-in-operations-tab"></a>Oplossen van fouten in de operations-tabblad
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
Wanneer er fouten zijn, zijn beide Hallo-object in de fout en Hallo fout zelf koppelingen met meer informatie.

Begin door te klikken op Hallo fouttekenreeks (**sync regel-fout-functie-geactiveerde** in Hallo afbeelding). Eerst krijgt u een overzicht van Hallo-object. toosee Hallo daadwerkelijke foutbericht, klikt u op Hallo **stacktracering**. Deze tracering biedt niveau foutopsporingsgegevens voor Hallo-fout.

U kunt met de rechtermuisknop in Hallo **call stack informatie** Kies **Alles selecteren**, en **kopie**. U kunt vervolgens Hallo stack kopiëren en bekijkt hello fout in uw favoriete teksteditor, zoals Kladblok.

* Als de fout Hallo afkomstig van is **SyncRulesEngine**, heeft de stack oproepgegevens Hallo eerst een lijst met alle kenmerken op Hallo-object. Schuif omlaag totdat u Hallo kop ziet **InnerException = >**.  
  ![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  Hallo regel na toont Hallo fout. In Hallo afbeelding hierboven is het Hallo-fout van een aangepaste regel-Fabrikam voor synchronisatie is gemaakt.

Als Hallo fout zelf niet voldoende informatie geven heeft, is het tijd toolook op Hallo gegevens zelf. U kunt op Hallo koppeling met de Hallo object-id en gaat u verder Hallo [connector ruimte van het geïmporteerde object](#cs-import).

## <a name="connector-space-object-properties"></a>Connector ruimte objecteigenschappen
Als er geen fouten gevonden in Hallo [operations](#operations) tabblad, dan is de volgende stap Hallo toofollow Hallo connector ruimte object op basis van Active Directory, toohello metaverse en tooAzure AD. In dit pad zult u waar Hallo probleem is.

### <a name="search-for-an-object-in-hello-cs"></a>Zoeken naar een object in Hallo CS

In **Synchronization Service Manager**, klikt u op **Connectors**, selecteer Hallo Active Directory-Connector en **Connectorgebied zoeken**.

In **bereik**, selecteer **RDN** (als u wilt dat toosearch op Hallo CN kenmerk) of **DN-naam of het anker** (als u wilt dat toosearch op Hallo distinguishedName kenmerk). Voer een waarde en klik op **Search**.  
![Connectorgebied zoeken](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Als u niet kunt Hallo-object vinden u zoekt, wordt deze mogelijk zijn gefilterd met [filteren op basis van een domein](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) of [filteren op basis van organisatie-eenheid](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Lees Hallo [configureert filtering](active-directory-aadconnectsync-configure-filtering.md) onderwerp tooverify die Hallo filteren is geconfigureerd zoals verwacht.

Een andere nuttige zoekactie is tooselect hello Azure AD-Connector in **bereik** Selecteer **in behandeling zijnde importeren**, en selecteer Hallo **toevoegen** selectievakje. Deze zoekopdracht kunt u alle gesynchroniseerde objecten in Azure AD die niet kan gekoppeld aan een lokaal object worden.  
![Connector ruimte zoeken zwevende](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Deze objecten zijn gemaakt door een andere synchronisatie-engine of een synchronisatie-engine met een andere configuratie filteren. Deze weergave is een lijst met **zwevende** objecten niet meer wordt beheerd. Controleer deze lijst en overwegen te verwijderen van deze objecten met behulp van Hallo [Azure AD PowerShell](http://aka.ms/aadposh) cmdlets.

### <a name="cs-import"></a>CS importeren
Wanneer u een object cs opent, zijn er meerdere tabbladen boven Hallo. Hallo **importeren** tabblad ziet u Hallo-gegevens die tijdelijk worden opgeslagen na importeren.  
![CS-object](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Hallo **oude waarde** ziet u wat momenteel wordt opgeslagen in het Connect en Hallo **nieuwe waarde** wat is ontvangen van het bronsysteem Hallo en is nog niet toegepast. Als er een fout op Hallo-object, worden wijzigingen niet verwerkt.

**Fout**  
![CS-object](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Hallo **synchronisatiefout** tabblad is alleen zichtbaar als er een probleem met het Hallo-object. Zie voor meer informatie [synchronisatiefouten oplossen](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>CS-afkomst
Hallo afkomst tabblad ziet u hoe Hallo ruimte connectorobject gerelateerde toohello metaverse-object is. Ziet u wanneer Hallo Connector een wijziging van de laatste geïmporteerd Hallo verbonden systeem en welke regels toegepast toopopulate gegevens op Hallo metaverse.  
![CS-afkomst](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
In Hallo **actie** kolom, kunt u zien er is een **inkomend** synchronisatieregel met Hallo actie **inrichten**. Die aangeeft, zolang deze connectorobject ruimte aanwezig is, wordt de metaverse-object Hallo blijft. Als Hallo lijst met regels voor synchronisatie in plaats daarvan ziet u een synchronisatieregel met richting **uitgaand** en **inrichten**, betekent dit dat dit object wordt verwijderd wanneer Hallo metaverse-object is verwijderd.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
U kunt ook zien in Hallo **PasswordSync** kolom die de inkomende connectorruimte Hallo wijzigingen toohello wachtwoord kan bijdragen omdat een synchronisatieregel Hallo waarde heeft **True**. Dit wachtwoord wordt tooAzure AD via de uitgaande regel Hallo verzonden.

Hallo afkomst tabblad kunt u toohello metaverse verkrijgen door te klikken op [eigenschappen Metaverse-Object](#mv-attributes).

Aan de onderkant Hallo van alle tabs zijn twee knoppen: **Preview** en **logboek**.

### <a name="preview"></a>Preview
Hallo-voorbeeldpagina is gebruikte toosynchronize een enkel object. Dit is handig als u bepaalde regels aangepaste synchronisatie oplossen wilt en toosee Hallo effect van een op een enkel object wilt. U kunt kiezen tussen **volledige synchronisatie** en **Deltasynchronisatie**. U kunt ook selecteren tussen **Preview genereren**, die alleen Hallo wijziging blijft in het geheugen en **Preview doorvoeren**, welke Hallo metaverse bijgewerkt en alle fasen tootarget connectorspaces wijzigingen.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
U kunt inspecteren Hallo object en welke regel wordt toegepast voor een bepaald kenmerk-stroom.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Logboek
Hallo logboek pagina is gebruikte toosee Hallo wachtwoord sync-status en geschiedenis. Zie voor meer informatie [Wachtwoordsynchronisatie oplossen](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Eigenschappen van Metaverse-object
Het is doorgaans beter toostart zoeken vanaf Hallo bron Active Directory [connectorruimte](#connector-space). Maar u kunt ook starten vanuit Hallo metaverse zoeken.

### <a name="search-for-an-object-in-hello-mv"></a>Zoeken naar een object in Hallo MV
In **Synchronization Service Manager**, klikt u op **Metaverse zoeken**. Maak een query die u vindt Hallo gebruiker weet. U kunt zoeken naar gangbare kenmerken, zoals accountName (sAMAccountName) en userPrincipalName. Zie voor meer informatie [Metaverse zoeken](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

In Hallo **zoekresultaten** venster, klikt u op Hallo-object.

Als u Hallo-object niet gevonden, is klikt u vervolgens het niet nog bereikt Hallo metaverse. Hallo Active Directory blijven toosearch voor Hallo object [connectorruimte](#connector-space-object-properties). Kan er een fout opgetreden in de synchronisatie is Hallo object uit de komende toohello metaverse blokkeert of er mogelijk een filter toegepast.

### <a name="mv-attributes"></a>MV-kenmerken
Op tabblad kenmerken hello, ziet u Hallo waarden en welke Connector het bijgedragen.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Als een object niet wordt gesynchroniseerd, klikt u vervolgens bekijken Hallo kenmerken in Hallo metaverse te volgen:
- Hallo-kenmerk **cloudFiltered** aanwezig is en stel te**true**? Als deze, wordt het filter is toegepast volgens de stappen in toohello [kenmerk gebaseerd filteren](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Hallo-kenmerk **sourceAnchor** aanwezig? Als dat niet het geval is, hebt u een topologie met account-resource forest? Als een object wordt geïdentificeerd als een gekoppeld postvak (Hallo kenmerk **msExchRecipientTypeDetails** heeft Hallo waarde 2), en vervolgens Hallo sourceAnchor is die is bijgedragen door Hallo-forest met een ingeschakelde Active Directory-account. Zorg ervoor dat de hoofdaccount Hallo is geïmporteerd en juist is gesynchroniseerd. Hallo hoofdaccount moet worden vermeld in Hallo [connectors](#mv-connectors) voor Hallo-object.

### <a name="mv-connectors"></a>MV-Connectors
Hallo Connectors tabblad ziet u alle connectorspaces waarvoor een representatie van Hallo-object.  
![Sync-Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
U hebt een connector voor:

- Elke gebruiker Hallo van Active Directory-forest wordt weergegeven. Deze weergave kan bestaan foreignSecurityPrincipals en neem contact op met objecten.
- Een connector in Azure AD.

Als u Hallo connector tooAzure AD ontbreekt, Lees [MV-kenmerken](#MV-attributes) tooverify Hallo criteria voor wordt ingericht tooAzure AD.

Op dit tabblad kunt u ook toonavigate toohello [ruimte connectorobject](#connector-space-object-properties). Selecteer een rij en klikt u op **eigenschappen**.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).
