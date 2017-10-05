---
title: Azure AD + Active Directory-vereisten voor Azure RemoteApp | Microsoft Docs
description: Informatie over het instellen van Active Directory om te werken met Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="9f888-103">Azure AD + Active Directory-vereisten voor Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9f888-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f888-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="9f888-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9f888-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9f888-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9f888-106">Voor uw Azure RemoteApp hybride verzameling of voor een cloudverzameling die u wilt federeren met AD Connect, moet u het volgende te doen.</span><span class="sxs-lookup"><span data-stu-id="9f888-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="9f888-107">Azure AD Connect en Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f888-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="9f888-108">Als u verbinding maken met uw Azure AD-tenant en uw on-premises Active Directory-omgevingen wilt, gebruikt u AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9f888-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="9f888-109">Het duurt u alleen [4 klikken](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) verbinding van de twee directory's.</span><span class="sxs-lookup"><span data-stu-id="9f888-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="9f888-110">Houd er rekening mee - Directory-synchronisatie is vereist voor hybride verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="9f888-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="9f888-111">Zorg ervoor dat uw '@domain.com' overeen met</span><span class="sxs-lookup"><span data-stu-id="9f888-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="9f888-112">Voordat u begint, controleert u of de UPN voor het lokale forest overeenkomt met het achtervoegsel van uw Azure AD-domein.</span><span class="sxs-lookup"><span data-stu-id="9f888-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="9f888-113">Na het instellen van het domein UPN-achtervoegsel in Azure AD alle gebruikers aan te melden bij Azure RemoteApp wordt aanmelden als ' gebruiker @<the suffix you set up>. "</span><span class="sxs-lookup"><span data-stu-id="9f888-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="9f888-114">Zorg ervoor dat gebruikers zich ook met dezelfde aanmelden kunnen user@suffix in het lokale domein.</span><span class="sxs-lookup"><span data-stu-id="9f888-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="9f888-115">In bepaalde gevallen kunt u een domeinnaam instellen in Azure AD tijdens het opgeven van een ander domeinachtervoegsel voor de gebruiker op-premises.</span><span class="sxs-lookup"><span data-stu-id="9f888-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="9f888-116">In dit geval uw gebruikers niet mogelijk verbinding maken met alle domeincomputers of resources via Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9f888-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="9f888-117">Bijvoorbeeld, als u uw domein UPN-achtervoegsel in van AAD als contoso.com hebt ingesteld, maar sommige gebruikers op lokale/AD zijn geconfigureerd voor logboekregistratie met @contoso.uk, kan die gebruikers niet correct aanmelden bij de ARA-verzameling.</span><span class="sxs-lookup"><span data-stu-id="9f888-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="9f888-118">Gebruikers UPN in AAD en AD moet hetzelfde zijn voor de aanmelding mogelijk'</span><span class="sxs-lookup"><span data-stu-id="9f888-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="9f888-119">Maken van objecten voor Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9f888-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="9f888-120">U moet ook de volgende on-premises Active Directory-objecten maken:</span><span class="sxs-lookup"><span data-stu-id="9f888-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="9f888-121">Een serviceaccount om toegang te bieden tot domeinbronnen voor RemoteApp-programma's door RDSH-eindpunten toevoegen aan het lokale-domein.</span><span class="sxs-lookup"><span data-stu-id="9f888-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="9f888-122">Een organisatie-eenheid (OE) RemoteApp machineobjecten bevatten.</span><span class="sxs-lookup"><span data-stu-id="9f888-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="9f888-123">Gebruik van de organisatie-eenheid wordt aanbevolen (maar niet vereist) voor het isoleren van de accounts en beleidsregels die u met RemoteApp gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="9f888-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="9f888-124">U moet deze beide objecten bij het maken van uw RemoteApp-collectie moet deze stappen eerst doen.</span><span class="sxs-lookup"><span data-stu-id="9f888-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

