---
title: "Active Directory implementatiemodel Playbook ingrediënten aaaAzure | Microsoft Docs"
description: Verkennen en snel implementeren scenario's voor Identity and Access Management
services: active-directory
keywords: Azure active directory, playbook, Proof-of-Concept, implementatiemodel
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a>Azure Active Directory-bewijs van Concept Playbook ingrediënten 

## <a name="theme"></a>Thema
Azure AD levert de oplossingen voor identiteits- en toegangsbeheer via meerdere gebieden in de onderneming Hallo. We classificeren Hallo scenario's in Hallo gebieden te volgen: 

* [Veel apps, één identiteit](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [De beveiliging verbeteren](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [Schaal met selfservice](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

Voor het definiëren van een thema tooframe Hallo implementatiemodel helpt toofocus Hallo inspanningen die binnen met zakelijke doelstellingen die vaak ook Hallo triggers van Hallo interesse in een POC in de eerste plaats Hallo zijn. 

## <a name="environment"></a>Omgeving

Het is belangrijk toodetermine Hallo details van Hallo-omgeving waarin u Hallo implementatiemodel levert. U kunt in het ideale geval bouwen voort op deze na Hallo die POC-fase is voltooid. Hallo doelomgeving is van cruciaal belang en vindt u de juiste balans Hallo tussen deze als echte mogelijk en Hallo overhead van beperkingen of extra overwegingen. Hallo typische omgevingen voor POC's zijn:
* **Productie:** Hallo scenario's zullen worden uitgevoerd in uw productieomgeving en Microsoft Cloud-services (productie AD, Office 365, Azure AD-tenant/SSO oplossing) al is geïmplementeerd. 
* **Gebruiker acceptatie testen (UAT) / Dev-omgeving:** u test-infrastructuur hebt (parallelle AD en mogelijk Azure AD-tenant/SSO oplossing) met testgegevens dat lijkt op productie. Normaal gesproken worden Hallo testomgeving verdeeld over meerdere projecten in Hallo onderneming.

De meeste scenario's in deze handleiding zijn additieve aard. Als gevolg hiervan kunnen ze worden geïmplementeerd in productie-tenant Hallo zonder gebruikers buiten Hallo implementatiemodel. In dit document bellen we uit welke scenario's tenant wide gevolgen zou hebben. U kunt in deze gevallen tooconsider een niet-productieomgeving. 


## <a name="target-users"></a>Doelgebruikers

Het is belangrijk toodetermine Hallo doel reeks gebruikers die Hallo scenario's, oefent vooral wanneer Hallo-omgeving testomgeving is. Hallo categorieën van doelgebruikers voor implementatiemodel zijn:
* **Testgebruikers:** taakfuncties echte gebruikers in Hallo-omgeving die Hallo-oplossing gaat gebruiken met Hallo account ze voor hun tooday dag gebruiken
* **Testgebruikers:** accounts die zijn gemaakt in Hallo omgeving testen 

De meeste scenario's in deze handleiding kunnen worden uitgeoefend door testgebruikers. In dit document zullen we contact uit doel gebruiker overwegingen indien nodig.


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]