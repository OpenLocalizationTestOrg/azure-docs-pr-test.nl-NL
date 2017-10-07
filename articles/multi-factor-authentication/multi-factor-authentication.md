---
title: aaaLearn over verificatie in twee stappen in de Azure MFA | Microsoft Docs
description: 'Wat is Azure multi-factor Authentication, MFA, meer informatie over Hallo multi-factor Authentication-client en de verschillende methoden Hallo en versies die beschikbaar zijn waarom gebruiken. '
keywords: Inleiding tooMFA mfa overzicht, wat is mfa
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>Wat is Azure Multi-Factor Authentication?
Verificatie in twee stappen is een authenticatiemethode die meer dan één verificatiemethode is vereist en voegt een cruciale tweede beveiligingslaag van beveiliging toouser aanmeldingen en transacties. Het werkt door te vereisen van twee of meer van Hallo verificatiemethoden te volgen:

* Iets u weet (doorgaans een wachtwoord)
* Iets er (een vertrouwd apparaat die niet eenvoudig wordt gedupliceerd, zoals een telefoon)
* Iets dat u (biometrie)

<center>![Gebruikersnaam en wachtwoord](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![certificaten](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![smartcard](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![virtuele smartcard](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![gebruikersnaam en wachtwoord](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) is een Microsoft-oplossing voor verificatie in twee stappen. Azure MFA helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Het biedt krachtige verificatie via een reeks verificatiemethoden waaronder verificatie per telefoon, sms of mobiele app.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Waarom Azure multi-factor Authentication gebruiken?
Vandaag de dag, meer dan ooit, zijn er steeds meer mensen verbonden. Met slim telefoons, tablets, laptops en pc's hebben mensen verschillende opties op hoe ze tooconnect gaat en blijf op elk gewenst moment. Gebruikers hebben toegang tot hun accounts en toepassingen vanaf elke locatie, wat betekent dat ze kunnen meer werk gedaan te krijgen en hun klanten fungeren beter.

Azure multi-factor Authentication is een eenvoudig toouse, schaalbare en betrouwbare oplossing die biedt een tweede methode voor verificatie zodat uw gebruikers zijn altijd is beveiligd.

| ![Eenvoudig tooUse](./media/multi-factor-authentication/simple.png) | ![Schaalbaar](./media/multi-factor-authentication/scalable.png) | ![Altijd is beveiligd](./media/multi-factor-authentication/protected.png) | ![Betrouwbaar](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Eenvoudig toouse** |**Schaalbare** |**Altijd is beveiligd** |**Betrouwbare** |

* **Eenvoudig tooUse** -Azure multi-factor Authentication is eenvoudig tooset up en gebruiken. Hallo kunt extra beveiliging die wordt geleverd met Azure multi-factor Authentication toomanage gebruikers hun eigen apparaten. Beste van alle in veel gevallen deze kan worden ingesteld met een paar eenvoudige klikken.
* **Schaalbare** -Azure multi-factor Authentication Hallo power van Hallo cloud gebruikt en kan worden geïntegreerd met uw on-premises AD en aangepaste apps. Deze beveiliging is zelfs uitgebreid tooyour hoog volume essentiële scenario's.
* **Altijd is beveiligd** -Azure multi-factor Authentication sterke verificatie met behulp van de hoogste industrienormen Hallo biedt.
* **Betrouwbare** -wordt gegarandeerd dat de beschikbaarheid van 99,9% van de Azure multi-factor Authentication. Hallo service wordt beschouwd als niet beschikbaar wanneer geen verzoeken voor de verificatie in twee stappen Hallo tooreceive of proces.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [de werking van Azure multi-factor Authentication](multi-factor-authentication-how-it-works.md)

- Meer informatie over andere Hallo [versies en verbruikmethoden voor Azure multi-factor Authentication](multi-factor-authentication-versions-plans.md)
