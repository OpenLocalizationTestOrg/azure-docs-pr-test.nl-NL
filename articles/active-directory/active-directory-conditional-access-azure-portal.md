---
title: voorwaardelijke toegang tot Active Directory aaaAzure | Microsoft Docs
description: "Gebruik voorwaardelijk toegangsbeheer in Azure Active Directory-toocheck voor specifieke condities bij het verifiëren voor toegang tot tooapplications."
services: active-directory
keywords: voorwaardelijke toegang tooapps, voorwaardelijke toegang in Azure AD, beveiligde toegang tot resources toocompany, beleidsregels voor voorwaardelijke toegang
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Voorwaardelijke toegang in Azure Active Directory

Azure Active Directory kunnen in een wereld mobiel eerste, cloud eerste toodevices voor eenmalige aanmelding, apps en services vanaf elke locatie. Werken met Hallo komst van apparaten (inclusief BYOD), zakelijke netwerken en SaaS-apps 3e partij, IT-professionals worden momenteel geconfronteerd met twee tegengestelde doelstellingen:

- Hallo eindgebruikers toobe productief zorgen overal en wanneer
- Beveiligen van zakelijke activa Hallo op elk gewenst moment

tooimprove productiviteit, Azure Active Directory biedt uw gebruikers met een groot aantal opties tooaccess uw zakelijke activa. Met Toepassingsbeheer toegang, Azure Active Directory kunt u alleen tooensure *Hallo van de juiste mensen* toegang tot uw toepassingen. Wat gebeurt er als u wilt dat toohave meer controle over hoe Hallo juiste mensen toegang hebben tot uw resources onder bepaalde omstandigheden? Wat gebeurt er als u ook hebt voorwaarden waaronder tooblock toegang toocertain apps zelfs voor Hallo *rechtermuisknop mensen*? Bijvoorbeeld, mogelijk OK voor u wanneer Hallo juiste mensen toegang hebben tot bepaalde apps van een vertrouwd netwerk. echter raadzaam niet deze tooaccess deze apps vanaf een netwerk dat u niet vertrouwt. U kunt deze vragen met behulp van voorwaardelijke toegang oplossen.

Voorwaardelijke toegang is een functie van Azure Active Directory waarmee u tooenforce besturingselementen op Hallo toegang tooapps in uw omgeving op basis van bepaalde voorwaarden. U kunt aanvullende vereisten toohello access ofwel verbinden met besturingselementen, of kunt u blokkeren. Hallo-implementatie van voorwaardelijke toegang is gebaseerd op beleidsregels. Een benadering op basis van beleid vereenvoudigt u uw ervaring configuratie Hallo manier die u over uw toegangsvereisten nadenken volgt.  

Normaal gesproken definieert u uw toegangsvereisten using-instructies die zijn gebaseerd op Hallo patroon volgen:

![Besturingselement](./media/active-directory-conditional-access-azure-portal/10.png)

Wanneer u twee exemplaren van Hallo vervangen '*dit*"met de werkelijke informatie hebt u een voorbeeld voor een overzicht van beleid dat waarschijnlijk bekend tooyou lijkt:

*Wanneer aannemers tooaccess onze cloud-apps van netwerken die geen vertrouwde probeert, klikt u vervolgens toegang te blokkeren.*

Beleidsverklaring Hallo bovenstaande licht Hallo power van voorwaardelijke toegang. Terwijl u kunt inschakelen aannemers toobasically toegang tot uw cloud-apps (**die**), met voorwaardelijke toegang ook kunt u voorwaarden onder welke Hallo toegang mogelijk is (**hoe**).

In de context Hallo van voorwaardelijke toegang van Azure Active Directory

- "**Wanneer dit gebeurt**' heet **voorwaarde-instructie**
- "**Voert u deze**' heet **besturingselementen**

![Besturingselement](./media/active-directory-conditional-access-azure-portal/11.png)

Hallo combinatie van een voorwaardeninstructie met de besturingselementen vertegenwoordigt een beleid voor voorwaardelijke toegang.

