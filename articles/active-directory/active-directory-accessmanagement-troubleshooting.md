---
title: aaaTroubleshooting dynamisch lidmaatschap voor groepen | Microsoft Docs
description: Tips voor probleemoplossing voor dynamisch lidmaatschap voor groepen in Azure AD.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 89bb04b6-a379-49c2-8465-fe386641816a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: d792fc406288844e2c5dbe3702c2c9870d09473e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Oplossen van problemen met dynamische lidmaatschappen voor groepen
**Ik een regel voor een groep hebt geconfigureerd, maar geen lidmaatschappen worden bijgewerkt in de groep Hallo**<br/>Controleer of deze Hallo **inschakelen gedelegeerd groepsbeheer** ingesteld te**Ja** in Hallo **configureren** tabblad. U ziet deze instelling alleen als u bent aangemeld als een gebruiker toowhom een Azure Active Directory Premium-licentie is toegewezen. Controleer Hallo waarden voor kenmerken van de gebruiker op Hallo regel: Er zijn van gebruikers die voldoen aan de regel Hallo?

**Ik een regel hebt geconfigureerd, maar nu Hallo bestaande leden van de regel Hallo zijn verwijderd**<br/>Dit is verwacht gedrag. Bestaande leden van Hallo groep worden verwijderd wanneer een regel is ingeschakeld of gewijzigd. Hallo-gebruikers heeft geretourneerd van de evaluatieversie van Hallo regel worden toegevoegd als leden toohello groep.     

**Ik zie niet met het lidmaatschap wordt gewijzigd direct als ik toevoegen of wijzigen van een regel, waarom niet?**<br/>Evaluatie toegewezen lidmaatschap wordt periodiek uitgevoerd in een asynchrone achtergrondproces. Hoe lang Hallo proces duurt is afhankelijk van Hallo aantal gebruikers in uw directory en Hallo grootte van Hallo-groep gemaakt naar aanleiding van Hallo regel. Mappen met een klein aantal gebruikers ziet doorgaans wijzigingen voor een groepslidmaatschap Hallo in minder dan een paar minuten. Mappen met een groot aantal gebruikers duurt 30 minuten of langer toopopulate.

### <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [What is Azure Active Directory?](active-directory-whatis.md) (Wat is Azure Active Directory?)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
