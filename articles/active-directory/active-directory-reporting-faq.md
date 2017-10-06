---
title: Active Directory Reporting Veelgestelde vragen over aaaAzure | Microsoft Docs
description: Azure Active Directory-Veelgestelde vragen over rapportage.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Azure Active Directory-Veelgestelde vragen over rapportage

Dit artikel bevat toofrequently van antwoorden op veelgestelde vragen (FAQ's) over Azure Active Directory-rapportage.  
Zie voor meer informatie [rapportage van Azure Active Directory](active-directory-reporting-azure-portal.md). 

**V: Wat is de Gegevensretentie hello om activiteitenlogboeken (Audit en aanmeldingen) in hello Azure-portal?** 

**A:** bieden We zeven dagen aan gegevens voor onze klanten gratis en door over te schakelen tooan Azure AD Premium 1 of 2 voor Premium-licentie, u toegang hebt tot gegevens voor too30 dagen. Zie voor meer informatie over bewaren [bewaarbeleid voor Azure Active Directory-rapport](active-directory-reporting-retention.md)

--- 

**V: hoe lang duurt het tot ik Hallo activiteitsgegevens zien kunt wanneer ik mijn taak hebt voltooid?**

**A:** controlelogboeken activiteit een latentie tussen 15 minuten tooan uur hebben. Aanmelden activiteitenlogboeken hebben een latentie tussen 15 minuten voor de meeste records en too2 uur voor een aantal records.

---

**V: moet ik een globale beheerder toosee Hallo activiteit geregistreerd in hello Azure Portal of tooget gegevens via Hallo API toobe?**

**A:** Nee. U kan zijn een **beveiliging lezer**, een **beveiliging Admin** of een **globale beheerder** toosee rapportagegegevens in Azure Portal of door deze te openen via Hallo API.

---

**V: kan ik Office 365 activiteit logboekgegevens via hello Azure-portal krijgen?**

**A:** Hoewel activiteit van de Office 365 en Azure AD activiteit logboeken share Hallo directory-bronnen, als u wilt een volledige weergave van veel Hallo activiteitenlogboeken Office 365, u logboekgegevens van toohello Office 365-beheercentrum tooget Office 365-activiteit moet gaan.

---


**V: wat API's ik tooget informatie over Office 365-activiteitenlogboeken gebruiken?**

**A:** gebruik Hallo Office 365 Management-API's tooaccess hello [Office 365 activiteit logboeken via een API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**V: hoe veel records die ik vanuit Azure-portal kunt downloaden?**

**A:** kunt u downloaden van too120K records uit hello Azure-portal. Hallo-records worden gesorteerd op *meest recente* en standaard u Hallo meest recente 120 K records. 

---

**V: hoe veel records kan ik opvragen via Hallo activiteiten API?**

**A:** u kunt een query too1 miljoen records (als u geen Hallo operator top, Hallo-record te sorteren door de meeste recente). Als u Hallo 'top' operator gebruikt, kunt u een query too500K records. U kunt voorbeeldquery's op hoe Hallo toouse API hier vinden [hier](active-directory-reporting-api-getting-started.md).

---

**V: hoe krijg ik een premium-licentie**

**A:** Zie [aan de slag met Azure Active Directory Premium](active-directory-get-started-premium.md) voor een antwoord toothis vraag.

---

**V: hoe snel moet ik activiteiten gegevens ziet nadat u een premium-licentie.**

**A:** als u al activiteiten gegevens als een beschikbare licentie hebt, dan kunt u zien dezelfde gegevens Hallo. Als u geen gegevens, duurt het een of twee dagen.

---

**V: kan ik gegevens van vorige maand nadat u een Azure AD premium-licentie zien?**

**A:** als u onlangs tooa Premium-versie (met inbegrip van een evaluatieversie) hebt ingeschakeld, kunt u gegevens too7 dagen in eerste instantie zien. Wanneer gegevens stelt samen, ziet u too30 dagen.

---

**V: Er is een risicogebeurtenis in Identity Protection maar ik zie niet overeenkomende aanmelden in Hallo alle aanmeldingen. Wordt dit verwacht?**

**A:** Ja, Identity Protection resulteert risico's voor alle verificatie-overdrachten of als interactieve of niet-interactieve. Alle aanmeldingen alleen rapport geeft alleen Hallo echter interactieve aanmeldingen.

---

**V: hoe kan ik 'Gebruikers gemarkeerd voor risico' Hallo-rapport in Azure-portal downloaden?**

**A:** Hallo optie toodownload *gebruikers die zijn gemarkeerd voor risico* rapport wordt binnenkort toegevoegd.

---

**V: hoe u weten waarom een aanmeldingspagina of een gebruiker is gemarkeerd riskant in hello Azure-portal?**

**A:** Premium edition klanten voor meer informatie over de onderliggende risico's door te klikken op Hallo-gebruiker in 'Gebruikers gemarkeerd voor risico' of door te klikken op Hallo 'Riskant aanmeldingen' Hallo. Gratis en Basic-editie klanten krijgen toosee Hallo welke gebruikers en aanmeldingen zonder Hallo onderliggende gebeurtenisgegevens risico.

---

**V: hoe IP-adressen in berekend Hallo aanmeldingen en riskant aanmeldingen rapport veldnamenrij?**

**A:** IP-adressen worden uitgegeven zodanig dat er is geen definitieve verbinding tussen een IP-adres en waar Hallo-computer met dit adres zich fysiek bevindt. Dit wordt bemoeilijkt door factoren, zoals mobiele providers en VPN-verbindingen uitgeven van IP-adressen uit de centrale pools vaak zeer ver van waar het clientapparaat Hallo daadwerkelijk wordt gebruikt. Hallo bovenstaande gegeven, is conversie van fysieke locatie van IP-adres tooa een zo goed mogelijke poging op basis van traceringen, registergegevens, omgekeerde uiterlijk-ups en andere informatie. 

---
