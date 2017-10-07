---
title: Azure AD-kenmerktoewijzingen aaaCustomizing | Microsoft Docs
description: Meer informatie over welke kenmerktoewijzingen voor SaaS-apps in Azure Active Directory zijn hoe u kunt deze aanpassen tooaddress uw bedrijf nodig heeft.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Gebruikers inrichten kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory aanpassen
Microsoft Azure AD biedt ondersteuning voor gebruikers inrichten toothird derden SaaS-toepassingen zoals Salesforce en Google Apps. Als er gebruikers inrichten voor een SaaS-toepassing van derden is ingeschakeld, bepaalt hello Azure Management Portal de kenmerkwaarden weer in de vorm van een configuratie met de naam "kenmerk wordt toegewezen."

Er is een set vooraf geconfigureerde kenmerktoewijzingen tussen Azure AD-gebruikersobjecten en gebruikersobjecten van elke SaaS-app. Sommige apps beheren andere soorten objecten, zoals groepen of contactpersonen. <br> 
 Hallo kenmerk standaardtoewijzingen volgens tooyour bedrijfsbehoeften, kunt u aanpassen. Dit houdt in dat u kunt wijzigen of verwijderen van bestaande kenmerktoewijzingen of nieuwe kenmerktoewijzingen maken.

In hello Azure AD-portal, opent u deze functie door te klikken op een **toewijzingen** configuratie onder **inrichten** in Hallo **beheren** gedeelte van een  **Bedrijfstoepassing**.


![SalesForce][5] 

Te klikken op een **toewijzingen** configuratie, geopend Hallo gerelateerde **kenmerk toewijzing** blade.  
Er zijn kenmerktoewijzingen die door een SaaS-toepassing toofunction correct vereist zijn. Voor de vereiste kenmerken Hallo **verwijderen** functie is niet beschikbaar.


![SalesForce][6]  

Hallo bovenstaande voorbeeld ziet u dat Hallo **gebruikersnaam** kenmerk van een beheerd object in Salesforce is gevuld met Hallo **userPrincipalName** waarde van hello Azure Active Directory-Object gekoppeld.

U kunt bestaande **kenmerktoewijzingen** door te klikken op een toewijzing. Hiermee opent u Hallo **kenmerk bewerken** blade.

![SalesForce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Kenmerk typen toewijzing
Met kenmerktoewijzingen, kunt u bepalen hoe kenmerken worden ingevuld in een SaaS-toepassing van derden. Er zijn vier verschillende toewijzingstypen ondersteund:

* **Directe** – Hallo target-kenmerk is gevuld met de waarde van een kenmerk van het gekoppelde object Hallo Hallo in Azure AD.
* **Constante** – Hallo target-kenmerk is gevuld met een specifieke tekenreeks die u hebt opgegeven.
* **Expressie** -Hallo target-kenmerk is ingevuld op basis van Hallo resultaat van een script-achtige-expressie. 
  Zie voor meer informatie [schrijven expressies voor kenmerktoewijzingen in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Geen** -Hallo doelkenmerk blijft ongewijzigd. Echter, als Hallo doelkenmerk ooit leeg is, wordt dit ingevuld met Hallo standaardwaarde die u opgeeft.

In de toevoeging toothese vier eenvoudige kenmerk toewijzingstypen aangepaste kenmerktoewijzingen Hallo concept van een optionele ondersteuning **standaard** waarde toewijzing. toewijzing van Hallo standaard waarde zorgt ervoor dat een target-kenmerk is gevuld met een waarde als er geen waarde in Azure AD, noch op Hallo-doelobject. meest voorkomende Hallo-configuratie is dit lege tooleave.


## <a name="understanding-attribute-mapping-properties"></a>Understanding toewijzing kenmerkeigenschappen

In de vorige sectie hello, hebt u al geïntroduceerd toohello kenmerk toewijzing type-eigenschap zijn.
Bij toevoeging toothis eigenschap ondersteunen kenmerktoewijzingen ook Hallo volgende kenmerken:

- **Bronkenmerk** -Hallo gebruikerskenmerk uit het bronsysteem hello (bijvoorbeeld: Azure Active Directory).
- **Doelkenmerk** – Hallo gebruikerskenmerk in het doelsysteem hello (bijvoorbeeld: ServiceNow).
- **Overeen met objecten met behulp van dit kenmerk** : of deze toewijzing moet worden gebruikt of niet toouniquely gebruikers tussen de bron en doel systemen Hallo identificeren. Dit is standaard ingesteld op Hallo userPrincipalName of e-mailkenmerk in Azure AD, die normaal gesproken tooa gebruikersnaam veld in een doeltoepassing toegewezen.
- **Overeenkomende voorrang** – meerdere overeenkomende kenmerken kan worden ingesteld. Wanneer er meerdere, moeten ze worden geëvalueerd in Hallo volgorde gedefinieerd door dit veld. Als een overeenkomst is gevonden, er is geen verdere overeenkomende kenmerken worden geëvalueerd.
- **Deze toewijzing is van toepassing**
    - **Altijd** : deze toewijzing is van toepassing op beide maken van een gebruikersaccount en acties bijwerken
    - **Alleen tijdens het maken van** -deze toewijzing is van toepassing alleen op gebruikersacties maken


## <a name="what-you-should-know"></a>Wat u moet weten

Microsoft Azure AD biedt een efficiënte implementatie van een synchronisatieproces. In een omgeving met geïnitialiseerde worden alleen objecten die moet worden bijgewerkt verwerkt tijdens een synchronisatiecyclus. Kenmerktoewijzingen bijwerken, heeft een invloed op Hallo prestaties van een synchronisatiecyclus. Een update toohello kenmerk toewijzing-configuratie is vereist voor alle beheerde objecten toobe opnieuw geëvalueerd. Het is een aanbevolen best practice tookeep Hallo aantal opeenvolgende wijzigingen tooyour kenmerktoewijzingen minimaal.

## <a name="next-steps"></a>Volgende stappen

* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Gebruiker inrichten/Deprovisioning tooSaaS Apps automatiseren](active-directory-saas-app-provisioning.md)
* [Expressies voor kenmerktoewijzingen schrijven](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Bereikfilters voor gebruikers inrichten](active-directory-saas-scoping-filters.md)
* [Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications](active-directory-scim-provisioning.md)
* [Meldingen inrichten van een account](active-directory-saas-account-provisioning-notifications.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

