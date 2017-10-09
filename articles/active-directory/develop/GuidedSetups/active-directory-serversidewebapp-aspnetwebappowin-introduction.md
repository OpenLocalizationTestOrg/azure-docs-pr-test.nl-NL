---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - Inleiding | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Aanmelden met Microsoft tooan ASP.NET-web-app toevoegen

Deze handleiding wordt uitgelegd hoe tooimplement aanmelden bij Microsoft met behulp van een ASP.NET MVC-oplossing met een traditioneel browser gebaseerde webtoepassing met OpenID Connect. 

Aan het einde van de Hallo van deze handleiding, wordt uw toepassing kunnen tooaccept aanmelding modules van persoonlijke accounts (inclusief outlook.com, live.com en anderen), evenals werken en schoolaccounts zijn uit een bedrijf of organisatie die is geïntegreerd met Azure Active Directory. 

> Deze handleiding is Visual Studio 2015 Update 3 of Visual Studio 2017 vereist.  Hebt u geen deze?  [Visual Studio 2017 gratis downloaden](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>De werking van deze handleiding

![De werking van deze handleiding](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Deze handleiding is gebaseerd op Hallo scenario waarbij een browser toegang heeft tot een ASP.NET-website aanvragen van een gebruiker tooauthenticate via een knop aanmelden. In dit scenario wordt de meeste Hallo werk toorender Hallo-webpagina op Hallo serverzijde plaats.

## <a name="libraries"></a>Bibliotheken

Deze handleiding gebruikt Hallo bibliotheken te volgen:

|Bibliotheek|Beschrijving|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Middleware waarmee een toepassing toouse OpenIdConnect voor verificatie|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Middleware waarmee een toepassing toomaintain gebruikerssessie met behulp van cookies|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Hiermee toorun OWIN-toepassingen op IIS met ASP.NET-aanvraag pipeline-Hallo|

