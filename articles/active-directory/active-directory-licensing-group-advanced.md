---
title: Active Directory-licentieverlening voor aanvullende scenario's op basis van groep aaaAzure | Microsoft Docs
description: Meer scenario's voor Azure Active Directory op basis van een groep licentieverlening
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Scenario's, beperkingen en bekende problemen met behulp van groepen toomanage licentieverlening in Azure Active Directory

Gebruik Hallo informatie over en voorbeelden toogain een uitgebreidere kennis van Azure Active Directory (Azure AD) op basis van een groep licenties te volgen.

## <a name="usage-location"></a>Gebruikslocatie

Sommige Microsoft-services zijn niet beschikbaar op alle locaties. Voordat u een licentie kan worden toegewezen als de gebruiker tooa, Hallo beheerder toospecify Hallo heeft **gebruikslocatie** -eigenschap op Hallo-gebruiker. In [hello Azure-portal](https://portal.azure.com), kunt u opgeven in **gebruiker** &gt; **profiel** &gt; **instellingen**.

Groep licentie wilt toewijzen neemt alle gebruikers zonder een gebruikslocatie opgegeven locatie op Hallo van Hallo directory. Als u gebruikers op meerdere locaties hebt, zorg ervoor dat tooreflect die correct in uw gebruikersobjecten voordat gebruikers toogroups met licenties toe te voegen.

> [!NOTE]
> Licentie groepstoewijzing wordt nooit een bestaande waarde van de locatie van informatie over het gebruik van een gebruiker wijzigen. Het is raadzaam altijd gebruikslocatie ingesteld als onderdeel van de stroom van de gebruiker maken in Azure AD (bijvoorbeeld via AAD Connect-configuratie) - Hallo resultaat van de licentietoewijzing altijd juist is en gebruikers ontvangen geen services op locaties die niet zo dat toegestaan.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Gebruik op basis van een groep met dynamische groepen-licentieverlening

U kunt gebruiken met een beveiligingsgroep, wat betekent dat kan worden gecombineerd met Azure AD-dynamische groepen op basis van een groep licenties. Dynamische groepen regels uitgevoerd door de gebruiker object kenmerken tooautomatically toevoegen en gebruikers verwijderen uit groepen.

U kunt bijvoorbeeld een dynamische groep maken voor een reeks producten die u wilt tooassign toousers. Elke groep wordt gevuld door een regel voor het toevoegen van gebruikers met hun kenmerken, en elke groep is toegewezen Hallo licenties dat u ze tooreceive wilt. U kunt Hallo kenmerk lokale toewijzen en gesynchroniseerd met Azure AD of u Hallo kenmerk rechtstreeks in de cloud Hallo kunt beheren.

Licenties zijn toohello gebruiker toegewezen kort nadat ze toohello groep worden toegevoegd. Hallo-kenmerk is gewijzigd, Hallo gebruiker verlaat Hallo groepen als Hallo-licenties worden verwijderd.

### <a name="example"></a>Voorbeeld

Bekijk Hallo voorbeeld van een lokale oplossing voor identiteitsbeheer die bepaalt welke gebruikers toegang tooMicrosoft web-services moeten hebben. Hierbij **extensionAttribute1** toostore een tekenreekswaarde die Hallo licenties Hallo gebruiker mag hebben. Azure AD Connect wordt deze gesynchroniseerd met Azure AD.

Gebruikers mogelijk moeten een licentie maar niet nog een of beide moet. Hier volgt een voorbeeld, waarin u distribueert Office 365 Enterprise E5- en Enterprise Mobility + Security (EMS) licenties toousers in groepen:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: base services

![Schermopname van Office 365 Enterprise E5 basisservices](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: gelicentieerde gebruikers

![Schermopname van Enterprise Mobility + Security gelicentieerde gebruikers](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

Bijvoorbeeld, een gebruiker wijzigt en stel de waarde van hun extensionAttribute1 toohello van `EMS;E5_baseservices;` desgewenst Hallo gebruiker toohave beide licenties. Deze wijziging kunt u lokale. Na het Hallo wijzigen wordt gesynchroniseerd met de cloud hello, Hallo gebruiker tooboth groepen automatisch toegevoegd en licenties zijn toegewezen.

![Schermopname die laat zien hoe tooset Hallo extensionAttribute1 van gebruiker](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Wees voorzichtig bij het wijzigen van de regel voor lidmaatschap van een bestaande groep. Wanneer een regel wordt gewijzigd, Hallo lidmaatschap van Hallo groep wordt opnieuw geëvalueerd en gebruikers die niet langer overeenkomen met de Hallo nieuwe regel wordt verwijderd (gebruikers die nog steeds voldoen aan de nieuwe regel Hallo wordt niet beïnvloed tijdens dit proces). Deze gebruikers hebben de licenties worden verwijderd tijdens het Hallo-proces wat leiden verlies van de service of in sommige gevallen tot kan, verlies van gegevens.

> Als u een grote dynamische groep die u afhankelijk van de licentietoewijzing hebt, overweeg geen grote wijzigingen op een kleinere testgroep valideren voordat u deze toohello hoofdgroep toepast.

## <a name="multiple-groups-and-multiple-licenses"></a>Meerdere groepen en meerdere licenties

Een gebruiker kan lid zijn van meerdere groepen met licenties zijn. Hier volgen enkele tooconsider dingen:

- Meerdere licenties voor Hallo hetzelfde product kunt overlappen, en ze ertoe leiden dat alle services ingeschakeld wordt de gebruiker toegepast toohello. Hallo volgende voorbeeld ziet u twee licentieverlening groepen: *E3 basisservices* Hallo foundation services toodeploy eerst tooall gebruikers bevat. En *E3 services uitgebreide* extra services (invloed en Planner) toodeploy alleen toosome gebruikers bevat. In dit voorbeeld is Hallo gebruiker tooboth groepen toegevoegd:

  ![Schermopname van ingeschakelde services](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Hallo gebruiker heeft als gevolg hiervan 7 van 12 Hallo-services in Hallo product ingeschakeld tijdens het gebruik van slechts één licentie voor dit product.

- Selecteren Hallo *E3* licentie bevat meer informatie, zoals informatie over welke groepen welke services toobe ingeschakeld voor de gebruiker Hallo veroorzaakt.

  ![Schermopname van ingeschakelde services per groep](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Directe licenties worden gecombineerd met de groep licenties

Wanneer een gebruiker een licentie uit een groep, u niet rechtstreeks verwijderen of wijzigen die de licentietoewijzing in Hallo gebruikerseigenschappen. De wijzigingen moeten worden aangebracht in Hallo groep en vervolgens doorgegeven tooall gebruikers.

Het is mogelijk, echter tooassign dezelfde productlicentie Hallo direct toohello gebruiker, in aanvulling toohello overgenomen licentie. U kunt extra services uit Hallo product slechts voor één gebruiker inschakelen zonder gevolgen voor andere gebruikers.

Direct toegewezen licenties kunnen worden verwijderd, en niet van invloed op overgenomen licenties. Overweeg het Hallo-gebruiker die een licentie voor Office 365 Enterprise E3 van een groep overneemt.

1. In eerste instantie Hallo gebruiker overneemt Hallo licentie alleen Hallo *E3 basisservices* groep, waardoor vier serviceplannen, zoals wordt weergegeven:

  ![Schermopname van E3 groep services ingeschakeld](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. U kunt selecteren **toewijzen** toodirectly een E3 licentie toohello gebruiker toewijzen. In dit geval gaat u alle service-, behalve Yammer Enterprise plannen toodisable:

  ![Schermopname van hoe u een licentie tooassign rechtstreeks tooa gebruiker](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Als gevolg hiervan Hallo gebruiker nog steeds slechts één licentie van Hallo E3-product gebruikt. Maar Hallo rechtstreekse toewijzing kunt Hallo Yammer Enterprise-service voor alleen die gebruiker. U kunt zien welke services zijn ingeschakeld door Hallo groepslidmaatschap versus Hallo rechtstreekse toewijzing:

  ![Schermopname van overgenomen versus rechtstreekse toewijzing](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Wanneer u rechtstreekse toewijzing, zijn Hallo volgende bewerkingen toegestaan:

  - Yammer Enterprise kan worden uitgeschakeld op het gebruikersobject Hallo rechtstreeks. Hallo **in- en uitgeschakeld** in-of uitschakelen in Hallo afbeelding is ingeschakeld voor deze service als tegengestelde toohello andere service in-of uitschakelen. Omdat Hallo service rechtstreeks op Hallo gebruiker is ingeschakeld, kan worden gewijzigd.
  - Extra services kunnen ook worden ingeschakeld als onderdeel van Hallo rechtstreeks licentie is toegewezen.
  - Hallo **verwijderen** knop gebruikte tooremove Hallo direct licentie van Hallo-gebruiker kan zijn. U kunt zien of Hallo gebruiker nu alleen Hallo overgenomen groepslicentie heeft, en alleen Hallo oorspronkelijke services ingeschakeld blijven:

    ![Schermopname die laat zien hoe tooremove rechtstreekse toewijzing](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>Het beheren van nieuwe services toegevoegd tooproducts
Wanneer Microsoft een nieuwe service tooa product toevoegt, wordt deze ingeschakeld in alle groepen toowhich die u hebt toegewezen standaard Hallo productlicentie. Gebruikers in uw tenant geabonneerde toonotifications over de productwijzigingen ontvangt e-mailberichten tevoren melding over Hallo toekomstige service toevoegingen.

Als beheerder, kunt u bekijken van alle groepen die worden beïnvloed door wijziging Hallo en de actie uitvoert, bijvoorbeeld het uitschakelen van de nieuwe service Hallo in elke groep. Bijvoorbeeld, als u groepen als doel voor de implementatie van alleen specifieke services hebt gemaakt, kunt u terugkeren naar deze groepen en zorg ervoor dat alle nieuw toegevoegde services zijn uitgeschakeld.

Hier volgt een voorbeeld van hoe dit proces eruit mogelijk:

1. Oorspronkelijk is aan u toegewezen Hallo *Office 365 Enterprise E5* product tooseveral groepen. Een van deze groepen, genaamd *O365 E5 - alleen Exchange* is ontworpen tooenable alleen Hallo *Exchange Online (2 plannen)* service voor de bijbehorende leden.

2. U hebt een melding ontvangen van Microsoft die Hallo E5 product zal worden uitgebreid met een nieuwe service - *Microsoft Stream*. Wanneer het Hallo-service beschikbaar in uw tenant, kunt u doen Hallo volgende:

3. Ga toohello [ **Azure Active Directory > licenties > alle producten** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) blade en selecteer *Office 365 Enterprise E5*, selecteer daarna **in licentie gegeven groepen**  tooview een lijst van alle groepen met dat product.

4. Klik op het Hallo-groep die u wilt tooreview (in dit geval *O365 E5 - alleen Exchange*). Hiermee opent u Hallo **licenties** tabblad. Op Hallo E5 licentie te klikken, wordt een lijst van alle ingeschakelde services blade geopend.
> [!NOTE]
> Hallo *Microsoft Stream* service is automatisch toegevoegd en ingeschakeld in deze groep, in aanvulling toohello *Exchange Online* service:

  ![Schermafbeelding van de nieuwe service toegevoegd tooa groepslicentie](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Als u toodisable Hallo nieuwe service in deze groep wilt, klikt u op Hallo **in- en uitgeschakeld** service op de volgende toohello in-of uitschakelen en klik op Hallo **opslaan** knop tooconfirm Hallo wijzigen. Azure AD wordt nu verwerkt alle gebruikers in Hallo groep tooapply Hallo wijziging; nieuwe gebruikers toegevoegd toohello groep geen Hallo *Microsoft Stream* -service is ingeschakeld.

  > [!NOTE]
  > Gebruikers hebben mogelijk nog steeds Hallo-service is ingeschakeld via een aantal andere licentietoewijzing (een andere groep zijn leden van of de licentietoewijzing van een directe).

6. Indien nodig, uitvoeren Hallo dezelfde stappen voor andere groepen met dit product is toegewezen.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Gebruik PowerShell toosee die overgenomen en directe licenties
U kunt een PowerShell-script toocheck gebruiken als gebruikers beschikken over een licentie toegewezen rechtstreeks of overgenomen van een groep.

1. Voer Hallo `connect-msolservice` cmdlet tooauthenticate en tooyour huurder verbinding.

2. `Get-MsolAccountSku`kan worden gebruikt toodiscover ingerichte productlicenties in Hallo-tenant.

  ![Schermafbeelding van de cmdlet Get-Msolaccountsku Hallo](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Gebruik Hallo *AccountSkuId* waarde voor Hallo licentie u geïnteresseerd in met bent [dit PowerShell-script](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Het resultaat is een lijst met gebruikers die deze licentie met Hallo informatie over hoe Hallo-licentie is toegewezen.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Gebruik de auditlogboeken licentieverlening activiteit toomonitor op basis van een groep

U kunt [auditlogboeken van Azure AD](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee alle activiteiten betrekking hebben op basis van toogroup-licentieverlening, met inbegrip van:
- die licenties van groepen die zijn gewijzigd
- Wanneer Hallo system begonnen met het verwerken van een wijziging in de groep licentie, en wanneer het voltooid
- welke licentie zijn tooa gebruiker als gevolg van een licentie groepstoewijzing aangebracht.

>[!NOTE]
> Controlelogboeken zijn beschikbaar op de meeste blades in hello Azure Active Directory-sectie van het Hallo-portal. Afhankelijk van waar u toegang toe, kunnen filters vooraf toegepaste tooonly weergeven activiteit relevante toohello context van de blade Hallo zijn. Als u niet Hallo resultaten oplevert ziet ze, controleert u [Hallo filteropties](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) of toegang tot de controlelogboeken Hallo niet gefilterd onder [ **Azure Active Directory > activiteit > controlelogboeken** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Weten wie een groepslicentie gewijzigd

1. Set Hallo **activiteit** te filteren*Set groepslicentie* en klik op **toepassen**.
2. Hallo resultaten bevatten alle gevallen van de licenties worden ingesteld of gewijzigd op groepen.
>[!TIP]
> U kunt ook de naam van groep Hallo Hallo typen in Hallo *doel* tooscope Hallo resultaten filteren.

3. Klik op een item in toosee Hallo details voor Hallo lijst weergeven van wat is er gewijzigd. Onder *eigenschappen gewijzigd* oude en nieuwe waarden voor de licentietoewijzing Hallo staan.

Hier volgt een voorbeeld van recente groep licentie wijzigingen met details:

![Schermopname licentie wijzigingen](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Nagaan wanneer wijzigingen gestart en wordt uitgevoerd

Wanneer een licentie voor een groep wordt gewijzigd, moet u Azure AD gaat Hallo wijzigingen tooall gebruikers toepassen.

1. toosee wanneer groepen gestart verwerking, stel Hallo **activiteit** te filteren*toe te passen op basis van groep licentie toousers*. Houd er rekening mee dat actor Hallo voor Hallo-bewerking is *Microsoft Azure AD op basis van een groep Licensing* -een systeem-account dat is gebruikt tooexecute alle wijzigingen van de groep licentie.
>[!TIP]
> Klik op een item in Hallo lijst toosee hello *eigenschappen gewijzigd* veld - toont het Hallo licentie wijzigingen die zijn opgepikt voor verwerking. Dit is handig als u meerdere wijzigingen tooa groep hebt gemaakt en u niet zeker weet welk is verwerkt.

2. Op deze manier toosee wanneer groepen klaar met de verwerking, gebruik Hallo filterwaarde *klaar bent met het toepassen van de groep op basis van licentie toousers*.
>[!TIP]
> In dit geval Hallo *eigenschappen gewijzigd* veld bevat een overzicht van resultaten Hallo - dit is nuttig tooquickly selectievakje als verwerking geresulteerd in eventuele fouten. Voorbeelduitvoer:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. toosee logboekset hello voltooid voor hoe een groep is verwerkt, met inbegrip van alle wijzigingen van de gebruiker, Hallo filters te volgen:
  - **Gestart door (Actor)**: ' Microsoft Azure AD op basis van een groep Licensing '
  - **Datumbereik** (optioneel): aangepast bereik voor wanneer u een specifieke groep weet gestart en wordt uitgevoerd

Deze voorbeelduitvoer bevat Hallo begindatum van verwerking, alle resulterende wijzigingen van gebruiker en Hallo voltooien wordt verwerkt.

![Schermopname licentie wijzigingen](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Items in verband te klikken*wijziging gebruikerslicentie* details voor licentie wijzigingen zijn toegepast tooeach afzonderlijke gebruiker wordt weergegeven.

## <a name="limitations-and-known-issues"></a>Bekende problemen en beperkingen

Als u op basis van een groep licentieverlening gebruikt, is een goed idee toofamiliarize zelf Hello lijst met bekende problemen en beperkingen te volgen.

- Op dit moment op basis van een groep licensing biedt geen ondersteuning voor groepen die geen andere groepen (geneste groepen). Als u een licentiegroep voor tooa geneste toepast, hebben alleen Hallo onmiddellijke eerste niveau gebruiker leden van groep Hallo Hallo-licenties die zijn toegepast.

- Hallo-functie kan alleen worden gebruikt met beveiligingsgroepen. Office-groepen worden momenteel niet ondersteund en u zich niet kunnen toouse ze in het toewijzingsproces Hallo-licentie.

- Hallo [Office 365-beheerportal](https://portal.office.com ) momenteel niet ondersteund op basis van een groep licenties. Als u een licentie voor een gebruiker overneemt van een groep, wordt deze licentie in Hallo Office-beheerportal weergegeven als een gewone gebruiker-licentie. Als u toomodify die licentie of probeer tooremove Hallo licentie probeert, retourneert Hallo portal een foutbericht weergegeven. Overgenomen groep licenties worden niet rechtstreeks op een gebruiker gewijzigd.

- Wanneer een gebruiker wordt verwijderd uit een groep en Hallo licentie verliest, service-abonnementen die licentie (bijvoorbeeld, SharePoint Online) Hallo tooa zijn ingesteld **onderbroken** status. Hallo service-abonnementen zijn niet ingesteld tooa def. status uitgeschakeld. Deze voorzorgsmaatregel kunt onbedoeld verwijderen van gebruikersgegevens, voorkomen als een beheerder een fout in het groepsbeheer lidmaatschap maakt.

- Wanneer licenties zijn toegewezen of gewijzigd voor een grote groep (bijvoorbeeld 100.000 gebruikers), kan dit de prestaties beïnvloeden. In het bijzonder Hallo omvang van de wijzigingen die zijn gegenereerd door Azure AD-automatisering mogelijk negatieve invloed hebben op Hallo prestaties van uw directory-synchronisatie tussen Azure AD en on-premises systemen.

- Licentie management automation reageert tooall typen wijzigingen in de omgeving Hallo niet automatisch. Bijvoorbeeld, u mogelijk hebt uitgevoerd buiten licenties, waardoor sommige toobe gebruikers in een foutstatus. toofree up Hallo beschikbaar seat count, kunt u sommige rechtstreeks toegewezen licenties verwijderen van andere gebruikers. Hallo system echter niet automatisch toothis wijziging reageren en gebruikers in de status van deze fout corrigeren.

  Als een tijdelijke oplossing toothese soorten beperkingen, gaat u toohello **groep** blade in Azure AD en klik op **opnieuw verwerken**. Met deze opdracht verwerkt alle gebruikers in die groep en Hallo fout statussen, indien mogelijk wordt omgezet.

- Op basis van een groep licentieverlening registreert geen fouten wanneer een licentie kan niet worden toegewezen gebruiker tooa vanwege tooa dubbele proxy-adresconfiguratie in Exchange Online; Deze gebruikers worden overgeslagen tijdens de licentietoewijzing. Voor meer informatie over het tooidentify en dit probleem kunt oplossen, raadpleegt [in deze sectie](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over andere scenario's voor Licentiebeheer via Groepsbeleid-licentieverlening, Zie:

* [Wat is licentieverlening in Azure Active Directory op basis van groep?](active-directory-licensing-whatis-azure-portal.md)
* [Toewijzen van licenties tooa groep in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Opsporen en oplossen van licentieproblemen met een voor een groep in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Hoe toomigrate afzonderlijk in licentie gegeven gebruikers licentieverlening in Azure Active Directory op basis van toogroup](active-directory-licensing-group-migration-azure-portal.md)
