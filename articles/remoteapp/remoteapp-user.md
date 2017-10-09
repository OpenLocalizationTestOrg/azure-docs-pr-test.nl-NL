---
title: een gebruiker tooyour Azure RemoteApp-verzameling aaaAdd | Microsoft Docs
description: Meer informatie over hoe tooadd gebruikers tooyour Azure RemoteApp-verzameling
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="e7dd2-103">Hoe tooadd een gebruiker tooyour Azure RemoteApp-verzameling</span><span class="sxs-lookup"><span data-stu-id="e7dd2-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e7dd2-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e7dd2-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e7dd2-106">Voordat u uw gebruikers kunnen zien en gebruiken van uw apps in Azure RemoteApp, hebben ze toegang krijgen tot tooyour verzameling toogrant.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="e7dd2-107">Dit is een eenvoudig onderdeel Hallo: op Hallo **gebruikerstoegang** tabblad, Voer Hallo accountgegevens voor de gebruiker Hallo en klik vervolgens op het vinkje Hallo.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="e7dd2-108">Welke accountgegevens hebt u nodig?</span><span class="sxs-lookup"><span data-stu-id="e7dd2-108">What account information do you need?</span></span> <span data-ttu-id="e7dd2-109">Dat hangt Hallo type verzameling u hebt gemaakt (cloud of hybride) en of u gebruikmaakt van Office 365 ProPlus in die verzameling.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="e7dd2-110">Ondersteunde gebruikers-id 's</span><span class="sxs-lookup"><span data-stu-id="e7dd2-110">Supported user identities</span></span>
<span data-ttu-id="e7dd2-111">Hallo verschillende verzamelingtypen (cloud versus hybride) ondersteuning voor het gebruik van andere gebruikers-id's voor toegang tot tooapplications.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="e7dd2-112">Voor een hybride verzameling van RemoteApp, u moet tooset van een infrastructuur voor Active Directory-domein lokale en een Azure Active Directory-tenant met Active Directory-integratie (en desgewenst eenmalige aanmelding).</span><span class="sxs-lookup"><span data-stu-id="e7dd2-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="e7dd2-113">Bovendien moet u toocreate sommige Active Directory-objecten in Hallo on-premises adreslijst.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="e7dd2-114">Voor een cloudverzameling van RemoteApp, kan elke gebruiker met Azure Active Directory ondersteuning voor identiteiten gebruiker toegang tooRemoteApp tooinclude Microsoft-Accounts worden verleend.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="e7dd2-115">Zie de onderstaande tabel voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-115">See hello table below.</span></span>

<span data-ttu-id="e7dd2-116">Office 365-gebruikers zijn Azure Active Directory-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="e7dd2-117">Als ze hybride Azure Active Directory hebt, kunnen Directory-accounts gesynchroniseerd ze gebruikerstoegang krijgen in een hybride implementatie van RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="e7dd2-118">U kunt deze tabel gebruiken als naslag waarvoor de identiteit die wordt ondersteund in de verzameling en wat Hallo Active Directory-vereisten zijn.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="e7dd2-119">Gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="e7dd2-119">User accounts</span></span> | <span data-ttu-id="e7dd2-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="e7dd2-120">Cloud</span></span> | <span data-ttu-id="e7dd2-121">Hybride</span><span class="sxs-lookup"><span data-stu-id="e7dd2-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7dd2-122">Microsoft-account</span><span class="sxs-lookup"><span data-stu-id="e7dd2-122">Microsoft Account</span></span> |<span data-ttu-id="e7dd2-123">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-123">Yes</span></span> |<span data-ttu-id="e7dd2-124">Nee</span><span class="sxs-lookup"><span data-stu-id="e7dd2-124">No</span></span> |
| <span data-ttu-id="e7dd2-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="e7dd2-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="e7dd2-126">Azure AD cloud</span><span class="sxs-lookup"><span data-stu-id="e7dd2-126">Azure AD cloud only</span></span> |<span data-ttu-id="e7dd2-127">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-127">Yes</span></span> |<span data-ttu-id="e7dd2-128">Nee</span><span class="sxs-lookup"><span data-stu-id="e7dd2-128">No</span></span> |
| <span data-ttu-id="e7dd2-129">ADsync met Wachtwoordsynchronisatie</span><span class="sxs-lookup"><span data-stu-id="e7dd2-129">ADsync with password sync</span></span> |<span data-ttu-id="e7dd2-130">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-130">Yes</span></span> |<span data-ttu-id="e7dd2-131">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-131">Yes</span></span> |
| <span data-ttu-id="e7dd2-132">ADsync zonder Wachtwoordsynchronisatie</span><span class="sxs-lookup"><span data-stu-id="e7dd2-132">ADsync without password sync</span></span> |<span data-ttu-id="e7dd2-133">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-133">Yes</span></span> |<span data-ttu-id="e7dd2-134">Nee</span><span class="sxs-lookup"><span data-stu-id="e7dd2-134">No</span></span> |
| <span data-ttu-id="e7dd2-135">ADsync met AD FS</span><span class="sxs-lookup"><span data-stu-id="e7dd2-135">ADsync with AD FS</span></span> |<span data-ttu-id="e7dd2-136">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-136">Yes</span></span> |<span data-ttu-id="e7dd2-137">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-137">Yes</span></span> |
| <span data-ttu-id="e7dd2-138">[3rd van derden door Azure ondersteunde identiteitsproviders](https://msdn.microsoft.com/library/azure/jj679342.aspx) (voorbeeld Ping)</span><span class="sxs-lookup"><span data-stu-id="e7dd2-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="e7dd2-139">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-139">Yes</span></span> |<span data-ttu-id="e7dd2-140">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-140">Yes</span></span> |
| <span data-ttu-id="e7dd2-141">Meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="e7dd2-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="e7dd2-142">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-142">Yes</span></span> |<span data-ttu-id="e7dd2-143">Ja</span><span class="sxs-lookup"><span data-stu-id="e7dd2-143">Yes</span></span> |

<span data-ttu-id="e7dd2-144">Bekijk [meer informatie](remoteapp-ad.md) over het configureren van Active Directory voor RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="e7dd2-145">Hello Azure Active Directory-gebruikers moeten uit Hallo-tenant die gekoppeld is aan uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="e7dd2-146">(U kunt bekijken en wijzigen van uw abonnement op Hallo **instellingen** tabblad in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="e7dd2-147">Zie [wijziging hello Azure Active Directory-tenant die wordt gebruikt door RemoteApp](remoteapp-changetenant.md) voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="e7dd2-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="e7dd2-148">Informatie over Office 365 ProPlus gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="e7dd2-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="e7dd2-149">Als u Office 365 ProPlus Hallo-sjablooninstallatiekopie in uw verzameling gebruikt *of* als u een aangepaste installatiekopie die gebruikmaakt van Office 365 hebt gemaakt, u mogen alleen tooadd Azure Active Directory-gebruikers die Office 365-abonnementen voor Hallo hebben standaarddomein van uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="e7dd2-150">Zie [Office 365 gebruiken met Azure RemoteApp](remoteapp-o365.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e7dd2-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

