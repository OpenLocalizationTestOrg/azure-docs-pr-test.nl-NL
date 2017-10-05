---
title: Azure AD v2 Windows Desktop aan de slag - Config | Microsoft Docs
description: Hoe een toepassing .NET Windows-bureaublad (XAML) ophalen van een toegangstoken en een API die wordt beveiligd door Azure Active Directory-v2-eindpunt niet aanroepen.
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
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="182bc-103">De registratiegegevens van de toepassing toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="182bc-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="182bc-104">In deze stap moet u de toepassings-Id toevoegen aan uw project.</span><span class="sxs-lookup"><span data-stu-id="182bc-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="182bc-105">Open `App.xaml.cs` en vervang de regel die de `ClientId` met:</span><span class="sxs-lookup"><span data-stu-id="182bc-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="182bc-106">Wat is de volgende</span><span class="sxs-lookup"><span data-stu-id="182bc-106">What is Next</span></span>

[<span data-ttu-id="182bc-107">Testen en valideren</span><span class="sxs-lookup"><span data-stu-id="182bc-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
