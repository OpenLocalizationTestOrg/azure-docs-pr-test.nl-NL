---
title: Aanmeldingen na meerdere mislukte pogingen
description: Een rapport dat gebruikers die zich heeft aangemeld na meerdere opeenvolgende aanmelding bij pogingen mislukte aangeeft.
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a>Aanmeldingen na meerdere mislukte pogingen
Dit rapport geeft aan dat gebruikers die zich heeft aangemeld na meerdere opeenvolgende aanmelding bij pogingen mislukte. Mogelijke oorzaken zijn:

* Gebruiker heeft hun wachtwoord vergeten</li><li>Gebruiker is het slachtoffer van een geslaagde wachtwoord raden brute force-aanvallen

Resultaten van deze lijst ziet u het aantal opeenvolgende mislukte aanmeldpogingen gemaakt voordat de geslaagde aanmelden en een tijdstempel die is gekoppeld aan de eerste geslaagde aanmelden.

**Instellingen rapporteren**: U kunt het minimum aantal opeenvolgende mislukte aanmelding configureren in pogingen dat optreden moeten voordat deze kan worden weergegeven in het rapport. Wanneer u wijzigingen in deze instelling aanbrengt is het belangrijk te weten dat deze wijzigingen niet worden toegepast op alle bestaande mislukte aanmelding modules die momenteel weergegeven in het bestaande rapport. Ze zullen echter worden toegepast op alle toekomstige aanmeldingen. Wijzigingen in dit rapport kunnen alleen worden gemaakt door de gelicentieerde beheerders.

![Aanmeldingen na meerdere mislukte pogingen](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