![Besturingselement](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Besturingselementen

In een beleid voor voorwaardelijke toegang definiëren besturingselementen wat is dat er moet gebeuren wanneer een instructie voor een voorwaarde is voldaan.  
Met besturingselementen, moet u de toegang blokkeren of toestaan van toegang met aanvullende vereisten.
Wanneer u een beleid waarmee toegang configureert, moet u tooselect ten minste een van de vereisten.   

### <a name="grant-controls"></a>Verleen besturingselementen
Hallo huidige implementatie van Azure Active Directory kunt u tooconfigure Hallo grant-vereisten voor toegangsbeheer te volgen:

![Besturingselement](./media/active-directory-conditional-access-azure-portal/05.png)

- **Multi-factor Authentication** -kunt u sterke verificatie door middel van meervoudige verificatie vereisen. Als de provider, kunt u Azure multi-factor of een lokale multi-factor authentication-provider, gecombineerd met Active Directory Federation Services (AD FS) gebruiken. Met multi-factor authentication helpt voorkomen dat bronnen worden geopend door onbevoegde gebruikers mogelijk hebben die toegang heeft gekregen toohello referenties van een geldige gebruiker.

- **Compatibel apparaat** -u kunt beleid voor voorwaardelijke toegang instellen op niveau Hallo-apparaten. U kunt een beleid tooonly inschakelen computers die voldoen aan het beleid instellen of mobiele apparaten die zijn ingeschreven in een mobiel apparaat management tooaccess bronnen van uw organisatie. U kunt bijvoorbeeld Intune toocheck apparaatcompatibiliteit gebruiken, en vervolgens rapporteren tooAzure AD voor afdwinging wanneer Hallo gebruiker een toepassing tooaccess probeert. Voor gedetailleerde richtlijnen over hoe toouse Intune tooprotect apps en gegevens, Zie [apps en gegevens beschermen met Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). Ook kunt u Intune tooenforce gegevensbeveiliging voor verloren of gestolen apparaten. Zie voor meer informatie [Help uw gegevens beschermen met volledig wissen of selectief wissen met Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **Domein apparaat** – u kunt dit verplicht Hallo u hebt gebruikt tooconnect tooAzure Active Directory toobe domein tooyour on-premises apparaten Active Directory (AD). Dit beleid geldt tooWindows desktops, laptops en tablets enterprise. 

Als u meerdere besturingselementen geselecteerd hebt, kunt u ook configureren of allemaal vereist zijn tijdens het verwerken van uw beleid.

![Besturingselement](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Sessie-besturingselementen
Sessie-besturingselementen inschakelen beperkende ervaring in een cloud-app. Hallo sessie besturingselementen worden afgedwongen door de cloud-apps en zijn gebaseerd op aanvullende informatie verstrekt door Azure AD-app toohello over Hallo-sessie.

![Besturingselement](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Afgedwongen app-beperkingen gebruiken
U kunt dit besturingselement toorequire Azure AD toopass Hallo apparaat informatie toohello cloud-app gebruiken. Dit helpt Hallo cloud app weten als Hallo gebruiker afkomstig is van een compatibel apparaat of een domein zijn toegevoegd apparaat. Dit besturingselement momenteel wordt alleen ondersteund met SharePoint als Hallo cloud-app. SharePoint maakt gebruik van Hallo apparaat informatie tooprovide gebruikers een ervaring beperkt of volledig afhankelijk van de apparaatstatus Hallo.
toolearn meer informatie over hoe toorequire beperkte toegang met SharePoint, ga [hier](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Voorwaardeninstructie

de vorige sectie Hallo toosupported opties tooblock heeft geïntroduceerd of beperken van toegang tot tooyour bronnen in de vorm van besturingselementen. In een beleid voor voorwaardelijke toegang definieert u Hallo criteria toobe voldaan hebt voor uw besturingselementen toobe toegepast vorm van een voorwaardeninstructie.  

U kunt opnemen Hallo toewijzingen in de voorwaardeninstructie te volgen:

![Besturingselement](./media/active-directory-conditional-access-azure-portal/07.png)


- **Wie** -In veel gevallen wilt u uw besturingselementen toobe toegepast tooa specifieke groep gebruikers. Een voorwaardeninstructie, kunt u definiëren in deze set Hallo-gebruikers en groepen die het beleid van toepassing op. Indien nodig, kunt u ook expliciet een set gebruikers van uw beleid uitsluiten door ze vrijstellen.  
Als u gebruikers en groepen selecteert, moet u Hallo bereik van het beleid van toepassing op gebruikers definiëren.    

    ![Besturingselement](./media/active-directory-conditional-access-azure-portal/08.png)



- **Wat** -er zijn meestal bepaalde apps die worden uitgevoerd in uw omgeving, vanuit het oogpunt van beveiliging van meer dat aandacht vereist dan andere. Dit geldt bijvoorbeeld apps waarvoor toegang tot toosensitive gegevens.
Als u cloud-apps selecteert, moet u Hallo bereik van uw beleid geldt voor cloud-apps definiëren. Indien nodig, kunt u ook expliciet een set apps uitsluiten van uw beleid.

    ![Besturingselement](./media/active-directory-conditional-access-azure-portal/09.png)


- **Hoe** - zolang toegang tooyour apps wordt uitgevoerd onder de voorwaarden die u kunt beheren, er mogelijk niet nodig voor extra controles opleggen hoe uw cloud-apps worden gebruikt door uw gebruikers. Echter dingen er mogelijk anders als toegang tooyour cloud-apps wordt uitgevoerd, bijvoorbeeld van netwerken die geen vertrouwde of apparaten die niet compatibel. U kunt bepaalde voorwaarden voor toegang tot die aanvullende vereisten gelden voor hoe toegang tooyour apps wordt uitgevoerd definiëren in een voorwaardeninstructie.

    ![Voorwaarden](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Voorwaarden

In de huidige implementatie Hallo van Azure Active Directory kunt u voorwaarden voor Hallo gebieden te volgen:

- Aanmelden risico
- Apparaatplatforms
- Locaties
- Client-apps

![Voorwaarden](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Aanmelden risico

Een risico aanmelden is een object dat wordt gebruikt door Azure Active Directory tootrack Hallo kans een aanmeldingspoging is niet uitgevoerd door Hallo legitieme eigenaar van een gebruikersaccount. In dit object Hallo kans (hoog, Gemiddeld of laag) wordt opgeslagen in de vorm van een kenmerk met de naam [aanmelden risiconiveau](active-directory-reporting-risk-events.md#risk-level). Dit object wordt gegenereerd tijdens een aanmeldingspagina van een gebruiker als aanmelden risico's zijn gedetecteerd door Azure Active Directory. Zie [Riskante aanmeldingen](active-directory-identityprotection.md#risky-sign-ins) voor meer informatie.  
U kunt Hallo berekend aanmelden risiconiveau gebruiken als voorwaarde in een beleid voor voorwaardelijke toegang. 

![Voorwaarden](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Apparaatplatforms

Hallo apparaatplatform wordt gekenmerkt door Hallo-besturingssysteem dat wordt uitgevoerd op uw apparaat:

- Android
- iOS
- Windows Phone
- Windows
- Mac OS (preview). 

![Voorwaarden](./media/active-directory-conditional-access-azure-portal/02.png)

Hallo-platforms voor apparaten die zijn opgenomen en de apparaatplatforms die zijn uitgesloten van een beleid, kunt u definiëren.  
toouse apparaatplatforms in Hallo-beleid, eerste wijziging Hallo configureren Schakelknoppen te**Ja**, en selecteer vervolgens alle of afzonderlijk apparaat platforms Hallo beleid van toepassing. Als u afzonderlijke apparaatplatforms selecteert, heeft Hallo beleid alleen invloed op deze platforms. Aanmeldingen tooother ondersteunde platforms zijn in dit geval wordt niet beïnvloed door het Hallo-beleid.


### <a name="locations"></a>Locaties

Hallo locatie wordt geïdentificeerd door Hallo IP-adres van de client Hallo u tooconnect tooAzure Active Directory hebt gebruikt. Deze voorwaarde vereist dat u bekend bent met toobe **locaties met de naam** en **MFA goedgekeurde IP-adressen**.  

**Met de naam locaties** is een functie van Azure Active Directory, waardoor u toolabel goedgekeurde IP-adresbereiken in uw organisaties. In uw omgeving, kunt u met de naam locaties in de context van Hallo van Hallo detectie van [bestaat de kans dat gebeurtenissen](active-directory-reporting-risk-events.md) en voorwaardelijke toegang. Zie voor meer informatie over het configureren van locaties in Azure Active Directory met de naam [locaties in Azure Active Directory met de naam](active-directory-named-locations.md).

Hallo-nummer van de locaties die u kunt configureren wordt begrensd door Hallo grootte van het gerelateerde object Hallo in Azure AD. U kunt configureren:
 
 - Een locatie met geen too500 IP-bereiken met de naam
 - Maximaal 60 benoemde locaties (preview) met één IP-adresbereik toegewezen tooeach hiervan 


**MFA goedgekeurde IP-adressen** is een functie van multi-factor authentication-server waarmee u toodefine goedgekeurde IP-adresbereiken die lokaal intranet van uw organisatie. Wanneer u de voorwaarden van een locatie configureert, kunt u goedgekeurde IP-adressen toodistinguish tussen verbindingen vanaf het netwerk van uw organisatie en alle andere locaties. Zie voor meer informatie [goedgekeurde IP-adressen](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Kunt u alle locaties opnemen of alle goedgekeurde IP-adressen en kunt u alle goedgekeurde IP-adressen uitsluiten.

![Voorwaarden](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>Client-app

Hallo client-app kan worden op een algemeen niveau Hallo-app (webbrowser, mobiele app, bureaubladclient) u tooconnect tooAzure Active Directory hebt gebruikt of u kunt Exchange Active Sync specifiek selecteren.  
Verouderde verificatie verwijst tooclients met behulp van basisverificatie zoals oudere Office-clients die gebruikmaken van moderne verificatie niet. Voorwaardelijke toegang wordt momenteel niet ondersteund met verouderde verificatie.

![Voorwaarden](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Algemene scenario's

### <a name="requiring-multi-factor-authentication-for-apps"></a>Meervoudige verificatie vereisen voor apps

Veel omgevingen hebben apps waarvoor een hoger niveau van beveiliging dan Hallo anderen.
Dit is bijvoorbeeld Hallo geval voor apps die u toegang tot toosensitive gegevens hebt.
Als u op een andere laag van beveiliging toothese apps tooadd wilt, kunt u een beleid voor voorwaardelijke toegang waarvoor multi-factor authentication-server is vereist wanneer gebruikers toegang hebben tot deze apps kunt configureren.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Meervoudige verificatie vereisen voor toegang via netwerken die geen vertrouwde

Dit scenario is vergelijkbaar toohello vorige scenario, omdat een vereiste voor multi-factor authentication wordt toegevoegd.
Hallo belangrijkste verschil is echter Hallo voorwaarde voor deze vereiste.  
Tijdens het Hallo focus van het vorige scenario Hallo werd op apps met toegang tot toosensitve gegevens, wordt dit scenario Hallo richt zich op vertrouwde locaties.  
U wellicht een vereiste voor multi-factor authentication met andere woorden, als een app wordt geopend door een gebruiker vanaf een netwerk dat u niet vertrouwt.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Alleen vertrouwde apparaten hebben toegang tot Office 365-services

Als u van Intune in uw omgeving gebruikmaakt, kunt u onmiddellijk starten met Hallo voorwaardelijk beleid interface in hello Azure-console.

Veel klanten van Intune voorwaardelijke toegang tooensure of alleen vertrouwde apparaten toegang Office 365-services tot gebruikt. Dit betekent dat mobiele apparaten zijn ingeschreven bij Intune en voldoen aan nalevingsvereisten van beleid en de Windows-pc's die zijn gekoppeld tooan lokaal domein. Een verbetering van de belangrijkste is dat u geen hebt tooset Hallo hetzelfde beleid voor elk Hallo Office 365-services.  Wanneer u een nieuw beleid maakt, configureert u Hallo Cloud-apps tooinclude elke Hallo O365-Apps die u wenst dat tooprotect met met voorwaardelijke toegang.

## <a name="next-steps"></a>Volgende stappen

Als u wilt dat tooknow hoe tooconfigure beleid voor voorwaardelijke toegang, Zie [aan de slag met voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Als u klaar tooconfigure-beleid voor voorwaardelijke toegang voor uw omgeving bent, Zie Hallo [best practices voor voorwaardelijke toegang in Azure Active Directory](active-directory-conditional-access-best-practices.md). 
