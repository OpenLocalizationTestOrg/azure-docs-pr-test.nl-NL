---
title: aaaAssigning beheerdersrollen in Azure Active Directory | Microsoft Docs
description: Een beheerdersrol kunt maken of bewerken van gebruikers, tooothers beheerdersrollen toewijzen, gebruikerswachtwoorden, Gebruikerslicenties beheren of domeinen beheren. Een gebruiker aan wie een beheerdersrol is toegewezen Hallo heeft dezelfde machtigingen over alle cloud-services toowhich uw organisatie een abonnement.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: it-pro;
ms.openlocfilehash: 41cddbf311767d9995c99ee386e6d276745dad18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Beheerrollen toewijzen in Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-assign-admin-roles-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-assign-admin-roles.md)
>
>

Met Azure Active Directory (Azure AD), kunt u aanwijzen afzonderlijke beheerders tooserve verschillende functies. Deze beheerders wordt toovarious toegangsfuncties in hello Azure-portal of de klassieke Azure-portal en, afhankelijk van hun rol kunnen toocreate of gebruikers bewerken, tooothers beheerdersrollen toewijzen, wachtwoorden opnieuw instellen, worden gebruikerslicenties, beheren en domeinen, onder andere beheren. Een gebruiker aan wie een beheerdersrol is toegewezen hebben Hallo dezelfde machtigingen voor alle Hallo cloud-services die uw organisatie zich heeft aangemeld, ongeacht of u toewijzen Hallo rol in Hallo Office 365-portal of in Hallo klassieke Azure-portal of met behulp van Hallo Azure AD-module voor Windows PowerShell.

Hallo na beheerdersrollen zijn beschikbaar:

* **Financieel medewerker**: doet aankopen, beheert abonnementen, beheert ondersteuningstickets en bewaakt de servicestatus.

* **Naleving beheerder**: gebruikers met deze functie hebben beheermachtigingen binnen in Office 365-beveiliging Hallo & Compliancecentrum en Exchange-beheercentrum. Meer informatie op '[over Office 365-beheerdersrollen](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d). "

