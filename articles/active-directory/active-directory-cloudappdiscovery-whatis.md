---
title: aaaFinding zonder begeleiding cloud-toepassingen met Cloud App Discovery | Microsoft Docs
description: Bevat informatie over het zoeken en beheren van toepassingen met Cloud App Discovery, wat zijn de voordelen Hallo en hoe het werkt.
services: active-directory
keywords: cloud app discovery, het beheren van toepassingen
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="81a36-104">Cloud-toepassingen zoeken die niet worden beheerd met Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="81a36-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="81a36-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="81a36-105">Overview</span></span>
<span data-ttu-id="81a36-106">In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle Hallo cloud-toepassingen dat leden van hun organisatie toodo hun werk gebruiken.</span><span class="sxs-lookup"><span data-stu-id="81a36-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="81a36-107">Het is gemakkelijk toosee waarom beheerders twijfels over onbevoegde toegang toocorporate gegevens, mogelijk gegevenslekken en andere beveiligingsrisico's hebt zou.</span><span class="sxs-lookup"><span data-stu-id="81a36-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="81a36-108">Dit gebrek aan bewustzijn over kunt maken met het maken van een plan voor het afhandelen van deze beveiligingsrisico's afschrikken.</span><span class="sxs-lookup"><span data-stu-id="81a36-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="81a36-109">Cloud App Discovery is een functie van Azure Active Directory (AD) Premium waarmee u toodiscover cloud-toepassingen wordt gebruikt door Hallo mensen in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="81a36-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="81a36-110">**Met Cloud App Discovery, kunt u het volgende doen:**</span><span class="sxs-lookup"><span data-stu-id="81a36-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="81a36-111">Zoek Hallo cloud-toepassingen wordt gebruikt en dat gebruik meten door het aantal gebruikers, hoeveelheid verkeer of het nummer van de webtoepassing aanvragen toohello.</span><span class="sxs-lookup"><span data-stu-id="81a36-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="81a36-112">Hallo-gebruikers die van een toepassing gebruikmaken te identificeren.</span><span class="sxs-lookup"><span data-stu-id="81a36-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="81a36-113">Exporteer gegevens voor offline-analyse.</span><span class="sxs-lookup"><span data-stu-id="81a36-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="81a36-114">Zorg ervoor dat deze toepassingen onder het IT-beheer en eenmalige aanmelding inschakelen voor gebruikersbeheer.</span><span class="sxs-lookup"><span data-stu-id="81a36-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="81a36-115">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="81a36-115">How it works</span></span>
1. <span data-ttu-id="81a36-116">Toepassing gebruik agents zijn geïnstalleerd op de computers van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="81a36-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="81a36-117">Hallo toepassing informatie over het gebruik wordt vastgelegd door Hallo agents wordt verzonden via een beveiligde, gecodeerde kanaal toohello cloud app discovery-service.</span><span class="sxs-lookup"><span data-stu-id="81a36-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="81a36-118">Hallo Cloud App Discovery-service evalueert Hallo gegevens en genereert rapporten.</span><span class="sxs-lookup"><span data-stu-id="81a36-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Cloud App Discovery-diagram](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="81a36-120">Zie tooget gestart met Cloud App Discovery [ophalen van de slag met Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="81a36-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="81a36-121">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="81a36-121">Related articles</span></span>
* [<span data-ttu-id="81a36-122">Cloud App Discovery beveiligings- en privacyoverwegingen</span><span class="sxs-lookup"><span data-stu-id="81a36-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="81a36-123">Cloud App Discovery Group Policy Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="81a36-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="81a36-124">Implementatiehandleiding voor cloud App Discovery System Center</span><span class="sxs-lookup"><span data-stu-id="81a36-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="81a36-125">Cloud App Discovery-registerinstellingen voor proxyservers met aangepaste poorten</span><span class="sxs-lookup"><span data-stu-id="81a36-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="81a36-126">Cloud App Discovery Agent Changelog</span><span class="sxs-lookup"><span data-stu-id="81a36-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="81a36-127">Veelgestelde vragen over de cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="81a36-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* <span data-ttu-id="81a36-128">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="81a36-128">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>

