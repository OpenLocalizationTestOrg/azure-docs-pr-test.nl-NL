---
title: 'Azure Active Directory B2C: Multi-Factor Authentication | Microsoft Docs'
description: Hoe tooenable multi-factor Authentication in consumententoepassingen beveiligd door Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 53ef86c4-1586-45dc-9952-dbbd62f68afc
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 29beb1e6ab5d8ab5a65f9c5c068d9e71c60418dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-enable-multi-factor-authentication-in-your-consumer-facing-applications"></a>Azure Active Directory B2C: Multi-Factor Authentication in uw consumententoepassingen inschakelen
Azure Active Directory (Azure AD) B2C wordt rechtstreeks geïntegreerd met [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) zodat u een tweede beveiligingslaag beveiliging toosign-up en meld u ervaringen in uw consumententoepassingen toevoegen kunt. En u kunt dit doen zonder een één regel code te schrijven. Wij ondersteunen momenteel verificatie voor telefoongesprekken en SMS-bericht. Als u zich kunnen registreren en aanmelden beleid hebt gemaakt, kunt u nog steeds multi-factor Authentication inschakelen.

> [!NOTE]
> Multi-factor Authentication kan ook worden ingeschakeld wanneer u zich kunnen registreren en aanmelden beleidsregels, niet alleen bestaande beleidsregels bewerken.
> 
> 

Deze functie helpt u bij verwerken van scenario's zoals Hallo volgende toepassingen:

* U geen multi-factor Authentication tooaccess één toepassing vereist, maar u tooaccess hebt nodig een andere naam. Bijvoorbeeld, Hallo consumer kunt aanmelden bij een automatische verzekering toepassing met een sociale of lokale account, maar Hallo telefoonnummer moet verifiëren voordat toegang tot thuis verzekering toepassing hello geregistreerd in Hallo dezelfde directory.
* U multi-factor Authentication tooaccess een toepassing in het algemeen niet vereist, maar u tooaccess Hallo gevoelige gedeelten erin hebt nodig. Bijvoorbeeld, Hallo consumer tooa banking toepassing met een sociale of lokale account en het saldo van selectievakje kunt aanmelden, maar Hallo telefoonnummer moet verifiëren voordat u probeert een overschrijving.

## <a name="modify-your-sign-up-policy-tooenable-multi-factor-authentication"></a>Uw registratiebeleid tooenable multi-Factor Authentication wijzigen
1. [Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Klik op **Registratiebeleid**.
3. Klik op uw tooopen registratiebeleid (bijvoorbeeld ' B2C_1_SiUp') deze.
4. Klik op **multi-factor authentication** en schakel Hallo **status** te**ON**. Klik op **OK**.
5. Klik op **opslaan** Hallo boven aan het Hallo-blade.

Hallo 'Nu uitvoeren' functie kunt u op Hallo beleid tooverify Hallo consumer ervaring. Bevestig Hallo volgende:

Een klantaccount opgehaald in uw directory gemaakt voordat Hallo multi-Factor Authentication stap plaatsvindt. Tijdens het Hallo-stap Hallo consumer tooprovide zijn of haar telefoonnummer en controleer of het gevraagd. Als controle geslaagd is, Hallo telefoonnummer dat is gekoppeld toohello consumentenaccount voor later gebruik. Zelfs als consument hello wordt geannuleerd of wegvalt, hij of zij vragen tooverify een telefoonnummer opnieuw tijdens Hallo volgende keer aanmelden (met multi-factor Authentication is ingeschakeld).

## <a name="modify-your-sign-in-policy-tooenable-multi-factor-authentication"></a>Wijzigen van uw beleid voor aanmelden tooenable multi-factor Authentication
1. [Volg deze stappen toonavigate toohello B2C-functiesblade op Hallo Azure-portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Klik op **aanmelden beleid**.
3. Klik op de aanmeldingspagina beleid (bijvoorbeeld ' B2C_1_SiIn') tooopen deze. Klik op **bewerken** Hallo boven aan het Hallo-blade.
4. Klik op **multi-factor authentication** en schakel Hallo **status** te**ON**. Klik op **OK**.
5. Klik op **opslaan** Hallo boven aan het Hallo-blade.

Hallo 'Nu uitvoeren' functie kunt u op Hallo beleid tooverify Hallo consumer ervaring. Bevestig Hallo volgende:

Wanneer Hallo consumenten zich (met behulp van een sociale of lokale account) aanmeldt als een geverifieerde telefoonnummer in dat is gekoppeld toohello consumentenaccount hij of zij tooverify gevraagd deze. Als er geen telefoonnummer dat is gekoppeld, wordt Hallo consumer tooprovide een wordt gevraagd en controleer of het. Op een geslaagde verificatie Hallo telefoonnummer dat is gekoppeld toohello consumentenaccount voor later gebruik.

## <a name="multi-factor-authentication-on-other-policies"></a>Multi-factor Authentication op andere beleidsregels
Voor registratie & aanmelden beleid hierboven beschreven, is ook mogelijk tooenable meervoudige authenticatie aanmelding of een beleid voor aanmelden en het wachtwoord opnieuw instellen beleidsregels. Deze zijn beschikbaar snel op profiel bewerken van beleid.

