---
title: Inrichting van apps met bereikfilters | Microsoft Docs
description: Informatie over het bereik filters gebruiken om te voorkomen dat de objecten in apps die ondersteuning bieden voor geautomatiseerde gebruikersinrichting van daadwerkelijk wordt ingericht als een object niet voldoet aan uw zakelijke vereisten.
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
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Inrichten van toepassing op basis van kenmerken met bereikfilters
Het doel van deze sectie is wordt uitgelegd hoe u bereik filters gebruiken om te bepalen op kenmerken gebaseerde regels die bepalen welke gebruikers zijn ingericht voor de toepassing.

## <a name="clauses-and-scope-groups"></a>Componenten en Scope-groepen
![Bereikfilter][1] 

Bereik filters zijn gedefinieerd door een of meer **bereik groepen**, elk van die een of meer houdt **componenten**. Overzicht van de componenten voor een bepaald bereik-groep, kunt u het uitbreiden door te klikken op de pijl naar links van de groepsnaam.

Een **component** bepaalt welke gebruikers kunnen het bereik filter doorgeven door elke gebruiker kenmerken te evalueren. U wellicht bijvoorbeeld één component die vereist dat een gebruikerskenmerk 'status' gelijk zijn aan New York, zodat alleen Den Haag gebruikers zijn ingericht in de toepassing.

![De naam van bereik][2] 

Elke **bereikgroep** begint met een verplichte **component**, zoals wordt weergegeven in de bovenstaande schermafbeelding. Deze component gewoon wordt aangegeven dat de gebruiker moet eerst worden toegewezen aan de toepassing voordat dit wordt geëvalueerd door uw bereik filters. Deze component kan niet worden verwijderd of gewijzigd.

U kunt nieuwe componenten of nieuwe scope groepen toevoegen door de juiste knop te drukken. U kunt elke scope-groep een naam geven door het bewerken van de **groep scopenaam** eigenschap.

## <a name="how-scoping-filters-are-evaluated"></a>Hoe Scoping Filters worden geëvalueerd
Tijdens het inrichten test u elke toegewezen gebruiker tegen bereik filters om te bepalen als die gebruiker toegang tot de toepassing verdient. U kunt zien van elk component als een test die moet worden doorgegeven in volgorde van de gebruiker om te voorkomen dat ophalen uitgefilterd. 

Als er meerdere scope-groepen gedefinieerd, moet elke gebruiker ten minste één van ze toegang krijgen tot de toepassing doorgeven. In elke bereikgroep echter de gebruiker moet doorgeven elke component doorgeven die bepaalde scope-groep. 

Met andere woorden, u kunt zien van bereikgroepen als of gekoppeld en u kunt zien van de componenten binnen deze als en gekoppeld. Neem bijvoorbeeld het volgende bereik filter:

![De naam van bereik][3]  

Gebruikers moeten voldoen aan de volgende criteria, moeten worden ingericht volgens dit bereik filter:

1. Ze moeten worden toegewezen aan de toepassing.
2. Moet worden gebruikt in de afdeling Engineering
3. Werk moeten echter in San Francisco of Canada.

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Automatisch gebruikers inrichten en opheffen van inrichting tot SaaS-toepassingen](active-directory-saas-app-provisioning.md)
* [Kenmerktoewijzingen voor gebruikers inrichten aanpassen](active-directory-saas-customizing-attribute-mappings.md)
* [Expressies voor kenmerktoewijzingen schrijven](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Meldingen inrichten van een account](active-directory-saas-account-provisioning-notifications.md)
* [Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications](active-directory-scim-provisioning.md) (SCIM gebruiken om in te stellen dat gebruikers en groepen van Azure Active Directory automatisch worden ingericht voor toepassingen)
* [Lijst met zelfstudies over het integreren van SaaS-Apps](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
