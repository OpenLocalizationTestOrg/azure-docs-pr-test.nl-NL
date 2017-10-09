---
title: aaaAdd huisstijl tooyour aanmelden en Toegangsvenster
description: Meer informatie over hoe een bedrijf huisstijl toohello Azure aanmelden pagina tooadd en Hallo toegang pagina met toegangspaneel tot
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a>Huisstijl tooyour aanmelden en Toegangsvenster toevoegen
tooavoid verwarring, willen veel bedrijven tooapply een consistent uiterlijk voor alle Hallo websites en services die ze beheren. Azure Active Directory biedt deze mogelijkheid doordat u toocustomize Hallo vormgeving van Hallo volgende webpagina's met uw bedrijfslogo en kleurenschema toepassen:

* **Aanmeldingspagina** -dit is Hallo-pagina die wordt weergegeven wanneer u zich aanmeldt tooOffice 365 of andere toepassingen op Internet die van Azure AD als id-provider gebruikmaken. U communiceert met deze pagina tijdens een Thuisrealmdetectie of tooenter uw referenties. Hallo Thuisrealmdetectie kunt Hallo system tooredirect federatieve gebruikers tootheir lokale STS (zoals AD FS).
* **Pagina met Toegangspaneel** - Hallo Toegangspaneel is een portal op Internet waarmee u tooview en starten Hallo cloud-toepassingen op basis van uw Azure AD-beheerder u heeft verleend, toegang tot. tooaccess Hallo paneel voor Apptoegang, gebruik Hallo volgende URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).

Dit onderwerp wordt uitgelegd hoe u de aanmeldingspagina Hallo en pagina met toegangspaneel Hallo kunt aanpassen.

> [!NOTE]
> * Huisstijl is een functie die is alleen beschikbaar als u een upgrade hebt uitgevoerd toohello Premium of Basic-editie van Azure Active Directory of een Office 365-gebruiker. Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.
> * Edities Azure Active Directory Premium en Basic zijn beschikbaar voor klanten in China Hallo wereldwijde exemplaar van Azure Active Directory. Edities Azure Active Directory Premium en Basic worden momenteel niet ondersteund in Microsoft Azure-service Hallo beheerd door 21Vianet in China. Voor meer informatie contact met ons opnemen Hallo [Azure Active Directory-Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).
>
>

## <a name="customizing-hello-sign-in-page"></a>Hallo-aanmeldingspagina aanpassen
Als u nodig hebt voor toegang op basis van een browser tooyour cloud-apps en services die uw organisatie op is geabonneerd, gebruikt u doorgaans de aanmeldingspagina Hallo.

Als u wijzigingen tooyour aanmeldingspagina hebt toegepast, kan het Hallo wijzigingen tooappear tooan uur duren.

Er wordt alleen een aanmeldingspagina met huisstijl weergegeven wanneer u een service opent met een tenantspecifieke URL, zoals https://outlook.com/**contoso**.com of https://mail.**contoso**.com.

