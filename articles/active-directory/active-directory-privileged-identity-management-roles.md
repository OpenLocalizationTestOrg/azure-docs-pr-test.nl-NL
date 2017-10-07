---
title: aaaRoles in Azure AD Privileged Identity Management | Microsoft Docs
description: Meer informatie over welke functies worden gebruikt voor bevoegde identiteiten met hello Azure Privileged Identity Management-extensie.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Andere administratieve rol in Azure Active Directory PIM
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

U kunt gebruikers in uw organisatie toodifferent administratieve rollen toewijzen in Azure AD. Deze roltoewijzingen bepalen welke taken, zoals gebruikers toevoegen of verwijderen of wijzigen van de service-instellingen zijn Hallo gebruikers kunnen tooperform op Azure AD, Office 365 en andere Microsoft Online Services en verbonden toepassingen.  

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.

Een globale beheerder kunt bijwerken die gebruikers **permanent** tooroles in Azure AD, met behulp van PowerShell-cmdlets, zoals toegewezen `Add-MsolRoleMember` en `Remove-MsolRoleMember`, of via de klassieke portal Hallo zoals beschreven in [ beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md).

Azure AD Privileged Identity Management (PIM) beheert de beleidsregels voor bevoorrechte toegang voor gebruikers in Azure AD. PIM toegewezen gebruikers tooone of meer rollen in Azure AD en kunt u iemand toewijzen toobe permanent in Hallo rol of komen in aanmerking voor Hallo-rol. Wanneer een gebruiker permanent tooa-rol is toegewezen of een in aanmerking komende roltoewijzing activeert vervolgens zij Azure Active Directory, Office 365 en andere toepassingen met Hallo machtigingen tootheir rollen toegewezen beheren kunnen.

Er is geen verschil in Hallo toegang gegeven toosomeone met een permanente ten opzichte van een in aanmerking komende roltoewijzing. Hallo enige verschil is dat sommige gebruikers geen tijd nodig die toegang alle Hallo hebt. Ze zijn gemaakt in aanmerking komen voor Hallo-rol en kunnen inschakelen en uitschakelen wanneer ze moeten.

## <a name="roles-managed-in-pim"></a>Rollen die worden beheerd in PIM
Privileged Identity Management kunt u gebruikers toocommon beheerdersrollen, met inbegrip van toewijzen:

* **Globale beheerder** (ook wel bekend als bedrijfsbeheerder) heeft toegang tot tooall beheerfuncties. U kunt meer dan één globale beheerder in uw organisatie hebben. Hallo persoon die zich registreert toopurchase Office 365 automatisch, wordt een globale beheerder.
* **Beheerder met bevoorrechte rol** beheert de Azure AD PIM en toewijzingen van rollen voor andere gebruikers.  
* **Financieel medewerker** doet aankopen, beheert abonnementen, beheert ondersteuningstickets en bewaakt de servicestatus.
* **Wachtwoordbeheerder** wachtwoorden opnieuw instellen, beheert serviceaanvragen en bewaakt de servicestatus. Wachtwoord beheerders zijn beperkt tooresetting wachtwoorden voor gebruikers.
* **Servicebeheerder** beheert serviceaanvragen en bewaakt de servicestatus.
  
  > [!NOTE]
  > Als u van Office 365 gebruikmaakt, vervolgens alvorens toe te wijzen Hallo beheerder rol tooa servicegebruiker, eerst toewijzen Hallo gebruiker beheerdersmachtigingen tooa service, zoals Exchange Online.
  > 
  > 
