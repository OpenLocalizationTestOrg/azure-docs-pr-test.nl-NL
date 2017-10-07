---
title: aaaHow toofind een specifieke API die nodig zijn voor een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Hoe tooconfigure Hallo machtigingen die u nodig hebt tooaccess een bepaalde API in uw aangepaste ontwikkeld voor Azure AD-toepassing
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Hoe toofind een specifieke API die nodig zijn voor een toepassing ontwikkelde aangepaste

Toegang tooAPIs vereist configuratie van toegang bereikwaarden en functies. Als u uw resource toepassing API's tooclient webtoepassingen tooexpose wilt, moet u tooconfigure toegangsbereiken en rollen voor Hallo API. Als u wilt dat een client toepassing tooaccess een web-API, moet u tooconfigure machtigingen tooaccess Hallo API in app-registratie Hallo.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configureren van een resource toepassing tooexpose-web-API 's

Bij het blootstellen van uw web-API, Hallo API worden weergegeven in Hallo **selecteert u een API** lijst bij het toevoegen van machtigingen tooan app-registratie. toegangsbereiken tooadd, stappen Hallo die worden beschreven in [tooyour resource toepassing toegang toe te voegen scopes](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configureren van een client toepassing tooaccess-web-API 's

Wanneer u de registratie van de app tooyour machtigingen toevoegt, kunt u **API toegang toevoegen** tooexposed web-API's. tooaccess web-API's, Hallo stappen die worden beschreven in [toevoegen referenties of machtigingen tooaccess web-API's](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Volgende stappen

-   [Toepassingen integreren met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Understanding hello Azure Active Directory-toepassingsmanifest](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


