---
title: apps met bereikfilters aaaProvisioning | Microsoft Docs
description: Meer informatie over hoe toouse scoping filtert tooprevent objecten in apps die ondersteuning bieden voor geautomatiseerde gebruikersinrichting van daadwerkelijk wordt ingericht als een object niet voldoet aan uw zakelijke vereisten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Inrichten van toepassing op basis van kenmerken met bereikfilters
Hallo-doel van deze sectie is tooexplain hoe toouse scoping filtert toodefine op kenmerken gebaseerde regels die bepalen welke gebruikers zijn ingericht toohello toepassing.

## <a name="clauses-and-scope-groups"></a>Componenten en Scope-groepen
![Bereikfilter][1] 

Bereik filters zijn gedefinieerd door een of meer **bereik groepen**, elk van die een of meer houdt **componenten**. toosee hello componenten voor een bepaald bereik-groep, weer door te klikken op Hallo pijl toohello links van de groepsnaam Hallo.

Een **component** bepaalt welke gebruikers de mogelijkheid toopass via Hallo bereikfilter door elke gebruiker kenmerken te evalueren. Bijvoorbeeld, wellicht u een component die dat vereist een gebruiker 'status'-kenmerk gelijk New York, zodat alleen Den Haag gebruikers zijn ingericht in de toepassing hello.

![De naam van bereik][2] 

Elke **bereikgroep** begint met een verplichte **component**, zoals weergegeven in de bovenstaande Hallo. Deze component gewoon aangegeven dat die Hallo-gebruiker moet eerst worden toegewezen toohello toepassing voordat dit wordt geëvalueerd door uw bereik filters. Deze component kan niet worden verwijderd of gewijzigd.

U kunt nieuwe componenten of nieuwe scope groepen toevoegen door de juiste knop hello te drukken. U kunt elke scope-groep een naam geven door het bewerken van de **groep scopenaam** eigenschap.

## <a name="how-scoping-filters-are-evaluated"></a>Hoe Scoping Filters worden geëvalueerd
Tijdens het inrichten testen we elke toegewezen gebruiker op basis van uw bereik filters toodetermine als die gebruiker toegang toohello toepassing verdient. U kunt zien van elk component als een test die moet worden doorgegeven om Hallo gebruiker tooavoid ophalen uitgefilterd. 

Als er meerdere scope-groepen gedefinieerd, moet elke gebruiker doorgeven ten minste één van deze tooaccess Hallo-toepassing. In elke bereikgroep echter Hallo gebruiker moet doorgeven elke toopass component die bepaalde scope-groep. 

Met andere woorden, u kunt zien van bereikgroepen als of gekoppeld en u kunt zien Hallo componenten binnen deze als en gekoppeld. Denk bijvoorbeeld Hallo bereikfilter hieronder:

![De naam van bereik][3]  

Volgens toothis bereikfilter, gebruikers moeten voldoen aan de volgende Hallo criteria, toobe ingericht:

1. Ze moeten toohello toepassing worden toegewezen.
2. Moet worden gebruikt in Hallo Engineering-afdeling
3. Werk moeten echter in San Francisco of Canada.

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Gebruikers inrichten en Deprovisioning tooSaaS toepassingen automatiseren](active-directory-saas-app-provisioning.md)
* [Kenmerktoewijzingen voor gebruikers inrichten aanpassen](active-directory-saas-customizing-attribute-mappings.md)
* [Expressies voor kenmerktoewijzingen schrijven](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Meldingen inrichten van een account](active-directory-saas-account-provisioning-notifications.md)
* [Met behulp van SCIM tooenable automatische inrichting van gebruikers en groepen van Azure Active Directory-tooapplications](active-directory-scim-provisioning.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
