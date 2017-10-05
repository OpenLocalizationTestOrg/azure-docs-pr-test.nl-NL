---
title: Aan de slag met Azure AD rapportage-API | Microsoft Docs
description: Hoe u aan de slag met de Azure Active Directory rapportage-API
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
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="8acf9-103">Aan de slag met de Azure Active Directory rapportage-API</span><span class="sxs-lookup"><span data-stu-id="8acf9-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="8acf9-104">Azure Active Directory beschikt u over tal van rapporten.</span><span class="sxs-lookup"><span data-stu-id="8acf9-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="8acf9-105">De gegevens van deze rapporten kunnen zeer nuttig zijn voor uw toepassingen, zoals SIEM-systemen, audit- en business intelligence-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="8acf9-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="8acf9-106">De API's van Azure AD Reporting bieden toegang tot de gegevens op programmeerniveau via een set op REST-gebaseerde API's.</span><span class="sxs-lookup"><span data-stu-id="8acf9-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="8acf9-107">U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="8acf9-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="8acf9-108">In dit artikel biedt u de informatie die u moet aan de slag met Azure AD rapportage-API's.</span><span class="sxs-lookup"><span data-stu-id="8acf9-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="8acf9-109">In de volgende sectie stelt u meer informatie over het gebruik van de audit en meld u API's.</span><span class="sxs-lookup"><span data-stu-id="8acf9-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="8acf9-110">Veelgestelde vragen Lees onze [Veelgestelde vragen over](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="8acf9-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="8acf9-111">Voer de gegevens voor problemen [een ondersteuningsticket bestand](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="8acf9-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="8acf9-112">Leertraject</span><span class="sxs-lookup"><span data-stu-id="8acf9-112">Learning map</span></span>
1. <span data-ttu-id="8acf9-113">**Voorbereiden** -voordat u uw API-voorbeelden testen kunt, u moet voltooien de [vereisten voor toegang tot de Azure AD rapportage-API](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8acf9-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="8acf9-114">**Verken** -ophalen van een eerste indruk van de rapportage-API's:</span><span class="sxs-lookup"><span data-stu-id="8acf9-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="8acf9-115">Met behulp van de voorbeelden voor de API-controle</span><span class="sxs-lookup"><span data-stu-id="8acf9-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="8acf9-116">Met behulp van de voorbeelden voor het rapport aanmeldingsactiviteiten API</span><span class="sxs-lookup"><span data-stu-id="8acf9-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="8acf9-117">**Aanpassen** -Maak uw eigen oplossing:</span><span class="sxs-lookup"><span data-stu-id="8acf9-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="8acf9-118">Met behulp van de audit API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="8acf9-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="8acf9-119">Met behulp van de aanmeldingsactiviteiten rapport API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="8acf9-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="8acf9-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8acf9-120">Next Steps</span></span>
<span data-ttu-id="8acf9-121">Als u wilt zien van alle beschikbare Azure AD Graph API-eindpunten, gebruikt u deze koppeling: [https://graph.windows.net/tenant-name/activities/$ metagegevens? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="8acf9-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

