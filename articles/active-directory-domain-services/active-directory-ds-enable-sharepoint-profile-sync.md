---
title: 'Azure Active Directory Domain Services: Ondersteuning voor het gebruikersprofiel SharePoint-service inschakelen | Microsoft Docs'
description: Azure Active Directory Domain Services beheerde domeinen toosupport profielsynchronisatie voor SharePoint-Server configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="a2fb7-103">Een beheerd domein toosupport profielsynchronisatie voor SharePoint-Server configureren</span><span class="sxs-lookup"><span data-stu-id="a2fb7-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="a2fb7-104">SharePoint Server bevat een User Profile-Service die wordt gebruikt voor synchronisatie van het profiel.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="a2fb7-105">tooset up Hallo User Profile-Service, gemachtigd moeten toobe toegekend op Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="a2fb7-106">Zie voor meer informatie [Active Directory Domain Services-machtigingen voor synchronisatie van het profiel in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2fb7-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="a2fb7-107">Dit artikel wordt uitgelegd hoe u Azure AD Domain Services beheerde domeinen toodeploy Hallo synchronisatie van SharePoint Server gebruikersprofielen service kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="a2fb7-108">Hallo AAD DC serviceaccounts groep</span><span class="sxs-lookup"><span data-stu-id="a2fb7-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="a2fb7-109">Een beveiligingsgroep aangeroepen '**AAD DC-serviceaccounts**' Hallo 'Gebruikers' organisatie-eenheid op uw beheerde domein beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="a2fb7-110">U kunt deze groep in Hallo zien **Active Directory: gebruikers en Computers** MMC-module op uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![DC-serviceaccounts AAD-beveiligingsgroep](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="a2fb7-112">Leden van deze beveiligingsgroep zijn gedelegeerd Hallo volgende bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="a2fb7-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="a2fb7-113">Hallo 'directorywijzigingen repliceren'-bevoegdheden op Hallo hoofdmap DSE Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="a2fb7-114">Hallo 'directorywijzigingen repliceren'-bevoegdheden op Hallo configuratienaamgevingscontext (cn = configuratiecontainer) Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="a2fb7-115">Deze beveiligingsgroep is ook lid zijn van de ingebouwde groep Hallo **Pre-Windows 2000-compatibele toegang**.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![DC-serviceaccounts AAD-beveiligingsgroep](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="a2fb7-117">Uw beheerde domein toosupport synchronisatie van gebruikersprofielen SharePoint-Server inschakelen</span><span class="sxs-lookup"><span data-stu-id="a2fb7-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="a2fb7-118">U kunt toevoegen Hallo-serviceaccount gebruikt voor SharePoint gebruiker profiel synchronisatie toohello **AAD DC-serviceaccounts** groep.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="a2fb7-119">Hallo-account voor synchronisatie opgehaald als gevolg hiervan voldoende bevoegdheden tooreplicate wijzigingen toohello directory.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="a2fb7-120">Deze stap in de configuratie kunt SharePoint Server gebruiker profiel sync toowork correct.</span><span class="sxs-lookup"><span data-stu-id="a2fb7-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![Serviceaccounts AAD DC - toevoegen leden](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Serviceaccounts AAD DC - toevoegen leden](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="a2fb7-123">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="a2fb7-123">Related Content</span></span>
* [<span data-ttu-id="a2fb7-124">Technische documentatie - machtigingen verlenen Active Directory Domain Services voor synchronisatie van het profiel in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="a2fb7-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
