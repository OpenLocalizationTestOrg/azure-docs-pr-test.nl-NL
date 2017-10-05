---
title: Een gebruiker toevoegen aan uw Azure RemoteApp-collectie | Microsoft Docs
description: Informatie over het toevoegen van gebruikers aan uw Azure RemoteApp-verzameling
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
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="6d624-103">Een gebruiker toevoegen aan uw Azure RemoteApp-verzameling</span><span class="sxs-lookup"><span data-stu-id="6d624-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d624-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="6d624-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6d624-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d624-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6d624-106">Voordat u uw gebruikers kunnen zien en gebruiken van uw apps in Azure RemoteApp, die u moet ze toegang verlenen tot uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="6d624-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="6d624-107">Dit is het eenvoudig gedeelte: op de **gebruikerstoegang** tabblad, voer de accountgegevens voor de gebruiker en klik vervolgens op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="6d624-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="6d624-108">Welke accountgegevens hebt u nodig?</span><span class="sxs-lookup"><span data-stu-id="6d624-108">What account information do you need?</span></span> <span data-ttu-id="6d624-109">Die afhankelijk is van het type van verzameling u hebt gemaakt (cloud of hybride) en of u gebruikmaakt van Office 365 ProPlus in die verzameling.</span><span class="sxs-lookup"><span data-stu-id="6d624-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="6d624-110">Ondersteunde gebruikers-id 's</span><span class="sxs-lookup"><span data-stu-id="6d624-110">Supported user identities</span></span>
<span data-ttu-id="6d624-111">De van verschillende verzamelingtypen (cloud versus hybride) ondersteuning voor het gebruik van andere gebruikers-id's voor toegang tot toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6d624-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="6d624-112">Voor een hybride verzameling van RemoteApp moet u een Active Directory-domein-infrastructuur lokale en een Azure Active Directory-tenant met Active Directory-integratie instellen (en desgewenst eenmalige aanmelding).</span><span class="sxs-lookup"><span data-stu-id="6d624-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="6d624-113">Bovendien moet u enkele Active Directory-objecten maken in de on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="6d624-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="6d624-114">Voor een cloudverzameling van RemoteApp, kan elke gebruiker met Azure Active Directory ondersteuning voor identiteiten gebruikerstoegang worden toegekend aan RemoteApp om op te nemen van Microsoft-Accounts.</span><span class="sxs-lookup"><span data-stu-id="6d624-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="6d624-115">Zie de onderstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="6d624-115">See the table below.</span></span>

<span data-ttu-id="6d624-116">Office 365-gebruikers zijn Azure Active Directory-gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6d624-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="6d624-117">Als ze hybride Azure Active Directory hebt, kunnen Directory-accounts gesynchroniseerd ze gebruikerstoegang krijgen in een hybride implementatie van RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6d624-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="6d624-118">U kunt deze tabel gebruiken als naslag waarvoor de identiteit die wordt ondersteund in de verzameling en wat de vereisten voor Active Directory zijn.</span><span class="sxs-lookup"><span data-stu-id="6d624-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="6d624-119">Gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="6d624-119">User accounts</span></span> | <span data-ttu-id="6d624-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="6d624-120">Cloud</span></span> | <span data-ttu-id="6d624-121">Hybride</span><span class="sxs-lookup"><span data-stu-id="6d624-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d624-122">Microsoft-account</span><span class="sxs-lookup"><span data-stu-id="6d624-122">Microsoft Account</span></span> |<span data-ttu-id="6d624-123">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-123">Yes</span></span> |<span data-ttu-id="6d624-124">Nee</span><span class="sxs-lookup"><span data-stu-id="6d624-124">No</span></span> |
| <span data-ttu-id="6d624-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="6d624-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="6d624-126">Azure AD cloud</span><span class="sxs-lookup"><span data-stu-id="6d624-126">Azure AD cloud only</span></span> |<span data-ttu-id="6d624-127">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-127">Yes</span></span> |<span data-ttu-id="6d624-128">Nee</span><span class="sxs-lookup"><span data-stu-id="6d624-128">No</span></span> |
| <span data-ttu-id="6d624-129">ADsync met Wachtwoordsynchronisatie</span><span class="sxs-lookup"><span data-stu-id="6d624-129">ADsync with password sync</span></span> |<span data-ttu-id="6d624-130">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-130">Yes</span></span> |<span data-ttu-id="6d624-131">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-131">Yes</span></span> |
| <span data-ttu-id="6d624-132">ADsync zonder Wachtwoordsynchronisatie</span><span class="sxs-lookup"><span data-stu-id="6d624-132">ADsync without password sync</span></span> |<span data-ttu-id="6d624-133">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-133">Yes</span></span> |<span data-ttu-id="6d624-134">Nee</span><span class="sxs-lookup"><span data-stu-id="6d624-134">No</span></span> |
| <span data-ttu-id="6d624-135">ADsync met AD FS</span><span class="sxs-lookup"><span data-stu-id="6d624-135">ADsync with AD FS</span></span> |<span data-ttu-id="6d624-136">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-136">Yes</span></span> |<span data-ttu-id="6d624-137">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-137">Yes</span></span> |
| <span data-ttu-id="6d624-138">[3rd van derden door Azure ondersteunde identiteitsproviders](https://msdn.microsoft.com/library/azure/jj679342.aspx) (voorbeeld Ping)</span><span class="sxs-lookup"><span data-stu-id="6d624-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="6d624-139">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-139">Yes</span></span> |<span data-ttu-id="6d624-140">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-140">Yes</span></span> |
| <span data-ttu-id="6d624-141">Meervoudige verificatie</span><span class="sxs-lookup"><span data-stu-id="6d624-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="6d624-142">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-142">Yes</span></span> |<span data-ttu-id="6d624-143">Ja</span><span class="sxs-lookup"><span data-stu-id="6d624-143">Yes</span></span> |

<span data-ttu-id="6d624-144">Bekijk [meer informatie](remoteapp-ad.md) over het configureren van Active Directory voor RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6d624-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="6d624-145">De Azure Active Directory-gebruikers moeten afkomstig zijn van de tenant die aan uw abonnement is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6d624-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="6d624-146">(U kunt uw abonnement bekijken en wijzigen op het tabblad **Instellingen** in de portal.</span><span class="sxs-lookup"><span data-stu-id="6d624-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="6d624-147">Zie [De Azure Active Directory-tenant wijzigen die wordt gebruikt door RemoteApp](remoteapp-changetenant.md) voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="6d624-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="6d624-148">Informatie over Office 365 ProPlus gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="6d624-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="6d624-149">Als u de Office 365 ProPlus-sjablooninstallatiekopie in uw verzameling gebruikt *of* als u een aangepaste installatiekopie die gebruikmaakt van Office 365 hebt gemaakt, mogen u alleen Azure Active Directory-gebruikers met Office 365-abonnementen voor het standaarddomein van uw abonnement toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="6d624-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="6d624-150">Zie [Office 365 gebruiken met Azure RemoteApp](remoteapp-o365.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6d624-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

