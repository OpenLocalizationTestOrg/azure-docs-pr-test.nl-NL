---
title: Aan de slag met Azure MFA in de cloud | Microsoft Docs
description: Dit is de pagina Azure Multi-Factor Authentication waarop wordt beschreven hoe u aan de slag kunt met Azure MFA in de cloud.
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
ms.openlocfilehash: 19f3228b874fc4e37bf83388dae4341428226482
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a><span data-ttu-id="768b2-103">Aan de slag met Azure Multi-Factor Authentication in de cloud</span><span class="sxs-lookup"><span data-stu-id="768b2-103">Getting started with Azure Multi-Factor Authentication in the cloud</span></span>
<span data-ttu-id="768b2-104">In het volgende artikel staat beschreven hoe u aan de slag gaat met Azure Multi-Factor Authentication in de cloud.</span><span class="sxs-lookup"><span data-stu-id="768b2-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="768b2-105">De volgende documentatie bevat informatie over hoe u het voor gebruikers mogelijk maakt de **klassieke Azure Portal** te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="768b2-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span></span> <span data-ttu-id="768b2-106">Ga naar [Multi-Factor Authentication instellen voor Office 365](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US) als u op zoek bent naar informatie over het instellen van Azure Multi-Factor Authentication voor O365-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="768b2-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA in de Cloud](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="768b2-108">Vereiste</span><span class="sxs-lookup"><span data-stu-id="768b2-108">Prerequisite</span></span>
<span data-ttu-id="768b2-109">[U moet u aanmelden voor een Azure-abonnement](https://azure.microsoft.com/pricing/free-trial/): als u nog geen Azure-abonnement hebt, moet u er een nemen.</span><span class="sxs-lookup"><span data-stu-id="768b2-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span></span> <span data-ttu-id="768b2-110">Als u net begint en Azure MFA gebruikt, kunt u een proefabonnement nemen</span><span class="sxs-lookup"><span data-stu-id="768b2-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="768b2-111">Azure Multi-Factor Authentication inschakelen</span><span class="sxs-lookup"><span data-stu-id="768b2-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="768b2-112">Als uw gebruikers licenties hebben die Azure Multi-Factor Authentication bevatten, hoeft u niets te doen om Azure MFA in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="768b2-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="768b2-113">U kunt starten met het vereisen van verificatie in twee stappen voor afzonderlijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="768b2-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="768b2-114">De licenties die Azure MFA inschakelen zijn:</span><span class="sxs-lookup"><span data-stu-id="768b2-114">The licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="768b2-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="768b2-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="768b2-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="768b2-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="768b2-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="768b2-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="768b2-118">Als u niet een van deze drie licenties hebt, of onvoldoende licenties hebt voor alle gebruikers, is dat ook geen probleem.</span><span class="sxs-lookup"><span data-stu-id="768b2-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span></span> <span data-ttu-id="768b2-119">U hoeft dan alleen een extra stap uit te voeren en [een Multi-Factor Authentication-provider te maken](multi-factor-authentication-get-started-auth-provider.md) in uw directory.</span><span class="sxs-lookup"><span data-stu-id="768b2-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="768b2-120">Verificatie in twee stappen inschakelen voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="768b2-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="768b2-121">Gebruik een van de procedures in de sectie [Verificatie in twee stappen vereisen voor een gebruiker of groep](multi-factor-authentication-get-started-user-states.md) om aan de slag te gaan met Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="768b2-121">Use one of the procedures listed in [How to require two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) to start using Azure MFA.</span></span> <span data-ttu-id="768b2-122">U kunt ervoor kiezen om verificatie in twee stappen af te dwingen voor alle aanmeldingen of u kunt een beleid voor voorwaardelijke toegang maken om verificatie in twee stappen alleen te vereisen wanneer dit voor u belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="768b2-122">You can choose to enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when it matters to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="768b2-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="768b2-123">Next Steps</span></span>
<span data-ttu-id="768b2-124">Nu dat u Multi-Factor Authentication in de cloud hebt ingesteld, kunt u uw implementatie configureren en instellen.</span><span class="sxs-lookup"><span data-stu-id="768b2-124">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="768b2-125">Zie [Azure Multi-Factor Authentication configureren](multi-factor-authentication-whats-next.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="768b2-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

