---
title: aaaAzure AD overzicht van de .NET-Protocol | Microsoft Docs
description: Hoe toouse HTTP-berichten tooauthorize toegang krijgen tot tooweb toepassingen en web-API's in uw tenant met behulp van Azure AD.
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## Uw toepassing registreren bij uw AD-tenant
Eerst moet u tooregister uw toepassing met de tenant van uw Azure Active Directory (Azure AD). Dit wordt bieden u een toepassings-ID voor uw toepassing, evenals tooreceive tokens inschakelen.

* Meld u aan toohello [Azure Portal](https://portal.azure.com).
* Kies uw Azure AD-tenant door te klikken op uw account in Hallo rechtsboven Hallo pagina.
* Klik in de linkerkant navigatiedeelvenster Hallo op **Azure Active Directory**.
* Klik op **App-registraties** en vervolgens op **Toevoegen**.
* Volg de aanwijzingen Hallo en maak een nieuwe toepassing. Dit kan een webtoepassing of een systeemeigen toepassing zijn. Voor deze zelfstudie maakt dat geen verschil. Als u behoefte hebt aan specifieke voorbeelden voor webtoepassingen of systeemeigen toepassingen, raadpleegt u onze [snelstartgidsen](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Geef voor webtoepassingen, Hallo **aanmeldings-URL** Hallo basis-URL van uw app, waarbij kunnen gebruikers zich aanmelden bijvoorbeeld is `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Voor systeemeigen toepassingen bieden een **omleidings-URI**, welke Azure AD tooreturn token antwoorden wilt gebruiken. Voer een waarde specifieke tooyour-toepassing. bijvoorbeeld`http://MyFirstAADApp`
* Zodra u inschrijving hebt voltooid, wordt Azure AD een unieke client-id van uw toepassing toewijzen, Hallo toepassing-ID. U moet deze waarde in de volgende secties hello, dus kopiëren van de pagina van de toepassing hello.
