---
title: aaaLicense gebruikers in Azure Active Directory | Microsoft Docs
description: Meer informatie over hoe toolicense uzelf en uw gebruikers in Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Snelstartgids: Licentie gebruikers in Azure Active Directory
Azure AD op basis van een licentie services werk door een abonnement voor Azure Active Directory (Azure AD) in uw Azure-tenant activeren. Nadat het Hallo-abonnement actief is, zijn servicefuncties beheerd door beheerders van Azure AD en gebruikt door gebruikers met een licentie. Wanneer u koopt Enterprise Mobility + Security, Azure AD Premium of Azure AD Basic, uw tenant wordt bijgewerkt met de Hallo abonnement, met inbegrip van de geldigheidsperiode en vooruitbetaald licenties. Uw abonnementsgegevens, waaronder het aantal licenties toegewezen of beschikbaar Hallo is beschikbaar via hello Azure portal onder **Azure Active Directory** door Hallo openen **licenties** tegel. Hallo **licenties** blade is ook Hallo voor best plaats toomanage uw toewijzen van licenties.

Hoewel het verkrijgen van een abonnement moet alle u tooconfigure mogelijkheden betaald, moet u nog steeds gebruikerslicenties toewijzen voor betaalde Azure AD betaalde functies. Elke gebruiker die toegang moeten hebben tot of die wordt beheerd via een Azure AD betaald functie moet een licentie worden toegewezen. De licentietoewijzing is geen toewijzing tussen een gebruiker en een gekochte service, zoals Azure AD Premium, Basic of Enterprise Mobility + Security.

