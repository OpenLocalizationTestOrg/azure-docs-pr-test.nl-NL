---
title: aaaSetting stellen Azure AD Join voor uw gebruikers | Microsoft Docs
description: Hier wordt uitgelegd hoe beheerders Azure AD Join kunnen instellen voor on-premises directory- en apparaatregistratie.
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a><span data-ttu-id="90f92-103">Azure AD Join instellen in uw organisatie</span><span class="sxs-lookup"><span data-stu-id="90f92-103">Setting up Azure AD Join in your organization</span></span>
<span data-ttu-id="90f92-104">Voordat u Azure Active Directory Join (Azure AD Join) instelt, moet u de synchronisatie tooeither registreert uw on-premises directory van gebruikers toohello cloud of handmatig beheerde accounts in Azure AD maken.</span><span class="sxs-lookup"><span data-stu-id="90f92-104">Before you set up Azure Active Directory Join (Azure AD Join), you need tooeither sync up your on-premises directory of users toohello cloud or manually create managed accounts in Azure AD.</span></span>

<span data-ttu-id="90f92-105">Gedetailleerde instructies voor het synchroniseren van uw lokale gebruikers tooAzure AD wordt beschreven in [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="90f92-105">Detailed instructions for syncing your on-premises users tooAzure AD is covered in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="90f92-106">toomanually maken en beheren van gebruikers in Azure AD, te verwijzen[Gebruikersbeheer in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span><span class="sxs-lookup"><span data-stu-id="90f92-106">toomanually create and manage users in Azure AD, refer too[User management in Azure AD](https://msdn.microsoft.com/library/azure/hh967609.aspx).</span></span>

## <a name="set-up-device-registration"></a><span data-ttu-id="90f92-107">Apparaatregistratie instellen</span><span class="sxs-lookup"><span data-stu-id="90f92-107">Set up device registration</span></span>
1. <span data-ttu-id="90f92-108">Meld u aan toohello Azure-portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="90f92-108">Log on toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="90f92-109">Selecteer in het linkerdeelvenster Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="90f92-109">On hello left pane, select **Active Directory**.</span></span>
3. <span data-ttu-id="90f92-110">Op Hallo **Directory** tabblad, selecteer uw directory.</span><span class="sxs-lookup"><span data-stu-id="90f92-110">On hello **Directory** tab, select your directory.</span></span>
4. <span data-ttu-id="90f92-111">Selecteer Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="90f92-111">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="90f92-112">Ga toohello **apparaten** sectie.</span><span class="sxs-lookup"><span data-stu-id="90f92-112">Go toohello **Devices** section.</span></span>
6. <span data-ttu-id="90f92-113">Op Hallo **apparaten** tabblad, Hallo volgende instellen:</span><span class="sxs-lookup"><span data-stu-id="90f92-113">On hello **devices** tab, set hello following:</span></span>  
   * <span data-ttu-id="90f92-114">**MAXIMUM aantal apparaten PER gebruiker**: Selecteer Hallo kunt u het maximum aantal apparaten dat een gebruiker in Azure AD hebben kan.</span><span class="sxs-lookup"><span data-stu-id="90f92-114">**MAXIMUM NUMBER OF DEVICES PER USER**: Select hello maximum number of devices that a user can have in Azure AD.</span></span>  <span data-ttu-id="90f92-115">Als een gebruiker dit quotum bereikt, worden ze niet kunnen tooadd extra apparaten worden totdat een of meer van de bestaande apparaten zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="90f92-115">If a user reaches this quota, they will not be able tooadd additional devices until one or more of their existing devices are removed.</span></span>
   * <span data-ttu-id="90f92-116">**VEREISEN multi-factor AUTH tooJOIN apparaten**: instellen of gebruikers zijn vereiste tooprovide een verificatie met tweede factor toojoin hun apparaat tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="90f92-116">**REQUIRE MULTI-FACTOR AUTH tooJOIN DEVICES**: Set whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="90f92-117">Zie voor meer informatie over Azure multi-factor Authentication [aan de slag met Azure multi-factor Authentication in de cloud Hallo](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="90f92-117">For more information on Azure Multi-Factor Authentication, see [Getting started with Azure Multi-Factor Authentication in hello cloud](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>
   * <span data-ttu-id="90f92-118">**GEBRUIKERS kunnen AZURE AD JOIN apparaten**: Hallo-gebruikers en groepen die zijn toegestaan toojoin apparaten tooAzure AD selecteren.</span><span class="sxs-lookup"><span data-stu-id="90f92-118">**USERS MAY AZURE AD JOIN DEVICES**: Select hello users and groups that are allowed toojoin devices tooAzure AD.</span></span>
   * <span data-ttu-id="90f92-119">**EXTRA beheerders op AZURE AD met toegevoegde apparaten**: met Azure AD Premium of Enterprise Mobility Suite (EMS) hello, kunt u kiezen welke gebruikers lokale administrator-rechten zijn verleend toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="90f92-119">**ADDITIONAL ADMINISTRATORS ON AZURE AD JOINED DEVICES**: With Azure AD Premium or hello Enterprise Mobility Suite (EMS), you can choose which users are granted local administrator rights toohello device.</span></span> <span data-ttu-id="90f92-120">Globale beheerders en eigenaren van de apparaten ontvangen standaard lokale beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="90f92-120">Global administrators and device owners are granted local administrator rights by default.</span></span>

<span data-ttu-id="90f92-121"><center>![Apparaatregistratie instellen](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span><span class="sxs-lookup"><span data-stu-id="90f92-121"><center>![Set up device regisration](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center></span></span>

<span data-ttu-id="90f92-122">Nadat u Azure AD Join voor uw gebruikers instellen, kunnen ze verbinding maken met tooAzure AD via hun zakelijke of persoonlijke apparaten.</span><span class="sxs-lookup"><span data-stu-id="90f92-122">After you set up Azure AD Join for your users, they can connect tooAzure AD through their corporate or personal devices.</span></span>

<span data-ttu-id="90f92-123">Hieronder volgen Hallo drie scenario's kunt u tooenable uw gebruikers tooset stellen Azure AD Join:</span><span class="sxs-lookup"><span data-stu-id="90f92-123">Following are hello three scenarios you can use tooenable your users tooset up Azure AD Join:</span></span>

* <span data-ttu-id="90f92-124">Gebruikers lid worden van een apparaat in Bedrijfseigendom rechtstreeks tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="90f92-124">Users join a company-owned device directly tooAzure AD.</span></span>
* <span data-ttu-id="90f92-125">Gebruikers domein een bedrijfseigen apparaten toohello on-premises Active Directory en vervolgens Hallo apparaat tooAzure AD uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="90f92-125">Users domain-join a company-owned device toohello on-premises Active Directory and then extend hello device tooAzure AD.</span></span>
* <span data-ttu-id="90f92-126">Gebruikers voegen werk of school tooWindows accounts op een persoonlijk apparaat</span><span class="sxs-lookup"><span data-stu-id="90f92-126">Users add work or school accounts tooWindows on a personal device</span></span>

## <a name="additional-information"></a><span data-ttu-id="90f92-127">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="90f92-127">Additional information</span></span>
* [<span data-ttu-id="90f92-128">Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.</span><span class="sxs-lookup"><span data-stu-id="90f92-128">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="90f92-129">Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden</span><span class="sxs-lookup"><span data-stu-id="90f92-129">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* <span data-ttu-id="90f92-130">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)</span><span class="sxs-lookup"><span data-stu-id="90f92-130">[Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)</span></span>
* [<span data-ttu-id="90f92-131">Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring</span><span class="sxs-lookup"><span data-stu-id="90f92-131">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="90f92-132">Azure AD Join instellen</span><span class="sxs-lookup"><span data-stu-id="90f92-132">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

