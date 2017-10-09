---
title: aaaGet gestart met licentieverlening in Azure Active Directory | Microsoft Docs
description: Hoe Azure Active Directory-licentieverlening werkt, hoe tooget gestart met best practices
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Licentie uzelf en uw gebruikers in Azure Active Directory

> [!div class="op_single_selector"]
> * [Azure portal-instructies](active-directory-licensing-get-started-azure-portal.md)
> * [Azure classic portal info ophalen](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) wordt een identiteit als een service (IDaaS)-oplossing en het platform van Microsoft. Azure AD wordt aangeboden in verschillende versies:

* Azure Active Directory vrij, dat meegeleverd met een Microsoft-service zoals Office 365, Dynamics, Microsoft Intune of Azure wordt. Azure AD genereert geen eventuele kosten verbruik in deze modus.

* Azure AD betaald edities, zoals:
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 en P2)
  - Azure AD Basic
  - Azure Multi-Factor Authentication

De meeste Azure AD betaald versies worden geleverd via een per gebruiker rechten net als veel van Microsoft online services, zoals in Office 365, Microsoft Intune en Azure AD. In dergelijke gevallen Hallo service aankoop wordt vertegenwoordigd door een of meer abonnementen en elk abonnement bevat enkele prepurchased licenties in uw tenant. Rechten per gebruiker worden bereikt door:

* Een licentie toewijzen. 
* Maken van een koppeling tussen gebruiker Hallo en Hallo product.
* Hallo-serviceonderdelen voor Hallo gebruiker inschakelen.
* Een Hallo verbruikt vooruitbetaalde licenties.

