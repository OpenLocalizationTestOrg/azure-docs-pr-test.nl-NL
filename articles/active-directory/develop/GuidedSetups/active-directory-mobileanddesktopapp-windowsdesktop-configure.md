---
title: aaaAzure AD v2 Windows Desktop aan de slag - Config | Microsoft Docs
description: Hoe een toepassing .NET Windows-bureaublad (XAML) ophalen van een toegangstoken en een API die wordt beveiligd door Azure Active Directory-v2-eindpunt niet aanroepen. | Microsoft Azure | Microsoft Azure
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="c19a6-104">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="c19a6-104">Create an application (Express)</span></span>
<span data-ttu-id="c19a6-105">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="c19a6-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="c19a6-106">Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="c19a6-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="c19a6-107">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="c19a6-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="c19a6-108">Zorg ervoor dat de optie Hallo voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="c19a6-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="c19a6-109">Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code</span><span class="sxs-lookup"><span data-stu-id="c19a6-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="c19a6-110">Toevoegen van uw toepassing registratie informatie tooyour oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="c19a6-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="c19a6-111">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="c19a6-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="c19a6-112">Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing</span><span class="sxs-lookup"><span data-stu-id="c19a6-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="c19a6-113">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="c19a6-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="c19a6-114">Zorg ervoor dat de optie Hallo voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="c19a6-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="c19a6-115">Klik op `Add Platform`, selecteer daarna `Native Application` en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="c19a6-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="c19a6-116">Hallo GUID kopiëren in toepassings-ID, gaat u terug tooVisual Studio open `App.xaml.cs` en vervang `your_client_id_here` Hello toepassings-ID die u zojuist hebt geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="c19a6-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
