---
title: Azure AD v2.0 universele Windows-App | Microsoft Docs
description: Het bouwen van een universele Windows-app die gebruikers met beide persoonlijke Microsoft-Account en werk-of schoolaccounts ondertekent.
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
ms.openlocfilehash: 369802f1a42b8720aa730d5ac7e5576ed20eeddf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-universal-app-using-the-v20-endpoint"></a><span data-ttu-id="34acd-103">Aanmelden met toevoegt aan een universele Windows-app het v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="34acd-103">Add sign-in to a Windows Universal app using the v2.0 endpoint</span></span>
  <span data-ttu-id="34acd-104">Snel starten-zelfstudie voor Windows universele apps niet erg gereed... Controleer of terug snel & zoekt u naar updates @AzureAD op Twitter.</span><span class="sxs-lookup"><span data-stu-id="34acd-104">The quick-start tutorial for Windows Universal apps isn't quite ready... Check back soon & look for updates from @AzureAD on Twitter.</span></span>

> [!NOTE]
> <span data-ttu-id="34acd-105">Niet alle Azure Active Directory-scenario's en functies worden ondersteund door het v2.0-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="34acd-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="34acd-106">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="34acd-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

    ## Get security updates for our products

<span data-ttu-id="34acd-107">We raden u aan in te stellen dat u meldingen ontvangt wanneer er beveiligingsincidenten optreden. Ga hiervoor naar [deze pagina](https://technet.microsoft.com/security/dd252948) en abonneer u op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="34acd-107">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

