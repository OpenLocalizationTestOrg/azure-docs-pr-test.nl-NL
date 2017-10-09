---
title: aaaFind uit wanneer een specifieke gebruiker kunnen tooaccess een toepassing worden | Microsoft Docs
description: Hoe toofind uit wanneer een gebruiker zeer belangrijk kunnen tooaccess een toepassing worden u hebt geconfigureerd voor gebruikers inrichten met Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a><span data-ttu-id="5cf1b-103">Nagaan wanneer een specifieke gebruiker kunnen tooaccess een toepassing worden</span><span class="sxs-lookup"><span data-stu-id="5cf1b-103">Find out when a specific user will be able tooaccess an application</span></span>
<span data-ttu-id="5cf1b-104">Wanneer u automatisch gebruikers inrichten met een toepassing, Azure AD automatisch inrichten en update gebruikersaccounts in een app op basis van items zoals [toewijzing van gebruikers en groepen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) op een regelmatig geplande tijdstip interval, doorgaans elke tien minuten.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-104">When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.</span></span>

## <a name="how-long-does-it-take"></a><span data-ttu-id="5cf1b-105">Hoe lang duurt het?</span><span class="sxs-lookup"><span data-stu-id="5cf1b-105">How long does it take?</span></span>

<span data-ttu-id="5cf1b-106">Hallo-tijd die nodig is voor een bepaalde gebruiker toobe ingericht afhankelijk hoofdzakelijk of er een initiële synchronisatie 'volledige' al is gebeurd.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-106">hello time it takes for a given user toobe provisioned depends mainly on whether or not an initial “full” sync has already occurred.</span></span>

<span data-ttu-id="5cf1b-107">Hallo eerste synchronisatie tussen Azure AD en een app kan overal 20 minuten tooseveral uur duren, afhankelijk van Hallo grootte van hello Azure AD-directory en Hallo aantal gebruikers in het bereik voor het inrichten.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-107">hello first sync between Azure AD and an app can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="5cf1b-108">Volgende synchronisaties na de initiële synchronisatie Hallo sneller zijn (bijvoorbeeld binnen 10 minuten), zoals het Hallo-service inricht watermerken waarbij Hallo status van beide systemen na de initiële synchronisatie hello, verbeterde prestaties van de volgende synchronisatie worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-108">Subsequent syncs after hello initial sync be faster (e.g. within 10 minutes), as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-toocheck-hello-status-of-a-user"></a><span data-ttu-id="5cf1b-109">Hoe toocheck Hallo status van een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5cf1b-109">How toocheck hello status of a user</span></span>

<span data-ttu-id="5cf1b-110">toosee hello inrichting status voor de geselecteerde gebruiker, raadpleegt u Hallo auditlogboeken in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-110">toosee hello provisioning status for a selected user, consult hello Audit logs in Azure AD.</span></span>

<span data-ttu-id="5cf1b-111">Hallo inrichting controlelogboeken kan worden geopend in hello Azure-portal, op Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt; Audit logboeken**tabblad. Filter Hallo Hallo aanmeldt **Account inrichten** categorie tooonly Zie Hallo gebeurtenissen voor die app-inrichting.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-111">hello provisioning audit logs can be accessed in hello Azure portal, in hello **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter hello logs on hello **Account Provisioning** category tooonly see hello provisioning events for that app.</span></span> <span data-ttu-id="5cf1b-112">U kunt zoeken naar gebruikers op basis van Hallo 'overeenkomende ID' die is geconfigureerd voor deze in Hallo kenmerktoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-112">You can search for users based on hello “matching ID” that was configured for them in hello attribute mappings.</span></span> 

<span data-ttu-id="5cf1b-113">Bijvoorbeeld, als u Hallo 'user principal name' of 'e-mailadres' als Hallo die overeenkomt met het kenmerk hello Azure AD-zijde geconfigureerd en Hallo gebruiker niet inrichten heeft de waarde 'audrey@contoso.com", klikt u vervolgens zoeken Hallo de auditlogboeken voor"audrey@contoso.com"en vervolgens controleren items geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-113">For example, if you configured hello “user principal name” or “email address” as hello matching attribute on hello Azure AD side, and hello user not being provisioning has a value of “audrey@contoso.com”, then search hello audit logs for “audrey@contoso.com” and review then entries returned.</span></span>

<span data-ttu-id="5cf1b-114">Hallo inrichting audit logboek vastgelegd alle bewerkingen die worden uitgevoerd door het Hallo-service, inrichting Hallo met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="5cf1b-114">hello provisioning audit logs record all hello operations performed by hello provisioning service, including:</span></span>

* <span data-ttu-id="5cf1b-115">Uitvoeren van query's Azure AD voor toegewezen gebruikers die zich binnen het bereik van de inrichting</span><span class="sxs-lookup"><span data-stu-id="5cf1b-115">Querying Azure AD for assigned users that are in scope for provisioning</span></span>
* <span data-ttu-id="5cf1b-116">Hallo doel app Hallo aanwezigheid van deze gebruikers opvragen</span><span class="sxs-lookup"><span data-stu-id="5cf1b-116">Querying hello target app for hello existence of those users</span></span>
* <span data-ttu-id="5cf1b-117">Hallo gebruikersobjecten tussen Hallo system vergelijken</span><span class="sxs-lookup"><span data-stu-id="5cf1b-117">Comparing hello user objects between hello system</span></span>
* <span data-ttu-id="5cf1b-118">Toevoegen, bijwerken of Hallo-gebruikersaccount in Hallo doelsysteem op basis van de vergelijking Hallo uitschakelen</span><span class="sxs-lookup"><span data-stu-id="5cf1b-118">Adding, updating, or disabling hello user account in hello target system based on hello comparison</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cf1b-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5cf1b-119">Next steps</span></span>
<span data-ttu-id="5cf1b-120">[Gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory automatiseren](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span><span class="sxs-lookup"><span data-stu-id="5cf1b-120">[Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''</span></span>
