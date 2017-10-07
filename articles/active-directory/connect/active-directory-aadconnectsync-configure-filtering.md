---
title: 'Azure AD Connect-synchronisatie: filtering configureren | Microsoft Docs'
description: Legt uit hoe tooconfigure filteren in Azure AD Connect-synchronisatie.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Azure AD Connect-synchronisatie: filtering configureren
U gebruikt voor het filteren, kunt u bepalen welke objecten worden weergegeven in Azure Active Directory (Azure AD) van uw on-premises directory. Hallo standaardconfiguratie neemt alle objecten in alle domeinen in forests Hallo geconfigureerd. Dit is in het algemeen Hallo aanbevolen configuratie. Gebruikers met behulp van Office 365-werkbelastingen, zoals Exchange Online en Skype voor bedrijven profiteren van een volledige lijst met globale adressen zodat ze kunnen e-mail verzenden en iedereen. Met standaardconfiguratie hello hebben ze Hallo die dezelfde ervaring dat ze met een lokale implementatie van Exchange- of Lync hebben zou.

In sommige gevallen echter je vereist de standaardconfiguratie van een aantal wijzigingen toohello maken. Hier volgen enkele voorbeelden:

* U van plan bent toouse hello [meerdere Azure AD-directory-topologie](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). Vervolgens moet u een filter toocontrol welke objecten gesynchroniseerd tooa bepaalde Azure AD-directory worden tooapply.
* U een test uitvoeren voor Azure of Office 365 en u wilt dat alleen een subset van gebruikers in Azure AD. In kleine Pilotimplementatie hello is het niet belangrijk toohave een volledige functionaliteit van algemene adreslijst toodemonstrate Hallo.
* U hebt veel serviceaccounts en andere alle niet-persoonlijke accounts die u niet dat in Azure AD wilt.
* U kunt elke gebruiker accounts lokale niet verwijdert om wettelijke redenen. U alleen uitschakelen deze. Maar in Azure AD kunt u alleen actieve accounts toobe aanwezig.

In dit artikel bevat informatie over hoe tooconfigure verschillende filtermethoden Hallo.

> [!IMPORTANT]
> Microsoft biedt geen ondersteuning te wijzigen of het besturingssysteem van Azure AD Connect-synchronisatie buiten Hallo-acties die formeel zijn gedocumenteerd. Een van deze acties kan leiden tot een inconsistente of niet-ondersteunde status van Azure AD Connect-synchronisatie. Microsoft kan niet als gevolg hiervan technische ondersteuning bieden voor dergelijke implementaties.

## <a name="basics-and-important-notes"></a>Basisbeginselen en belangrijke opmerkingen
In Azure AD Connect-synchronisatie, kunt u filteren op elk gewenst moment inschakelen. Als u met een standaardconfiguratie van directory-synchronisatie begint en filtering configureren, zijn Hallo-objecten die worden gefilterd niet meer gesynchroniseerd tooAzure AD. Vanwege deze wijziging worden alle objecten in Azure AD die eerder zijn gesynchroniseerd, maar vervolgens zijn gefilterd verwijderd in Azure AD.

