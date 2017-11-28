---
title: rapporten voor Azure MFA aaaAccess en gebruik | Microsoft Docs
description: Hier wordt beschreven hoe toouse Hallo functie van Azure multi-factor Authentication - rapporten.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="101d5-103">Rapporten in Azure multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="101d5-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="101d5-104">Azure multi-factor Authentication bevat verschillende rapporten die kunnen worden gebruikt door u en uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="101d5-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="101d5-105">Deze rapporten zijn toegankelijk via Hallo multi-factor Authentication-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="101d5-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="101d5-106">Hallo Hier volgt een lijst met beschikbare Hallo-rapporten:</span><span class="sxs-lookup"><span data-stu-id="101d5-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="101d5-107">Rapport</span><span class="sxs-lookup"><span data-stu-id="101d5-107">Report</span></span> | <span data-ttu-id="101d5-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="101d5-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="101d5-109">Gebruik</span><span class="sxs-lookup"><span data-stu-id="101d5-109">Usage</span></span> |<span data-ttu-id="101d5-110">Hallo gebruik rapporten informatie weergeven over algemene gebruik Gebruikersoverzicht en details van gebruiker.</span><span class="sxs-lookup"><span data-stu-id="101d5-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="101d5-111">Status van de server</span><span class="sxs-lookup"><span data-stu-id="101d5-111">Server Status</span></span> |<span data-ttu-id="101d5-112">Dit rapport geeft Hallo-status van de multi-factor Authentication-Servers die zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="101d5-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="101d5-113">Geschiedenis van geblokkeerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="101d5-113">Blocked User History</span></span> |<span data-ttu-id="101d5-114">Deze rapporten Hallo geschiedenis van aanvragen tooblock weergeven of gebruikers.</span><span class="sxs-lookup"><span data-stu-id="101d5-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="101d5-115">Geschiedenis van overgeslagen gebruikers</span><span class="sxs-lookup"><span data-stu-id="101d5-115">Bypassed User History</span></span> |<span data-ttu-id="101d5-116">Hallo geeft geschiedenis weer van aanvragen toobypass multi-factor Authentication voor het telefoonnummer van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="101d5-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="101d5-117">Fraudewaarschuwing</span><span class="sxs-lookup"><span data-stu-id="101d5-117">Fraud Alert</span></span> |<span data-ttu-id="101d5-118">Geeft een historie weer van Fraudewaarschuwingen die zijn ingediend in Hallo datumbereik dat die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="101d5-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="101d5-119">In de wachtrij</span><span class="sxs-lookup"><span data-stu-id="101d5-119">Queued</span></span> |<span data-ttu-id="101d5-120">Een lijst met rapporten in de wachtrij voor verwerking en hun status.</span><span class="sxs-lookup"><span data-stu-id="101d5-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="101d5-121">Een koppeling toodownload of weergave Hallo-rapport wordt verstrekt wanneer Hallo rapport voltooid is.</span><span class="sxs-lookup"><span data-stu-id="101d5-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="101d5-122">Rapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="101d5-122">View reports</span></span>
1. <span data-ttu-id="101d5-123">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="101d5-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="101d5-124">Selecteer aan de linkerkant hello, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="101d5-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="101d5-125">Ga als volgt op een van deze twee opties, afhankelijk van of u Auth-Providers gebruiken:</span><span class="sxs-lookup"><span data-stu-id="101d5-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="101d5-126">**Optie 1**: klik op Hallo multi-factor Auth-Providers tabblad. Selecteer de MFA-provider en klikt u op Hallo **beheren** knop Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="101d5-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="101d5-127">**Optie 2**: Selecteer uw directory en ga toohello **configureren** tabblad. Selecteer onder de sectie multi-factor authentication hello, **service-instellingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="101d5-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="101d5-128">Aan de onderkant van de Hallo van Hallo MFA-Service-instellingen pagina, klikt u op Hallo Ga toohello portal-koppeling.</span><span class="sxs-lookup"><span data-stu-id="101d5-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="101d5-129">Selecteer in hello Azure multi-factor Authentication-beheerportal, Hallo type rapport dat u wilt van Hallo **een rapport weergeven** sectie in Hallo linkernavigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="101d5-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="101d5-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="101d5-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="101d5-131">**Aanvullende resources**</span><span class="sxs-lookup"><span data-stu-id="101d5-131">**Additional Resources**</span></span>

* [<span data-ttu-id="101d5-132">Voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="101d5-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="101d5-133">Azure multi-factor Authentication op MSDN</span><span class="sxs-lookup"><span data-stu-id="101d5-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