* **Gebruikerstoegangbeheerder** wachtwoorden opnieuw instellen, bewaakt de servicestatus en beheert gebruikersaccounts, gebruikersgroepen en serviceaanvragen. Hallo-Gebruikerbeheerder management kan niet verwijderen van een globale beheerder, andere beheerdersrollen maken of opnieuw instellen van wachtwoorden voor financieel medewerkers, algemeen beheerders en servicebeheerders.
* **Exchange-beheerder** heeft beheerderstoegang tooExchange Online via Hallo Exchange-beheercentrum (tijdens elke Exportactie) en bijna alle taken kunt uitvoeren in Exchange Online.
* **SharePoint-beheerder** Online tooSharePoint beheerderstoegang heeft tot en met SharePoint Online beheercentrum Hallo en bijna alle taken kunt uitvoeren in SharePoint Online.
* **Skype voor bedrijven beheerder** tooSkype beheerderstoegang toewijzen voor bedrijven heeft via Hallo Skype voor bedrijven-beheercentrum en bijna alle taken kunt uitvoeren in Skype voor bedrijven Online.

Deze artikelen voor meer informatie lezen over [beheerdersrollen toewijzen in Azure AD](active-directory-assign-admin-roles.md) en [beheerdersrollen toewijzen in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


Vanuit PIM, kunt u [toewijzen van de gebruiker van deze rollen tooa](active-directory-privileged-identity-management-how-to-add-role-to-user.md) zodat hello gebruiker kan [Hallo rol wanneer deze nodig activeren](active-directory-privileged-identity-management-how-to-activate-role.md).

Als u een andere gebruiker toegang toomanage in PIM zelf, Hallo rollen waarvoor u PIM Hallo gebruiker toohave worden beschreven verder in toogive wilt [hoe toogive toegang krijgen tot tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Functies die niet worden beheerd in PIM
Rollen in Exchange Online of SharePoint Online, behalve die hierboven vermeld, worden niet weergegeven in Azure AD en dus zijn niet zichtbaar in PIM. Zie voor meer informatie over het wijzigen van fijnmazig roltoewijzingen in deze Office 365-services [machtigingen in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Azure-abonnementen en resourcegroepen worden ook niet weergegeven in Azure AD. toomanage Azure-abonnementen, Zie [hoe tooadd of wijzig Azure-beheerdersrollen](../billing/billing-add-change-azure-subscription-administrator.md) en voor meer informatie over Azure RBAC Zie [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Gebruikersrollen en aanmelden
Voor sommige Microsoft-services en toepassingen voor het toewijzen van een gebruikersrol tooa mogelijk niet voldoende tooenable die toobe gebruiker een beheerder zijn.

Toegang toohello klassieke Azure-portal vereist Hallo gebruiker zijn een servicebeheerder of medebeheerder van een Azure-abonnement, zelfs als Hallo niet de moet toomanage, Azure-abonnementen Hallo.  Bijvoorbeeld: toomanage configuratie-instellingen voor Azure AD in Hallo klassieke portal een gebruiker moet zowel een globale beheerder in Azure AD en de medebeheerder voor een abonnement op een Azure-abonnement.  hoe tooadd gebruikers tooAzure abonnementen zien toolearn [hoe tooadd of wijzig Azure-beheerdersrollen](../billing/billing-add-change-azure-subscription-administrator.md).

Toegang tooMicrosoft Online Services mogelijk Hallo gebruiker ook een licentie worden toegewezen voordat ze kunnen Hallo serviceportal openen of beheertaken uit te voeren.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Een licentie tooa gebruiker toewijzen in Azure AD
1. Meld u aan toohello [klassieke Azure-portal](http://manage.windowsazure.com) met een globale beheerdersaccount of een collega administrator-account.
2. Selecteer **alle Items** vanuit het hoofdmenu Hallo.
3. Selecteer gewenste toowork met en dat heeft licenties gekoppeld aan het Hallo-directory.
4. Selecteer **licenties**. Hallo-lijst met beschikbare licenties wordt weergegeven.
5. Selecteer Hallo licentieabonnement die Hallo licenties dat u wilt dat toodistribute bevat.
6. Selecteer **gebruikers toewijzen**.
7. Selecteer Hallo-gebruiker die u wilt dat tooassign een licentie aan.
8. Klik op Hallo **toewijzen** knop.  Hallo-gebruiker kan nu aanmelden met tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

