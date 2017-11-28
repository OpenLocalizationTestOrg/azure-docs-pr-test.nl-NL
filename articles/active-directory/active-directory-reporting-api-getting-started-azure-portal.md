---
title: aaaGetting gestart met hello Azure AD-rapportage-API | Microsoft Docs
description: Hoe tooget gestart Hello Azure Active Directory-rapportage-API
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="db2a6-103">Aan de slag met Azure Active Directory-rapportage API Hallo</span><span class="sxs-lookup"><span data-stu-id="db2a6-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="db2a6-104">Azure Active Directory beschikt u over tal van rapporten.</span><span class="sxs-lookup"><span data-stu-id="db2a6-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="db2a6-105">Hallo-gegevens van deze rapporten kunnen zeer nuttig tooyour toepassingen, zoals de SIEM-systemen, controle en hulpprogramma's voor bedrijfsinformatie worden.</span><span class="sxs-lookup"><span data-stu-id="db2a6-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="db2a6-106">Hello Azure AD rapportage-API's bieden toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's.</span><span class="sxs-lookup"><span data-stu-id="db2a6-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="db2a6-107">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="db2a6-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="db2a6-108">In dit artikel vindt u Hallo informatie moet u de slag met Azure AD Hallo rapportage tooget API's.</span><span class="sxs-lookup"><span data-stu-id="db2a6-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="db2a6-109">In de volgende sectie hello u meer informatie over het gebruik van Hallo controleren en meld u API's.</span><span class="sxs-lookup"><span data-stu-id="db2a6-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="db2a6-110">Veelgestelde vragen Lees onze [Veelgestelde vragen over](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="db2a6-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="db2a6-111">Voer de gegevens voor problemen [een ondersteuningsticket bestand](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="db2a6-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="db2a6-112">Leertraject</span><span class="sxs-lookup"><span data-stu-id="db2a6-112">Learning map</span></span>
1. <span data-ttu-id="db2a6-113">**Voorbereiden** -voordat u uw API-voorbeelden testen kunt, moet u toocomplete hello [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db2a6-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="db2a6-114">**Verken** -ophalen van een eerste indruk Hallo rapportage-API's:</span><span class="sxs-lookup"><span data-stu-id="db2a6-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="db2a6-115">Met behulp van Hallo voorbeelden voor Hallo audit API</span><span class="sxs-lookup"><span data-stu-id="db2a6-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="db2a6-116">Met behulp van Hallo voorbeelden voor Hallo aanmeldingsactiviteiten rapport API</span><span class="sxs-lookup"><span data-stu-id="db2a6-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="db2a6-117">**Aanpassen** -Maak uw eigen oplossing:</span><span class="sxs-lookup"><span data-stu-id="db2a6-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="db2a6-118">Met behulp van Hallo audit API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="db2a6-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="db2a6-119">Hallo aanmeldingsactiviteiten rapport met API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="db2a6-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="db2a6-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="db2a6-120">Next Steps</span></span>
<span data-ttu-id="db2a6-121">Als u weten toosee alle beschikbare Azure AD Graph API-eindpunten, gebruik je deze link: [https://graph.windows.net/tenant-name/activities/$ metagegevens? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="db2a6-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

