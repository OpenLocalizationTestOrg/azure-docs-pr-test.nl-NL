---
title: aaaSet van een Windows 10-apparaat met Azure AD via instellingen | Microsoft Docs
description: Legt uit hoe gebruikers kunnen deelnemen aan tooAzure AD via het menu Hallo-instellingen.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="20b03-103">Instellen van een Windows 10-apparaat met Azure AD via instellingen</span><span class="sxs-lookup"><span data-stu-id="20b03-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="20b03-104">Als u al bent bijgewerkte tooWindows 10 met behulp van Windows 7 of Windows 8 en uw computer of apparaat is, kunt u deelnemen aan tooAzure Active Directory (Azure AD) via het menu Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="20b03-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="20b03-105">toojoin tooAzure AD in Hallo-instellingen</span><span class="sxs-lookup"><span data-stu-id="20b03-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="20b03-106">Van Hallo **Start** menu, klikt u op Hallo **instellingen** charm.</span><span class="sxs-lookup"><span data-stu-id="20b03-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="20b03-107">Van **instellingen**, selecteer **System**->**over**->**Azure AD Join**.</span><span class="sxs-lookup"><span data-stu-id="20b03-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="20b03-108"><center>
   ![Deelnemen aan Azure AD in Hallo-instellingen](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="20b03-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="20b03-109">Klik op **doorgaan** in hello Azure AD Join berichtvenster.</span><span class="sxs-lookup"><span data-stu-id="20b03-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="20b03-110"><center>
   ![Azure AD join berichtvenster](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="20b03-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="20b03-111">Geef uw referenties aanmelden.</span><span class="sxs-lookup"><span data-stu-id="20b03-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="20b03-112">Deze aanmeldingservaring bevat alle Hallo stappen die vereist toocomplete verificatie zijn.</span><span class="sxs-lookup"><span data-stu-id="20b03-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="20b03-113">Als u deel van een federatieve tenant uitmaken, bieden de systeembeheerder u Hallo federation-ervaring bieden die wordt gehost door uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="20b03-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="20b03-114"><center>
   ![Geef aanmeldingsreferenties](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="20b03-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="20b03-115">Als uw organisatie heeft Azure multi-factor Authentication om lid te worden tooAzure AD geconfigureerd, bieden de tweede factor Hallo voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="20b03-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="20b03-116">Klik op **accepteren** op Hallo **toestaan dit apparaat toobe beheerd** scherm.</span><span class="sxs-lookup"><span data-stu-id="20b03-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="20b03-117">U ziet het Hallo-bericht 'uw apparaat is nu lid tooyour organisatie in Azure AD'.</span><span class="sxs-lookup"><span data-stu-id="20b03-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="20b03-118">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="20b03-118">Additional information</span></span>
* <span data-ttu-id="20b03-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="20b03-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* [<span data-ttu-id="20b03-120">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="20b03-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="20b03-121">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="20b03-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="20b03-122">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="20b03-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