[Probeer Azure AD Premium nu.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Zie voor een breed overzicht van Azure AD-servicefuncties [wat is Azure AD?](active-directory-whatis.md). Zie voor meer informatie onze [Service Level Agreements pagina](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Azure-abonnementen betalen naar gebruik maken van een Azure-resources en vervolgens toe te wijzen tooyour betalingswijze. Er zijn geen licentieaantallen Hallo-abonnement gekoppeld. Als u een gebruiker machtiging toooperate op Azure-resources toegewezen toohello abonnement verleent, ze zijn gekoppeld aan Hallo-abonnement en beheren van abonnementresources.

## <a name="how-does-azure-active-directory-licensing-work"></a>Hoe Azure Active Directory werkt licentieverlening?

Azure AD op basis van een licentie services werk door een abonnement in uw Azure AD-service-tenant activeren. Nadat het Hallo-abonnement actief is, zijn Hallo servicefuncties beheerd door beheerders van Azure AD en gebruikt door gebruikers met een licentie.

### <a name="manage-subscription-information"></a>Beheer de abonnementsgegevens

Wanneer u koopt Enterprise Mobility + Security, Azure AD Premium of Azure AD Basic, uw tenant wordt bijgewerkt met de Hallo abonnement, met inbegrip van de geldigheidsperiode en vooruitbetaald licenties. Uw abonnementsgegevens, waaronder het aantal licenties toegewezen of beschikbaar Hallo is beschikbaar via hello Azure-portal: onder **Azure Active Directory**Open Hallo **licenties** tegel voor Hallo specifieke map. Hallo **licenties** blade is ook Hallo voor best plaats toomanage uw toewijzen van licenties.

Elk abonnement bestaat uit een of meer service-abonnementen, zoals Azure AD multi-factor Authentication, Intune, Exchange Online of SharePoint Online.  Azure AD-Licentiebeheer biedt *niet* plan-serviceniveaubeheer vereisen. Office 365 verschilt omdat deze afhankelijk van deze geavanceerde configuratie modus toomanage toegang tooincluded services is. Azure AD is afhankelijk van de configuratie van de in gebruik zijnde tooenable functies en afzonderlijke machtigingen beheren.

> [!IMPORTANT]
> Azure AD Premium, Azure AD Basic en Enterprise Mobility + Security abonnementen zijn beperkt tootheir ingericht directory/tenant. Abonnementen kunnen niet worden gesplitst tussen voltooiing mappen of gebruikte tooentitle gebruikers in andere directory's. Verplaatsen van een abonnement tussen mappen is mogelijk, maar vereist voor het verzenden van een ondersteuningsticket of annulering en repo voor rechtstreeks aankopen.
>
> Wanneer Azure AD of Enterprise Mobility + Security is aangeschaft via een Volume Licensing-abonnement en wanneer Hallo overeenkomst bevat andere Microsoft Online services (bijvoorbeeld Office 365), activering gebeurt automatisch. 

### <a name="assign-licenses"></a>Licenties toewijzen

Hoewel het verkrijgen van een abonnement moet alle u tooconfigure mogelijkheden betaald, moet u nog steeds licenties voor Azure AD betaalde functies toousers distribueren. Een licentie moet worden toegewezen aan elke gebruiker die toegang tooor die wordt beheerd via een Azure AD betaald functie moet hebben. De licentietoewijzing is geen toewijzing tussen een gebruiker en een gekochte service, zoals Azure AD Premium, Basic of Enterprise Mobility + Security.


Beheren welke gebruikers in uw directory moeten beschikken over een licentie kan worden uitgevoerd door: 

* Toewijzen van licenties toogroups in Hallo [Azure-portal](active-directory-licensing-whatis-azure-portal.md).
* Toewijzen van licenties rechtstreeks toousers in Hallo-portal, PowerShell of API's. 

Als u licenties tooa groep toewijst, worden alle groepsleden een licentie toegewezen. Als gebruikers worden toegevoegd of verwijderd uit groep hello, wordt de juiste licentie Hallo toegewezen of verwijderd. Groepstoewijzing kan gebruikmaken van elke groep management beschikbaar tooyou en consistent zijn met toewijzing op basis van een groep tooapplications is.

U kunt [op basis van een groep licentietoewijzing](active-directory-licensing-whatis-azure-portal.md) tooset van regels, zoals Hallo volgende:
* Alle gebruikers in uw directory ophalen automatisch een licentie
* Iedereen met de juiste functie Hallo een licentie opgehaald
* U kunt het Hallo besluit tooother managers in Hallo organisatie overdragen (met behulp van [selfservice groepen](active-directory-accessmanagement-self-service-group-management.md))

Voor een gedetailleerde bespreking van de licentie toewijzing toogroups, met inbegrip van geavanceerde scenario's en Office 365-licentieverlening scenario's, Zie [toewijzen licenties toousers door het lidmaatschap in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Aan de slag met Azure AD-licentieverlening

Aan de slag met Azure AD is eenvoudig. U kunt altijd maken met uw directory als onderdeel van zich aanmelden voor een [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

Hallo volgende best practices kunnen ervoor te zorgen dat uw tenant wordt uitgelijnd met andere Microsoft-services die u mogelijk worden verbruikt en uw doelstellingen voor Hallo-service:

- Als u al van een van de organisatie-services van Microsoft hello gebruikmaakt, hebt u al een Azure AD-tenant. Het is nuttig toouse Hallo die dezelfde voor andere services, tenant zodat de identiteitsbeheer core, met inbegrip van inrichting en hybride eenmalige aanmelding (SSO), kunnen worden gebruikt op Hallo-services. Met eenmalige aanmelding profiteren uw gebruikers van de uitgebreide mogelijkheden Hallo op Hallo-services. Dus als u toobuy een Azure AD betaald-service voor uw werknemers besluit, raden wij aan dat u dezelfde opnieuw tenant Hallo.

- Het wordt aangeraden om een nieuwe tenant in hello Azure-portal te gebruiken als u van plan bent te:
  - Gebruik Azure AD voor een andere set gebruikers (zoals partners of klanten).
  - Denk na over Azure AD-services in de isolatie van uw productieservice.
  - Instellen van een sandbox-omgeving voor uw services.

  Hallo nieuwe map gemaakt met uw account als een externe gebruiker met globale beheerdersmachtigingen. Wanneer u zich aanmeldt toohello Azure-portal aan dit account, kunt u deze tenant weergeven en toegang tot alle beheertaken.

> [!NOTE]
> Azure AD biedt ondersteuning voor 'gastgebruikers', die gebruikersaccounts in een Azure AD-tenant die zijn gemaakt via een Microsoft-account of een Azure AD-identiteit van een andere tenant. Hallo Office 365-beheerportal biedt momenteel geen ondersteuning voor deze gebruikers. Gastgebruikers met Microsoft-accounts zijn niet kunnen tooaccess Hallo Office 365-beheerportal, terwijl gastgebruikers van andere Azure AD-tenants, worden genegeerd. In de laatste geval Hallo Hallo alleen lokale gebruikersaccount, in hello Azure AD of Office 365-tenant waarin de gebruiker Hallo oorspronkelijk is gemaakt, is toegankelijk.

### <a name="select-one-or-more-license-trials"></a>Selecteer een of meer licentie-experimenten

U kunt een Azure AD Premium of Enterprise Mobility + Security proefabonnement onder activeren **Azure Active Directory** &gt; **snel starten**.

![Selecteer een proefversie licentie](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Evaluatieversie licenties zijn beschikbaar op Hallo **licenties** blade.

### <a name="assign-licenses-toousers-and-groups"></a>Toousers licenties en groepen toewijzen

Nadat het Hallo-abonnement actief is, moet u een licentie tooyourself toewijzen. Vernieuw Hallo browser tooensure dat u alle functies van de Hallo ziet. de volgende stap Hallo is tooassign licenties toohello gebruikers die toegang toopaid Azure AD-functies nodig hebben. Zoals beschreven in [licenties toewijzen](#assign-licenses), een eenvoudige manier tooassign licenties is tooidentify Hallo groep Hallo die doelgroep gewenst en Hallo licentie tooit toewijzen. Op deze manier kunnen gebruikers die zijn toegevoegd of verwijderd uit groep Hallo gedurende de levenscyclus toegewezen of verwijderd uit het Hallo-licentie, respectievelijk.

> [!NOTE]
> Sommige Microsoft-services zijn niet beschikbaar op alle locaties. Voordat u een licentie kan worden toegewezen als de gebruiker tooa, Hallo beheerder Hallo moet opgeven **gebruikslocatie** eigenschap voor Hallo-gebruiker. U kunt instellen dat deze eigenschap onder **gebruiker** &gt; **profiel** &gt; **instellingen** in hello Azure-portal. Wanneer u de licentietoewijzing van de groep, neemt een gebruiker waarvan gebruikslocatie is niet opgegeven locatie op Hallo van Hallo directory.

een licentie tooassign onder **Azure Active Directory** &gt; **licenties** &gt; **alle producten**, selecteer een of meerdere producten, en selecteer vervolgens **Toewijzen** op Hallo opdrachtbalk klikken.

![Selecteer een tooassign licentie](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

U kunt Hallo **gebruikers en groepen** blade toochoose meerdere gebruikers of groepen of toodisable service-in Hallo product plannen. Hallo zoekvak op de bovenste toosearch gebruiken voor de namen van gebruikers en groepen.

![Selecteer een gebruiker of groep voor de licentietoewijzing](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Wanneer u een licentiegroep tooa toewijst, kan het even duren voordat alle gebruikers Hallo-licentie, al naar gelang het aantal gebruikers in de groep Hallo Hallo overnemen. U kunt controleren Hallo verwerkingsstatus op Hallo **groep** blade onder Hallo **licenties** tegel.

![Licentie-toewijzingsstatus](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Toewijzingsfouten kunnen optreden tijdens de toewijzing van Azure AD-licentie, maar relatief zeldzame zijn bij het beheren van Azure AD en Enterprise Mobility + Security-producten. Mogelijke toewijzingsfouten zijn beperkt tot:
- Toewijzing conflict: wanneer een gebruiker een licentie die niet compatibel is met de huidige licentie Hallo was toegewezen. In dit geval moet Hallo nieuwe licentie toewijzen Hallo huidige worden verwijderd.
- Beschikbare licenties overschreden: wanneer het aantal gebruikers in de toegewezen groepen Hallo Hallo beschikbare licenties overschrijdt, duidt op een tooassign is mislukt vanwege toomissing licenties status van de toewijzing van een gebruiker.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B-samenwerking licentieverlening

B2B-samenwerking kunt u tooinvite gastgebruikers in uw Azure AD-tenant tooprovide toegang tooAzure AD-services en alle Azure-resources u beschikbaar maken.  

Er zijn geen kosten voor B2B-gebruikers en eraan tooan toepassing in Azure AD toe te wijzen. Up too10 apps per Gast zijn en gebruiker 3 Basisrapporten ook gratis voor B2B-samenwerking gebruikers. Als uw gastgebruiker juiste licenties in Azure AD-tenant van Hallo partner toegewezen heeft, wordt ze ook in jouw e-mailadres worden licentie.

Dit is niet vereist, maar als u tooprovide access toopaid Azure AD-functies wilt, die gebruikers van de Gast B2B moeten een licentie hebben met de desbetreffende Azure AD-licenties. Een uitnodiging tenant met een betaalde licentie met Azure AD B2B-samenwerking gebruikersrechten kunt toewijzen tooan extra vijf gastgebruikers uitgenodigd toohello tenant. Zie voor scenario's en informatie [B2B-samenwerking richtlijnen licentieverlening](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Weergave toegewezen licenties

Een samenvatting weergegeven van de licenties toegewezen en beschikbaar wordt weergegeven onder **Azure Active Directory** &gt; **licenties** &gt; **alle producten**.

![Een samenvatting weergeven van licenties](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Een gedetailleerde lijst met toegewezen gebruikers en groepen is beschikbaar bij het selecteren van een specifiek product. Hallo **gebruikers met een licentie** lijst bevat alle gebruikers die momenteel die een licentie en Hiermee wordt aangegeven of Hallo-licentie is toegewezen rechtstreeks toohello gebruiker of als deze is overgenomen van een groep.

![Details van de licentie weergeven](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Op deze manier Hallo **groepen in licentie gegeven** lijst ziet u alle groepen toowhich licenties zijn toegewezen. Selecteer een gebruiker of groep tooopen hello **licenties** blade waarin alle licenties toegewezen toothat-object.

### <a name="remove-a-license"></a>Een licentie verwijderen

een licentie tooremove gaat toohello gebruiker of groep en open Hallo **licenties** tegel. Selecteer Hallo licentie, en klik op **verwijderen**.

![Een licentie verwijderen](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Licenties die zijn overgenomen door de gebruiker Hallo uit een groep kunnen niet rechtstreeks worden verwijderd. In plaats daarvan Hallo gebruiker verwijderen uit Hallo-groep waarvan ze Hallo licentie worden overgenomen.

### <a name="extend-trials"></a>Proefversies uitbreiden

Evaluatieversie uitbreidingen voor klanten zijn beschikbaar als self-service aanmelding via Hallo Office 365-portal. Een beheerder van de klant kunt gaan toohello Office-portal (toegang is afhankelijk van de machtigingen voor de Office-portal Hallo) en selecteer hello Azure AD Premium-proefversie. Te klikken op Hallo **uitbreiden proefversie** koppeling Hallo uitbreidingsproces wordt gestart. Er is een creditcard vereist, maar het is niet in rekening gebracht.

![Uitbreiden van een proefversie in hello Azure-portal](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Volgende stappen

toolearn informatie over geavanceerde scenario's voor Licentiebeheer via groepen, lees Hallo artikel [toewijzen licenties tooa groep](active-directory-licensing-group-assignment-azure-portal.md).

Hier vindt u informatie over het tooconfigure en andere Azure AD betaalde functies gebruikt:

* [Selfservice voor wachtwoordherstel](active-directory-manage-passwords.md)
* [Self-service groepsbeheer](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect health](active-directory-aadconnect-health.md)
* [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Directe aankoop van Azure AD Premium-licenties](http://aka.ms/buyaadp)
