---
title: Zoeken naar niet-beheerde cloud-toepassingen met Cloud App Discovery | Microsoft Docs
description: Bevat informatie over het zoeken en beheren van toepassingen met Cloud App Discovery, wat zijn de voordelen en hoe het werkt.
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="5710b-104">Cloud-toepassingen zoeken die niet worden beheerd met Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="5710b-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="5710b-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5710b-105">Overview</span></span>
<span data-ttu-id="5710b-106">In moderne ondernemingen zijn IT-afdelingen vaak niet op de hoogte van alle cloudtoepassingen die leden van hun organisatie gebruikmaken voor hun werk.</span><span class="sxs-lookup"><span data-stu-id="5710b-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="5710b-107">Het is gemakkelijk om te zien waarom beheerders zou twijfels hebt over niet-geautoriseerde toegang tot zakelijke gegevens, mogelijk gegevenslekken en andere beveiligingsrisico's.</span><span class="sxs-lookup"><span data-stu-id="5710b-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="5710b-108">Dit gebrek aan bewustzijn over kunt maken met het maken van een plan voor het afhandelen van deze beveiligingsrisico's afschrikken.</span><span class="sxs-lookup"><span data-stu-id="5710b-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="5710b-109">Cloud App Discovery is een functie van Azure Active Directory (AD) Premium waarmee u voor het detecteren van cloud-toepassingen wordt gebruikt door mensen in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="5710b-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="5710b-110">**Met Cloud App Discovery, kunt u het volgende doen:**</span><span class="sxs-lookup"><span data-stu-id="5710b-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="5710b-111">Zoeken naar de cloudtoepassingen die worden gebruikt en dat gebruik meten door het aantal gebruikers, hoeveelheid verkeer of aantal webaanvragen naar de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5710b-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="5710b-112">De gebruikers die van een toepassing gebruikmaken te identificeren.</span><span class="sxs-lookup"><span data-stu-id="5710b-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="5710b-113">Exporteer gegevens voor offline-analyse.</span><span class="sxs-lookup"><span data-stu-id="5710b-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="5710b-114">Zorg ervoor dat deze toepassingen onder het IT-beheer en eenmalige aanmelding inschakelen voor gebruikersbeheer.</span><span class="sxs-lookup"><span data-stu-id="5710b-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="5710b-115">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="5710b-115">How it works</span></span>
1. <span data-ttu-id="5710b-116">Toepassing gebruik agents zijn geïnstalleerd op de computers van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="5710b-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="5710b-117">De gebruiksgegevens van de toepassing wordt vastgelegd door de agents is verzonden via een beveiligde, gecodeerde kanaal naar de cloud app discovery-service.</span><span class="sxs-lookup"><span data-stu-id="5710b-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="5710b-118">De Cloud App Discovery-service evalueert de gegevens en genereert rapporten.</span><span class="sxs-lookup"><span data-stu-id="5710b-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Cloud App Discovery-diagram](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="5710b-120">Aan de slag met Cloud App Discovery Zie [ophalen van de slag met Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="5710b-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="5710b-121">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="5710b-121">Related articles</span></span>
* [<span data-ttu-id="5710b-122">Cloud App Discovery beveiligings- en privacyoverwegingen</span><span class="sxs-lookup"><span data-stu-id="5710b-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="5710b-123">Cloud App Discovery Group Policy Deployment Guide</span><span class="sxs-lookup"><span data-stu-id="5710b-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="5710b-124">Implementatiehandleiding voor cloud App Discovery System Center</span><span class="sxs-lookup"><span data-stu-id="5710b-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="5710b-125">Cloud App Discovery-registerinstellingen voor proxyservers met aangepaste poorten</span><span class="sxs-lookup"><span data-stu-id="5710b-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="5710b-126">Cloud App Discovery Agent Changelog</span><span class="sxs-lookup"><span data-stu-id="5710b-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="5710b-127">Veelgestelde vragen over de cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="5710b-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* <span data-ttu-id="5710b-128">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="5710b-128">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>

