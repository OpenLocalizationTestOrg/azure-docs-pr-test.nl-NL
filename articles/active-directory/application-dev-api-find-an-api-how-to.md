---
title: Het zoeken van een specifieke API die nodig zijn voor een toepassing ontwikkelde aangepaste | Microsoft Docs
description: Het configureren van de machtigingen die u nodig hebt voor toegang tot een bepaalde API in uw aangepaste ontwikkeld Azure AD-toepassing
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="aa560-103">Het zoeken van een specifieke API die nodig zijn voor een toepassing ontwikkelde aangepaste</span><span class="sxs-lookup"><span data-stu-id="aa560-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="aa560-104">Toegang tot API's moeten worden geconfigureerd met toegangsbereiken en rollen.</span><span class="sxs-lookup"><span data-stu-id="aa560-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="aa560-105">Als u uw resource toepassing web-API's voor clienttoepassingen weergeven wilt, moet u toegangsscopes en -rollen configureren voor de API.</span><span class="sxs-lookup"><span data-stu-id="aa560-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="aa560-106">Als u een clienttoepassing toegang krijgt tot een web-API wilt, moet u machtigingen voor toegang tot de API in de registratie van de app te configureren.</span><span class="sxs-lookup"><span data-stu-id="aa560-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="aa560-107">Configureren van de toepassing van een resource te kunnen stellen van web-API 's</span><span class="sxs-lookup"><span data-stu-id="aa560-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="aa560-108">Bij het blootstellen van uw web-API, de API weergegeven in de **selecteert u een API** lijst bij het toevoegen van machtigingen aan een app te registreren.</span><span class="sxs-lookup"><span data-stu-id="aa560-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="aa560-109">Volg de stappen in om toe te voegen toegangsbereiken, [toegangsbereiken toe te voegen aan uw toepassing resource](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="aa560-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="aa560-110">Een clienttoepassing toegang krijgt tot de web-API's configureren</span><span class="sxs-lookup"><span data-stu-id="aa560-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="aa560-111">Als u machtigingen aan uw app-registratie toevoegen, kunt u **API toegang toevoegen** naar blootgestelde web-API's.</span><span class="sxs-lookup"><span data-stu-id="aa560-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="aa560-112">Voor toegang tot web-API's moet u de stappen [referenties of machtigingen voor toegang tot web-API's toevoegen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="aa560-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa560-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa560-113">Next steps</span></span>

-   [<span data-ttu-id="aa560-114">Toepassingen integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa560-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="aa560-115">Inzicht in de Azure Active Directory-toepassingsmanifest</span><span class="sxs-lookup"><span data-stu-id="aa560-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


