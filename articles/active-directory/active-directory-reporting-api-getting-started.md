---
title: aaaGetting de slag met Azure AD Hallo reporting API in de klassieke portal hello Azure AD | Microsoft Docs
description: Hoe tooget gestart Hello Azure Active Directory-rapportage-API
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="c5246-103">Aan de slag met Azure Active Directory rapportage-API in de klassieke portal hello Azure AD Hallo</span><span class="sxs-lookup"><span data-stu-id="c5246-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="c5246-104">*In dit onderwerp maakt deel uit van Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="c5246-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="c5246-105">Azure Active Directory beschikt u over tal van rapporten.</span><span class="sxs-lookup"><span data-stu-id="c5246-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="c5246-106">Hallo-gegevens van deze rapporten kunnen zeer nuttig tooyour toepassingen, zoals de SIEM-systemen, controle en hulpprogramma's voor bedrijfsinformatie worden.</span><span class="sxs-lookup"><span data-stu-id="c5246-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="c5246-107">Hello Azure AD rapportage-API's bieden toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="c5246-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="c5246-108">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="c5246-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c5246-109">In dit artikel vindt u Hallo informatie moet u de slag met Azure AD Hallo rapportage tooget API's.</span><span class="sxs-lookup"><span data-stu-id="c5246-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="c5246-110">In de volgende sectie hello u meer informatie over het gebruik van Hallo controleren en meld u API's.</span><span class="sxs-lookup"><span data-stu-id="c5246-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="c5246-111">Zie voor andere API Hallo [Azure AD-rapporten en events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artikel.</span><span class="sxs-lookup"><span data-stu-id="c5246-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="c5246-112">Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c5246-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="c5246-113">Leertraject</span><span class="sxs-lookup"><span data-stu-id="c5246-113">Learning map</span></span>
1. <span data-ttu-id="c5246-114">**Voorbereiden** -voordat u uw API-voorbeelden testen kunt, moet u toocomplete hello [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c5246-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="c5246-115">**Verken** -ophalen van een eerste indruk Hallo rapportage-API's:</span><span class="sxs-lookup"><span data-stu-id="c5246-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="c5246-116">Met behulp van Hallo voorbeelden voor Hallo audit API</span><span class="sxs-lookup"><span data-stu-id="c5246-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="c5246-117">Met behulp van Hallo voorbeelden voor Hallo aanmeldingsactiviteiten rapport API</span><span class="sxs-lookup"><span data-stu-id="c5246-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="c5246-118">**Aanpassen** -Maak uw eigen oplossing:</span><span class="sxs-lookup"><span data-stu-id="c5246-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="c5246-119">Met behulp van Hallo audit API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="c5246-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="c5246-120">Hallo aanmeldingsactiviteiten rapport met API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="c5246-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="c5246-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c5246-121">Next Steps</span></span>
<span data-ttu-id="c5246-122">Als u weten toosee alle beschikbare Azure AD Graph API-eindpunten door te navigeren Hallo[https://graph.windows.net/tenant-name/reports/$ metagegevens? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="c5246-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

