---
title: aaaAzure AD + Active Directory-vereisten voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooset up toowork Active Directory met Azure RemoteApp.
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="bdeb0-103">Azure AD + Active Directory-vereisten voor Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bdeb0-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bdeb0-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bdeb0-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bdeb0-106">Uw hybride Azure RemoteApp-verzameling of voor een cloudverzameling die u wilt dat toofederate via AD Connect, moet u toodo Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="bdeb0-107">Azure AD Connect en Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdeb0-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="bdeb0-108">Als u tooconnect uw Azure AD-tenant en uw on-premises Active Directory-omgevingen wilt, gebruikt u AD Connect.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="bdeb0-109">Het duurt u alleen [4 klikken](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect Hallo twee directory's.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="bdeb0-110">Houd er rekening mee - Directory-synchronisatie is vereist voor hybride verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="bdeb0-111">Zorg ervoor dat uw '@domain.com' overeen met</span><span class="sxs-lookup"><span data-stu-id="bdeb0-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="bdeb0-112">Voordat u begint, controleert u dat Hallo UPN voor uw lokale forest komt overeen met Hallo achtervoegsel van uw Azure AD-domein.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="bdeb0-113">Na het instellen van Hallo UPN domeinachtervoegsel in Azure AD alle gebruikers aan te melden bij Azure RemoteApp wordt aanmelden als ' gebruiker @<hello suffix you set up>. "</span><span class="sxs-lookup"><span data-stu-id="bdeb0-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="bdeb0-114">Zorg ervoor dat gebruikers ook met Hallo dezelfde aanmelden kunnen user@suffix in Hallo lokaal domein.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="bdeb0-115">In bepaalde gevallen kunt u een domeinnaam instellen in Azure AD tijdens het opgeven van een ander domeinachtervoegsel voor Hallo gebruiker op-premises.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="bdeb0-116">In dit geval uw gebruikers niet kunnen tooconnect tooany Domeincomputers of resources via Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="bdeb0-117">Bijvoorbeeld, als u uw domein UPN-achtervoegsel in van AAD als contoso.com hebt ingesteld, maar sommige gebruikers op lokale/AD zijn geconfigureerde toolog met @contoso.uk, kan die gebruikers niet kunnen toocorrectly Meld u aan bij Hallo ARA-verzameling.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="bdeb0-118">Gebruikers die UPN in AAD en AD moet hello dezelfde voor Hallo aanmelding toobe mogelijk"</span><span class="sxs-lookup"><span data-stu-id="bdeb0-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="bdeb0-119">Maken van objecten voor Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bdeb0-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="bdeb0-120">U moet ook toocreate Hallo lokale Active Directory-objecten te volgen:</span><span class="sxs-lookup"><span data-stu-id="bdeb0-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="bdeb0-121">Een service-account tooprovide toodomain hulpmiddelen voor RemoteApp-programma's door RDSH eindpunten toohello lokaal domein.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="bdeb0-122">Een organisatie-eenheid (OE) toocontain RemoteApp-machineobjecten.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="bdeb0-123">Gebruik van Hallo organisatie-eenheid is aanbevolen (maar niet vereist) tooisolate Hallo accounts en beleidsregels die u met RemoteApp gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="bdeb0-124">U moet deze beide objecten bij het maken van uw RemoteApp-collectie, dus wees zeker toodo deze stappen eerst.</span><span class="sxs-lookup"><span data-stu-id="bdeb0-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

