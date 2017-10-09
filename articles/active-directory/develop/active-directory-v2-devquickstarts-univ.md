---
title: aaaAzure AD v2.0 universele Windows-App | Microsoft Docs
description: Hoe toobuild een universele Windows-app die zich aanmeldt gebruikers met beide persoonlijke Microsoft-Account en werk- of schoolaccount accounts.
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: d2c92b65-3c1d-46d1-81c8-88f32f6b2c4b
ms.service: active-directory
ms.workload: identity
ms.topic: article
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.date: 02/20/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 49b26c74fa5a76664c3229256c9bd128563b830c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-universal-app-using-hello-v20-endpoint"></a><span data-ttu-id="7e16e-103">Aanmelden tooa universele Windows-app met behulp van Hallo v2.0-eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="7e16e-103">Add sign-in tooa Windows Universal app using hello v2.0 endpoint</span></span>
  <span data-ttu-id="7e16e-104">Hallo snel starten-zelfstudie voor Windows universele apps niet erg gereed... Controleer of terug snel & zoekt u naar updates @AzureAD op Twitter.</span><span class="sxs-lookup"><span data-stu-id="7e16e-104">hello quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="7e16e-105">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="7e16e-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="7e16e-106">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7e16e-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="7e16e-107">We raden u meldingen van wanneer er beveiligingsincidenten door bezoeken optreden tooget [deze pagina](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="7e16e-107">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

