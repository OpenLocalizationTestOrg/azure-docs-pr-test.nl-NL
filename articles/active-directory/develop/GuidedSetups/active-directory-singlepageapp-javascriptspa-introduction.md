---
title: aaaAzure AD v2 JS SPA begeleide Setup - Inleiding | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Hallo Microsoft Graph API aanroepen vanuit een JavaScript één pagina toepassing (SPA)

Deze handleiding wordt uitgelegd hoe een JavaScript één pagina toepassing (SPA) persoonlijk, werk kunt aanmelden en schoolaccounts, een toegangstoken ophalen en Hallo Microsoft Graph API aanroepen of andere API's waarvoor toegangstokens van hello Azure Active Directory-v2-eindpunt.

### <a name="how-this-guide-works"></a>De werking van deze handleiding

![De werking van Hallo voorbeeld-app is gegenereerd door deze handleiding](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Meer informatie

Hallo-voorbeeldtoepassing die is gemaakt door deze handleiding laat een JavaScript-SPA tooquery Hallo Microsoft Graph API of een Web-API die tokens van Azure Active Directory-v2-eindpunt accepteert. In dit scenario wordt een toegangstoken nadat een gebruiker zich aanmeldt, aangevraagde en toegevoegde tooHTTP-aanvragen via Hallo autorisatie-header. Token verkrijgen en verlenging worden afgehandeld door Hallo Microsoft Authentication Library (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Bibliotheken

Deze handleiding gebruikt Hallo bibliotheek te volgen:

|Bibliotheek|Beschrijving|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Microsoft-Verificatiebibliotheek voor JavaScript-Preview|

> [!NOTE]
> *msal.js* doelen Hallo *Azure Active Directory-v2-eindpunt* -die Hiermee privé, school- als accounts toosign in- en tokens verkrijgen. Hallo *Azure Active Directory-v2-eindpunt* heeft [enkele beperkingen](..\active-directory-v2-limitations.md). Als u alleen geïnteresseerd in school- als accounts, gebruikt *adal.js* en Hallo *V1 eindpunt*. verschillen tussen de Hallo v1- en v2-eindpunten toounderstand lezen Hallo [v1-v2 vergelijking](..\active-directory-v2-compare.md).

<!--end-collapse-->
