---
title: Aan de slag met Azure AD rapportage-API in de klassieke Azure AD-portal | Microsoft Docs
description: Hoe u aan de slag met de Azure Active Directory rapportage-API
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="888c3-103">Aan de slag met de Azure Active Directory rapportage-API in de klassieke Azure AD-portal</span><span class="sxs-lookup"><span data-stu-id="888c3-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="888c3-104">*In dit onderwerp maakt deel uit van de [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="888c3-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="888c3-105">Azure Active Directory beschikt u over tal van rapporten.</span><span class="sxs-lookup"><span data-stu-id="888c3-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="888c3-106">De gegevens van deze rapporten kunnen zeer nuttig zijn voor uw toepassingen, zoals SIEM-systemen, audit- en business intelligence-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="888c3-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="888c3-107">De API's van Azure AD Reporting bieden toegang tot de gegevens op programmeerniveau via een set op REST-gebaseerde API's.</span><span class="sxs-lookup"><span data-stu-id="888c3-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="888c3-108">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="888c3-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="888c3-109">In dit artikel biedt u de informatie die u moet aan de slag met Azure AD rapportage-API's.</span><span class="sxs-lookup"><span data-stu-id="888c3-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="888c3-110">In de volgende sectie stelt u meer informatie over het gebruik van de audit en meld u API's.</span><span class="sxs-lookup"><span data-stu-id="888c3-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="888c3-111">Voor alle andere API's, Zie de [Azure AD-rapporten en events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artikel.</span><span class="sxs-lookup"><span data-stu-id="888c3-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="888c3-112">Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="888c3-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="888c3-113">Leertraject</span><span class="sxs-lookup"><span data-stu-id="888c3-113">Learning map</span></span>
1. <span data-ttu-id="888c3-114">**Voorbereiden** -voordat u uw API-voorbeelden testen kunt, u moet voltooien de [vereisten voor toegang tot de Azure AD rapportage-API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="888c3-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="888c3-115">**Verken** -ophalen van een eerste indruk van de rapportage-API's:</span><span class="sxs-lookup"><span data-stu-id="888c3-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="888c3-116">Met behulp van de voorbeelden voor de API-controle</span><span class="sxs-lookup"><span data-stu-id="888c3-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="888c3-117">Met behulp van de voorbeelden voor het rapport aanmeldingsactiviteiten API</span><span class="sxs-lookup"><span data-stu-id="888c3-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="888c3-118">**Aanpassen** -Maak uw eigen oplossing:</span><span class="sxs-lookup"><span data-stu-id="888c3-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="888c3-119">Met behulp van de audit API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="888c3-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="888c3-120">Met behulp van de aanmeldingsactiviteiten rapport API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="888c3-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="888c3-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="888c3-121">Next Steps</span></span>
<span data-ttu-id="888c3-122">Als u wilt alle van de beschikbare Azure AD Graph API-eindpunten bekijken door te navigeren naar [https://graph.windows.net/tenant-name/reports/$ metagegevens? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="888c3-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

