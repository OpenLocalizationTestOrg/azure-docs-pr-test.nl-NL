---
title: aaaAzure AD v2 iOS Getting Started - Inleiding | Microsoft Docs
description: Hoe iOS (Swift)-toepassingen met een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Hallo Microsoft Graph API aanroepen vanuit een iOS-app

Deze handleiding wordt uitgelegd hoe een systeemeigen iOS-toepassing (Swift) kan een toegangstoken ophalen en roep Hallo Microsoft Graph API of andere API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt.

Aan het einde van de Hallo van deze handleiding, uw toepassing wordt kunnen toocall worden een beveiligde API met persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts van een bedrijf of organisatie die Azure Active Directory heeft.

> ### <a name="pre-requisites"></a>Vereisten
> - XCode 8.x is vereist voor deze handleiding. U kunt downloaden XCode [hiervandaan](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode downloaden URL").
> - [Carthage](https://github.com/Carthage/Carthage) voor het beheer van het pakket

### <a name="how-this-guide-works"></a>De werking van deze handleiding

![De werking van deze handleiding](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

Hallo-voorbeeldtoepassing die is gemaakt door deze handleiding kunt een iOS-toepassing tooquery Hallo Microsoft Graph API of een Web-API die tokens van Azure Active Directory-v2-eindpunt accepteert. In dit scenario wordt een token tooHTTP-aanvragen via de autorisatie-header Hallo toegevoegd. Token verkrijgen en verlenging wordt verwerkt door Hallo Microsoft Authentication Library (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Afhandeling van token verkrijgen voor toegang tot Web-API's beveiligd

Nadat Hallo gebruiker zich verifieert, ontvangt de voorbeeldtoepassing Hallo een token dat worden kan gebruikt tooquery Hallo Microsoft Graph API of een Web-API worden beveiligd door Microsoft Azure Active Directory-v2.

API's, zoals Microsoft Graph vereisen een access token tooallow toegang tot specifieke bronnen – bijvoorbeeld tooread een gebruikersprofiel, toegang tot de agenda gebruiker of een e-mailbericht verzenden. Uw toepassing kan een toegangstoken MSAL door te geven van de API-scopes met aanvragen. Deze toegangstoken is toegevoegd toohello HTTP-autorisatie-header voor elke aanroep ten opzichte van Hallo beveiligde resource.

MSAL kunt opslaan in cache en vernieuwen toegangstokens voor u, zodat uw toepassing niet te hoeft beheren.


### <a name="nuget-packages"></a>NuGet-pakketten

Deze handleiding gebruikt Hallo NuGet-pakketten te volgen:

|Bibliotheek|Beschrijving|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Preview van Microsoft verificatie-bibliotheek voor iOS|

