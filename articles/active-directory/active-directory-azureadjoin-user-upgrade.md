---
title: Instellen van een Windows 10-apparaat met Azure AD via instellingen | Microsoft Docs
description: Legt uit hoe gebruikers kunnen toevoegen aan Azure AD via het menu instellingen.
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="e5ff0-103">Instellen van een Windows 10-apparaat met Azure AD via instellingen</span><span class="sxs-lookup"><span data-stu-id="e5ff0-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="e5ff0-104">Als u al Windows 7 of Windows 8 gebruikt en uw computer of apparaat is bijgewerkt naar Windows 10, kunt u koppelen aan Azure Active Directory (Azure AD) via het menu instellingen.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="e5ff0-105">Koppelen aan Azure AD in het menu instellingen</span><span class="sxs-lookup"><span data-stu-id="e5ff0-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="e5ff0-106">Van de **Start** menu, klikt u op de **instellingen** charm.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="e5ff0-107">Van **instellingen**, selecteer **System**->**over**->**Azure AD Join**.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="e5ff0-108"><center>
   ![Deelnemen aan Azure AD in het menu instellingen](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="e5ff0-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="e5ff0-109">Klik op **doorgaan** in het venster Azure AD Join-bericht.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="e5ff0-110"><center>
   ![Azure AD join berichtvenster](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="e5ff0-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="e5ff0-111">Geef uw referenties aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="e5ff0-112">Deze aanmeldingservaring bevat de stappen die nodig voor de volledige verificatie zijn.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="e5ff0-113">Als u deel van een federatieve tenant uitmaken, bieden de systeembeheerder u met de federation-ervaring die wordt gehost door uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="e5ff0-114"><center>
   ![Geef aanmeldingsreferenties](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="e5ff0-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="e5ff0-115">Als uw organisatie is Azure multi-factor Authentication om lid te worden naar Azure AD geconfigureerd, geeft u de tweede factor voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="e5ff0-116">Klik op **accepteren** op de **toestaan dat dit apparaat worden beheerd** scherm.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="e5ff0-117">U ziet het bericht 'uw apparaat is nu lid van uw organisatie in Azure AD'.</span><span class="sxs-lookup"><span data-stu-id="e5ff0-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="e5ff0-118">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="e5ff0-118">Additional information</span></span>
* <span data-ttu-id="e5ff0-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="e5ff0-119">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* <span data-ttu-id="e5ff0-120">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)</span><span class="sxs-lookup"><span data-stu-id="e5ff0-120">[Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md)</span></span>
* [<span data-ttu-id="e5ff0-121">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="e5ff0-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="e5ff0-122">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="e5ff0-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