Wanneer u een service gebruikt met niet-tenantspecifieke URL’s (bijvoorbeeld https://mail.office365.com), wordt er een aanmeldingspagina zonder huisstijl weergegeven. In dat geval wordt uw huisstijl weergegeven zodra u uw gebruikers-id hebt ingevoerd of een gebruikerstegel hebt geselecteerd.

> [!NOTE]
> * Uw domeinnaam moet worden weergegeven als 'Actief' in hello **Active Directory** > **Directory** > **domeinen** sectie Hallo klassieke Azure-portal waarin u huisstijl hebt geconfigureerd.
> * Aanmeldingspagina huisstijl niet meegenomen toohello consumenten zich op de pagina van Microsoft. Als u zich met een persoonlijk Microsoft-account aanmeldt, wordt er een reeks wordt door Azure AD gebruikerstegels met, maar Hallo huisstijl van uw organisatie aanmeldingspagina van Microsoft toohello niet van toepassing.
>
>

Als u tooshow uw bedrijfsmerk en -kleuren en andere aanpasbare elementen op deze pagina wilt, Zie Hallo installatiekopieën toounderstand Hallo verschil tussen de twee ervaringen hello te volgen.

Hallo volgende schermafbeelding ziet en voorbeeld voor Hallo Office 365-aanmeldingspagina op een desktopcomputer **voordat** het aanpassen:

![De Office 365-aanmeldingspagina vóór het aanpassen][1]

Hallo volgende schermafbeelding ziet en voorbeeld voor Hallo Office 365-aanmeldingspagina op een desktopcomputer **nadat** het aanpassen:

![De Office 365-aanmeldingspagina na het aanpassen][2]

Hallo volgende Schermafbeelding toont een voorbeeld van Hallo Office 365-aanmeldingspagina op een mobiel apparaat **voordat** het aanpassen:

![De Office 365-aanmeldingspagina vóór het aanpassen][3]

Hallo volgende Schermafbeelding toont een voorbeeld van Hallo Office 365-aanmeldingspagina op een mobiel apparaat **nadat** het aanpassen:

![De Office 365-aanmeldingspagina na het aanpassen][4]

Wanneer u het formaat van een browservenster, Hallo grote afbeelding, zoals Hallo is een eerder weergegeven andere beeldverhouding aspect tooaccommodate vaak bijgesneden. Met dat gegeven in gedachte, moet u tookeep Hallo belangrijkste visuele elementen in de afbeelding Hallo proberen zodat ze altijd worden weergegeven in Hallo linkerbovenhoek (rechtsboven voor v.r.n.l.-talen). Dit is belangrijk omdat de grootte meestal altijd van Hallo rechterbenedenhoek gaat naar Hallo bovenste / links of van beneden naar boven Hallo Hallo.

Hallo volgende afbeelding ziet u hoe Hallo afbeelding wordt bijgesneden wanneer Hallo browser formaat is gewijzigd toohello links:

![][6]

Hier ziet u hoe deze wordt weergegeven nadat Hallo browser formaat wordt gewijzigd naar de bovenkant Hallo:

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a>Welke elementen op de pagina Hallo kan ik aanpassen?
U kunt na de elementen op de aanmeldingspagina Hallo Hallo aanpassen:

![][5]

| Pagina-element | Locatie op de pagina Hallo |
|:--- | --- |
| Logo in banner |Hallo rechtsboven van Hallo pagina weergegeven. Vervangt Hallo logo Hallo doelsite die u in toodisplays (bijvoorbeeld aanmeldt zich) Office 365 of Azure). |
| Grote afbeelding/achtergrondkleur |Aan de linkerkant Hallo van Hallo pagina weergegeven. Vervangt Hallo installatiekopie Hallo doelsite die u toodisplays zich aanmeldt. Hallo achtergrondkleur worden mogelijk weergegeven in plaats van Hallo grote afbeelding op verbindingen met een lage bandbreedte of op het scherm erg smal. |
| Aangemeld blijven |Onder Hallo wachtwoordtekstvak wordt weergegeven. |
| Tekst van aanmeldingspagina |Hierboven Hallo paginavoettekst weergegeven als u nuttige informatie tooconvey voordat iemand zich aanmeldt met een werk- of schoolaccount-account nodig. U kunt bijvoorbeeld, tooinclude Hallo phone nummer tooyour-helpdesk of een juridische mededeling. |

> [!NOTE]
> Alle elementen zijn optioneel. Als u een Logo in Banner maar geen grote afbeelding opgeeft, bevat Hallo-aanmeldingspagina uw logo en Hallo afbeelding voor de doelsite hello (dat wil zeggen, Hallo Office 365 snelweg in Californië).
>
>

Op de aanmeldingspagina Hallo **aangemeld blijven** selectievakje kunt u een tooremain gebruiker is aangemeld wanneer ze sluiten en opnieuw hun browser openen. Dit heeft geen invloed op de levensduur van de sessie. U kunt Hallo selectievakje op Hallo Azure Active Directory-aanmeldingspagina verbergen.

