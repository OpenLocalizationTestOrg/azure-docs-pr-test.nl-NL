---
title: ontwerpoverwegingen voor aaaAzure Active Directory hybride identiteit - directory-synchronisatievereisten bepalen | Microsoft Docs
description: Identificeren welke vereisten nodig zijn voor het synchroniseren van alle Hallo gebruikers tussen on = eigen locatie en cloud voor Hallo enterprise.
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Vereisten voor directory-synchronisatie bepalen
Synchronisatie is alles over een identiteit in Hallo-cloud op basis van hun on-premises identiteits zodat gebruikers beschikken. Of ze gesynchroniseerde account gebruiken voor verificatie of federatieve verificatie, al dan niet nog steeds Hallo-gebruikers een toohave een identiteit in Hallo cloud.  Deze identiteit moet toobe behouden en regelmatig bijgewerkt.  Hallo-updates kunnen vele vormen aannemen, van titel wijzigingen toopassword wijzigingen.  

Begin door te evalueren Hallo organisaties on-premises identity-oplossing en de gebruiker vereisten. Deze evaluatie is belangrijk toodefine Hallo technische vereisten voor hoe gebruikers-id's worden gemaakt en onderhouden in de cloud Hallo.  De meeste organisaties, Active Directory is lokale en Hallo on-premises adreslijst dat gebruikers worden door gesynchroniseerd uit, maar in sommige gevallen dit ook niet Hallo-aanvraag.  

Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Hebt u één AD-forest, meerdere of geen?
  
  * Hoeveel Azure AD-mappen wordt u synchroniseren met?
    
    1. U gebruikt voor het filteren?
    2. Hebt u meerdere Azure AD Connect-servers gepland?
* Op dit moment hebt u een synchronisatie lokale hulpprogramma?
  
  * Zo ja, biedt uw gebruikers als gebruikers beschikken over een virtuele map/integratie van identiteiten?
* Hebt u een andere directory lokale dat u wilt dat toosynchronize (bijvoorbeeld LDAP-adreslijst, HR-database, enzovoort)?
  * Gaat u tijdens het doorzoeken van alle GALSync toobe?
  * Wat is de huidige status Hallo van UPN's in uw organisatie? 
  * Hebt u een andere map die het authenticeren van gebruikers?
  * Maakt uw bedrijf gebruik van Microsoft Exchange?
    * Wel ze van plan bent een hybride implementatie voor exchange hebben?

Nu u een idee hebt over de synchronisatievereisten van uw, moet u toodetermine hulpprogramma dat juist een toomeet Hallo is deze vereisten.  Microsoft biedt verschillende hulpprogramma's voor tooaccomplish Active directory-integratie en synchronisatie.  Zie Hallo [extra vergelijkingstabel voor hybride identiteit directory-integratie](active-directory-hybrid-identity-design-considerations-tools-comparison.md) voor meer informatie. 

Nu dat u hebt uw synchronisatievereisten en het Hallo-hulpprogramma dat u dit voor uw bedrijf doen, moet u tooevaluate Hallo toepassingen die gebruikmaken van deze directoryservices. Deze evaluatie is belangrijk toodefine Hallo technische vereisten toointegrate deze toepassingen toohello cloud. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Deze toepassingen worden verplaatst toohello cloud en Hallo directory gebruikt?
* Zijn er speciale kenmerken die toobe gesynchroniseerd toohello cloud nodig hebben om deze toepassingen kunnen worden gebruikt met succes?
* Moeten deze toepassingen toobe opnieuw geschreven tootake voordeel van cloud-verificatie?
* Deze toepassingen blijven toolive lokale terwijl gebruikers toegang toe hebben met behulp van de cloud-identiteit Hallo?

U moet ook toodetermine Hallo beveiliging vereisten en beperkingen directory-synchronisatie. Deze evaluatie is belangrijk tooget een lijst met Hallo vereisten die nodig zijn in de volgorde toocreate en onderhouden van gebruikersidentiteiten in Hallo cloud. Zorg ervoor dat tooanswer Hallo vragen te volgen:

* Waar de synchronisatieserver Hallo worden geplaatst?
* Kan het zijn verbonden met het domein?
* Hallo-server bevindt zich in een beperkte netwerk achter een firewall, zoals een Perimeternetwerk?
  * U kunt tooopen Hallo vereist firewall-poorten toosupport synchronisatie worden?
* Hebt u een noodherstelplan voor Hallo synchronisatieserver?
* Hebt u een account met de juiste machtigingen voor alle forests die u wilt dat toosynch met Hallo?
  * Als uw bedrijf komt niet voor deze vraag Hallo-antwoord niet weet, bekijk Hallo sectie 'Machtigingen voor Wachtwoordsynchronisatie' hello artikel [installeren hello Azure Active Directory-synchronisatieservice](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) en bepalen of u al hebt een account met deze machtigingen of als u toocreate een nodig.
* Als u hebt is zijn forest sync Hallo synchronisatie kunnen tooget tooeach-serverforest?

> [!NOTE]
> Zorg ervoor dat tootake notities van elk antwoord en Hallo logica achter Hallo antwoord begrijpt. [Vereisten voor respons op incidenten bepalen](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) gaat over Hallo opties die beschikbaar zijn. Moet door deze vragen die u selecteert welke optie het beste past bij uw bedrijf te beantwoorden.
> 
> 

## <a name="next-steps"></a>Volgende stappen
[Vereisten multi-factor authentication bepalen](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Zie ook
[Overzicht ontwerpoverwegingen](active-directory-hybrid-identity-design-considerations-overview.md)

