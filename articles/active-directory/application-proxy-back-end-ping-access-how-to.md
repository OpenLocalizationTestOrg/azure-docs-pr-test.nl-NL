---
title: Het configureren van een toepassing toepassingsproxy gebruiken PingAccess | Microsoft Docs
description: Informatie over het gebruik van PingAccess uit te breiden, de voordelen van toepassingsproxy van toepassingen via verificatie op basis van een koptekst
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="f7d08-103">Het configureren van een toepassing toepassingsproxy PingAccess gebruiken</span><span class="sxs-lookup"><span data-stu-id="f7d08-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="f7d08-104">Onze samenwerking met PingAccess kunt u de voordelen van toepassingsproxy van toepassingen via verificatie op basis van een koptekst uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="f7d08-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="f7d08-105">Als uw toepassingen headers niet gebruikt, raadpleegt u onze [Single Sign-On documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) voor meer informatie over andere opties.</span><span class="sxs-lookup"><span data-stu-id="f7d08-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="f7d08-106">Overzicht van stappen en aanbevolen documenten</span><span class="sxs-lookup"><span data-stu-id="f7d08-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="f7d08-107">Voor het configureren van een toepassing met PingAccess, zijn er vier stappen:</span><span class="sxs-lookup"><span data-stu-id="f7d08-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="f7d08-108">Application Proxy Connectors configureren</span><span class="sxs-lookup"><span data-stu-id="f7d08-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="f7d08-109">Een Azure AD-toepassing Proxy-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f7d08-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="f7d08-110">& Downloaden PingAccess configureren</span><span class="sxs-lookup"><span data-stu-id="f7d08-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="f7d08-111">Toepassingen in PingAccess configureren</span><span class="sxs-lookup"><span data-stu-id="f7d08-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="f7d08-112">Zie voor meer informatie over elk van deze stappen onze [eenmalige aanmelding met koppen documentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="f7d08-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