Voordat u begint met het maken van wijzigingen toofiltering, zorg ervoor dat u [uitschakelen van de geplande taak Hallo](#disable-scheduled-task) zodat u wijzigingen dat u toobe juist nog niet hebt geverifieerd per ongeluk niet exporteren.

Omdat veel objecten op Hallo filtering kunt verwijderen dezelfde tijd gewenste toomake of uw nieuwe filters juist zijn voordat u begint met het exporteren van een tooAzure AD wordt gewijzigd. Nadat u Hallo configuratiestappen hebt voltooid, wordt aangeraden dat u Hallo volgt [verificatiestappen](#apply-and-verify-changes) voordat u exporteren en wijzigingen tooAzure AD.

functie tooprotect u verwijderen veel objecten per ongeluk, Hallo '[onopzettelijk verwijderen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)' is standaard ingeschakeld. Als u veel objecten vanwege verwijdert toofiltering (500 standaard), moet u toofollow Hallo stappen in dit artikel tooallow hello toogo via tooAzure AD worden verwijderd.

Als u een build vóór November 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)), maakt u een tooa filter-configuratie wijzigen en Wachtwoordsynchronisatie, gebruiken, moet u een volledige synchronisatie van alle wachtwoorden tootrigger nadat u Hallo configuratie hebt voltooid. Zie voor stappen op hoe een wachtwoord tootrigger volledige synchronisatie [activeren van een volledige synchronisatie van wachtwoorden voor alle](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Als u versie 1.0.9125 of hoger, klikt u vervolgens Hallo regular **volledige synchronisatie** actie berekent ook Hiermee wordt aangegeven of wachtwoorden moeten worden gesynchroniseerd en als deze extra stap niet langer vereist is.

Als **gebruiker** objecten onbedoeld in Azure AD zijn verwijderd vanwege een fout filteren, kunt u opnieuw maken Hallo gebruikersobjecten in Azure AD door het verwijderen van uw filteren configuraties. Vervolgens kunt u uw adreslijsten opnieuw synchroniseren. Deze actie herstelt Hallo gebruikers vanuit de Prullenbak Hallo in Azure AD. U kunt andere objecttypen echter kan niet ongedaan. Bijvoorbeeld, als u per ongeluk een beveiligingsgroep verwijdert en was het gebruikte tooACL een resource, worden de ACL's en het Hallo-groep niet hersteld.

Azure AD Connect verwijdert u alleen objecten die deze heeft één keer beschouwd als toobe binnen het bereik. Er zijn objecten die zijn gemaakt door een andere synchronisatie-engine in Azure AD en deze objecten niet binnen het bereik, verwijderen toe te voegen filteren niet. Bijvoorbeeld, als u begint met een DirSync-server die een volledige kopie van uw gehele map in Azure AD gemaakt en u een nieuwe Azure AD Connect-synchronisatieserver parallel met filtering is ingeschakeld vanaf het begin van de Hallo installeert, verwijderen Azure AD Connect niet Hallo extra objecten die zijn gemaakt door DirSync.

Hallo configuratie voor het filteren is behouden wanneer u installeren of upgraden van tooa nieuwere versie van Azure AD Connect. Het is altijd een best practice tooverify die Hallo configuratie is niet per ongeluk gewijzigd na een nieuwere versie van de upgrade tooa voordat Hallo eerste synchronisatiecyclus wordt uitgevoerd.

Als u meer dan één forest hebt, hebt u Hallo filteren configuraties die worden beschreven in dit onderwerp tooevery forest moet toepassen (ervan uitgaande dat u wilt dat Hallo dezelfde configuratie voor alle paden).

### <a name="disable-hello-scheduled-task"></a>De geplande taak Hallo uitschakelen
toodisable hello ingebouwde scheduler waarmee een synchronisatiecyclus elke 30 minuten wordt geactiveerd als volgt te werk:

1. Ga tooa PowerShell-prompt.
2. Voer `Set-ADSyncScheduler -SyncCycleEnabled $False` toodisable Hallo scheduler.
3. Breng Hallo-wijzigingen die zijn beschreven in dit artikel.
4. Voer `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable Hallo scheduler opnieuw.

**Als u een Azure AD Connect-build voordat 1.1.105.0**  
toodisable hello geplande taak die activeert een synchronisatiecyclus elke drie uur, als volgt te werk:

1. Start **Task Scheduler** van Hallo **Start** menu.
2. Direct onder **bibliotheek voor Taakplanner**, de taak Hallo zoeken met de naam **Azure AD Sync Scheduler**, klik met de rechtermuisknop en selecteer **uitschakelen**.  
   ![Taakplanner](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. U kunt nu configuratiewijzigingen aanbrengen en de synchronisatie-engine Hallo handmatig uitvoeren vanuit Hallo **Synchronization Service Manager** console.

Nadat u uw filteren wijzigingen hebt voltooid, vergeet dan niet terug toocome en **inschakelen** Hallo taak opnieuw.

## <a name="filtering-options"></a>Opties voor het filteren
U kunt toepassen Hallo filteren configuratie typen toohello hulpprogramma directory-synchronisatie te volgen:

* [**Op basis van een groep**](#group-based-filtering): filteren op basis van een groep kan alleen worden geconfigureerd op de eerste installatie met behulp van de installatiewizard Hallo.
* [**Op basis van een domein**](#domain-based-filtering): deze optie gebruikt, kunt u selecteren welke domeinen tooAzure AD synchroniseren. U kunt ook toevoegen en domeinen verwijderen uit de configuratie voor synchronisatie-engine Hallo wanneer u wijzigingen tooyour on-premises infrastructuur nadat u Azure AD Connect-synchronisatie hebt geïnstalleerd.
* [**Organisatie-eenheid (OE) – op basis van**](#organizational-unitbased-filtering): deze optie gebruikt, kunt u selecteren welke organisatie-eenheden tooAzure AD synchroniseren. Deze optie is voor alle objecttypen in de geselecteerde OE's.
* [**Op kenmerken gebaseerde**](#attribute-based-filtering): deze optie gebruikt, kunt u objecten op basis van de kenmerkwaarden voor Hallo objecten filteren. U kunt ook verschillende filters voor verschillende objecttypen hebben.

U kunt meerdere filteropties op Hallo hetzelfde moment. Bijvoorbeeld, kunt u filteren op basis van organisatie-eenheid tooonly objecten opnemen in een organisatie-eenheid. AT Hallo dezelfde tijd, kunt u verder op kenmerken gebaseerde filteren toofilter Hallo objecten gebruiken. Wanneer u meerdere filtermethoden, gebruik Hallo filters een logische 'en' hello filters.

## <a name="domain-based-filtering"></a>Filteren op basis van een domein
Deze sectie biedt u Hallo stappen tooconfigure uw domein-filter. Als u toegevoegd of verwijderd van domeinen in uw forest nadat u Azure AD Connect geïnstalleerd, hebt u ook tooupdate Hallo configuratie filteren.

Hallo voorkeur manier toochange filteren op basis van een domein is door de installatiewizard Hallo en wijzigen van [domein en OE filteren](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Hallo-installatiewizard automatiseert alle Hallo-taken die worden beschreven in dit onderwerp.

Volg deze stappen alleen als u toorun Hallo-installatiewizard om een bepaalde reden bent.

Filteren configuratie op basis van een domein bestaat uit de volgende stappen uit:

1. [Selecteer Hallo domeinen](#select-domains-to-be-synchronized) dat u wilt dat tooinclude in Hallo synchronisatie.
2. Aan elk toegevoegd en verwijderd domein, pas Hallo [uitvoeringsprofielen](#update-run-profiles).
3. [Van toepassing en controleer of wijzigingen](#apply-and-verify-changes).

### <a name="select-hello-domains-toobe-synchronized"></a>Selecteer Hallo domeinen toobe gesynchroniseerd
tooset hello domein filteren, Hallo volgende stappen:

1. Meld u aan toohello server waarop Azure AD Connect-synchronisatie wordt uitgevoerd met behulp van een account dat lid is van Hallo **ADSyncAdmins** beveiligingsgroep.
2. Start **synchronisatieservice** van Hallo **Start** menu.
3. Selecteer **Connectors**, en in Hallo **Connectors** Selecteer Hallo Connector met het type Hallo **Active Directory Domain Services**. In **acties**, selecteer **eigenschappen**.  
   ![Connectoreigenschappen](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Klik op **mappartities configureren**.
5. In Hallo **mappartities selecteren** optie en domeinen Schakel indien nodig. Controleer of dat alleen Hallo partities die u wilt dat toosynchronize zijn geselecteerd.  
   ![Partities](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Als u hebt gewijzigd van uw on-premises Active Directory-infrastructuur en toegevoegd of verwijderd van domeinen uit Hallo forest, klikt u op Hallo **vernieuwen** knop tooget een bijgewerkte lijst. Wanneer u vernieuwt, wordt u gevraagd om referenties. Geef referenties met leestoegang tooWindows Server Active Directory. Heeft geen toobe Hallo gebruiker die vooraf is ingevuld in het dialoogvenster Hallo.  
   ![Vernieuwen vereist](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. Wanneer u bent klaar, sluit u Hallo **eigenschappen** dialoogvenster door te klikken op **OK**. Als u domeinen verwijderd uit Hallo forest, bericht een pop-dat een domein is verwijderd en dat de configuratie worden opgeschoond.
7. Doorgaan tooadjust hello [uitvoeringsprofielen](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Hallo uitvoeren profielen bijwerken
Als u uw domein filter hebt bijgewerkt, moet u ook tooupdate Hallo uitvoeren profielen.

1. In Hallo **Connectors** lijst, zorg ervoor dat Hallo-Connector die u hebt gewijzigd in de vorige stap Hallo is geselecteerd. In **acties**, selecteer **Uitvoeringsprofielen configureren**.  
   ![Connector uitvoeringsprofielen 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Vinden en identificeren van Hallo profielen te volgen:
    * Volledige Import
    * Volledige synchronisatie
    * Delta-Import
    * Deltasynchronisatie
    * Exporteren
3. Voor elk profiel aanpassen Hallo **toegevoegd** en **verwijderd** domeinen.
    1. Voor elk van de profielen Hallo vijf Hallo volgende stappen uit voor elk **toegevoegd** domein:
        1. Hallo uitvoeren profiel selecteren en klik op **nieuwe stap**.
        2. Op Hallo **stap configureren** pagina in Hallo **Type** vervolgkeuzelijst, selecteer Hallo staptype Hello dezelfde naam als het Hallo-profiel dat u configureert. Klik op **Volgende**.  
        ![Connector uitvoeringsprofielen 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. Op Hallo **connectorconfiguratie** pagina in Hallo **partitie** vervolgkeuzelijst, selecteer Hallo-naam van het Hallo-domein dat u tooyour domein filter hebt toegevoegd.  
        ![Connector uitvoeringsprofielen 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. Hallo tooclose **Uitvoeringsprofiel configureren** dialoogvenster, klikt u op **voltooien**.
    2. Voor elk van de profielen Hallo vijf Hallo volgende stappen uit voor elk **verwijderd** domein:
        1. Selecteer een profiel Hallo uitvoeren.
        2. Als hello **waarde** Hallo **partitie** kenmerk is een GUID op, selecteer Hallo stap en klik op uitvoeren **verwijderen stap**.  
        ![Connector uitvoeringsprofielen 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Controleer of de wijziging. Elk domein dat u wilt dat toosynchronize moet worden vermeld als een stap voor elk uitvoeringsprofiel.
4. Hallo tooclose **Uitvoeringsprofielen configureren** dialoogvenster, klikt u op **OK**.
5.  toocomplete hello configuratie, moet u toorun een **volledige import** en een **Deltasynchronisatie**. Hallo sectie gaan [toepassen en controleer of de wijzigingen](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Organisatie-eenheid – gebaseerd filteren
Hallo voorkeur manier toochange filteren op basis van organisatie-eenheid is door de installatiewizard Hallo en wijzigen van [domein en OE filteren](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Hallo-installatiewizard automatiseert alle Hallo-taken die worden beschreven in dit onderwerp.

Volg deze stappen alleen als u toorun Hallo-installatiewizard om een bepaalde reden bent.

tooconfigure organisatie-eenheid – gebaseerd filteren, Hallo volgende stappen:

1. Meld u aan toohello server waarop Azure AD Connect-synchronisatie wordt uitgevoerd met behulp van een account dat lid is van Hallo **ADSyncAdmins** beveiligingsgroep.
2. Start **synchronisatieservice** van Hallo **Start** menu.
3. Selecteer **Connectors**, en in Hallo **Connectors** Selecteer Hallo Connector met het type Hallo **Active Directory Domain Services**. In **acties**, selecteer **eigenschappen**.  
   ![Connectoreigenschappen](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Klik op **mappartities configureren**, selecteer Hallo domein dat u tooconfigure wilt en klik vervolgens op **Containers**.
5. Wanneer u wordt gevraagd, moet u alle referenties opgeven met leestoegang tooyour on-premises Active Directory. Heeft geen toobe Hallo gebruiker die vooraf is ingevuld in het dialoogvenster Hallo.
6. In Hallo **Containers selecteren** in het dialoogvenster wissen Hallo organisatie-eenheden u niet wilt toosynchronize met de clouddirectory hello, en klik vervolgens op **OK**.  
   ![Organisatie-eenheden in Hallo van het dialoogvenster Containers selecteren](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Hallo **Computers** container moet worden geselecteerd voor uw Windows 10-computers toobe tooAzure AD gesynchroniseerd. Als uw domein computers bevinden zich in een andere organisatie-eenheden, zorg er dan voor dat die zijn geselecteerd.
   * Hallo **ForeignSecurityPrincipals** container moet worden geselecteerd als er meerdere forests met vertrouwensrelaties. Deze container kunt forest-overschrijdende beveiliging groepslidmaatschap toobe opgelost.
   * Hallo **Geregistreerdeapparaten** organisatie-eenheid moet worden geselecteerd als u Hallo apparaat terugschrijven functie ingeschakeld. Als u een andere Write-back-functie, zoals Write-back van groep controleert u of dat deze locaties zijn geselecteerd.
   * Selecteer een andere organisatie-eenheid waar gebruikers, iNetOrgPersons, groepen, contactpersonen en Computers zich bevinden. In afbeelding Hallo bevinden deze organisatie-eenheden zich in Hallo ManagedObjects OU.
   * Als u filteren op basis van een groep, moet klikt u vervolgens Hallo organisatie-eenheid waar Hallo groep bevindt worden opgenomen.
   * Houd er rekening mee dat u configureren kunt of nieuwe OE's die worden toegevoegd nadat Hallo filteren configuratie is voltooid die zijn gesynchroniseerd of niet gesynchroniseerd. Zie de volgende sectie Hallo voor meer informatie.
7. Wanneer u bent klaar, sluit u Hallo **eigenschappen** dialoogvenster door te klikken op **OK**.
8. toocomplete hello configuratie, moet u toorun een **volledige import** en een **Deltasynchronisatie**. Hallo sectie gaan [toepassen en controleer of de wijzigingen](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Synchroniseren van nieuwe organisatie-eenheden
Nieuwe OE's die zijn gemaakt nadat het filteren is geconfigureerd, worden standaard gesynchroniseerd. Deze status wordt aangegeven door het selectievakje is ingeschakeld. U kunt ook het vakje sommige sub-OU's. tooget dit gedrag, klikt u op Hallo-vak totdat deze wit met een blauw vinkje (de standaardstatus) verandert. Vervolgens moet u alle sub-OE toosynchronize niet wilt verwijderen.

Als alle sub-OU's worden gesynchroniseerd, zijn Hallo vak is wit met een blauw vinkje.  
![Organisatie-eenheid met alle selectievakjes zijn geselecteerd](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Als sommige sub-OU's hebt niet geselecteerd, is Hallo selectievakje grijs met een wit vinkje.  
![Organisatie-eenheid met sommige sub-OU's uitgeschakeld](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

Met deze configuratie is een nieuwe organisatie-eenheid die is gemaakt onder ManagedObjects gesynchroniseerd.

Hello Azure AD Connect-installatiewizard wordt altijd gemaakt voor deze configuratie.

### <a name="dont-synchronize-new-ous"></a>Nieuwe OE's niet synchroniseren
Kunt u Hallo sync engine toonot nieuwe OE's gesynchroniseerd nadat Hallo filteren configuratie is voltooid. Deze status wordt aangegeven in Hallo UI door Hallo vak effen grijs zonder vinkje worden weergegeven. tooget dit gedrag, klikt u op Hallo-vak totdat deze wit zonder vinkje verandert. Selecteer vervolgens Hallo sub-OE's die u toosynchronize wilt.

![Organisatie-eenheid met Hallo hoofdmap uitgeschakeld](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

Met deze configuratie is niet een nieuwe organisatie-eenheid die is gemaakt onder ManagedObjects gesynchroniseerd.

## <a name="attribute-based-filtering"></a>Filteren op basis van het kenmerk
Zorg ervoor dat u Hallo November 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) of een latere versie van deze stappen toowork.

Filteren op basis van het kenmerk is Hallo meest flexibele manier toofilter objecten. U kunt Hallo macht van [declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol bijna elk aspect van wanneer een object is tooAzure AD gesynchroniseerd.

U kunt toepassen [inkomende](#inbound-filtering) voor het filteren van Active Directory toohello metaverse, en [uitgaande](#outbound-filtering) voor het filteren van Hallo metaverse tooAzure AD. Het is raadzaam dat u inkomende filteren omdat dat Hallo eenvoudigste toomaintain toepassen. Gebruik alleen uitgaande filteren als dit toojoin objecten uit meer dan één forest is vereist voordat het Hallo-evaluatie kan plaatsvinden.

### <a name="inbound-filtering"></a>Inkomende filteren
Inkomende filteren maakt gebruik van Hallo de standaardconfiguratie, waarbij objecten gaan tooAzure AD Hallo metaverse-kenmerk cloudFiltered is niet ingesteld tooa waarde toobe gesynchroniseerd moeten hebben. Als de waarde van dit kenmerk is ingesteld, te**True**, en vervolgens het Hallo-object is niet gesynchroniseerd. Mag niet te worden ingesteld**False**, aan het ontwerp. toomake dat andere regels Hallo mogelijkheid toocontribute een waarde hebben, dit kenmerk moet alleen toohave Hallo waarden **True** of **NULL** (afwezig).

In het inkomende filteren, gebruikt u Hallo macht **bereik** toodetermine die objecten toosynchronize of niet synchroniseren. Dit is waar u aanpassingen toofit vereisten van uw eigen organisatie maken. Hallo bereik module heeft een **groep** en een **component** toodetermine wanneer een synchronisatieregel binnen het bereik is. Een groep bevat een of meer componenten. Er is een logische 'en' tussen meerdere componenten en een logische 'of' tussen meerdere groepen.

Laat het ons Bekijk een voorbeeld:  
![Bereik](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
Dit moet worden gelezen als **(afdeling = IT) of (afdeling = verkoop-en c = US)**.

In Hallo volgen voorbeelden en stappen, gebruik van het gebruikersobject Hallo als voorbeeld, maar u kunt deze gebruiken voor alle objecttypen.

In de Hallo volgen voorbeelden, begint Hallo prioriteitswaarde met 50. Dit is een nummer niet gebruikt, maar moet lager zijn dan 100 zijn.

#### <a name="negative-filtering-do-not-sync-these"></a>Negatieve filteren: 'Synchroniseer niet deze'
In de Hallo voorbeeld te volgen, u kunt uitfilteren (niet synchroniseren) alle gebruikers waar **extensionAttribute15** Hallo waarde **NoSync**.

1. Meld u aan toohello server waarop Azure AD Connect-synchronisatie wordt uitgevoerd met behulp van een account dat lid is van Hallo **ADSyncAdmins** beveiligingsgroep.
2. Start **synchronisatie regeleditor** van Hallo **Start** menu.
3. Zorg ervoor dat **inkomend** is geselecteerd en klik op **nieuwe regel toevoegen**.
4. Geef Hallo regel een beschrijvende naam, zoals '*In uit Active Directory-gebruiker DoNotSyncFilter*'. Selecteer Hallo juiste forest, selecteert **gebruiker** als Hallo **CS objecttype**, en selecteer **persoon** als Hallo **MV-objecttype**. In **koppelingstype**, selecteer **Join**. In **voorrang**, typt u een waarde die niet wordt momenteel gebruikt door andere synchronisatieregels (bijvoorbeeld 50) en klik vervolgens op **volgende**.  
   ![Inkomende 1 Beschrijving](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. In **Scoping filter**, klikt u op **groep toevoegen**, en klik op **component toevoegen**. In **kenmerk**, selecteer **ExtensionAttribute15**. Zorg ervoor dat **Operator** te is ingesteld,**gelijk**, en typ de waarde Hallo **NoSync** in Hallo **waarde** vak. Klik op **Volgende**.  
   ![Inkomende 2 bereik](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Hallo laat **Join** regels leeg en klik vervolgens op **volgende**.
7. Klik op **transformatie toevoegen**, selecteer Hallo **FlowType** als **constante**, en selecteer **cloudFiltered** als Hallo  **Doel kenmerk**. In Hallo **bron** in het tekstvak **True**. Klik op **toevoegen** toosave Hallo regel.  
   ![Inkomende 3 transformatie](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. toocomplete hello configuratie, moet u toorun een **volledige synchronisatie**. Hallo sectie gaan [toepassen en controleer of de wijzigingen](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Filteren van positieve: 'alleen synchroniseren deze'
Uitdrukken positief filteren kan moeilijker omdat u ook tooconsider-objecten die niet voor de hand liggende toobe gesynchroniseerd hebt, zoals vergaderruimten zijn. Bent u ook gaat toooverride Hallo standaardfilter in Hallo out of box regel **In uit Active Directory - gebruiker toevoegen**. Wanneer u uw aangepaste filter maakt, moet toonot essentiële systeemobjecten, replicatieobjecten conflict, speciale postvakken en serviceaccounts Hallo voor Azure AD Connect.

Hallo positief filteroptie vereist twee regels voor synchronisatie. U moet één regel (of meerdere) met het juiste bereik van objecten toosynchronize Hallo. U moet ook een tweede synchronisatieregel catch all-gefilterd op alle objecten die nog niet hebt is geïdentificeerd als een object dat moet worden gesynchroniseerd.

In Hallo voorbeeld te volgen, u alleen gebruikersobjecten waar Hallo afdeling kenmerk heeft de waarde van de Hallo synchroniseren **verkoop**.

1. Meld u aan toohello server waarop Azure AD Connect-synchronisatie wordt uitgevoerd met behulp van een account dat lid is van Hallo **ADSyncAdmins** beveiligingsgroep.
2. Start **synchronisatie regeleditor** van Hallo **Start** menu.
3. Zorg ervoor dat **inkomend** is geselecteerd en klik op **nieuwe regel toevoegen**.
4. Geef Hallo regel een beschrijvende naam, zoals '*In uit Active Directory-gebruiker verkoop synchroniseren*'. Selecteer Hallo juiste forest, selecteert **gebruiker** als Hallo **CS objecttype**, en selecteer **persoon** als Hallo **MV-objecttype**. In **koppelingstype**, selecteer **Join**. In **voorrang**, typt u een waarde die niet wordt momenteel gebruikt door andere synchronisatieregels (bijvoorbeeld 51) en klik vervolgens op **volgende**.  
   ![Inkomende 4 beschrijving](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. In **Scoping filter**, klikt u op **groep toevoegen**, en klik op **component toevoegen**. In **kenmerk**, selecteer **afdeling**. Zorg ervoor dat de Operator te is ingesteld**gelijk**, en typ de waarde Hallo **verkoop** in Hallo **waarde** vak. Klik op **Volgende**.  
   ![Inkomende 5 bereik](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Hallo laat **Join** regels leeg en klik vervolgens op **volgende**.
7. Klik op **transformatie toevoegen**, selecteer **constante** als Hallo **FlowType**, en selecteer Hallo **cloudFiltered** als Hallo  **Doel kenmerk**. In Hallo **bron** in het vak **False**. Klik op **toevoegen** toosave Hallo regel.  
   ![Inkomende 6 transformatie](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Dit is een speciaal geval waar u expliciet cloudFiltered te instellen**False**.
8. We hebben nu toocreate Hallo catch all-sync-regel. Geef Hallo regel een beschrijvende naam, zoals '*In uit Active Directory-gebruiker Catch all-filter*'. Selecteer Hallo juiste forest, selecteert **gebruiker** als Hallo **CS objecttype**, en selecteer **persoon** als Hallo **MV-objecttype**. In **koppelingstype**, selecteer **Join**. In **voorrang**, typt u een waarde die niet wordt momenteel gebruikt door andere synchronisatieregels (bijvoorbeeld 99). U kunt een prioriteit die hoger (lagere prioriteit) dan de vorige synchronisatieregel Hallo hebt geselecteerd. Maar u hebt ook ruimte zodat u meer synchronisatie-filterregels later toevoegen kunt als u wilt synchroniseren van aanvullende afdelingen toostart. Klik op **Volgende**.  
   ![Inkomende 7 beschrijving](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Laat **Scoping filter** leeg en klik op **volgende**. Een filternaam is leeg geeft aan dat Hallo-regel is toegepast toobe tooall objecten.
10. Hallo laat **Join** regels leeg en klik vervolgens op **volgende**.
11. Klik op **transformatie toevoegen**, selecteer **constante** als Hallo **FlowType**, en selecteer **cloudFiltered** als Hallo  **Doel kenmerk**. In Hallo **bron** in het vak **True**. Klik op **toevoegen** toosave Hallo regel.  
    ![Inkomende 3 transformatie](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. toocomplete hello configuratie, moet u toorun een **volledige synchronisatie**. Hallo sectie gaan [toepassen en controleer of de wijzigingen](#apply-and-verify-changes).

Als u wilt, kunt u meer regels van de eerste type Hallo waar u meer objecten in Hallo synchronisatie opnemen.

### <a name="outbound-filtering"></a>Uitgaande filteren
In sommige gevallen kan is het benodigde toodo Hallo filteren alleen nadat Hallo objecten hebt toegevoegd in de metaverse Hallo. Het kan bijvoorbeeld nodig toolook op Hallo e-mailkenmerk van Hallo bronforest en Hallo userPrincipalName kenmerk uit het accountforest hello, toodetermine als een object moet worden gesynchroniseerd zijn. In dergelijke gevallen kunt u filteren op Hallo uitgaande regel Hallo maken.

In dit voorbeeld wijzigt u Hallo filteren zodat alleen gebruikers die hun e-mail en de userPrincipalName eindigt op @contoso.com worden gesynchroniseerd:

1. Meld u aan toohello server waarop Azure AD Connect-synchronisatie wordt uitgevoerd met behulp van een account dat lid is van Hallo **ADSyncAdmins** beveiligingsgroep.
2. Start **synchronisatie regeleditor** van Hallo **Start** menu.
3. Onder **regels Type**, klikt u op **uitgaand**.
4. Zoeken naar Hallo regel voor licentiecontrole **uit tooAAD – gebruiker toevoegen**, en klik op **bewerken**.
5. In het pop-upvenster Hallo beantwoorden **Ja** toocreate een kopie van het Hallo-regel.
6. Op Hallo **beschrijving** pagina, wijzigt u **voorrang** tooan ongebruikte waarde, zoals 50.
7. Klik op **Scoping filter** op Hallo linkermenubalk en klik vervolgens op **toevoegen component**. In **kenmerk**, selecteer **mail**. In **Operator**, selecteer **ENDSWITH**. In **waarde**, type  **@contoso.com** , en klik vervolgens op **toevoegen component**. In **kenmerk**, selecteer **userPrincipalName**. In **Operator**, selecteer **ENDSWITH**. In **waarde**, type  **@contoso.com** .
8. Klik op **Opslaan**.
9. toocomplete hello configuratie, moet u toorun een **volledige synchronisatie**. Hallo sectie gaan [toepassen en controleer of de wijzigingen](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Van toepassing en controleer of wijzigingen
Nadat u uw wijzigingen hebt aangebracht, moet u deze toohello-objecten die al aanwezig in Hallo system zijn toepassen. Het kan ook zijn dat Hallo-objecten die zich momenteel niet in de synchronisatie-engine Hallo moeten worden verwerkt (en de synchronisatie-engine Hallo moet tooread Hallo bronsysteem opnieuw tooverify de inhoud ervan).

Als u Hallo configuratie hebt gewijzigd met behulp van **domein** of **organisatie-eenheid** filteren, moet u toodo een **volledige import**, gevolgd door **Delta synchronisatie**.

Als u Hallo configuratie hebt gewijzigd met behulp van **kenmerk** filteren, moet u toodo een **volledige synchronisatie**.

Hallo volgende stappen:

1. Start **synchronisatieservice** van Hallo **Start** menu.
2. Selecteer **Connectors**. In Hallo **Connectors** Selecteer Hallo Connector waar u eerder een configuratiewijziging hebt gemaakt. In **acties**, selecteer **uitvoeren**.  
   ![Connector uitvoeren](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. In **Uitvoeringsprofielen**, Hallo bewerking selecteren die is vermeld in de vorige sectie Hallo. Als u twee acties toorun moet, Voer Hallo tweede na Hallo eerste klaar is. (Hallo **status** kolom is **inactief** voor connector Hallo geselecteerd.)

Alle wijzigingen zijn na de synchronisatie van hello, gefaseerde toobe geëxporteerd. Voordat u daadwerkelijk Hallo wijzigingen in Azure AD aanbrengt, wilt u tooverify dat alle wijzigingen in deze juist zijn.

1. Start een opdrachtprompt en ga te`%Program Files%\Microsoft Azure AD Sync\bin`.
2. Voer `csexport "Name of Connector" %temp%\export.xml /f:x` uit.  
   Hallo naam Hallo Connector is in de synchronisatieservice. Heeft een naam vergelijkbare too"contoso.com – AAD' voor Azure AD.
3. Voer `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv` uit.
4. U hebt nu een bestand in % temp % met de naam export.csv die kan worden onderzocht in Microsoft Excel. Dit bestand bevat alle Hallo-wijzigingen die over toobe geëxporteerd zijn.
5. Breng wijzigingen Hallo toohello gegevens of configuratie, en voer deze stappen opnieuw (importeren, synchroniseren en controleer of) pas Hallo wijzigingen die over toobe geëxporteerd zijn zijn wat u verwacht.

Wanneer u tevreden bent, exporteert u Hallo wijzigingen tooAzure AD.

1. Selecteer **Connectors**. In Hallo **Connectors** Selecteer hello Azure AD-Connector. In **acties**, selecteer **uitvoeren**.
2. In **Uitvoeringsprofielen**, selecteer **exporteren**.
3. Als uw configuratiewijzigingen veel objecten verwijdert, vervolgens ziet u een fout in Hallo exporteren wanneer Hallo aantal hoger dan de drempelwaarde Hallo geconfigureerd (standaard 500 is). Als u deze fout te zien, moet u tootemporarily uitschakelen Hallo '[onopzettelijk verwijderen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)' functie.

Nu is het tijd tooenable Hallo scheduler opnieuw.

1. Start **Task Scheduler** van Hallo **Start** menu.
2. Direct onder **bibliotheek voor Taakplanner**, de taak Hallo zoeken met de naam **Azure AD Sync Scheduler**, klik met de rechtermuisknop en selecteer **inschakelen**.

## <a name="group-based-filtering"></a>Filteren op basis van een groep
U kunt filteren Hallo op basis van een groep configureren eerst Azure AD Connect te installeren met behulp van [aangepaste installatie](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). De bedoeld voor een proef-implementatie waar u een kleine set objecten toobe gesynchroniseerd. Wanneer u filteren op basis van een groep uitschakelt, kunnen deze kan niet worden ingeschakeld. Deze heeft *niet ondersteund* toouse filteren in een aangepaste configuratie op basis van groep. Het is alleen tooconfigure deze functie ondersteund met behulp van de installatiewizard Hallo. Wanneer u uw proefproject hebt voltooid, voert u een van Hallo andere filteropties in dit onderwerp. Wanneer u filteren op basis van organisatie-eenheid in combinatie met filteren op basis van een groep, is Hallo OU('s) waar Hallo groep en de bijbehorende leden zich bevinden moet worden opgenomen.

Bij het synchroniseren van meerdere AD-forests, kunt u filteren op basis van een groep door op te geven van een andere groep voor elk AD-connector kunt configureren. Als u wenst toosynchronize dat een gebruiker in één AD-forest en hello dezelfde gebruiker een heeft of meer bijbehorende FSP (afwijkende beveiligings-Principal) objecten in andere AD-forests, u ervoor dat Hallo gebruikersobject en alle de bijbehorende zorgen moet zijn FSP objecten in op basis van een groep bereik filteren. Als een of meer van de Hallo FSP objecten zijn uitgesloten door te filteren op basis van een groep, worden Hallo gebruikersobject gesynchroniseerde tooAzure AD niet.

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.
- Meer informatie over [uw on-premises identiteiten integreren met Azure AD](active-directory-aadconnect.md).
