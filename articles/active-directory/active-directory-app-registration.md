---
title: Active Directory-App-registratie aaaAzure | Microsoft Docs
description: Dit artikel wordt beschreven hoe toouse hello Azure portal tooregister een toepassing met Azure Active Directory
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Uw toepassing registreren met uw Azure Active Directory-tenant

U kunt hello Azure portal tooregister uw toepassing gebruiken met de tenant van uw Azure Active Directory (Azure AD). Dit maakt een toepassings-ID voor de toepassing hello en schakelt u deze tooreceive tokens.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. In Hallo links navigatiedeelvenster kiest **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.
4. Volg de aanwijzingen Hallo en maak een nieuwe toepassing. Als u specifieke voorbeelden voor webtoepassingen of systeemeigen toepassingen wilt, Bekijk onze [snelstartgidsen](active-directory-developers-guide.md).
  * Geef voor webtoepassingen, Hallo **aanmeldings-URL**, namelijk Hallo basis-URL van uw app, waar gebruikers bijvoorbeeld kunnen aanmelden `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Voor systeemeigen toepassingen bieden een **omleidings-URI**, welke Azure AD gebruikt tooreturn token antwoorden. Voer een waarde specifieke tooyour-toepassing. bijvoorbeeld`http://MyFirstAADApp`
5. Zodra u inschrijving hebt voltooid, wijst Azure AD van uw toepassing een unieke client-id en het Hallo-id van toepassing.

## <a name="update-application-settings-from-hello-azure-portal"></a>Toepassingsinstellingen van hello Azure-portal bijwerken

U kunt eenvoudig hello Azure-portal met een bestaande toepassing-instellingen wijzigen. U wilt mogelijk een antwoord-URL is waar Azure AD geeft token antwoorden tooconfigure. U kunt ook tooconfigure machtigingen tooother toepassingen, voor het exemplaar tooallow Hallo uw toepassing tooaccess Microsoft Graph API. U kunt alle dit via de pagina met toepassingsinstellingen Hallo doen.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. In Hallo links navigatiedeelvenster kiest **meer Services**, klikt u op **App registraties**, en kies uw toepassing uit Hallo-lijst.
4. Klik op **instellingen** tooopen van pagina met instellingen voor de toepassing hello Hallo.
  * Hallo **eigenschappen** pagina kunt u algemene informatie voor de toepassing hello Hallo wijzigen. Dit omvat de naam van de toepassing hello, Hallo aanmeldings-URL en Hallo afmelding URL.
  * Hallo **antwoord-URL's** pagina kunt u tooadd een antwoord-URL is waar Azure AD token antwoorden verzendt.
  * Hallo **eigenaars** pagina kunt u tooadd toepassingseigenaars.
  * Hallo **machtigingen** pagina kunt u machtigingen voor Hallo app tooconfigure. Bijvoorbeeld tooaccess Hallo Microsoft Graph API, klikt u op **toevoegen** en selecteer **Microsoft Graph** Kies Hallo machtiging is vereist, bijvoorbeeld in Hallo API selector **Directory-gegevens lezen** .
  * Hallo **sleutels** pagina kunt u tooadd toepassing geheimen. Hallo geheim wordt alleen weergegeven eenmaal onmiddellijk na het maken, dus zorg ervoor dat toocopy voor verdere gebruik.

## <a name="use-hello-inline-manifest-editor"></a>Hallo inline manifest-editor gebruiken

U kunt Hallo inline manifest editor toomodify bepaalde eigenschappen van toepassingen die niet rechtstreeks in beschikbaar hello Azure-portal gebruiken. Bijvoorbeeld, kunt u toomodify Hallo toepassing App ID URI of tooenable hello OAuth2.0 impliciete stroom in plaats van Hallo standaard autorisatie verlenen code stroom.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD-tenant.
3. In Hallo links navigatiedeelvenster kiest **meer Services**, klikt u op **App registraties**, en kies uw toepassing uit Hallo-lijst.
4. Klik op **Manifest** van Hallo toepassing pagina tooopen Hallo inline manifest-editor.
5. Rechtstreeks kunt u wijzigingen toohello manifest en op te slaan wanneer u klaar bent. U kunt ook Hallo manifest tooopen downloaden in uw favoriete editor en uploaden Hallo manifest bijgewerkt.

## <a name="next-steps"></a>Volgende stappen

1. Bekijk Hallo [snelstartgidsen](active-directory-developers-guide.md) voor gedetailleerde scenario's van toepassingen die verificatie met behulp van Azure AD.
2. Bekijk onze volledige lijst van de codevoorbeelden in [GitHub](https://github.com/azure-samples).
