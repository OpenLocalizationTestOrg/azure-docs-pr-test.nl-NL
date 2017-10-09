---
title: aaaAzure AD v2 Android aan de slag - Inleiding | Microsoft Docs
description: Hoe een Android-app kunt ophalen van een toegangstoken en Microsoft Graph API of API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Hallo Microsoft Graph API aanroepen vanuit een Android-app

Deze handleiding wordt uitgelegd hoe een systeemeigen Android-toepassing kunt ophalen van een toegangstoken en Microsoft Graph API of andere API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt niet aanroepen.

Aan het einde van de Hallo van deze handleiding, uw toepassing wordt kunnen toocall worden een beveiligde API met persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts van een bedrijf of organisatie die Azure Active Directory heeft.  

### <a name="how-this-sample-works"></a>De werking van dit voorbeeld
![De werking van dit voorbeeld](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

Hallo-voorbeeld gemaakt door deze handleiding is gebaseerd op een scenario waarbij een Android-toepassing gebruikte tooquery een Web-API die tokens van Azure Active Directory v2-eindpunt: in dit geval Microsoft Graph API accepteert. In dit scenario wordt een token tooHTTP-aanvragen via de autorisatie-header Hallo toegevoegd. Token verkrijgen en verlenging wordt verwerkt door Hallo Microsoft Authentication Library (MSAL).

### <a name="pre-requisites"></a>Vereisten
* Deze Begeleide instelprocedure is gericht op Android Studio, maar ook alle andere Android-toepassing-ontwikkelomgeving aanvaardbaar is. 
* Android SDK 21 of hoger is vereist (25 SDK wordt aanbevolen).
* Google Chrome of een webbrowser met de tabbladen voor aangepaste is vereist voor deze release van Microsoft Authentication Library (MSAL) voor Android.

> Opmerking: Google Chrome is niet opgenomen in Visual Studio-Emulator voor Android. We raden u tootest deze code die met Google Chrome geïnstalleerd op een Emulator met 25 API of een afbeelding met API-21 of hoger.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Hoe toohandle token overname tooaccess beveiligde Web-API

Nadat Hallo gebruiker zich verifieert, ontvangt de voorbeeldtoepassing Hallo een token dat gebruikt tooquery Microsoft Graph API of een Web-API worden beveiligd door Microsoft Azure Active Directory-v2 worden kan.

API's, zoals Microsoft Graph vereisen een access token tooallow toegang tot specifieke bronnen – bijvoorbeeld tooread een gebruikersprofiel, toegang tot de agenda gebruiker of een e-mailbericht verzenden. Uw toepassing kan een toegangstoken MSAL tooaccess met deze resources aanvragen door op te geven van de API-scopes. Deze toegangstoken is toegevoegd toohello HTTP-autorisatie-header voor elke aanroep ten opzichte van Hallo beveiligde resource. 

MSAL kunt opslaan in cache en vernieuwen toegangstokens voor u, zodat uw toepassing niet te hoeft beheren.

### <a name="libraries"></a>Bibliotheken

Deze handleiding gebruikt Hallo bibliotheken te volgen:

|Bibliotheek|Beschrijving|
|---|---|
|[com.Microsoft.Identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Microsoft-Verificatiebibliotheek (MSAL)|
