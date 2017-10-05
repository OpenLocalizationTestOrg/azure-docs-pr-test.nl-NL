---
title: Aan de slag met Azure AD in Visual Studio WebApi projecten | Microsoft Docs
description: Hoe u aan de slag met Azure Active Directory in WebApi projecten nadat verbinding maken met of maken van een Azure AD met Visual Studio services verbonden
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="d37f5-103">Aan de slag met Azure Active Directory en Visual Studio verbonden services (WebApi-projecten)</span><span class="sxs-lookup"><span data-stu-id="d37f5-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d37f5-104">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="d37f5-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="d37f5-105">Wat is er gebeurd</span><span class="sxs-lookup"><span data-stu-id="d37f5-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="d37f5-106">Verificatie te vereisen voor toegang tot domeincontrollers</span><span class="sxs-lookup"><span data-stu-id="d37f5-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="d37f5-107">Alle domeincontrollers in uw project zijn adorned met de **autoriseren** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="d37f5-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="d37f5-108">Dit kenmerk moet de gebruiker moet worden geverifieerd voordat toegang tot de API's die door deze domeincontrollers gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="d37f5-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="d37f5-109">Verwijder dit kenmerk van de controller zodat de controller voor anonieme toegang.</span><span class="sxs-lookup"><span data-stu-id="d37f5-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="d37f5-110">Als u de machtigingen instelt op een meer gedetailleerd niveau wilt, toepassen van het kenmerk voor elke methode waarvoor de autorisatie in plaats van aan de controllerklasse toepast.</span><span class="sxs-lookup"><span data-stu-id="d37f5-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d37f5-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d37f5-111">Next steps</span></span>
[<span data-ttu-id="d37f5-112">Meer informatie over Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d37f5-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