Hiermee wordt aangegeven of Hallo selectievakje wordt weergegeven, hangt af van Hallo-instelling van **KMSI verbergen**.

![][9]

toohide Hallo selectievakje, configureer deze instelling te**verborgen**.

> [!NOTE]
> Sommige functies van Office 2010 en SharePoint Online, is afhankelijk van gebruikers kunnen toocheck wordt dit selectievakje in. Als u deze instelling toohidden configureert, kunnen aanvullende en onverwachte prompts toosign in uw gebruikers te zien.
>
>

U kunt alle elementen op deze pagina lokaliseren. Wanneer u een standaardset aangepaste elementen hebt geconfigureerd, kunt u meer versies configureren voor verschillende talen. U kunt ook een combinatie van verschillende elementen gebruiken. U kunt bijvoorbeeld:

* Een grote standaardafbeelding maken die geschikt is voor alle culturen en afzonderlijke versies maken voor Engels- en Franstaligen. Bij het instellen van uw tooone browsers van die twee talen Hallo specifieke afbeelding wordt weergegeven, terwijl de standaardafbeelding hello wordt weergegeven voor alle andere talen.
* Voor uw organisatie verschillende logo's configureren (bijvoorbeeld een Japanse en een Hebreeuwse versie).

## <a name="access-panel-page-customization"></a>De pagina met het toegangspaneel aanpassen
Hallo Toegangsvenster pagina is ware een portalpagina voor snelle toegang toohello cloud-apps die u hebt gekregen tooby uw beheerder tot. Op deze pagina worden uw apps weergegeven als toepassingstegels waarop kan worden geklikt.

Hallo volgende Schermafbeelding toont een voorbeeld van een pagina met toegangspaneel na het aanpassen.

![][8]

## <a name="configure-your-directory-with-company-branding"></a>Uw directory configureren met de huisstijl van uw bedrijf
U kunt één standaardset aanpasbare elementen per directory configureren in Hallo klassieke Azure-portal. Nadat Hallo standaardwaarden zijn opgeslagen, kan een beheerder vertaalde versies van elk element voor verschillende talen toevoegen / landinstellingen. Alle aanpasbare elementen zijn optioneel.

Bijvoorbeeld, als u een standaard-Logo in Banner maar geen grote afbeelding configureert, worden Hallo-aanmeldingspagina uw logo in de rechterbovenhoek Hallo. Evenwel de standaardafbeelding Hallo van Hallo site wordt weergegeven.

Stel u Hallo volgende configuratie:

* Een standaardlogo voor in de banner en aanmeldingspaginatekst in het Engels
* Een taalspecifieke aanmeldingspaginatekst in het Duits

Als uw voorkeurstaal Duits is, krijgt u Hallo standaard Logo in Banner maar Hallo Duitse tekst.

Terwijl u een andere set voor elke taal die wordt ondersteund door Azure AD technisch configureren kan, adviseren we dat u het aantal variaties Hallo lage omwille van onderhoud en prestaties.

> [!IMPORTANT]
> Yammer komt niet weergeven hello Azure AD huisstijl aanmeldingspagina pas nadat het Hallo-gebruiker zich aanmeldt. Hallo gebruiker ziet eerst algemene Office 365-aanmeldingspagina Hallo en vervolgens Hallo pagina huisstijl daarna.   
 
 
**tooadd huisstijl tooyour directory voor de bedrijfsportal, voert u Hallo stappen te volgen:**

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder van de directory Hallo gewenste toocustomize.
2. Selecteer Hallo directory gewenste toocustomize.
3. Klik in de werkbalk bovenaan Hallo Hallo op **configureren**.
4. Klik op **Huisstijl aanpassen**.
5. Hallo-elementen die u wilt dat toocustomize wijzigen. Alle velden zijn optioneel.
6. Klik op **Opslaan**.

Kan duren tooan uur voor een nieuwe wijziging u toohello aanmeldingspagina huisstijl tooappear aangebracht.

