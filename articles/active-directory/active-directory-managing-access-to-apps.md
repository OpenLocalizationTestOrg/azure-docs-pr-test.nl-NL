---
title: aaaManaging toegang tooapps gebruikmaken van Azure AD | Microsoft Docs
description: Hierin wordt beschreven hoe Azure Active Directory kunnen organisaties toospecify Hallo apps toowhich elke gebruiker toegang heeft.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Het beheren van toegang tooapps
Beheer lopende toegang, gebruik beoordeling en rapportage blijven toobe een challenge nadat een app is geïntegreerd in uw organisatie identiteitsbeheersysteem. In veel gevallen IT-beheerders of helpdesk hebben tootake een lopende actieve rol bij het beheren van toegang tooyour apps. Soms wordt toewijzing uitgevoerd door een algemene of divisie IT-team. Hallo toewijzing besluit is vaak beoogde toobe gedelegeerd toohello besluitvormer, vereisen van hun goedkeuring voordat IT heeft Hallo toewijzing.  Andere organisaties Investeer in integratie met een bestaand geautomatiseerde identiteits- en toegangsbeheer management-systeem, zoals rollen gebaseerd toegangsbeheer (RBAC) of toegangsbeheer op basis van kenmerken (ABAC). Zowel Hallo-integratie en ontwikkeling van de regel vaak toobe gespecialiseerde en duur. Controleren of rapportage over de aanpak van beide management is een eigen afzonderlijke, complexe en dure investering.