* **Servicebeheerder CRM**: gebruikers aan deze rol globale machtigingen in Microsoft CRM Online, wanneer Hallo-service aanwezig is, evenals Hallo mogelijkheid toomanage ondersteuningstickets en bewaakt de servicestatus. Meer informatie op [over Office 365-beheerdersrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Apparaatbeheerders**: gebruikers met deze rol worden beheerders van de lokale computer op alle Windows 10-apparaten die gekoppeld tooAzure Active Directory zijn. Hebben geen Hallo mogelijkheid toomanage apparaten objecten in Azure Active Directory.

* **Directory lezers**: dit is een verouderde rol die is toegewezen toobe tooapplications die geen ondersteuning bieden voor Hallo [Framework toestemming](active-directory-integrating-applications.md). Deze mag niet worden toegewezen tooany gebruikers.

* **Directory-synchronisatie Accounts**: niet gebruiken. Deze rol is wordt automatisch toegewezen toohello Azure AD Connect-service, en niet bedoeld of ondersteund voor ander gebruik.

* **Directory schrijvers**: dit is een verouderde rol die is toegewezen toobe tooapplications die geen ondersteuning bieden voor Hallo [Framework toestemming](active-directory-integrating-applications.md). Deze mag niet worden toegewezen tooany gebruikers.

* **Exchange-servicebeheerder**: gebruikers met deze rol globale machtigingen in Microsoft Exchange Online zijn wanneer het Hallo-service aanwezig is. Meer informatie op [over Office 365-beheerdersrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Globale beheerder / Company Administrator**: gebruikers met deze rol hebben toegang tooall beheerfuncties in Azure Active Directory, evenals die federate tooAzure Active Directory, zoals Exchange Online, SharePoint Online-services en Skype voor bedrijven Online. Hallo persoon die zich voor hello Azure Active Directory-tenant aanmeldt wordt een globale beheerder. Alleen globale beheerders kunnen andere beheerdersrollen toewijzen. Er zijn meer dan één globale beheerder in uw bedrijf. Globale beheerders kunnen Hallo het wachtwoord voor elke gebruiker en alle andere beheerders ingesteld.

  > [!NOTE]
  > Deze rol wordt in Microsoft Graph API, Azure AD Graph API en Azure AD PowerShell geïdentificeerd als "Company Administrator". Hallo 'Globale beheerder' wordt [Azure-portal](https://portal.azure.com).
  >
  >

* **Gast uitnodiging antwoorden**: gebruikers met deze rol kunnen Azure Active Directory B2B Gast gebruiker uitnodigingen beheren wanneer Hallo 'Leden kunnen uitnodigen' gebruikersinstelling tooNo is ingesteld. Meer informatie over B2B-samenwerking op [over hello Azure AD B2B-samenwerking preview](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Dit omvat geen andere machtigingen.

* **Intune-servicebeheerder**: gebruikers met deze rol globale machtigingen in Microsoft Intune Online zijn wanneer het Hallo-service aanwezig is. Bovendien deze rol bevat Hallo mogelijkheid toomanage gebruikers en apparaten in de volgorde tooassociate beleid, evenals groepen maken en beheren.

* **Postvak beheerder**: deze rol wordt alleen gebruikt als onderdeel van Exchange Online e-mailondersteuning voor RIM Blackberry-apparaten. Gebruik deze functie niet als uw organisatie geen Exchange Online e-mail op RIM Blackberry-apparaten gebruikt.

* **Ondersteuning voor laag 1 partner**: niet gebruiken. Deze rol is gedeprecieerd en wordt verwijderd uit Azure AD in toekomstige Hallo. Deze rol is bedoeld voor gebruik door een klein aantal Microsoft-partners zijn doorverkoop en is niet bedoeld voor algemeen gebruik.

* **Laag 2-ondersteuning partner**: niet gebruiken. Deze rol is gedeprecieerd en wordt verwijderd uit Azure AD in toekomstige Hallo. Deze rol is bedoeld voor gebruik door een klein aantal Microsoft-partners zijn doorverkoop en is niet bedoeld voor algemeen gebruik.

* **Wachtwoordbeheerder / Helpdesk beheerder**: gebruikers met deze rol kunnen wachtwoorden opnieuw instellen, serviceaanvragen beheren en controleren van de servicestatus. Wachtwoordbeheerders kunnen wachtwoorden alleen voor gebruikers en andere wachtwoordbeheerders opnieuw instellen.

  > [!NOTE]
  > Deze rol wordt in Microsoft Graph API, Azure AD Graph API en Azure AD PowerShell aangeduid als 'Helpdesk-beheerder'. Hallo ' wachtwoord beheerder ' wordt [Azure-portal](https://portal.azure.com/).
  >
  >
  
* **Power BI-servicebeheerder**: gebruikers aan deze rol globale machtigingen in Microsoft Power BI, wanneer Hallo-service aanwezig is, evenals Hallo mogelijkheid toomanage ondersteuningstickets en bewaakt de servicestatus. Meer informatie op [over Office 365-beheerdersrollen](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Bevoegde rol beheerder**: gebruikers met deze rol roltoewijzingen in Azure Active Directory, evenals in Azure AD Privileged Identity Management kunnen beheren. Bovendien kan deze rol beheer van alle aspecten van Privileged Identity Management.

* **Beveiligingsbeheerder**: gebruikers met deze rol alle Hallo alleen-lezen machtigingen van de rol Lezer hello, plus Hallo mogelijkheid toomanage configuratie voor beveiliging gerelateerde services hebben: Azure Active Directory: Identity Protection Privileged Identity Management en Office 365-beveiliging en naleving Center. Meer informatie over machtigingen voor Office 365 is beschikbaar op [machtigingen in Office 365-beveiliging Hallo & Compliancecentrum](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Beveiliging lezer**: gebruikers met deze rol globale alleen-lezen toegang hebben, met inbegrip van alle gegevens in Azure Active Directory, Identity Protection, Privileged Identity Management, evenals Hallo mogelijkheid tooread Azure Active Directory-aanmeldingspagina rapporten en controlelogboeken. Hallo-rol hebben ook alleen-lezen toegang in Office 365-beveiliging en naleving Center. Meer informatie over machtigingen voor Office 365 is beschikbaar op [machtigingen in Office 365-beveiliging Hallo & Compliancecentrum](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Ondersteuning voor servicebeheerder**: gebruikers met deze rol kunnen ondersteuningsaanvragen openen met Microsoft voor Azure en Office 365-services en weergaven Hallo dashboard en het bericht servicecentrum in hello Azure-portal en Office 365-beheerportal. Meer informatie op [over Office 365-beheerdersrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **SharePoint-servicebeheerder**: gebruikers aan deze rol globale machtigingen in Microsoft SharePoint Online, wanneer Hallo-service aanwezig is, evenals Hallo mogelijkheid toomanage ondersteuningstickets en bewaakt de servicestatus. Meer informatie op [over Office 365-beheerdersrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype voor bedrijven / Lync servicebeheerder**: gebruikers met deze rol gemachtigd globale binnen Microsoft Skype voor bedrijven, wanneer het Hallo-service aanwezig is, evenals de gebruikerskenmerken Skype-specifieke in Azure Active Directory beheren. Deze rol verleent Hallo mogelijkheid toomanage ondersteuningstickets en monitor service bovendien health. Meer informatie op [over Office 365-beheerdersrollen](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > Deze rol wordt in Microsoft Graph API, Azure AD Graph API en Azure AD PowerShell geïdentificeerd als 'Lync servicebeheerder'. Hallo 'Skype voor bedrijven-servicebeheerder' wordt [Azure-portal](https://portal.azure.com/).
  >
  >

* **De accountbeheerder gebruiker**: gebruikers met deze rol kunnen maken en beheren van alle aspecten van gebruikers en groepen. Bovendien deze rol omvat Hallo mogelijkheid toomanage ondersteuningstickets en monitors health-service. Er zijn enkele beperkingen van toepassing. Bijvoorbeeld: deze rol is niet toegestaan voor het verwijderen van een globale beheerder en terwijl u toelaat wijzigen van wachtwoorden voor niet-beheerders, kunnen geen wijzigen van wachtwoorden voor globale beheerders of andere bevoorrechte beheerders.

## <a name="administrator-permissions"></a>Administrator-machtigingen

### <a name="billing-administrator"></a>Financieel medewerker

| Kan doen | Is niet mogelijk |
| --- | --- |
|<p>Gegevens van bedrijfs- en gebruikersgegevens weergeven</p><p>Office-ondersteuningstickets beheren</p><p>Factuur- en bewerkingen voor Office-producten</p> |<p>Gebruikerswachtwoorden opnieuw instellen</p><p>Gebruiker weergaven maken en beheren</p><p>Maken, bewerken, en gebruikers en groepen verwijderen en gebruikerslicenties beheren</p><p>Domeinen beheren</p><p>Beheren van bedrijfsgegevens</p><p>Beheerdersrollen tooothers delegeren</p><p>Adreslijstsynchronisatie gebruiken</p><p>Auditlogboeken weergeven</p>|

### <a name="global-administrator"></a>Globale beheerder
| Kan doen | Is niet mogelijk |
| --- | --- |
| <p>Gegevens van bedrijfs- en gebruikersgegevens weergeven</p><p>Office-ondersteuningstickets beheren</p><p>Factuur- en bewerkingen voor Office-producten</p><p>Gebruikerswachtwoorden opnieuw instellen</p>
<p>Andere beheerder de wachtwoorden opnieuw instellen</p> <p>Gebruiker weergaven maken en beheren</p><p>Maken, bewerken, en gebruikers en groepen verwijderen en gebruikerslicenties beheren</p><p>Domeinen beheren</p><p>Beheren van bedrijfsgegevens</p><p>Beheerdersrollen tooothers delegeren</p><p>Adreslijstsynchronisatie gebruiken</p><p>In- of uitschakelen van multi-factor authentication-server</p><p>Auditlogboeken weergeven</p> |N.v.t. |

### <a name="password-administrator"></a>Wachtwoordbeheerder
| Kan doen | Is niet mogelijk |
| --- | --- |
| <p>Gegevens van bedrijfs- en gebruikersgegevens weergeven</p><p>Office-ondersteuningstickets beheren</p><p>Gebruikerswachtwoorden opnieuw instellen</p> <p>Andere beheerder de wachtwoorden opnieuw instellen</p>|<p>Factuur- en bewerkingen voor Office-producten</p><p>Gebruiker weergaven maken en beheren</p><p>Maken, bewerken, en gebruikers en groepen verwijderen en gebruikerslicenties beheren</p><p>Domeinen beheren</p><p>Beheren van bedrijfsgegevens</p><p>Beheerdersrollen tooothers delegeren</p><p>Adreslijstsynchronisatie gebruiken</p><p>Rapporten weergeven</p>|

### <a name="service-administrator"></a>Servicebeheerder
| Kan doen | Is niet mogelijk |
| --- | --- |
| <p>Gegevens van bedrijfs- en gebruikersgegevens weergeven</p><p>Office-ondersteuningstickets beheren</p> |<p>Gebruikerswachtwoorden opnieuw instellen</p><p>Factuur- en bewerkingen voor Office-producten</p><p>Gebruiker weergaven maken en beheren</p><p>Maken, bewerken, en gebruikers en groepen verwijderen en gebruikerslicenties beheren</p><p>Domeinen beheren</p><p>Beheren van bedrijfsgegevens</p><p>Beheerdersrollen tooothers delegeren</p><p>Adreslijstsynchronisatie gebruiken</p><p>Auditlogboeken weergeven</p> |

### <a name="user-administrator"></a>De Gebruikersbeheerder van de
| Kan doen | Is niet mogelijk |
| --- | --- |
| <p>Gegevens van bedrijfs- en gebruikersgegevens weergeven</p><p>Office-ondersteuningstickets beheren</p><p>Gebruikerswachtwoorden, met beperkingen.</p><p>Andere beheerder de wachtwoorden opnieuw instellen</p><p>Opnieuw instellen van wachtwoorden van andere gebruikers</p><p>Gebruiker weergaven maken en beheren</p><p>Maken, bewerken, en gebruikers en groepen verwijderen en gebruikerslicenties met beperkingen te beheren. Hij of zij kan geen algemeen beheerder verwijderen of andere beheerders maken.</p> |<p>Factuur- en bewerkingen voor Office-producten</p><p>Domeinen beheren</p><p>Beheren van bedrijfsgegevens</p><p>Beheerdersrollen tooothers delegeren</p><p>Adreslijstsynchronisatie gebruiken</p><p>In- of uitschakelen van multi-factor authentication-server</p><p>Auditlogboeken weergeven</p> |

### <a name="security-reader"></a>Beveiliging lezer
| in | Kan doen |
| --- | --- |
| Identity Protection Center |Alle beveiligingsrapporten en informatie over de instellingen voor beveiligingsfuncties lezen<ul><li>Tegen ongewenste e-mail<li>Versleuteling<li>Preventie van gegevensverlies<li>Anti-malware<li>Geavanceerde threat protection<li>Antiphishing-<li>Mailflow regels |
| Privileged Identity Management |<p>Is alleen-lezentoegang tooall informatie opgehaald in Azure AD PIM: beleidsregels en rapporten voor Azure AD-roltoewijzingen beoordeelt de beveiliging en in Hallo gelezen toekomstige toegang tot toopolicy gegevens en rapporten voor scenario's naast de roltoewijzing Azure AD.<p>**Kan geen** aanmelden voor Azure AD PIM of eventuele tooit wijzigingen aanbrengen. In de PIM-portal of via PowerShell kunt iemand met deze rol aanvullende functies (bijvoorbeeld globale beheerder of beheerder met bevoorrechte rol) activeren als de gebruiker Hallo geschikt is voor deze. |
| <p>Monitor voor Office 365-servicestatus</p><p>Office 365-beveiliging en naleving Center</p> |<ul><li>Lees- en waarschuwingen beheren<li>Lezen van beveiligingsbeleid<li>Lezen dreigingen en Cloud App Discovery quarantaine in zoeken en onderzoeken<li>Alle rapporten lezen |

### <a name="security-administrator"></a>Beveiligingsbeheerder
| in | Kan doen |
| --- | --- |
| Identity Protection Center |<ul><li>Alle machtigingen van de rol van de lezer van de beveiliging Hallo.<li>Bovendien Hallo mogelijkheid tooperform alle IPC-bewerkingen, met uitzondering van opnieuw instellen van wachtwoorden. |
| Privileged Identity Management |<ul><li>Alle machtigingen van de rol van de lezer van de beveiliging Hallo.<li>**Kan geen** rollidmaatschappen voor Azure AD of instellingen beheren. |
| <p>Monitor voor Office 365-servicestatus</p><p>Office 365-beveiliging en naleving Center |<ul><li>Alle machtigingen van de rol van de lezer van de beveiliging Hallo.<li>Kan alle instellingen configureren in Hallo Advanced Threat Protection-functie (malware & virus beveiliging, schadelijke URL config, URL tracering, enzovoort). |

## <a name="details-about-hello-global-administrator-role"></a>Meer informatie over de globale beheerdersrol Hallo
Hallo globale beheerder heeft toegang tot tooall beheerfuncties. Hallo persoon die zich voor een Azure-abonnement aanmeldt is standaard Hallo globale beheerdersrol voor Hallo directory worden toegewezen. Alleen globale beheerders kunnen andere beheerdersrollen toewijzen.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd een collega als globale beheerder

1. Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor de tenantmap Hallo.

   ![Azure AD-beheercentrum te openen](./media/active-directory-assign-admin-roles-azure-portal/active-directory-admin-center.png)

2. Selecteer **gebruikers en groepen &gt; alle gebruikers**

3. Hallo gebruiker u wilt dat toodesignate als globale beheerder blade en open Hallo voor die gebruiker vinden.

4. Selecteer op de blade Hallo gebruiker **functie Directory**.
 
5. Selecteer op Hallo directory rolblade Hallo **globale beheerder** rol, en op te slaan.

## <a name="assign-or-remove-administrator-roles"></a>Toewijzen of verwijderen van beheerdersrollen
hoe tooassign beheerdersrollen tooa gebruiker in Azure Active Directory, Zie toolearn [tooadministrator rollen in Azure Active Directory-voorbeeld voor een gebruiker toewijzen](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Afgeschafte functies

Hallo rollen na mag niet worden gebruikt. Ze zijn gedeprecieerd en wordt verwijderd uit Azure AD in toekomstige Hallo.

* De beheerder van de ad-hoc-licentie
* De maker van de geverifieerde gebruiker e-mail
* Apparaat Join
* Apparaatbeheer
* Gebruikers van apparaten
* Werkplekkoppeling apparaat

## <a name="next-steps"></a>Volgende stappen

* toolearn informatie over hoe beheerders voor een Azure-abonnement toochange zien [hoe tooadd of wijzig Azure-beheerdersrollen](../billing-add-change-azure-subscription-administrator.md)
* Zie toolearn meer informatie over hoe de toegang tot resources wordt beheerd in Microsoft Azure [informatie over toegang tot bronnen in Azure](active-directory-understanding-resource-access.md)
* Zie voor meer informatie over hoe tooyour Azure-abonnement in Azure Active Directory is gekoppeld, [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Gebruikers beheren](active-directory-create-users.md)
* [Wachtwoorden beheren](active-directory-manage-passwords.md)
* [Groepen beheren](active-directory-manage-groups.md)
