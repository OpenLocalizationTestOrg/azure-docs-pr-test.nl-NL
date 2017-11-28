---
title: aaaSet van een nieuw apparaat met Azure AD tijdens de installatie | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe gebruikers kunnen Azure AD Join instellen tijdens hun first-run experience.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a><span data-ttu-id="cbf61-103">Instellen van een nieuw apparaat met Azure AD tijdens de installatie</span><span class="sxs-lookup"><span data-stu-id="cbf61-103">Set up a new device with Azure AD during Setup</span></span>
<span data-ttu-id="cbf61-104">In Windows 10, kunnen gebruikers hun apparaten tooAzure Active Directory (Azure AD) toevoegen in de eerste uitvoering van Windows hello (FRX).</span><span class="sxs-lookup"><span data-stu-id="cbf61-104">In Windows 10, users can join their devices tooAzure Active Directory (Azure AD) in hello first-run experience (FRX).</span></span> <span data-ttu-id="cbf61-105">Dit kan organisaties toodistribute krimp apparaten tootheir werknemers en studenten of kan ze hun eigen apparaten (CYOD) te kiezen.</span><span class="sxs-lookup"><span data-stu-id="cbf61-105">This allows organizations toodistribute shrink-wrapped devices tootheir employees or students, or let them choose their own devices (CYOD).</span></span>
<span data-ttu-id="cbf61-106">Als Windows 10 Professional of Windows 10 Enterprise-editie is geïnstalleerd op een apparaat, ervaren Hallo standaardwaarden toohello setup-proces voor apparaten in Bedrijfseigendom.</span><span class="sxs-lookup"><span data-stu-id="cbf61-106">If either Windows 10 Professional or Windows 10 Enterprise editions is installed on a device, hello experience defaults toohello setup process for company-owned devices.</span></span>