**tooadd taalspecifieke huisstijl, Voer Hallo stappen te volgen:**

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder van de directory Hallo gewenste toocustomize.
2. Selecteer Hallo directory gewenste toocustomize.
fs3. Klik in de werkbalk bovenaan Hallo Hallo op **configureren**.
4. Klik op **Huisstijl aanpassen**.
5. Klik op **Huisstijl voor een specifieke taal toevoegen**.
6. Selecteer Hallo gewenste taal toocustomize Hallo logo voor, en klik vervolgens op **volgende**.
7. Bewerk alleen Hallo elementen waarvoor u wenst tooconfigure taalspecifieke overschrijft. Alle velden zijn optioneel. Als een veld leeg blijft, vervolgens de aangepaste standaardwaarde Hallo in plaats daarvan wordt weergegeven (of Hallo van Microsoft-standaard als er geen aangepaste standaard is niet geconfigureerd).
8. Klik op **Opslaan**.

**tooremove huisstijl van uw directory uitvoeren Hallo stappen te volgen:**

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder van de directory Hallo gewenste toocustomize.
2. Selecteer Hallo directory gewenste toocustomize.
3. Klik in de werkbalk bovenaan Hallo Hallo op **configureren**.
4. Klik op **Huisstijl aanpassen**.
5. Selecteer op de pagina huisstijl aanpassen Hallo **bestaande huisstijlinstellingen bewerken** en gaat u de volgende pagina toohello.
6. Afhankelijk van de elementen tooremove wilt, kunt u een of meer van de volgende Hallo:

    a. Selecteer onder **Logo in banner** de optie **Geüploade logo verwijderen**.

    b. Selecteer onder **Logo in tegel** de optie **Geüploade logo verwijderen**.

    c. Verwijder Hallo tekst uit alle tekstvakken.

    d. Klik op **Volgende**.

    e. Verwijder Hallo tekst uit alle tekstvakken.
7. Klik op **opslaan** tooremove Hallo elementen.
8. Klik indien nodig op **huisstijl aanpassen** opnieuw en Herhaal deze stappen voor alle taalspecifieke Huisstijlonderdelen die moeten toobe verwijderd.
    Alle huisstijlinstellingen zijn verwijderd wanneer u klikt op **huisstijl aanpassen** en Zie Hallo **Standaardhuisstijl aanpassen** formulier geen bestaande instellingen geconfigureerd.

## <a name="testing-and-examples"></a>Testen en voorbeelden
U doet er verstandig aan om te experimenteren met een testtenant voordat u wijzigingen aanbrengt aan uw productieomgeving.

**tooverify of uw huisstijl is toegepast:**

1. Open een InPrivate- of Incognito-browsersessie.
2. Ga naar https://outlook.com/contoso.com en vervang contoso.com door Hallo domein die u hebt aangepast.

Dit geldt ook voor domeinen met de volgende indeling: contoso.onmicrosoft.com.

toohelp u eenvoudiger effectieve aanpassingssets sets maken, zijn aangepast Hallo twee fictieve aanmeldingspagina's te volgen:

