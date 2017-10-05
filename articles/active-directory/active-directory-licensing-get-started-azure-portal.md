---
title: Aan de slag met licentieverlening in Azure Active Directory | Microsoft Docs
description: Hoe Azure Active Directory-licentieverlening werkt, hoe u aan de slag met aanbevolen procedures
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
ms.openlocfilehash: 6fa7cbbc452861870136482aa320d268e78fe3d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
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

De meeste Azure AD betaald versies worden geleverd via een per gebruiker rechten net als veel van Microsoft online services, zoals in Office 365, Microsoft Intune en Azure AD. In dergelijke gevallen de aankoop van de service wordt vertegenwoordigd door een of meer abonnementen en elk abonnement bevat enkele prepurchased licenties in uw tenant. Rechten per gebruiker worden bereikt door:

* Een licentie toewijzen. 
* Maken van een koppeling tussen de gebruiker en het product.
* Inschakelen van de onderdelen van de service voor de gebruiker.
* Een van de vooruitbetaalde licenties verbruikt.

[Probeer Azure AD Premium nu.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Zie voor een breed overzicht van Azure AD-servicefuncties [wat is Azure AD?](active-directory-whatis.md). Zie voor meer informatie onze [Service Level Agreements pagina](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Azure-abonnementen betalen naar gebruik maken van een Azure-resources en vervolgens toe te wijzen aan uw betalingswijze. Er zijn geen licentieaantallen gekoppeld aan het abonnement. Als u een gebruiker machtigingen verleent voor het Azure-resources toegewezen aan het abonnement niet bewerken, ze zijn gekoppeld aan het abonnement en beheren van abonnementresources.

## <a name="how-does-azure-active-directory-licensing-work"></a>Hoe Azure Active Directory werkt licentieverlening?

Azure AD op basis van een licentie services werk door een abonnement in uw Azure AD-service-tenant activeren. Nadat het abonnement actief is, worden de servicemogelijkheden worden beheerd door beheerders van Azure AD en gebruikt door gebruikers met een licentie.

### <a name="manage-subscription-information"></a>Beheer de abonnementsgegevens

Bij de aankoop van Enterprise Mobility + Security, Azure AD Premium of Azure AD Basic, wordt uw tenant wordt bijgewerkt met het abonnement, met inbegrip van de geldigheidsperiode en vooruitbetaalde licenties. Uw abonnementsgegevens, waaronder het aantal licenties toegewezen of beschikbaar is, is beschikbaar via de Azure-portal: onder **Azure Active Directory**, open de **licenties** tegel voor de specifieke map. De **licenties** blade is ook de beste plaats voor het beheren van uw licentietoewijzingen.

Elk abonnement bestaat uit een of meer service-abonnementen, zoals Azure AD multi-factor Authentication, Intune, Exchange Online of SharePoint Online.  Azure AD-Licentiebeheer biedt *niet* plan-serviceniveaubeheer vereisen. Office 365 verschilt omdat deze afhankelijk van deze modus geavanceerde configuratie is voor het beheren van toegang tot services opgenomen. Azure AD afhankelijk is in gebruik zijnde configuratie functies inschakelen en beheren van afzonderlijke machtigingen.

> [!IMPORTANT]
> Azure AD Premium, Azure AD Basic en Enterprise Mobility + Security abonnementen zijn beperkt tot hun ingerichte directory/tenant. Abonnementen kunnen niet worden gesplitst tussen voltooiing van mappen of gebruikt voor het machtigen van gebruikers in andere directory's. Verplaatsen van een abonnement tussen mappen is mogelijk, maar vereist voor het verzenden van een ondersteuningsticket of annulering en repo voor rechtstreeks aankopen.
>
> Wanneer Azure AD of Enterprise Mobility + Security is aangeschaft via een Volume Licensing-abonnement en wanneer de overeenkomst bevat andere Microsoft Online services (bijvoorbeeld Office 365), Activering automatisch uitgevoerd. 

### <a name="assign-licenses"></a>Licenties toewijzen

Hoewel het verkrijgen van een abonnement hoeft u alleen betaald mogelijkheden configureren, moet u nog steeds licenties voor Azure AD betaalde functies aan gebruikers distribueren. Elke gebruiker die toegang moeten hebben tot of die wordt beheerd via een Azure AD betaald functie moet een licentie worden toegewezen. De licentietoewijzing is geen toewijzing tussen een gebruiker en een gekochte service, zoals Azure AD Premium, Basic of Enterprise Mobility + Security.


Beheren welke gebruikers in uw directory moeten beschikken over een licentie kan worden uitgevoerd door: 

* Licenties toewijzen aan groepen in de [Azure-portal](active-directory-licensing-whatis-azure-portal.md).
* Licenties toewijzen rechtstreeks aan gebruikers via de portal, PowerShell of API's. 

Als u licenties aan een groep toewijst, worden alle groepsleden een licentie toegewezen. Als gebruikers worden toegevoegd of verwijderd uit de groep, wordt de juiste licentie toegewezen of verwijderd. Groepstoewijzing kan gebruikmaken van een groep management voor u beschikbaar en is consistent met toewijzing op basis van een groep van toepassingen.

U kunt [op basis van een groep licentietoewijzing](active-directory-licensing-whatis-azure-portal.md) voor het instellen van regels, zoals het volgende:
* Alle gebruikers in uw directory ophalen automatisch een licentie
* Iedereen met de juiste functie een licentie opgehaald
* U kunt het besluit om andere beheerders in de organisatie te delegeren (met behulp van [selfservice groepen](active-directory-accessmanagement-self-service-group-management.md))

Voor een gedetailleerde bespreking van de licentietoewijzing voor groepen, met inbegrip van geavanceerde scenario's en Office 365-licentieverlening scenario's, Zie [licenties toewijzen aan gebruikers door het lidmaatschap in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Aan de slag met Azure AD-licentieverlening

Aan de slag met Azure AD is eenvoudig. U kunt altijd maken met uw directory als onderdeel van zich aanmelden voor een [gratis proefversie van Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

De volgende aanbevolen procedures kunt ervoor te zorgen dat uw tenant wordt uitgelijnd met andere Microsoft-services die u mogelijk worden verbruikt en uw doelstellingen voor de service:

- Als u al van een van de organisatie-services van Microsoft gebruikmaakt, hebt u al een Azure AD-tenant. Dit is handig voor het gebruik van dezelfde tenant voor andere services, zodat core identity management, met inbegrip van inrichting en hybride eenmalige aanmelding (SSO) door de services kunnen worden gebruikt. Met eenmalige aanmelding profiteren uw gebruikers van de uitgebreide mogelijkheden in services. Dus als u besluit een Azure AD-service voor uw werknemers betaald aanschaffen, raden wij aan dat u dezelfde tenant opnieuw gebruiken.

- Het wordt aangeraden om een nieuwe tenant in de Azure portal te gebruiken als u van plan bent te:
  - Gebruik Azure AD voor een andere set gebruikers (zoals partners of klanten).
  - Denk na over Azure AD-services in de isolatie van uw productieservice.
  - Instellen van een sandbox-omgeving voor uw services.

  De nieuwe map gemaakt met uw account als een externe gebruiker met globale beheerdersmachtigingen. Wanneer u zich bij de Azure portal met dit account aanmelden, kunt u deze tenant weergeven en toegang tot alle beheertaken.

> [!NOTE]
> Azure AD biedt ondersteuning voor 'gastgebruikers', die gebruikersaccounts in een Azure AD-tenant die zijn gemaakt via een Microsoft-account of een Azure AD-identiteit van een andere tenant. De Office 365-beheerportal biedt momenteel geen ondersteuning voor deze gebruikers. Gastgebruikers met Microsoft-accounts zich niet tot de Office 365-beheerportal, terwijl gastgebruikers van andere Azure AD-tenants, worden genegeerd. In dat geval wordt alleen het lokale gebruikersaccount, in de Azure AD of Office 365-tenant waarin de gebruiker oorspronkelijk is gemaakt, is toegankelijk.

### <a name="select-one-or-more-license-trials"></a>Selecteer een of meer licentie-experimenten

U kunt een Azure AD Premium of Enterprise Mobility + Security proefabonnement onder activeren **Azure Active Directory** &gt; **snel starten**.

![Selecteer een proefversie licentie](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Evaluatieversie licenties zijn beschikbaar op de **licenties** blade.

### <a name="assign-licenses-to-users-and-groups"></a>Licenties toewijzen aan gebruikers en groepen

Nadat het abonnement actief is, moet u een licentie toewijzen aan uzelf. Vernieuw de browser om ervoor te zorgen dat u alle functies ziet. De volgende stap is om licenties te wijzen aan de gebruikers die toegang nodig tot betaalde Azure AD-functies. Zoals beschreven in [licenties toewijzen](#assign-licenses), een eenvoudige manier zijn om licenties toe te wijzen, is de groep die de gewenste doelgroep identificeren en de licentie toewijzen aan deze. Op deze manier kunnen gebruikers die zijn toegevoegd of verwijderd uit de groep gedurende de levenscyclus toegewezen of verwijderd uit de licentie, respectievelijk.

> [!NOTE]
> Sommige Microsoft-services zijn niet beschikbaar op alle locaties. Voordat u een licentie kan worden toegewezen aan een gebruiker, de beheerder moet opgeven de **gebruikslocatie** eigenschap voor de gebruiker. U kunt instellen dat deze eigenschap onder **gebruiker** &gt; **profiel** &gt; **instellingen** in de Azure portal. Wanneer u de licentietoewijzing van de groep, krijgt een gebruiker waarvan gebruikslocatie is niet opgegeven dan de locatie van de map.

Wijs een licentie onder **Azure Active Directory** &gt; **licenties** &gt; **alle producten**, selecteer een of meerdere producten, en selecteer vervolgens **toewijzen** op de opdrachtbalk.

![Selecteer een licentie toewijzen](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

U kunt de **gebruikers en groepen** blade voor meerdere gebruikers of groepen kiezen of uitschakelen van de service-abonnementen in het product. Gebruik het zoekvak op de voorgrond om te zoeken naar gebruikers- en groepsnamen.

![Selecteer een gebruiker of groep voor de licentietoewijzing](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Wanneer u een licentie aan een groep toewijst, kan het even duren voordat alle gebruikers de licentie, afhankelijk van het aantal gebruikers in de groep overnemen. U kunt de verwerkingsstatus controleren op de **groep** blade onder de **licenties** tegel.

![Licentie-toewijzingsstatus](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Toewijzingsfouten kunnen optreden tijdens de toewijzing van Azure AD-licentie, maar relatief zeldzame zijn bij het beheren van Azure AD en Enterprise Mobility + Security-producten. Mogelijke toewijzingsfouten zijn beperkt tot:
- Toewijzing conflict: wanneer een gebruiker een licentie die niet compatibel is met de huidige licentie was toegewezen. In dit geval moet de nieuwe licentie toewijzen de huidige verwijdert.
- Beschikbare licenties overschreden: wanneer het aantal gebruikers in de toegewezen groepen de beschikbare licenties overschrijdt, status van de toewijzing van een gebruiker duidt op een mislukt als gevolg van ontbrekende licenties toewijzen.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B-samenwerking licentieverlening

B2B-samenwerking kunt u gastgebruikers uitnodigen in uw Azure AD-tenant voor toegang tot Azure AD-services en alle Azure-resources u beschikbaar maken.  

Er zijn geen kosten voor B2B-gebruikers en eraan toe te wijzen aan een toepassing in Azure AD. Maximaal 10 apps per gastgebruiker en 3 Basisrapporten zijn ook gratis voor B2B-samenwerking gebruikers. Als uw gastgebruiker juiste licenties in Azure AD-tenant van de partner toegewezen heeft, wordt ze ook in jouw e-mailadres worden licentie.

Dit is niet vereist, maar als u toegang bieden tot betaalde Azure AD-functies wilt, die gebruikers van de Gast B2B moeten een licentie hebben met de desbetreffende Azure AD-licenties. Een uitnodiging tenant met een Azure AD betaalde licentie kunt B2B-samenwerking gebruikersrechten toewijzen aan een extra vijf gastgebruikers uitgenodigd voor de tenant. Zie voor scenario's en informatie [B2B-samenwerking richtlijnen licentieverlening](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Weergave toegewezen licenties

Een samenvatting weergegeven van de licenties toegewezen en beschikbaar wordt weergegeven onder **Azure Active Directory** &gt; **licenties** &gt; **alle producten**.

![Een samenvatting weergeven van licenties](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Een gedetailleerde lijst met toegewezen gebruikers en groepen is beschikbaar bij het selecteren van een specifiek product. De **gebruikers met een licentie** lijst bevat alle gebruikers die momenteel die een licentie en of de licentie is toegewezen aan de gebruiker rechtstreeks of als deze is overgenomen van een groep.

![Details van de licentie weergeven](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Op dezelfde manier de **groepen in licentie gegeven** lijst ziet u alle groepen waarop licenties zijn toegewezen. Selecteer een gebruiker of groep openen de **licenties** blade waarin alle licenties die zijn toegewezen aan dit object.

### <a name="remove-a-license"></a>Een licentie verwijderen

Als u wilt verwijderen van een licentie, gaat u naar de gebruiker of groep en open de **licenties** tegel. Selecteer de licentie, en klik op **verwijderen**.

![Een licentie verwijderen](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Licenties die zijn overgenomen door de gebruiker uit een groep kunnen niet rechtstreeks worden verwijderd. De gebruiker in plaats daarvan verwijderd uit de groep waarvan ze de licentie worden overgenomen.

### <a name="extend-trials"></a>Proefversies uitbreiden

Evaluatieversie uitbreidingen voor klanten zijn beschikbaar als self-service aanmelding via de Office 365-portal. Een beheerder van de klant kunt gaat u naar de Office-portal (toegang is afhankelijk van de machtigingen voor de Office-portal) en selecteer de proefversie van Azure AD Premium. Te klikken op de **uitbreiden proefversie** koppeling het extensieproces wordt gestart. Er is een creditcard vereist, maar het is niet in rekening gebracht.

![Uitbreiden van een proefversie in de Azure portal](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Volgende stappen

Lees het artikel voor meer informatie over geavanceerde scenario's voor Licentiebeheer via groepen, [licenties toewijzen aan een groep](active-directory-licensing-group-assignment-azure-portal.md).

Hier vindt u informatie over het configureren en gebruiken van andere Azure AD betaalde functies:

* [Selfservice voor wachtwoordherstel](active-directory-manage-passwords.md)
* [Self-service groepsbeheer](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect health](active-directory-aadconnect-health.md)
* [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Directe aankoop van Azure AD Premium-licenties](http://aka.ms/buyaadp)