U kunt [op basis van een groep licentietoewijzing](active-directory-licensing-whatis-azure-portal.md) tooset van regels, zoals Hallo volgende:
* Alle gebruikers in uw directory ophalen automatisch een licentie
* Iedereen met de juiste functie Hallo een licentie opgehaald
* U kunt het Hallo besluit tooother managers in Hallo organisatie overdragen (met behulp van [selfservice groepen](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Voor een gedetailleerde bespreking van de licentie toewijzing toogroups, met inbegrip van geavanceerde scenario's en Office 365-licentieverlening scenario's, Zie [toewijzen licenties toousers door het lidmaatschap in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Toousers licenties en groepen toewijzen
Met behulp van een actief abonnement, moet u eerst een tooyourself licentie toewijzen en vernieuw uw browser tooensure die u alle functies Hallo verwacht met uw abonnement ziet. de volgende stap Hallo is tooassign licenties toohello gebruikers die toegang toopaid Azure AD-functies nodig hebben. Een eenvoudige manier tooassign licenties tooassign licenties toogroups van gebruikers in plaats van tooindividuals is. Als u licenties tooa groep toewijst, worden alle groepsleden een licentie toegewezen. Als gebruikers worden toegevoegd of verwijderd uit groep hello, wordt automatisch de juiste licentie Hallo toegewezen of verwijderd. 

> [!NOTE]
> Sommige Microsoft-services zijn niet beschikbaar op alle locaties. Voordat u een licentie kan worden toegewezen als de gebruiker tooa, Hallo beheerder Hallo moet opgeven **gebruikslocatie** eigenschap voor Hallo-gebruiker. U kunt instellen dat deze eigenschap onder **gebruiker** &gt; **profiel** &gt; **instellingen** in hello Azure-portal. Wanneer u de licentietoewijzing van de groep, neemt een gebruiker waarvan gebruikslocatie is niet opgegeven locatie op Hallo van Hallo directory.

een licentie tooassign onder **Azure Active Directory** &gt; **licenties** &gt; **alle producten**, selecteer een of meerdere producten, en selecteer vervolgens **Toewijzen** op Hallo opdrachtbalk klikken.

![Selecteer een tooassign licentie](media/license-users-groups/select-license-to-assign.png)

U kunt Hallo **gebruikers en groepen** blade toochoose meerdere gebruikers of groepen of toodisable service-in Hallo product plannen. Hallo zoekvak op de bovenste toosearch gebruiken voor de namen van gebruikers en groepen.

![Selecteer een gebruiker of groep voor de licentietoewijzing](media/license-users-groups/select-user-for-license-assignment.png)

Als u licenties tooa groep toewijst, kan het even duren voordat alle gebruikers Hallo-licentie, afhankelijk van Hallo grootte van de groep Hallo overnemen. U kunt controleren Hallo verwerkingsstatus op Hallo **groep** blade onder Hallo **licenties** tegel.

![Licentie-toewijzingsstatus](media/license-users-groups/license-assignment-status.png)

Toewijzingsfouten kunnen optreden tijdens de toewijzing van Azure AD-licentie, maar relatief zeldzame zijn bij het beheren van Azure AD en Enterprise Mobility + Security-producten. Mogelijke toewijzingsfouten zijn beperkt tot:
- Toewijzing conflict: wanneer een gebruiker een licentie die niet compatibel is met de huidige licentie Hallo was toegewezen. In dit geval moet Hallo nieuwe licentie toewijzen Hallo huidige worden verwijderd.
- Beschikbare licenties overschreden: wanneer het aantal gebruikers in de toegewezen groepen Hallo Hallo beschikbare licenties overschrijdt, duidt op een tooassign is mislukt vanwege toomissing licenties status van de toewijzing van een gebruiker.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure AD B2B-samenwerking licentieverlening

B2B-samenwerking kunt u tooinvite gastgebruikers in uw Azure AD-tenant tooprovide toegang tooAzure AD-services en alle Azure-resources u beschikbaar maken.  

Er zijn geen kosten voor B2B-gebruikers en eraan tooan toepassing in Azure AD toe te wijzen. Up too10 apps per Gast zijn en gebruiker 3 Basisrapporten ook gratis voor B2B-samenwerking gebruikers. Als uw gastgebruiker juiste licenties in Azure AD-tenant van Hallo partner toegewezen heeft, wordt ze ook in jouw e-mailadres worden licentie.

Dit is niet vereist, maar als u tooprovide access toopaid Azure AD-functies wilt, die gebruikers van de Gast B2B moeten een licentie hebben met de desbetreffende Azure AD-licenties. Een uitnodiging tenant met een betaalde licentie met Azure AD B2B-samenwerking gebruikersrechten kunt toewijzen tooan extra vijf gastgebruikers uitgenodigd toohello tenant. Zie voor scenario's en informatie [B2B-samenwerking richtlijnen licentieverlening](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Weergave toegewezen licenties

Een samenvatting weergegeven van de licenties toegewezen en beschikbaar wordt weergegeven onder **Azure Active Directory** &gt; **licenties** &gt; **alle producten**.

![Een samenvatting weergeven van licenties](media/license-users-groups/view-license-summary.png)

Een gedetailleerde lijst met toegewezen gebruikers en groepen is beschikbaar bij het selecteren van een specifiek product. Hallo **gebruikers met een licentie** lijst bevat alle gebruikers die momenteel die een licentie en Hiermee wordt aangegeven of Hallo-licentie is toegewezen rechtstreeks toohello gebruiker of als deze is overgenomen van een groep.

![Details van de licentie weergeven](media/license-users-groups/view-license-detail.png)

Op deze manier Hallo **groepen in licentie gegeven** lijst ziet u alle groepen toowhich licenties zijn toegewezen. Selecteer een gebruiker of groep tooopen hello **licenties** blade waarin alle licenties toegewezen toothat-object.

## <a name="remove-a-license"></a>Een licentie verwijderen

een licentie tooremove gaat toohello gebruiker of groep en open Hallo **licenties** tegel. Selecteer Hallo licentie, en klik op **verwijderen**.

![Een licentie verwijderen](media/license-users-groups/remove-license.png)

Licenties die zijn overgenomen door de gebruiker Hallo uit een groep kunnen niet rechtstreeks worden verwijderd. In plaats daarvan Hallo gebruiker verwijderen uit Hallo-groep waarvan ze Hallo licentie worden overgenomen.


## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u geleerd hoe tooassign licenties toousers en groepen in Azure AD-directory. 

U kunt Hallo na het toewijzen van koppeling tooconfigure abonnement licenties in Azure AD uit hello Azure-portal gebruiken.

> [!div class="nextstepaction"]
> [Azure AD-licenties toewijzen](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 