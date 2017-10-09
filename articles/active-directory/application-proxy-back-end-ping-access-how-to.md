---
title: aaaHow tooconfigure een toepassingsproxy toepassing toouse PingAccess | Microsoft Docs
description: Meer informatie over hoe toouse PingAccess tooextend Hallo voordelen van toepassingsproxy tooapplications verificatie op basis van een koptekst
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fa4c9747b7bf5a135425be270e4f7eadf95248fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-pingaccess"></a><span data-ttu-id="8cb6c-103">Hoe een toepassingsproxy toepassing toouse PingAccess tooconfigure</span><span class="sxs-lookup"><span data-stu-id="8cb6c-103">How tooconfigure an Application Proxy application toouse PingAccess</span></span>

<span data-ttu-id="8cb6c-104">Onze samenwerking met PingAccess kunt u tooextend Hallo voordelen van toepassingsproxy tooapplications verificatie op basis van header.</span><span class="sxs-lookup"><span data-stu-id="8cb6c-104">Our collaboration with PingAccess now allows you tooextend hello benefits of Application Proxy tooapplications using header-based authentication.</span></span> <span data-ttu-id="8cb6c-105">Als uw toepassingen headers niet gebruikt, raadpleegt u onze [Single Sign-On documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) voor meer informatie over andere opties.</span><span class="sxs-lookup"><span data-stu-id="8cb6c-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="8cb6c-106">Overzicht van stappen en aanbevolen documenten</span><span class="sxs-lookup"><span data-stu-id="8cb6c-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="8cb6c-107">tooconfigure een toepassing met PingAccess, er zijn vier stappen:</span><span class="sxs-lookup"><span data-stu-id="8cb6c-107">tooconfigure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="8cb6c-108">Application Proxy Connectors configureren</span><span class="sxs-lookup"><span data-stu-id="8cb6c-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="8cb6c-109">Een Azure AD-toepassing Proxy-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="8cb6c-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="8cb6c-110">& Downloaden PingAccess configureren</span><span class="sxs-lookup"><span data-stu-id="8cb6c-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="8cb6c-111">Toepassingen in PingAccess configureren</span><span class="sxs-lookup"><span data-stu-id="8cb6c-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="8cb6c-112">Zie voor meer informatie over elk van deze stappen onze [eenmalige aanmelding met koppen documentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="8cb6c-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
