---
title: 'Azure AD Connect-synchronisatie: een configuratiewijziging in Azure AD Connect-synchronisatie wijzigen | Microsoft Docs'
description: Begeleidt u bij hoe toomake een toohello-configuratie wijzigen in Azure AD Connect synchroniseren.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Azure AD Connect-synchronisatie: hoe een wijziging toohello toomake standaard configuratie
Hallo-doel van dit onderwerp is toowalk u stapsgewijs hoe toomake toohello standaardconfiguratie in Azure AD Connect-synchronisatie wordt gewijzigd. Het bevat stappen voor enkele algemene scenario's. U moet met deze kennis kunnen toomake enkele eenvoudige wijzigingen tooyour configuratie op basis van uw eigen bedrijfsregels eigenaar.

## <a name="synchronization-rules-editor"></a>Synchronisatie regeleditor
Hallo regeleditor synchronisatie is gebruikte toosee en wijzig Hallo standaardconfiguratie. U vindt deze in het Menu Start Hallo onder Hallo **Azure AD Connect** groep.  
![Met de regeleditor voor synchronisatie van het Menu Start](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Wanneer u het opent, ziet u de standaardregels out of box Hallo.

![Synchronisatie regeleditor](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Navigeren in Hallo-editor
Hallo-keuzelijsten Hallo boven aan het Hallo-editor kunnen u tooquickly zoeken naar een bepaalde regel. Als u toosee Hallo regels waarin Hallo kenmerk proxyAddresses opgenomen wilt is, zou u bijvoorbeeld Hallo-keuzelijsten toohello volgende wijzigen:  
![SRE filteren](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
tooreset filteren en laden van een nieuwe configuratie, drukt u op **F5** op Hallo toetsenbord.

rechtsboven op toohello, hebt u een knop **nieuwe regel toevoegen**. Deze knop is gebruikte toocreate uw eigen aangepaste regel.

Hallo onder hebt u knoppen voor fungeert voor een geselecteerde synchronisatieregel. **Bewerken** en **verwijderen** doen wat u verwacht. **Exporteren** produceert een PowerShell-script voor de synchronisatieregel Hallo opnieuw te maken. Deze procedure kunt u een synchronisatieregel van één server tooanother toomove.

## <a name="create-your-first-custom-rule"></a>Uw eerste aangepaste regel maken
de meest voorkomende wijziging Hallo is wijzigingen toohello kenmerkstromen. Hallo-gegevens in de bronmap mogelijk niet zoals in Azure AD. In Hallo voorbeeld in deze sectie die u wilt ervoor dat de voornaam Hallo van een gebruiker zich altijd in toomake **juiste geval**.

### <a name="disable-hello-scheduler"></a>Hallo scheduler uitschakelen
Hallo [scheduler](active-directory-aadconnectsync-feature-scheduler.md) wordt standaard elke 30 minuten uitgevoerd. Wilt u toomake of dat het is niet gestart terwijl u wijzigingen aanbrengen wilt en oplossen van uw nieuwe regels. tootemporarily hello scheduler uitschakelen, start PowerShell en voer`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Hallo scheduler uitschakelen](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Hallo-regel maken
1. Klik op **nieuwe regel toevoegen**.
2. Op Hallo **beschrijving** pagina Voer Hallo volgende:  
   ![Binnenkomende regel filteren](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Naam: Geven Hallo regel een beschrijvende naam.
   * Beschrijving: Sommige informatie zodat iemand anders welke Hallo-regel begrijpen te is voor.
   * Verbonden systeem: Hallo Hallo systeemobject vindt u in. Selecteer in dit geval Hallo Active Directory-Connector.
   * Verbonden systeem/Metaverseobjecttype: Selecteer **gebruiker** en **persoon** respectievelijk.
   * Koppelingstype: Deze waarde te wijzigen**Join**.
   * Prioriteit: Geef een waarde die uniek is in Hallo-systeem. Een lagere numerieke waarde geeft aan dat hogere prioriteit.
   * -Tag: Leeg laten. Alleen out-of-box regels van Microsoft, moeten dit vak gevuld met een waarde hebben.
3. Op Hallo **Scoping filter** pagina **givenName ISNOTNULL**.  
   ![De binnenkomende regel bereikfilter](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   Deze sectie is gebruikte toodefine welke objecten Hallo-regel moet worden toegepast op. Als leeg wordt gelaten, zou gebruikersobjecten tooall Hallo-regel van toepassing. Maar dat zou vergaderruimten, service-accounts en andere niet-mensen gebruikersobjecten bevatten.
4. Op Hallo **Join regels**, laat het veld leeg.
5. Op Hallo **transformaties** pagina, Hallo FlowType ook wijzigen**expressie**. Selecteer Hallo doelkenmerk **givenName**, en voer in de bron `PCase([givenName])`.
   ![Regel voor binnenkomende verbindingen transformaties](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   Hallo synchronisatie-engine is hoofdlettergevoelig op Hallo functienaam en Hallo-naam van Hallo-kenmerk. Als u iets mis typt, ziet u een waarschuwing wanneer u Hallo regel toevoegen. Hallo-editor kunt u toosave en doorgaan, zodat tooreopen Hallo regel en de juiste Hallo regel.
6. Klik op **toevoegen** toosave Hallo regel.

Uw nieuwe aangepaste regel moet zichtbaar Hello andere regels in Hallo-systeem gesynchroniseerd.

### <a name="verify-hello-change"></a>Controleer of Hallo wijzigen
Met deze nieuwe wijziging wilt u toomake controleren of het werkt zoals verwacht en is fouten niet genereren. Afhankelijk van Hallo aantal objecten dat u hebt, zijn er twee verschillende manieren toodo deze stap.

1. Een volledige synchronisatie worden uitgevoerd op alle objecten
2. Een voorbeeld en een volledige synchronisatie uitvoeren op een enkel object

Start **synchronisatieservice** vanuit het startmenu Hallo. Hallo stappen in deze sectie zijn alle in dit hulpprogramma.

1. **Volledige synchronisatie van alle objecten**  
   Selecteer **Connectors** Hallo bovenaan. Identificeren van Hallo Connector die u hebt een wijziging tooin Hallo voorgaande sectie hebt aangebracht, in dit geval Hallo Active Directory Domain Services en selecteert u deze. Selecteer **uitvoeren** van acties en selecteer **volledige synchronisatie** en **OK**.
   ![Volledige synchronisatie](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   Hallo-objecten worden nu in Hallo metaverse bijgewerkt. U wordt nu toolook op Hallo-object in Hallo metaverse.
2. **Preview en een volledige synchronisatie van een enkel object**  
   Selecteer **Connectors** Hallo bovenaan. Identificeren van Hallo Connector die u hebt een wijziging tooin Hallo voorgaande sectie hebt aangebracht, in dit geval Hallo Active Directory Domain Services en selecteert u deze. Selecteer **Connectorgebied zoeken**. Gebruik bereik toofind een object dat u wilt dat toouse tootest Hallo wijziging. Hallo-object selecteert en op **Preview**. Selecteer in het welkomstscherm voor nieuwe **doorvoeren Preview**.  
   ![Voorbeeld van doorvoeren](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   Hallo wijziging is doorgevoerd toohello metaverse.

**Bekijkt hello-object in Hallo metaverse**  
Nu u toopick die enkele objecten toomake ervoor Hallo Voorbeeldwaarde wordt verwacht en die Hallo regel toegepast. Selecteer **Metaverse zoeken** van Hallo boven. Een filter dat u moet toofind Hallo relevante objecten toevoegen. Open in het zoekresultaat hello, een object. Bekijkt hello kenmerkwaarden en ook controleren in Hallo **Sync regels** kolom Hallo regel toegepast zoals verwacht.  
![Metaverse zoeken](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Hallo scheduler inschakelen
Als alles zoals verwacht, kunt u Hallo scheduler opnieuw inschakelen. Voer vanuit PowerShell `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Andere algemene wijzigingen van de kenmerk-stroom
Hallo vorige sectie wordt beschreven hoe toomake tooan kenmerkstroom verandert. In deze sectie vindt u enkele aanvullende voorbeelden. Hallo-stappen voor hoe toocreate hello synchronisatieregel is afgekort, maar u kunt Hallo volledige stappen in de vorige sectie Hallo vinden.

### <a name="use-another-attribute-than-hello-default"></a>Een ander kenmerk dan Hallo standaardwaarde gebruiken
Bij Fabrikam is er een forest waarbij Hallo lokale alfabet wordt gebruikt voor de voornaam en achternaam weergavenaam. Hallo Latijnse representatie van deze kenmerken kan worden gevonden in Hallo uitbreidingskenmerken. Tijdens het bouwen van de globale adreslijst Hallo in Azure AD en Office 365, Hallo organisatie wil deze kenmerken toobe in plaats daarvan gebruikt.

Met een standaardconfiguratie is een object van het lokale forest Hallo ziet er als volgt:  
![Kenmerkstroom 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

een regel met andere kenmerkstromen toocreate Hallo te volgen:

* Start **Synchronization Rule Editor** vanuit het startmenu Hallo.
* Met **inkomend** nog steeds geselecteerde toohello links, klikt u Hallo **nieuwe regel toevoegen**.
* Hallo regel geeft een naam en beschrijving. Selecteer Hallo lokale Active Directory en Hallo relevante objecttypen. In **koppelingstype**, selecteer **Join**. Kies voor hogere prioriteit, een getal dat niet wordt gebruikt door een andere regel. Hallo out of box regels beginnen met 100, Hallo waarde 50 kan worden gebruikt in dit voorbeeld.
  ![Kenmerkstroom 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Bereik leeg laten (dat wil zeggen, wordt aangeraden tooall gebruikersobjecten in Hallo forest).
* Laat de eigenschap join regels leeg (waarmee wordt, out of box regel ingang Hallo joins).
* Maak in transformaties Hallo stromen te volgen:  
  ![Kenmerkstroom 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Klik op **toevoegen** toosave Hallo regel.
* Ga te**Synchronization Service Manager**. Op **Connectors**, selecteer Hallo Connector waar we Hallo regel toegevoegd. Selecteer **uitvoeren**, en **volledige synchronisatie**. Een volledige synchronisatie wordt opnieuw berekend alle objecten met behulp van de huidige Hallo-regels.

Dit is resultaat voor hetzelfde met deze aangepaste regel object Hallo Hallo:  
![Kenmerkstroom 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Lengte van kenmerken
Tekenreekskenmerken zijn als standaard instellen toobe worden geïndexeerd en Hallo maximumlengte is 448 tekens. Als u met tekenreekskenmerken die meer bevatten werkt mogelijk, brengt u ervoor dat tooinclude Hallo volgende in Hallo kenmerkstroom:  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>Hallo userPrincipalSuffix wijzigen
Hallo userPrincipalName kenmerk in Active Directory is niet altijd bekend door Hallo-gebruikers en mogelijk geen geschikte zoals Hallo aanmeldings-ID. Hello Azure AD Connect sync-installatiewizard kunt verzamelen van een ander kenmerk, bijvoorbeeld een e-mail sturen. Maar in sommige gevallen Hallo kenmerk moet worden berekend. Hallo bedrijf Contoso heeft bijvoorbeeld twee Azure AD-mappen, één voor productie en één voor het testen. Ze willen Hallo gebruikers in hun test tenant toouse een ander achtervoegsel in Hallo aanmeldings-ID.  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

In deze expressie, nemen alles links van de Hallo eerst @-sign (Word) en samenvoegen met een vaste tekenreeks.

### <a name="convert-a-multi-value-tooa-single-value"></a>Een met meerdere waarden tooa single-waarde niet converteren
Bepaalde kenmerken in Active Directory zijn met meerdere waarden in het Hallo-schema, zelfs als ze op zoek één waarde in Active Directory: gebruikers en Computers. Een voorbeeld is Hallo beschrijvingskenmerk.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

In deze expressie geval Hallo-kenmerk heeft een waarde, Hallo eerste item (opdracht) duren in Hallo-kenmerk, Verwijder voorloopspaties en afsluitende spaties (Trim) en vervolgens behouden eerst 448 tekens (links) in de tekenreeks Hallo Hallo.

### <a name="do-not-flow-an-attribute"></a>Niet laten doorlopen voor een kenmerk
Zie voor achtergrondinformatie over Hallo scenario voor deze sectie, [Hallo kenmerk stroom proces regelen](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Er zijn twee manieren toonot stromen een kenmerk. Hallo eerst is beschikbaar in de installatiewizard Hallo en kunt u te[geselecteerde kenmerken verwijderen](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Deze optie werkt als u nooit Hallo kenmerk voordat hebt gesynchroniseerd. Echter als u toosynchronize dit kenmerk hebt gestart en later met deze functie te verwijderen, klikt u vervolgens Hallo synchronisatie-engine stopt met het kenmerk Hallo beheer en Hallo bestaande standaardwaarden worden gehandhaafd in Azure AD.

Als u tooremove Hallo-waarde van een kenmerk wilt en zorg ervoor dat deze wordt niet uitgebreid in toekomstige hello, moet u een aangepaste regel maken.

Bij Fabrikam, hebben we gerealiseerde dat sommige Hallo kenmerken we toohello synchroniseren cloud niet er worden moeten. We willen zeker van te zijn dat deze kenmerken worden verwijderd uit Azure AD toomake.  
![Ongeldige Uitbreidingskenmerken](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Een nieuwe regel voor binnenkomende synchronisatie maken en vullen Hallo beschrijving ![beschrijvingen](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Maken van kenmerkstromen van het type **expressie** en met Hallo bron **AuthoritativeNull**. Hallo letterlijke **AuthoritativeNull** geeft aan dat Hallo-waarde mag niet leeg zijn in Hallo MV zelfs als een regel voor synchronisatie van lagere prioriteit toopopulate Hallo waarde probeert.
  ![Transformatie voor Uitbreidingskenmerken](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Hallo Synchronisatieregel opslaan. Start **synchronisatieservice**, Hallo Connector zoeken, selecteert u **uitvoeren**, en **volledige synchronisatie**. Deze stap opnieuw alle kenmerkstromen berekend.
* Controleer of dat Hallo bedoeld wijzigingen zijn over toobe geëxporteerd door te zoeken naar Hallo connectorgebied overgebracht.
  ![Gefaseerde verwijderen](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>Regels maken met PowerShell
Wanneer u slechts enkele wijzigingen toomake, werkt goed samen met het Hallo sync regeleditor gebruiken. Als u toomake veel wijzigingen moet, kan een betere optie zijn door PowerShell. Sommige geavanceerde functies zijn alleen beschikbaar met PowerShell.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Hallo PowerShell-script ophalen voor een out-of-box-regel
toosee Hallo PowerShell-script dat een out-of-box-regel, selecteer Hallo regel in Hallo-sync gemaakt-editor en klikt u op regels **exporteren**. Deze actie geeft Hallo van PowerShell script die gemaakte Hallo-regel.

### <a name="advanced-precedence"></a>Geavanceerde prioriteit
Hallo out of box sync regels beginnen met een prioriteitswaarde 100. Als u veel forests hebt en u toomake moet veel aangepaste wijzigingen en vervolgens regels 99 synchronisatie mogelijk niet voldoende.

U kunt de opdracht geven Hallo synchronisatie-Engine die u wilt dat extra regels ingevoegd vóór Hallo out-of-box-regels. tooget dit probleem als volgt te werk:

1. Markeren Hallo eerste out-of-box-sync-regel (met deze regel is Hallo **In van het AD-gebruiker toevoegen**) in Hallo sync regeleditor en selecteer **exporteren**. Kopieer Hallo SR-id-waarde.  
![PowerShell voor wijziging](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Nieuwe regel voor synchronisatie Hallo maken. Hallo sync regel editor toocreate kunt u deze. Hallo regel tooa PowerShell-script exporteren.
3. In de eigenschap Hallo **PrecedenceBefore**, Hallo id-waarde uit het Hallo out of box regel invoegen. Set Hallo **voorrang** te**0**. Zorg ervoor dat het kenmerk Hallo-id is uniek en u niet opnieuw gebruiken van een GUID van een andere regel. Ook voor zorgen dat Hallo **ImmutableTag** eigenschap is niet ingesteld; deze eigenschap mag alleen worden ingesteld voor een out-of-box-regel. Sla Hallo PowerShell-script en voer dit. Hallo-resultaat is dat uw aangepaste regel Hallo prioriteitswaarde 100 is toegewezen en alle andere out-of-box-regels worden verhoogd.  
![PowerShell na wijziging](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

U kunt hebben veel aangepaste synchronisatie regels die gebruikmaken van dezelfde Hallo **PrecedenceBefore** waarde indien nodig.


## <a name="enable-synchronization-of-preferreddatalocation"></a>Synchronisatie van PreferredDataLocation inschakelen
Azure AD Connect ondersteunt synchronisatie van Hallo **PreferredDataLocation** kenmerk voor **gebruiker** objecten in versie 1.1.524.0 en na. Meer specifiek, zijn de volgende wijzigingen geïntroduceerd:

* Hallo-schema van het objecttype Hallo **gebruiker** in hello Azure AD-Connector tooinclude PreferredDataLocation kenmerk is van het type tekenreeks en één waarde wordt uitgebreid.

* Hallo-schema van het objecttype Hallo **persoon** in Hallo Metaverse tooinclude PreferredDataLocation kenmerk is van het type tekenreeks en één waarde wordt uitgebreid.

Standaard is Hallo PreferredDataLocation kenmerk niet ingeschakeld voor synchronisatie omdat er geen overeenkomend PreferredDataLocation-kenmerk in de lokale Active Directory. U moet handmatig synchronisatie inschakelen.

> [!IMPORTANT]
> Azure AD kan op dit moment Hallo PreferredDataLocation kenmerk op gesynchroniseerde gebruikersobjecten en cloud gebruiker objecten toobe rechtstreeks geconfigureerd met behulp van Azure AD PowerShell. Wanneer u de synchronisatie van Hallo PreferredDataLocation kenmerk hebt ingeschakeld, moet u stoppen met behulp van Azure AD PowerShell tooconfigure Hallo-kenmerk op **gesynchroniseerd gebruikersobjecten** als Azure AD Connect overschrijft toe op basis van kenmerkwaarden van Hallo-bron in de lokale Active Directory.

> [!IMPORTANT]
> Op 1 September 2017 Azure AD wordt niet langer Hallo PreferredDataLocation kenmerk op toestaan **gesynchroniseerd gebruikersobjecten** toobe rechtstreeks geconfigureerd met behulp van Azure AD PowerShell. tooconfigure PreferredLocation-kenmerk op gebruikersobjecten gesynchroniseerd, moet u Azure AD Connect.

Voordat u de synchronisatie van Hallo PreferredDataLocation kenmerk inschakelt, moet u het volgende doen:

 * Bepaal eerst welke lokale Active Directory-kenmerk toobe als Hallo bronkenmerk gebruikt. Deze moet van het type **tekenreeks** en **één waarde**.

 * Als u Hallo PreferredDataLocation kenmerk eerder hebt geconfigureerd op bestaande gebruikersobjecten gesynchroniseerd in Azure AD dat gebruikmaakt van Azure AD PowerShell, moet u **backport** Hallo kenmerk waarden bijbehorende gebruikersobjecten toohello in on-premises Active Directory.
 
    > [!IMPORTANT]
    > Als u niet backport Hallo kenmerk waarden toohello bijbehorende gebruikersobjecten in lokale Active Directory dit, wordt Azure AD Connect Hallo bestaande kenmerkwaarden in Azure AD wanneer synchronisatie voor Hallo PreferredDataLocation kenmerk is verwijderd ingeschakeld.

 * Configuratie van het bronkenmerk Hallo het beste op ten minste twee lokale AD-gebruiker objecten nu, die kan worden gebruikt voor verificatie later.
 
Hallo stappen tooenable synchronisatie van Hallo PreferredDataLocation kenmerk kan worden samengevat als:

1. Schakel de sync scheduler uit en controleer of dat er vindt geen synchronisatie uitgevoerd

2. Hallo bron kenmerk toohello lokale AD-Connector toevoegen schema

3. PreferredDataLocation toohello Azure AD-Connector schema toevoegen

4. Maken van een binnenkomende synchronisatie regel tooflow Hallo-kenmerkwaarde van lokale Active Directory

5. Een uitgaande synchronisatie regel tooflow Hallo kenmerk waarde tooAzure AD maken

6. Volledige synchronisatiecyclus uitvoeren

7. Sync scheduler inschakelen

> [!NOTE]
> Hallo rest van deze sectie bevat informatie over deze stappen in de details. Ze worden beschreven in de context van een Azure AD-implementatie met één forest topologie en zonder aangepaste synchronisatieregels Hallo. Als u een topologie met meerdere forests hebt, aangepaste synchronisatieregels geconfigureerd of een tijdelijke server hebt, moet u tooadjust Hallo stappen dienovereenkomstig.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Stap 1: Schakel de sync scheduler uit en controleer of dat er vindt geen synchronisatie uitgevoerd
Zorg ervoor dat er geen synchronisatie plaats terwijl u in het midden bent van het bijwerken van synchronisatie Hallo regels tooavoid onbedoelde wijzigingen worden tooAzure AD geëxporteerd. toodisable hello ingebouwde sync scheduler:

 1. Start PowerShell-sessie op Hallo Azure AD Connect-server.

 2. Geplande synchronisatie uitschakelen door de cmdlet uit te voeren:`Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Hallo Start **Synchronization Service Manager** door te gaan tooSTART → Synchronization-Service.
 
 4. Ga toohello **Operations** tabblad en er is geen bewerking met de status bevestigen *'wordt uitgevoerd.'*

![Controleer de Synchronization Service Manager - er zijn geen bewerkingen uitgevoerd](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>Stap 2: Hallo bron kenmerk toohello lokale AD-Connector toevoegen schema
Niet alle AD-kenmerken worden geïmporteerd in Hallo lokale AD Connectorgebied overgebracht. tooadd hello kenmerk toohello bronlijst Hallo geïmporteerd kenmerken:

 1. Ga toohello **Connectors** tabblad in Hallo Synchronization Service Manager.
 
 2. Met de rechtermuisknop op Hallo **on-premises AD-Connector** en selecteer **eigenschappen**.
 
 3. Ga in het pop-upvenster hello, toohello **kenmerken selecteren** tabblad.
 
 4. Zorg ervoor dat bronkenmerk Hallo Hallo kenmerkenlijst is ingecheckt.
 
 5. Klik op **OK** toosave.

![Toevoegen van bron kenmerk tooon-premises AD-Connector schema](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>Stap 3: PreferredDataLocation toohello Azure AD-Connector schema toevoegen
Hallo PreferredDataLocation kenmerk is standaard niet worden geïmporteerd in hello Azure AD Connect-ruimte. tooadd hello PreferredDataLocation kenmerk toohello lijst met geïmporteerde kenmerken:

 1. Ga toohello **Connectors** tabblad in Hallo Synchronization Service Manager.

 2. Met de rechtermuisknop op Hallo **Azure AD-Connector** en selecteer **eigenschappen**.

 3. Ga in het pop-upvenster hello, toohello **kenmerken selecteren** tabblad.

 4. Zorg ervoor dat Hallo PreferredDataLocation kenmerk in de kenmerkenlijst Hallo is ingeschakeld.

 5. Klik op **OK** toosave.

![Bron kenmerk tooAzure AD-Connector schema toevoegen](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>Stap 4: Een kenmerkwaarde voor binnenkomende synchronisatie regel tooflow Hallo van lokale Active Directory maken
synchronisatieregel voor binnenkomende Hallo toestaat Hallo kenmerk waarde tooflow van het bronkenmerk Hallo van lokale Active Directory toohello Metaverse:

1. Hallo Start **synchronisatie regeleditor** door te gaan tooSTART → synchronisatie Editor regels.

2. Set Hallo zoekfilter **richting** toobe **inkomend**.

3. Klik op **nieuwe regel toevoegen** toocreate knop een nieuwe regel voor binnenkomende verbindingen.

4. Onder Hallo **beschrijving** tabblad, bieden Hallo volgende configuratie:
 
    | Kenmerk | Waarde | Details |
    | --- | --- | --- |
    | Naam | *Geef een naam* | Bijvoorbeeld: *' In uit Active Directory-gebruiker PreferredDataLocation '* |
    | Beschrijving | *Geef een beschrijving* |  |
    | Verbonden systeem | *Kies Hallo lokale AD-connector* |  |
    | Verbonden systeem objecttype | **Gebruiker** |  |
    | Metaverse-objecttype | **Persoon** |  |
    | Koppelingstype | **Koppelen** |  |
    | Prioriteit | *Kies een getal tussen 1-99* | 1-99 is gereserveerd voor aangepaste synchronisatie regels. Een waarde die wordt gebruikt door andere synchronisatieregels niet opgenomen. |

5. Ga toohello **Scoping filter** tabblad en voeg een **één filter bereikgroep Hello volgende component**:
 
    | Kenmerk | Operator | Waarde |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Gebruiker\_ | 
 
    Bereik filter bepaalt welke on-premises AD-objecten dat deze synchronisatieregel voor binnenkomende wordt toegepast op. In dit voorbeeld gebruiken we Hallo hetzelfde bereik filter als gebruikt *' In uit Active Directory-gebruiker algemene '* OOB-synchronisatieregel, die voorkomt Hallo synchronisatieregel wordt dat toegepast tooUser-objecten die zijn gemaakt via Write-back van Azure AD-gebruiker functie. Mogelijk moet u tootweak Hallo bereik filteren op basis van tooyour Azure AD Connect-implementatie.

6. Ga toohello **transformatie tabblad** en implementeren van Hallo transformatieregel te volgen:
 
    | Stroomtype | Doelkenmerk | Bron | Eenmaal toepassen | Type samenvoeging |
    | --- | --- | --- | --- | --- |
    | Directe | PreferredDataLocation | Kies het bronkenmerk Hallo | Dit selectievakje is uitgeschakeld | Update |

7. Klik op **toevoegen** toocreate Hallo binnenkomende regel.

![Synchronisatieregel voor binnenkomende maken](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>Stap 5: Maak een uitgaande synchronisatie regel tooflow Hallo kenmerk waarde tooAzure AD
Hallo uitgaande synchronisatieregel toestaat Hallo kenmerk waarde tooflow van Hallo Metaverse toohello PreferredDataLocation-kenmerk in Azure AD:

1. Ga toohello **synchronisatieregels** Editor.

2. Set Hallo zoekfilter **richting** toobe **uitgaand**.

3. Klik op **nieuwe regel toevoegen** knop.

4. Onder Hallo **beschrijving** tabblad, bieden Hallo volgende configuratie:

    | Kenmerk | Waarde | Details |
    | --- | --- | --- |
    | Naam | *Geef een naam* | Bijvoorbeeld, 'Out tooAAD – gebruiker PreferredDataLocation' |
    | Beschrijving | *Geef een beschrijving* |
    | Verbonden systeem | *Selecteer Hallo AAD-connector* |
    | Verbonden systeem objecttype | Gebruiker ||
    | Metaverse-objecttype | **Persoon** ||
    | Koppelingstype | **Koppelen** ||
    | Prioriteit | *Kies een getal tussen 1-99* | 1-99 is gereserveerd voor aangepaste synchronisatie regels. YDo niet een waarde die wordt gebruikt door andere synchronisatieregels opgenomen. |

5. Ga toohello **Scoping filter** tabblad en voeg een **één filter bereikgroep met twee componenten**:
 
    | Kenmerk | Operator | Waarde |
    | --- | --- | --- |
    | Bronobjecttype | GELIJK ZIJN AAN | Gebruiker |
    | cloudMastered | NOTEQUAL | True |

    Bereik filter bepaalt welke deze uitgaande synchronisatieregel wordt toegepast op Azure AD-objecten. In dit voorbeeld gebruiken we Hallo hetzelfde bereik filter van 'Out tooAD – gebruikersidentiteit' OOB-synchronisatieregel. Het verhindert dat de synchronisatieregel Hallo toegepaste tooUser-objecten die niet zijn gesynchroniseerd vanuit de lokale Active Directory. Mogelijk moet u tootweak Hallo bereik filteren op basis van tooyour Azure AD Connect-implementatie.
    
6. Ga toohello **transformatie** tabblad en implementeren van Hallo transformatieregel te volgen:

    | Stroomtype | Doelkenmerk | Bron | Eenmaal toepassen | Type samenvoeging |
    | --- | --- | --- | --- | --- |
    | Directe | PreferredDataLocation | PreferredDataLocation | Dit selectievakje is uitgeschakeld | Update |

7. Sluit **toevoegen** toocreate Hallo uitgaande regel.

![Uitgaande synchronisatieregel maken](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>Stap 6: De volledige synchronisatie uitvoeren cyclus
Volledige synchronisatiecyclus in het algemeen is vereist omdat we hebben nieuwe kenmerken tooboth Hallo AD en Azure AD-Connector schema toegevoegd en aangepaste synchronisatieregels geïntroduceerd. Het is raadzaam Hallo wijzigingen te controleren voordat u ze tooAzure AD exporteert. U kunt Hallo volgende stappen tooverify Hallo wijzigingen tijdens het Hallo-stappen die gezamenlijk een volledige synchronisatiecyclus handmatig uit te voeren. 

1. Voer **volledige import** stap op Hallo **on-premises AD-Connector**:

   1. Ga toohello **Operations** tabblad in Hallo Synchronization Service Manager.

   2. Met de rechtermuisknop op Hallo **on-premises AD-Connector** en selecteer **uitvoeren...**

   3. Selecteer in het pop-upvenster hello, **volledige Import** en klik op **OK**.
    
   4. Wacht u totdat de bewerking toocomplete.

    > [!NOTE]
    > U kunt de volledige Import overslaan op Hallo lokale AD-Connector als Hallo bronkenmerk al in het Hallo-lijst met geïmporteerde kenmerken opgenomen is. Met andere woorden, u hebt geen toomake elke wijziging gedurende [stap 2: Hallo bron kenmerk toohello lokale AD-Connector toevoegen schema](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Voer **volledige import** stap op Hallo **Azure AD-Connector**:

   1. Met de rechtermuisknop op Hallo **Azure AD-Connector** en selecteer **uitvoeren...**

   2. Selecteer in het pop-upvenster hello, **volledige Import** en klik op **OK**.
   
   3. Wacht u totdat de bewerking toocomplete.

3. Controleer of Hallo synchronisatie van wijzigingen in de regel op een bestaande gebruikersobject:

Hallo bronkenmerk van on-premises Active Directory en PreferredDataLocation van Azure AD zijn geïmporteerd in Hallo respectieve connector ruimte. Voordat u doorgaat met de stap van de volledige synchronisatie wordt aanbevolen dat u wilt een **Preview** op een bestaande gebruiker-object in Hallo lokale AD Connectorgebied overgebracht. Hallo-object die u verzameld hebt Hallo bronkenmerk ingevuld. Een geslaagde **Preview** Hello PreferredDataLocation ingevuld in Hallo Metaverse is een goede indicatie Hallo synchronisatieregels juist geconfigureerd. Voor informatie over het toodo een **Preview**, Raadpleeg toosection [Controleer Hallo wijziging](#verify-the-change).

4. Voer **volledige synchronisatie** stap op Hallo **on-premises AD-Connector**:

   1. Met de rechtermuisknop op Hallo **on-premises AD-Connector** en selecteer **uitvoeren...**
  
   2. Selecteer in het pop-upvenster hello, **volledige synchronisatie** en klik op **OK**.
   
   3. Wacht u totdat de bewerking toocomplete.

5. Controleer of **geplande uitvoerbewerkingen** tooAzure AD:

   1. Met de rechtermuisknop op Hallo **Azure AD-Connector** en selecteer **Connectorgebied zoeken**.

   2. In het pop-upvenster Hallo Connectorgebied zoeken:

      1. Stel **bereik** te**in behandeling exporteren**.
      
      2. Controleer alle drie selectievakjes, met inbegrip van **toevoegen, wijzigen en verwijderen**.
      
      3. Klik op Hallo **Search** knop tooget Hallo lijst met objecten met wijzigingen toobe geëxporteerd. tooexamine hello wijzigingen voor een bepaald object, dubbelklik op Hallo-object.
      
      4. Controleer of Hallo wijzigingen worden verwacht.

6. Voer **exporteren** stap op Hallo **Azure AD-Connector**
      
   1. Klik met de rechtermuisknop Hallo **Azure AD-Connector** en selecteer **uitvoeren...**
   
   2. Selecteer in het pop-upvenster Hallo Connector uitvoeren, **exporteren** en klik op **OK**.
   
   3. Export tooAzure AD toocomplete wacht.

> [!NOTE]
> U merkt u wellicht dat Hallo stappen geen Hallo volledige synchronisatie stap en exporteren op Hallo Azure AD-Connector omvatten. Hallo stappen zijn niet vereist omdat Hallo kenmerkwaarden van de lokale Active Directory tooAzure AD alleen stromen.

### <a name="step-7-re-enable-sync-scheduler"></a>Stap 7: Sync scheduler opnieuw inschakelen
Hallo ingebouwde sync scheduler opnieuw inschakelen:

1. Start PowerShell-sessie.

2. Geplande synchronisatie opnieuw inschakelen door de cmdlet uit te voeren:`Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Volgende stappen
* Lees meer over Hallo configuratiemodel in [Understanding declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Lees meer over Hallo expressietaal in [Understanding declaratieve inrichting expressies](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Overzichtsonderwerpen**

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
