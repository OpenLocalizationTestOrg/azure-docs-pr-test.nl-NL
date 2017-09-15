---
title: Azure AD v2 Windows Desktop aan de slag - Config | Microsoft Docs
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
ms.openlocfilehash: 1dfaa7ade664e43dcb9aa788b0197ca17e6ec4cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="2b4c5-104">Maken van een toepassing (snelle)</span><span class="sxs-lookup"><span data-stu-id="2b4c5-104">Create an application (Express)</span></span>
<span data-ttu-id="2b4c5-105">Nu gaat u naar het registreren van uw toepassing in de *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="2b4c5-105">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="2b4c5-106">Registreren van uw toepassingen via de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="2b4c5-106">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="2b4c5-107">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="2b4c5-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="2b4c5-108">Zorg ervoor dat de optie voor begeleide Setup is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="2b4c5-108">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="2b4c5-109">Volg de instructies voor het verkrijgen van de toepassings-ID en plak deze in uw code</span><span class="sxs-lookup"><span data-stu-id="2b4c5-109">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="2b4c5-110">De registratiegegevens van uw toepassing toevoegen aan uw oplossing (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="2b4c5-110">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="2b4c5-111">Nu gaat u naar het registreren van uw toepassing in de *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="2b4c5-111">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="2b4c5-112">Ga naar de [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) een toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="2b4c5-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="2b4c5-113">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="2b4c5-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="2b4c5-114">Zorg ervoor dat de optie voor begeleide Setup is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="2b4c5-114">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="2b4c5-115">Klik op `Add Platform`, selecteer daarna `Native Application` en klik op Opslaan</span><span class="sxs-lookup"><span data-stu-id="2b4c5-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="2b4c5-116">Kopiëren van de GUID in toepassings-ID, gaat u terug naar Visual Studio, open `App.xaml.cs` en vervang `your_client_id_here` met de toepassings-ID die u zojuist hebt geregistreerd:</span><span class="sxs-lookup"><span data-stu-id="2b4c5-116">Copy the GUID in Application ID, go back to Visual Studio, open `App.xaml.cs` and replace `your_client_id_here` with the Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
