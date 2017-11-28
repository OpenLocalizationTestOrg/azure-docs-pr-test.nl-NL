---
title: aaaGet Azure MFA in de cloud Hallo gestart | Microsoft Docs
description: Dit is Hallo Microsoft Azure multi-factor authentication-pagina waarop wordt beschreven hoe tooget met Azure MFA in de cloud Hallo gestart.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="af4ed-103">Aan de slag met Azure multi-factor Authentication in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="af4ed-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="af4ed-104">In dit artikel wordt uitgelegd hoe tooget gestart met behulp van Azure multi-factor Authentication in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="af4ed-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="af4ed-105">Hallo volgende documentatie bevat informatie over hoe gebruikers in tooenable Hallo **klassieke Azure-Portal**.</span><span class="sxs-lookup"><span data-stu-id="af4ed-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="af4ed-106">Als u naar informatie over het zoekt tooset van Azure multi-factor Authentication voor O365-gebruikers, Zie [instellen van multi-factor authentication voor Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="af4ed-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA in Hallo Cloud](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="af4ed-108">Vereiste</span><span class="sxs-lookup"><span data-stu-id="af4ed-108">Prerequisite</span></span>
<span data-ttu-id="af4ed-109">[Aanmelden voor een Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/) -als u nog geen Azure-abonnement, moet u toosign-up voor een.</span><span class="sxs-lookup"><span data-stu-id="af4ed-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="af4ed-110">Als u net begint en Azure MFA gebruikt, kunt u een proefabonnement nemen</span><span class="sxs-lookup"><span data-stu-id="af4ed-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="af4ed-111">Azure Multi-Factor Authentication inschakelen</span><span class="sxs-lookup"><span data-stu-id="af4ed-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="af4ed-112">Zolang uw gebruikers beschikken over licenties met Azure multi-factor Authentication, is er niets hoeft toodo tooturn op Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="af4ed-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="af4ed-113">U kunt starten met het vereisen van verificatie in twee stappen voor afzonderlijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="af4ed-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="af4ed-114">Hallo-licenties die Azure MFA inschakelen zijn:</span><span class="sxs-lookup"><span data-stu-id="af4ed-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="af4ed-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="af4ed-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="af4ed-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="af4ed-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="af4ed-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="af4ed-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="af4ed-118">Als u niet een van deze drie licenties hebt, of u niet voldoende licenties toocover hebt alle gebruikers, dat te ok.</span><span class="sxs-lookup"><span data-stu-id="af4ed-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="af4ed-119">U hoeft alleen toodo een extra stap en [maken van een multi-factor Authentication-Provider](multi-factor-authentication-get-started-auth-provider.md) in uw directory.</span><span class="sxs-lookup"><span data-stu-id="af4ed-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="af4ed-120">Verificatie in twee stappen inschakelen voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="af4ed-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="af4ed-121">Gebruik een van Hallo procedures die worden vermeld in [hoe verificatie van toorequire in twee stappen voor een gebruiker of groep](multi-factor-authentication-get-started-user-states.md) toostart Azure MFA gebruiken.</span><span class="sxs-lookup"><span data-stu-id="af4ed-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="af4ed-122">U kunt verificatie van tooenforce in twee stappen voor alle aanmeldingen of kunt u verificatie van voorwaardelijk beleid toorequire in twee stappen alleen wanneer deze tooyou is van belang.</span><span class="sxs-lookup"><span data-stu-id="af4ed-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af4ed-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af4ed-123">Next Steps</span></span>
<span data-ttu-id="af4ed-124">Nu dat u Azure multi-factor Authentication in de cloud Hallo hebt ingesteld, kunt u configureren en instellen van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="af4ed-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="af4ed-125">Zie [Azure Multi-Factor Authentication configureren](multi-factor-authentication-whats-next.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="af4ed-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

