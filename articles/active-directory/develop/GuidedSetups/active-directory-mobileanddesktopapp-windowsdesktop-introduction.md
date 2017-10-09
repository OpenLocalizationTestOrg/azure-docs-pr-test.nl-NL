---
title: aaaAzure AD v2 Windows Desktop aan de slag - Inleiding | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Hallo Microsoft Graph API aanroepen vanuit een Windows-bureaublad-app

Deze handleiding wordt uitgelegd hoe een systeemeigen Windows Desktop .NET (XAML)-toepassing kunt ophalen van een toegangstoken en Microsoft Graph API of andere API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt niet aanroepen.

Aan het einde van de Hallo van deze handleiding, uw toepassing wordt kunnen toocall worden een beveiligde API met persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts van een bedrijf of organisatie die Azure Active Directory heeft.  

> Deze handleiding is Visual Studio 2015 Update 3 of Visual Studio 2017 vereist.  Hebt u geen deze? [Visual Studio 2017 gratis downloaden](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>De werking van deze handleiding

![De werking van deze handleiding](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

Hallo-voorbeeldtoepassing die is gemaakt door deze handleiding kunt een Windows-bureaubladtoepassingen tooquery Microsoft Graph API of een Web-API die tokens van Azure Active Directory-v2-eindpunt accepteert. In dit scenario wordt een token tooHTTP-aanvragen via de autorisatie-header Hallo toegevoegd. Token verkrijgen en verlenging wordt verwerkt door Hallo Microsoft Authentication Library (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Afhandeling van token verkrijgen voor toegang tot Web-API's beveiligd

Nadat Hallo gebruiker zich verifieert, ontvangt de voorbeeldtoepassing Hallo een token dat gebruikt tooquery Microsoft Graph API of een Web-API worden beveiligd door Microsoft Azure Active Directory-v2 worden kan.

API's, zoals Microsoft Graph vereisen een access token tooallow toegang tot specifieke bronnen – bijvoorbeeld tooread een gebruikersprofiel, toegang tot de agenda gebruiker of een e-mailbericht verzenden. Uw toepassing kan een toegangstoken MSAL tooaccess met deze resources aanvragen door op te geven van de API-scopes. Deze toegangstoken is toegevoegd toohello HTTP-autorisatie-header voor elke aanroep ten opzichte van Hallo beveiligde resource. 

MSAL kunt opslaan in cache en vernieuwen toegangstokens voor u, zodat uw toepassing niet te hoeft beheren.


### <a name="nuget-packages"></a>NuGet-pakketten

Deze handleiding gebruikt Hallo NuGet-pakketten te volgen:

|Bibliotheek|Beschrijving|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Microsoft-Verificatiebibliotheek (MSAL)|

