---
title: 'Azure Active Directory Domain Services: Ondersteuning voor het gebruikersprofiel SharePoint-service inschakelen | Microsoft Docs'
description: Azure Active Directory Domain Services beheerde domeinen ter ondersteuning van synchronisatie van het profiel voor SharePoint-Server configureren
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
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="d4c25-103">Een beheerd domein ter ondersteuning van synchronisatie van het profiel voor SharePoint-Server configureren</span><span class="sxs-lookup"><span data-stu-id="d4c25-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="d4c25-104">SharePoint Server bevat een User Profile-Service die wordt gebruikt voor synchronisatie van het profiel.</span><span class="sxs-lookup"><span data-stu-id="d4c25-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="d4c25-105">Als u de Service-profiel instelt, moeten geschikte machtigingen worden toegekend op Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="d4c25-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="d4c25-106">Zie voor meer informatie [Active Directory Domain Services-machtigingen voor synchronisatie van het profiel in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4c25-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="d4c25-107">Dit artikel wordt uitgelegd hoe u Azure AD Domain Services beheerde domeinen voor het implementeren van de service voor SharePoint serversynchronisatie van gebruikersprofielen kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="d4c25-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="d4c25-108">De groep AAD DC serviceaccounts</span><span class="sxs-lookup"><span data-stu-id="d4c25-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="d4c25-109">Een beveiligingsgroep genaamd '**AAD DC-serviceaccounts**' is beschikbaar in de organisatie-eenheid 'Gebruikers' in uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="d4c25-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="d4c25-110">Ziet u deze groep in de **Active Directory: gebruikers en Computers** MMC-module op uw beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="d4c25-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![DC-serviceaccounts AAD-beveiligingsgroep](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="d4c25-112">Leden van deze beveiligingsgroep gedelegeerde de volgende bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="d4c25-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="d4c25-113">De bevoegdheid 'directorywijzigingen repliceren' in de hoofdmap DSE van het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="d4c25-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="d4c25-114">De bevoegdheid 'directorywijzigingen repliceren' in de naamgevingscontext configuratie (cn = configuratiecontainer) van het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="d4c25-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="d4c25-115">Deze beveiligingsgroep is ook lid zijn van de ingebouwde groep **Pre-Windows 2000-compatibele toegang**.</span><span class="sxs-lookup"><span data-stu-id="d4c25-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![DC-serviceaccounts AAD-beveiligingsgroep](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="d4c25-117">Uw beheerde domein voor de ondersteuning van synchronisatie van gebruikersprofielen SharePoint-Server inschakelen</span><span class="sxs-lookup"><span data-stu-id="d4c25-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="d4c25-118">U kunt het serviceaccount dat wordt gebruikt voor SharePoint gebruiker profielsynchronisatie toevoegen de **AAD DC-serviceaccounts** groep.</span><span class="sxs-lookup"><span data-stu-id="d4c25-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="d4c25-119">De Synchronisatieaccount opgehaald als gevolg hiervan onvoldoende machtigingen om wijzigingen te repliceren naar de map.</span><span class="sxs-lookup"><span data-stu-id="d4c25-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="d4c25-120">Deze stap in de configuratie kunt synchronisatie van gebruikersprofielen SharePoint-Server correct te laten werken.</span><span class="sxs-lookup"><span data-stu-id="d4c25-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![Serviceaccounts AAD DC - toevoegen leden](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Serviceaccounts AAD DC - toevoegen leden](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="d4c25-123">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="d4c25-123">Related Content</span></span>
* [<span data-ttu-id="d4c25-124">Technische documentatie - machtigingen verlenen Active Directory Domain Services voor synchronisatie van het profiel in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="d4c25-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