## <a name="toojoin-a-device-tooazure-ad"></a><span data-ttu-id="cbf61-107">een apparaat tooAzure AD toojoin</span><span class="sxs-lookup"><span data-stu-id="cbf61-107">toojoin a device tooAzure AD</span></span>
1. <span data-ttu-id="cbf61-108">Wanneer u het nieuwe apparaat inschakelen en Hallo-installatieproces start, ziet u Hallo **gereed ophalen** bericht.</span><span class="sxs-lookup"><span data-stu-id="cbf61-108">When you turn on your new device and start hello setup process, you should see hello  **Getting Ready** message.</span></span> <span data-ttu-id="cbf61-109">Ga als volgt Hallo prompts tooset van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="cbf61-109">Follow hello prompts tooset up your device.</span></span>
2. <span data-ttu-id="cbf61-110">Start op het aanpassen van uw regio en taal.</span><span class="sxs-lookup"><span data-stu-id="cbf61-110">Start by customizing your region and language.</span></span> <span data-ttu-id="cbf61-111">Accepteer Hallo Microsoft-softwarelicentievoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="cbf61-111">Then accept hello Microsoft Software License Terms.</span></span>
   <span data-ttu-id="cbf61-112">![Aanpassen voor uw regio](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span><span class="sxs-lookup"><span data-stu-id="cbf61-112">![Customize for your region](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)</span></span>
3. <span data-ttu-id="cbf61-113">Selecteer Hallo netwerk gewenste toouse toohello Internet verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="cbf61-113">Select hello network you want toouse for connecting toohello Internet.</span></span>
4. <span data-ttu-id="cbf61-114">Selecteer of u een persoonlijk apparaat of een apparaat in Bedrijfseigendom.</span><span class="sxs-lookup"><span data-stu-id="cbf61-114">Select whether you're using a personal device or a company-owned device.</span></span> <span data-ttu-id="cbf61-115">Als het eigendom van het bedrijf, klikt u op **dit apparaat is van de organisatie toomy**.</span><span class="sxs-lookup"><span data-stu-id="cbf61-115">If it's company-owned, click **This device belongs toomy organization**.</span></span> <span data-ttu-id="cbf61-116">Hiermee start u hello Azure AD Join-ervaring.</span><span class="sxs-lookup"><span data-stu-id="cbf61-116">This starts hello Azure AD Join experience.</span></span> <span data-ttu-id="cbf61-117">Hier volgt een scherm die wordt weergegeven als u Windows 10 Professional.</span><span class="sxs-lookup"><span data-stu-id="cbf61-117">Following is a screen that you'll see if you're using Windows 10 Professional.</span></span>
   <span data-ttu-id="cbf61-118"><center>
   ![Wie is eigenaar van dit scherm PC](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span><span class="sxs-lookup"><span data-stu-id="cbf61-118"><center>
![Who owns this PC screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)</span></span>
5. <span data-ttu-id="cbf61-119">Geef referenties op Hallo die tooyou zijn geleverd door uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="cbf61-119">Enter hello credentials that were provided tooyou by your organization.</span></span>
   <span data-ttu-id="cbf61-120"><center>
   ![Aanmeldingsscherm](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span><span class="sxs-lookup"><span data-stu-id="cbf61-120"><center>
![Sign-in screen](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</span></span>
6. <span data-ttu-id="cbf61-121">Nadat u uw gebruikersnaam hebt ingevoerd, wordt een overeenkomende tenant bevindt zich in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbf61-121">After you have entered your user name, a matching tenant is located in Azure AD.</span></span> <span data-ttu-id="cbf61-122">Als u zich in een federatieve domein, wordt u omgeleid tooyour lokale Secure Token Service (STS) server--bijvoorbeeld Active Directory Federation Services (AD FS) zijn.</span><span class="sxs-lookup"><span data-stu-id="cbf61-122">If you are in a federated domain, you will be redirected tooyour on-premises Secure Token Service (STS) server--for example, Active Directory Federation Services (AD FS).</span></span>
7. <span data-ttu-id="cbf61-123">Als u een gebruiker in een niet-gefedereerde domein, Geef uw referenties rechtstreeks op Hallo Azure AD gehost pagina.</span><span class="sxs-lookup"><span data-stu-id="cbf61-123">If you are a user in a non-federated domain, enter your credentials directly on hello Azure AD-hosted page.</span></span> <span data-ttu-id="cbf61-124">Als de huisstijl van uw bedrijf is geconfigureerd, wordt u ook Zie logo van uw organisatie en tekst ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="cbf61-124">If company branding was configured, you will also see your organization’s logo and support text.</span></span>
8. <span data-ttu-id="cbf61-125">U wordt gevraagd om een challenge multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="cbf61-125">You're prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="cbf61-126">Deze uitdaging kan worden geconfigureerd door een IT-beheerder.</span><span class="sxs-lookup"><span data-stu-id="cbf61-126">This challenge is configurable by an IT administrator.</span></span>
9. <span data-ttu-id="cbf61-127">Azure AD wordt gecontroleerd of deze gebruiker/apparaat is vereist voor inschrijving in beheer van mobiele apparaten.</span><span class="sxs-lookup"><span data-stu-id="cbf61-127">Azure AD checks whether this user/device requires enrollment in mobile device management.</span></span>
10. <span data-ttu-id="cbf61-128">Windows hello apparaat geregistreerd bij Hallo organisatiemap in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="cbf61-128">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
11. <span data-ttu-id="cbf61-129">Als u een beheerde gebruiker bent, gaat u in Windows desktop toohello via automatische Hallo aanmelden proces.</span><span class="sxs-lookup"><span data-stu-id="cbf61-129">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in process.</span></span>
12. <span data-ttu-id="cbf61-130">Als u een federatieve gebruiker bent, wordt u omgeleid toohello Windows aanmelden scherm tooenter uw referenties.</span><span class="sxs-lookup"><span data-stu-id="cbf61-130">If you are a federated user, you are directed toohello Windows sign-in screen tooenter your credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="cbf61-131">Lidmaatschap van een lokale Windows Server Active Directory-domein in Windows hello wordt out-of-box experience niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cbf61-131">Joining an on-premises Windows Server Active Directory domain in hello Windows out-of-box experience is not supported.</span></span> <span data-ttu-id="cbf61-132">Als u een domein computer tooa toojoin plant, moet u daarom Hallo koppeling selecteren **Windows instellen met een lokaal account** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="cbf61-132">Therefore, if you plan toojoin a computer tooa domain, you should select hello link **Set up Windows with a local account** instead.</span></span> <span data-ttu-id="cbf61-133">Vervolgens kunt u Hallo domein uit Hallo-instellingen op uw computer koppelen als u eerder hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cbf61-133">You can then join hello domain from hello settings on your computer as you’ve done before.</span></span>
> 
> 

## <a name="additional-information"></a><span data-ttu-id="cbf61-134">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="cbf61-134">Additional information</span></span>
* [<span data-ttu-id="cbf61-135">Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.</span><span class="sxs-lookup"><span data-stu-id="cbf61-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="cbf61-136">Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden</span><span class="sxs-lookup"><span data-stu-id="cbf61-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="cbf61-137">Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren</span><span class="sxs-lookup"><span data-stu-id="cbf61-137">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* <span data-ttu-id="cbf61-138">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="cbf61-138">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* [<span data-ttu-id="cbf61-139">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="cbf61-139">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="cbf61-140">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="cbf61-140">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

