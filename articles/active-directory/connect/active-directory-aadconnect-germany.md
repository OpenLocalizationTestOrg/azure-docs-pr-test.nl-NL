---
title: aaaAzure AD Connect in de Microsoft Cloud Duitsland
description: "Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide."
keywords: Inleiding tooAzure AD Connect, overzicht van Azure AD Connect, wat is Azure AD Connect, active directory, Duitsland, zwart Forest installeren
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="c98c2-105">Azure AD Connect in Microsoft Cloud Duitsland - Openbare preview</span><span class="sxs-lookup"><span data-stu-id="c98c2-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="c98c2-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="c98c2-106">Introduction</span></span>
<span data-ttu-id="c98c2-107">Azure AD Connect voorziet in synchronisatie tussen uw on-premises Active Directory en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c98c2-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="c98c2-108">Op dit moment veel Hallo scenario's in [Microsoft Cloud Duitsland](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) door Hallo operator moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c98c2-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="c98c2-109">Wanneer u Microsoft Cloud Duitsland gebruikt, moet u zich bewust zijn van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c98c2-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="c98c2-110">Hallo die volgende URL's moeten worden geopend op een proxyserver voor synchronisatie toooccur is:</span><span class="sxs-lookup"><span data-stu-id="c98c2-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="c98c2-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="c98c2-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="c98c2-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="c98c2-112">*.windows.net</span></span>
  * * <span data-ttu-id="c98c2-113">Certificaatintrekkingslijsten</span><span class="sxs-lookup"><span data-stu-id="c98c2-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="c98c2-114">Wanneer u Azure AD-directory tooyour aanmelden, moet u een account in Hallo onmicrosoft.de domein.</span><span class="sxs-lookup"><span data-stu-id="c98c2-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="c98c2-115">Hallo volgende kenmerken zijn niet beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="c98c2-115">hello following features are not available:</span></span>
  * <span data-ttu-id="c98c2-116">Azure AD Connect Health (Engelstalig)</span><span class="sxs-lookup"><span data-stu-id="c98c2-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="c98c2-117">Automatische updates</span><span class="sxs-lookup"><span data-stu-id="c98c2-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="c98c2-118">Downloaden</span><span class="sxs-lookup"><span data-stu-id="c98c2-118">Download</span></span>
<span data-ttu-id="c98c2-119">U kunt Azure AD Connect downloaden van Azure AD Connect-blade Hallo binnen Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="c98c2-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="c98c2-120">Gebruik onderstaande toolocate hello Azure AD Connect-blade Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="c98c2-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="c98c2-121">Hello Azure AD Connect-Blade</span><span class="sxs-lookup"><span data-stu-id="c98c2-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="c98c2-122">Wanneer u bent aangemeld in toohello Azure-portal, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="c98c2-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="c98c2-123">Ga tooBrowse</span><span class="sxs-lookup"><span data-stu-id="c98c2-123">Go tooBrowse</span></span>
2. <span data-ttu-id="c98c2-124">Selecteer Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c98c2-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="c98c2-125">Selecteer vervolgens Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c98c2-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="c98c2-126">Hier ziet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c98c2-126">You should see hello following:</span></span>

![De Azure AD Connect-blade](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="c98c2-128">Hello volgende tabel worden weergegeven in de blade Hallo Hallo-functies.</span><span class="sxs-lookup"><span data-stu-id="c98c2-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="c98c2-129">Titel</span><span class="sxs-lookup"><span data-stu-id="c98c2-129">Title</span></span> | <span data-ttu-id="c98c2-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c98c2-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c98c2-131">SYNCHRONISATIESTATUS</span><span class="sxs-lookup"><span data-stu-id="c98c2-131">SYNC STATUS</span></span> |<span data-ttu-id="c98c2-132">Hier ziet u of synchronisatie is in- of uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c98c2-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="c98c2-133">LAATSTE SYNCHRONISATIE</span><span class="sxs-lookup"><span data-stu-id="c98c2-133">LAST SYNC</span></span> |<span data-ttu-id="c98c2-134">Hallo laatste keer dat een geslaagde synchronisatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c98c2-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="c98c2-135">FEDERATIEVE DOMEINEN</span><span class="sxs-lookup"><span data-stu-id="c98c2-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="c98c2-136">Toont Hallo aantal federatieve domeinen die momenteel zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c98c2-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="c98c2-137">Installeren</span><span class="sxs-lookup"><span data-stu-id="c98c2-137">Installation</span></span>
<span data-ttu-id="c98c2-138">Azure AD Connect tooinstall, kunt u documentatie Hallo [hier](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="c98c2-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="c98c2-139">Geavanceerde functies en aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="c98c2-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="c98c2-140">Zie [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md) voor meer informatie en tips over aangepaste instellingen en geavanceerde configuraties.</span><span class="sxs-lookup"><span data-stu-id="c98c2-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="c98c2-141">Deze pagina bevat informatie en koppelingen tooadditional richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="c98c2-141">This page provides information and links tooadditional guidance.</span></span>