## <a name="how-does-azure-active-directory-help"></a>Hoe helpt Azure Active Directory?
 Azure AD ondersteunt uitgebreide access management voor geconfigureerde applicaties, waardoor organisaties tooeasily rechts toegangsbeleid Hallo variërend van automatische, op basis van kenmerken toewijzing (ABAC of RBAC scenario's) via delegering en inclusief bereiken beheerdersbeheer. Met Azure AD kunt u eenvoudig bereiken complexe beleid combineren van meerdere management modellen voor één toepassing en kunnen zelfs hergebruik regels van verschillende toepassingen met dezelfde doelgroepen Hallo.

* [Toevoegen van nieuwe of bestaande toepassingen](active-directory-sso-integrate-saas-apps.md)

 Toewijzing van Azure AD-toepassing is gericht op twee primaire toewijzing modi:

* **Afzonderlijke toewijzing** een IT-beheerder met de globale beheerder mapmachtigingen kunt selecteren van afzonderlijke gebruikersaccounts en toegang verlenen toohello toepassing.
* **Toewijzing op basis van een groep (betaald alleen Azure AD)** een IT-beheerder met globale beheerdersmachtigingen voor directory een groep toohello toepassing kunt toewijzen. Specifieke gebruikers toegang is afhankelijk van dat of ze deel uitmaken van de groep Hallo Hallo gelijktijdig ze proberen tooaccess Hallo-toepassing. Een beheerder kan met andere woorden, een mededeling 'alle leden van de groep toegewezen Hallo heeft toegang tot toohello toepassing' toewijzingsregel effectief maken. Met deze optie toewijzing beheerders kunnen profiteren van een Azure AD-groep voor beheeropties, met inbegrip van [dynamische groepen op basis van kenmerken](active-directory-accessmanagement-manage-groups.md), extern systeemgroepen (bijvoorbeeld on-premises Active Directory of werkdag) of de Administrator beheerde of zelfstandige-verkeer beheerde groepen. Een groep kan worden eenvoudig toegewezen toomultiple apps, ervoor te zorgen dat toepassingen met toewijzing affiniteit toewijzingsregels, kunnen delen minder Hallo algehele beheercomplexiteit. Houd er rekening mee dat geneste groep lidmaatschappen worden niet ondersteund voor toewijzing op basis van een groep tooapplications op dit moment.

Met behulp van deze toewijzing van de twee modi, kunnen beheerders eventuele wenselijk toewijzing managementbenadering bereiken.

Met Azure AD is gebruiks- en rapportage over volledig geïntegreerd, waardoor beheerders tooeasily rapport over de status van sitetoewijzing toewijzingsfouten en zelfs informatie over het gebruik.

## <a name="complex-application-assignment-with-azure-ad"></a>Toewijzing van complexe toepassingen met Azure AD
U kunt een toepassing zoals Salesforce. In veel organisaties wordt Salesforce voornamelijk gebruikt door Hallo marketing- en organisaties. Vaak uitgebreide leden van Hallo marketing team maximaal toegang tooSalesforce, terwijl de leden van het verkoopteam Hallo beperkte toegang hebben. In veel gevallen hebben een algemene populatie van IT-medewerkers toegang toohello toepassing beperkt. Uitzonderingen toothese regels bemoeilijken belangrijk is. Het is vaak het recht van Hallo marketing- of leidinggevende teams toogrant een gebruikerstoegang Hallo of hun rollen onafhankelijk van deze algemene regels wijzigen.

Met Azure AD kunnen toepassingen zoals Salesforce zijn vooraf geconfigureerd voor eenmalige aanmelding (SSO) en de geautomatiseerde inrichting. Zodra de toepassing hello is geconfigureerd, kan een beheerder Hallo eenmalige actie toocreate nemen en Hallo juiste groepen toewijzen. In dit voorbeeld kan een beheerder Hallo toewijzingen volgende uitvoeren:

* [Dynamische groepen](active-directory-accessmanagement-manage-groups.md) kan worden gedefinieerd tooautomatically vertegenwoordigen alle leden van Hallo marketing- en teams met kenmerken zoals afdeling of rol:
  
  * Alle leden van marketing groepen wordt toohello 'marketing' rol in Salesforce toegewezen
  * Alle leden van de verkoop team groepen toohello 'verkoop' rol in Salesforce wordt toegewezen. Een verdere verfijning kan meerdere groepen die overeenkomen met regionale sales-teams toodifferent Salesforce rollen toegewezen gebruiken.
* uitzonderingsmechanisme tooenable hello, een groepsbeheer met Self-service kan worden gemaakt voor elke rol. Hallo 'Salesforce marketing uitzondering' groep kan bijvoorbeeld worden gemaakt als een groepsbeheer met Self-service. Hallo-groep marketing toohello Salesforce-rol kan worden toegewezen en marketing leiding Hallo eigenaren kan worden gemaakt. Leden van de marketing leiding Hallo kunnen toevoegen of verwijderen gebruikers, stelt u een beleid join of zelfs goedkeuren of weigeren van afzonderlijke gebruikers aanvragen toojoin. Dit wordt ondersteund door een information worker juiste ervaring die geen speciale training voor eigenaars of leden vereist.

In dit geval alle toegewezen gebruikers die automatisch ingerichte tooSalesforce zou zijn, omdat ze toegevoegde toodifferent groepen die hun roltoewijzing zou worden bijgewerkt in Salesforce. Gebruikers zou kunnen toodiscover en toegang tot de Salesforce via Hallo toepassing toegang Configuratiescherm van Microsoft Office web-clients, of zelfs door te navigeren tootheir organisatie Salesforce-aanmeldingspagina. Beheerders zijn kunnen tooeasily gebruiks- en toewijzing status weergeven met behulp van Azure AD-rapportage.

Beheerders kunnen gebruikmaken van [voorwaardelijke toegang van Azure AD](active-directory-conditional-access.md) tooset toegangsbeleid voor specifieke rollen. Deze beleidsregels kunnen bevatten of toegang is toegestaan buiten de bedrijfsomgeving Hallo en zelfs multi-factor Authentication of vereisten tooachieve Apparaattoegang in verschillende gevallen.

## <a name="how-can-i-get-started"></a>Hoe kan ik aan de slag?
Eerste, als u niet al Azure AD gebruikt en u een IT-beheerder:

* [Probeer het nu!](https://azure.microsoft.com/trial/get-started-active-directory/) -u kunt zich aanmelden voor een gratis proefversie van 30 dagen vandaag en implementeren van uw eerste cloudoplossing onder 5 minuten via deze koppeling

Azure AD-functies die delen van het account inschakelen:

* [Toewijzing van updategroep](active-directory-accessmanagement-self-service-group-management.md)
* Toepassingen tooAzure AD toevoegen
* Aan de slag met toewijzing
* Toewijzing van de toepassing Veelgestelde vragen
* [App-dashboard/gebruiksrapporten](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Waar vind ik meer informatie?
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Apps met voorwaardelijke toegang beveiligen](active-directory-conditional-access.md)
* [Groepsbeheer met Self-Service management/SSAA](active-directory-accessmanagement-self-service-group-management.md)