* [http://aka.ms/aaddemo001](http://aka.ms/aaddemo001)
* [http://aka.ms/aaddemo002](http://aka.ms/aaddemo002)

tootest hello taalspecifieke instellingen, moet u toomodify hello standaardtaalvoorkeuren in uw web browser tooa taal die u in de aanpassingen hebt ingesteld. In Internet Explorer, u dit configureren in Hallo **Internetopties** menu.

## <a name="customizable-elements"></a>Aanpasbare elementen
Sommige aanpasbare elementen in Azure AD hebben meerdere gebruiksmogelijkheden. U kunt configureren bedrijfslogo eenmaal per directory en wordt gebruikt voor zowel Hallo aanmelden als Toegangsvenster. Sommige aanpasbare elementen zijn specifieke alleen toohello aanmeldingspagina. Hallo volgende tabel biedt details voor Hallo verschillende aanpasbare elementen.

| Naam | Beschrijving | Beperkingen | Aanbevelingen |
| --- | --- | --- | --- |
| Logo in banner |Hallo Logo in Banner wordt weergegeven op de aanmeldingspagina Hallo en Hallo Toegangsvenster. |<p>JPG of PNG</p><p>60 x 280 pixels</p><p>10 kB</p> |<p>Gebruik het volledige logo van uw organisatie (inclusief pictogram en logotype)</p><p>Houd het maximaal 30 pixels hoog tooavoid schuifbalken worden weergegeven op mobiele apparaten</p><p>Gebruik een grootte van maximaal 4 kB</p><p>Gebruik een transparant PNG-bestand (niet wordt ervan uitgegaan dat Hallo-aanmeldingspagina altijd een witte achtergrond heeft)</p> |
| Logo in tegel |(momenteel niet gebruikt in de aanmeldingspagina Hallo) Deze tekst mogelijk in toekomstige hello, gebruikte tooreplace Hallo algemene werk- of schoolaccount' pictogram op verschillende plaatsen in Hallo-ervaring. |<p>JPG of PNG</p><p>120 x 120 pixels</p><p>10 kB</p> |<p>Houd het eenvoudig (geen kleine tekst), omdat deze installatiekopie van het formaat is gewijzigd too50% |
| </p> | | | |
| Gebruikersnaamlabel op aanmeldingspagina |(momenteel niet gebruikt in de aanmeldingspagina Hallo) Deze tekst mogelijk in toekomstige hello, gebruikte tooreplace Hallo algemene werk- of schoolaccount' tekenreeks op verschillende plaatsen in Hallo-ervaring. U kunt instellen dat deze toosomething zoals 'Contoso-account' of 'Contoso-ID.' |<p>Unicodetekst, up too50 tekens</p><p>Alleen tekst zonder opmaak (geen koppelingen of HTML-tags)</p> |<p>Houd het kort en eenvoudig</p><p>Vraag uw gebruikers hoe ze meestal verwijzen toohello werk- of schoolaccount die u ze van voorziet.</p> |
| Tekst van aanmeldingspagina |Deze ' standaardtekst ' onder Hallo aanmeldingspagina formulier wordt weergegeven en kunt aanvullende instructies gebruikte toocommunicate, of indien tooget help en ondersteuning. |<p>Unicodetekst, up too256 tekens</p><p>Alleen tekst zonder opmaak (geen koppelingen of HTML-tags)</p> |Houd het korter dan 250 tekens (ongeveer 3 regels tekst) |
| Afbeelding op aanmeldingspagina |Hallo-afbeelding is een grote afbeelding die wordt weergegeven op het Hallo-aanmeldingspagina toohello links van Hallo aanmeldingspagina formulier. |<p>JPG of PNG</p><p>1420 x 1200</p><p>500 kB</p> |<p>1420 x 1200 pixels</p><p>Belangrijk: houd de afbeelding zo klein mogelijk, liefst kleiner dan 200 kB. Als deze afbeelding te groot is, Hallo prestaties van Hallo-aanmeldingspagina beïnvloeden wanneer Hallo-installatiekopie is niet opgeslagen in de cache</p><p>Deze afbeelding wordt vaak bijgesneden, tooaccommodate andere beeldverhouding. Houd primaire visuele elementen Hallo Hallo linkerbovenhoek (rechtsboven voor V.r.n.l.-talen), omdat de grootte altijd vanuit Hallo onder/rechterbenedenhoek, waarna er naar Hallo bovenste / links, zoals Hallo browservenster verkleind.</p> |
| Achtergrondkleur van de aanmeldingspagina |Hallo-aanmeldingspagina achtergrondkleur wordt gebruikt in Hallo gebied toohello links van Hallo aanmeldingspagina formulier. |Dit moet een RGB-kleur zijn met een hexadecimale notatie (voorbeeld: #FFFFFF) |<p>Hallo achtergrondkleur kan worden weergegeven in plaats van Hallo grote afbeelding lage bandbreedte</p><p>Hallo primaire kleur van Hallo Logo in Banner is een goed idee</p> |

## <a name="next-steps"></a>Volgende stappen
* [Aan de slag met Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
