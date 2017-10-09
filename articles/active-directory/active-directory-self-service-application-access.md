---
title: toegang tot toepassingen aaaSelf-service en gedelegeerd beheer met Azure Active Directory | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooenable selfservice toepassing toegang tot en gedelegeerd beheer met Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Toegang tot de toepassing zelf en gedelegeerd beheer met Azure Active Directory
Het inschakelen van selfservice mogelijkheden voor eindgebruikers is een veelvoorkomend scenario voor bedrijven. Veel gebruikers door veel toepassingen en Hallo persoon best-informed toomake toegang verlenen beslissingen mogelijk niet Hallo directory-beheerder. Vaak Hallo best persoon toodecide wie toegang een toepassing tot is een lead team of een andere gedelegeerde beheerder. Het is echter Hallo-gebruiker die Hallo app gebruikt en Hallo gebruiker weet wat ze kunnen toodo toobe moeten hun taak.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. 

Toegang tot de toepassing zelf is een functie van [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 en P2 licensing die directory-beheerders toestaan:

* Gebruikers toorequest toegang met behulp van een 'ophalen meer toepassingen' tooapplications-tegel in Hallo [Azure AD-Toegangsvenster](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Instellen welke gebruikers toepassingen toegang tot aanvragen kunnen
* Al dan niet een goedkeuring vereist voor gebruikers toobe kunnen tooself toewijzen access tooan-toepassing is instellen
* Set wie moet goedkeuren Hallo aanvragen en beheren van toegang voor elke toepassing

Vandaag de dag deze mogelijkheid wordt ondersteund voor alle vooraf geïntegreerde en aangepaste apps die ondersteuning bieden voor federatieve of op basis van wachtwoorden eenmalige aanmelding in Hallo [Azure Active Directory-toepassingsgalerie](https://azure.microsoft.com/marketplace/active-directory/all/), met inbegrip van apps zoals Salesforce, Dropbox, Google Apps, en meer.
Dit artikel wordt beschreven hoe:

* Toegang tot toepassingen selfservice voor eindgebruikers, inclusief het configureren van een optionele goedkeuringswerkstroom configureren 
* Delegeren van beheer van toegang voor specifieke toepassingen toohello meest geschikte mensen in uw organisatie, en ze toouse hello Azure AD access Configuratiescherm tooapprove toegangsaanvragen inschakelen, rechtstreeks toegang tooselected gebruikers toewijzen of (optioneel) instellen referenties voor toegang tot toepassingen wanneer op basis van wachtwoorden eenmalige aanmelding is geconfigureerd

## <a name="configuring-self-service-application-access"></a>Toegang tot selfservice-toepassingen configureren
toegang tot de toepassing zelf van tooenable en welke toepassingen kunnen worden toegevoegd of aangevraagd door uw eindgebruikers, volgt u deze instructies geconfigureerd.

1. Meld u aan bij Hallo [klassieke Azure-portal](https://manage.windowsazure.com/).

2.   Onder Hallo **Active Directory** sectie, selecteer uw directory en selecteer vervolgens Hallo **toepassingen** tabblad. 

3. Selecteer Hallo **toevoegen** knop en Hallo galerie optie tooselect gebruiken en een toepassing toevoegen.

4. Nadat uw app is toegevoegd, krijgt u Hallo app snel starten-pagina. Klik op **configureren Single Sign-On**Hallo gewenste aanmelding modus voor één en selecteer Hallo-configuratie op te slaan. 

5. Selecteer vervolgens Hallo **configureren** tabblad tooenable gebruikers toorequest access toothis-app van hello Azure AD-Toegangsvenster, stel **toestaan van toegang tot de toepassing zelf** te**Ja**.
  
  ![][1]

6. toooptionally configureren een goedkeuringswerkstroom voor toegangsaanvragen, stel **moeten worden goedgekeurd voordat u toegang verleent** te**Ja**. Een of meer goedkeurders kunnen worden geselecteerd met Hallo **goedkeurders** knop.

  Een goedkeurder elke gebruiker in de organisatie Hallo met een Azure AD-account, en kan worden verantwoordelijk voor het account inrichten, licenties, of andere bedrijfsproces uw organisatie vereist voordat u verleent toegang tooan app. Hallo goedkeurder kan zelfs worden de Groepseigenaar Hallo van een of meer gedeelde accountgroepen en Hallo gebruikers tooone van deze groepen toogive ze benaderen via een gedeeld account kunt toewijzen. 

  Als geen goedkeuring vereist is, klikt u vervolgens krijgen onmiddellijk gebruikers Hallo toepassing toegevoegde tootheir Azure AD-Toegangsvenster. Als de toepassing hello is ingesteld voor [automatisch gebruikers inrichten](active-directory-saas-app-provisioning.md), of is ingesteld ['gebruikers wordt beheerd' wachtwoord SSO modus](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), Hallo-gebruiker moet een gebruiker account en wachtwoord Hallo weten al hebben.

7. Als de toepassing hello geconfigureerde toouse is is op basis van wachtwoorden eenmalige aanmelding, klikt u vervolgens een optie voor het toestaan van Hallo goedkeurder tooset Hallo SSO-referenties voor elke gebruiker ook beschikbaar. Zie voor meer informatie Hallo-sectie op [gedelegeerd beheer van toegang](#delegated-application-access-management).

8. Ten slotte Hallo **groep voor Self-Assigned gebruikers** toont Hallo naam van groep Hallo gebruikte toostore Hallo gebruikers die zijn verleend of toegewezen toegang toohello toepassing is. Hallo toegang goedkeurder wordt Hallo eigenaar van deze groep. Als Hallo groepsnaam weergegeven niet bestaat, wordt deze automatisch gemaakt. Hallo groepsnaam kunt eventueel toohello naam van een bestaande groep instellen.

9. toosave hello configuratie, klikt u op **opslaan** Hallo onder welkomstscherm aan. Gebruikers kunnen nu toorequest access toothis-app van het toegangsvenster Hallo.

10. tootry eindgebruikerservaring hello, meld u aan bij Azure AD-Toegangsvenster voor van uw organisatie op https://myapps.microsoft.com, bij voorkeur met een ander account die niet een goedkeurder app. 

11. Onder Hallo **toepassingen** en klik op Hallo **meer toepassingen ophalen** tegel. Deze tegel wordt tal van alle Hallo-toepassingen die zijn ingeschakeld voor toegang tot selfservice toepassingen in de directory Hallo met Hallo mogelijkheid toosearch en filteren op categorie aan de linkerkant Hallo app weergegeven. 

12. Te klikken op een app serversysteemstatus Hallo-proces voor aanvragen. Als er geen goedkeuringsproces vereist is, wordt de toepassing hello onmiddellijk wordt toegevoegd onder Hallo **toepassingen** tabblad na een korte bevestiging. Goedkeuring is vereist, vervolgens ziet u een dialoogvenster waarmee dit wordt aangegeven als een e-mailbericht wordt verzonden toohello goedkeurders. U moet worden aangemeld bij Hallo toegang van het deelvenster als een niet-goedkeurder toosee dit proces voor aanvragen.

13. Hallo e directe ondergeschikten Hallo goedkeurder toosign in Azure AD-Toegangsvenster Hallo en Hallo aanvraag goedkeuren. Zodra het Hallo-aanvraag is goedgekeurd (en eventuele speciale processen die u definieert door Hallo goedkeurder zijn uitgevoerd), Hallo gebruiker Hallo-toepassing worden weergegeven onder ziet hun **toepassingen** tabblad waar ze kunnen zich in de App.

## <a name="delegated-application-access-management"></a>Gedelegeerde toegang voor toepassingsbeheer
Een toepassing toegang goedkeurder kan elke gebruiker in uw organisatie die het meest geschikte persoon tooapprove Hallo is of weigeren van toegang toohello toepassing in kwestie. Deze gebruiker kan verantwoordelijk voor het account inrichten, licenties, of andere bedrijfsproces uw organisatie vereist voordat u verleent toegang tooan app.

Bij het configureren van selfservice toepassing toegang die hierboven worden beschreven, een toegewezen toepassing goedkeurders Zie een extra **toepassingen beheren** tegel in hello Azure AD-Toegangsvenster, waarin ze welke toepassingen die ze Hallo beheerder van de toegang voor. Te klikken op een app, wordt een scherm met verschillende opties weergegeven.

![][2]

### <a name="approve-requests"></a>Goedkeuren van aanvragen
Hallo **aanvragen goedkeuren** tegel kunt goedkeurders toosee in behandeling zijnde goedkeuringen specifieke toothat app en omleidingen toohello goedkeuringen tabblad waar Hallo-aanvragen kan worden bevestigd of geweigerd. Automatische e-mailberichten ontvangt Hallo goedkeurder ook wanneer een aanvraag zodat deze welke toodo wordt gemaakt.

### <a name="add-users"></a>Gebruikers toevoegen
Hallo **gebruikers toevoegen** tegel kan goedkeurders toodirectly grant geselecteerde gebruikers toegang toohello toepassing. Wanneer u op deze tegel klikt, ziet Hallo goedkeurder dat een dialoogvenster kan ze tooview en zoek naar gebruikers in de directory. De resultaten van een gebruiker toevoegen in Hallo-toepassing wordt weergegeven in deze gebruiker Azure AD access panelen of Office 365. Als een handmatige gebruiker inrichtingsproces vereist is op Hallo app voordat de gebruiker Hallo kunnen toosign in, wordt Hallo goedkeurder moet dit proces uitvoeren alvorens toegang toe te wijzen.  

### <a name="manage-users"></a>Gebruikers beheren
Hallo **gebruikers beheren** tegel kan goedkeurders toodirectly bijwerken of verwijderen welke gebruikers toegang hebben toohello toepassing. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Wachtwoord SSO-referenties configureren (indien van toepassing)
Hallo **configureren** tegel wordt alleen weergegeven als Hallo toepassing is geconfigureerd door Hallo IT-beheerder toouse op basis van wachtwoorden eenmalige aanmelding en Hallo beheerder verleend Hallo goedkeurder Hallo mogelijkheid tooset wachtwoord SSO-referenties zoals eerder beschreven. Wanneer u selecteert, Hallo goedkeurder krijgt verschillende opties voor hoe Hallo referenties doorgegeven tooassigned gebruikers zijn:

![][3]

* **Gebruikers zich aanmelden met hun eigen wachtwoorden** : In deze modus Hallo toegewezen gebruikers weten wat de gebruikersnamen en wachtwoorden zijn voor de toepassing hello en vraag tooenter zijn ze bij de eerste aanmelding toohello bestemming. Hallo scenario overeenkomt met toohello wachtwoord SSO geval waar hello [gebruikers referenties beheren](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Gebruikers automatisch afgemeld bij het gebruik van afzonderlijke accounts die ik beheer** : In deze modus Hallo toegewezen gebruikers zijn niet vereist tooenter of hun referenties app-specifiek weten wanneer aanmeldt bij de toepassing hello. In plaats daarvan Hallo goedkeurder Hallo referenties instellen voor elke gebruiker na het toewijzen van toegang met behulp van Hallo **gebruiker toevoegen** tegel. Wanneer Hallo gebruiker op Hallo-toepassing in het deelvenster toegang of Office 365 klikt, worden ze automatisch afgemeld bij het gebruik van Hallo-referenties die zijn ingesteld door Hallo goedkeurder. Hallo scenario overeenkomt met toohello wachtwoord SSO geval waar hello [beheerders referenties beheren](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Gebruikers worden automatisch aangemeld met een enkele account die ik beheer** -een speciaal geval deze aanvraag is juiste toouse als alle toegewezen gebruikers moeten toobe met een enkele account voor gedeelde toegang verleend. meest voorkomende gebruiksvoorbeeld Hallo voor deze functie is met sociale mediatoepassingen, waarbij een organisatie heeft een enkele ' ' bedrijfsaccount en meerdere gebruikers toomake updates toothat-account nodig. Hallo scenario ook overeenkomt met toohello wachtwoord SSO geval waar hello [beheerders referenties beheren](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Nadat u deze optie selecteert, wordt Hallo goedkeurder echter wel na vragen aan gebruiker tooenter Hallo gebruikersnaam en wachtwoord voor Hallo één gedeelde account. Als voltooid, worden alle toegewezen gebruikers zijn ondertekend in dit account wordt gebruikt wanneer op de toepassing hello in hun Azure AD access panelen of Office 365 te klikken.

## <a name="additional-resources"></a>Aanvullende resources
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
