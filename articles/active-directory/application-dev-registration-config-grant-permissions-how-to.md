---
title: aaaHow toogrant machtigingen tooa ontwikkeld met een aangepaste toepassing | Microsoft Docs
description: Hoe gebruikt door toogrant machtigingen tooyour ontwikkeld met een aangepaste toepassing hello Azure AD-portal of een URL-parameter
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="22f02-103">Hoe toogrant machtigingen tooa aangepaste ontwikkelde toepassing</span><span class="sxs-lookup"><span data-stu-id="22f02-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="22f02-104">Als u wilt dat optie preventief toogrant toestemming van uw app of worden uitgevoerd in een fout dat u tooan app geen toestemming hebt gegeven, kunt u onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="22f02-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="22f02-105">Hoe tooperform-beheerder toestemming voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="22f02-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="22f02-106">Dit heeft Hallo effect voor het verlenen van toestemming toohello-toepassing voor alle gebruikers in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="22f02-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="22f02-107">Navigeer toohello **App registraties** blade als een **hoofdbeheerder**, selecteer daarna Hallo app.</span><span class="sxs-lookup"><span data-stu-id="22f02-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="22f02-108">Selecteer **Required Permissions**, en klik tot slot op Hallo **machtiging verlenen** knop Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="22f02-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="22f02-109">U kunt ook kunt u een aanvraag te maken*login.microsoftonline.com* met de configuraties van uw app en toe te voegen op *& vragen = admin\_toestemming*.</span><span class="sxs-lookup"><span data-stu-id="22f02-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="22f02-110">Na het aanmelden met beheerdersreferenties, heeft Hallo app gekregen toestemming voor alle gebruikers.</span><span class="sxs-lookup"><span data-stu-id="22f02-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="22f02-111">Hoe tooforce gebruiker toestemming geven voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="22f02-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="22f02-112">Toevoegen op auth-aanvragen *& vragen toestemming =* die eindgebruikers tooconsent vereisen telkens wanneer ze verifiëren.</span><span class="sxs-lookup"><span data-stu-id="22f02-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22f02-113">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22f02-113">Next steps</span></span>

[<span data-ttu-id="22f02-114">TooAzureAD toestemming en integratie van Apps</span><span class="sxs-lookup"><span data-stu-id="22f02-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="22f02-115">Toestemming en rollen voor AzureAD v2.0 geconvergeerde Apps</span><span class="sxs-lookup"><span data-stu-id="22f02-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="22f02-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="22f02-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
