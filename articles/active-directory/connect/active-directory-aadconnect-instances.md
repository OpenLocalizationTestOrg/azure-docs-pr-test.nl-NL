---
title: 'Azure AD Connect: Service-exemplaren synchroniseren | Microsoft Docs'
description: Deze pagina worden speciale overwegingen voor exemplaren van Azure AD.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="7f585-103">Azure AD Connect: Speciale overwegingen voor exemplaren</span><span class="sxs-lookup"><span data-stu-id="7f585-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="7f585-104">Azure AD Connect wordt meestal gebruikt met hello world wide exemplaar van Azure AD en Office 365.</span><span class="sxs-lookup"><span data-stu-id="7f585-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="7f585-105">Maar er zijn ook andere exemplaren en deze hebben verschillende vereisten voor de URL's en andere speciale overwegingen.</span><span class="sxs-lookup"><span data-stu-id="7f585-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="7f585-106">Microsoft Cloud Duitsland</span><span class="sxs-lookup"><span data-stu-id="7f585-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="7f585-107">Hallo [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) is een soevereine cloud beheerd door een beheerder Duitse gegevens.</span><span class="sxs-lookup"><span data-stu-id="7f585-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="7f585-108">URL's tooopen in proxyserver</span><span class="sxs-lookup"><span data-stu-id="7f585-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="7f585-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="7f585-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="7f585-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="7f585-110">\*.windows.net</span></span> |
| <span data-ttu-id="7f585-111">+ Intrekkingslijsten voor certificaten</span><span class="sxs-lookup"><span data-stu-id="7f585-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="7f585-112">Wanneer u zich aanmeldt tooyour Azure AD-tenant, moet u een account in Hallo onmicrosoft.de domein gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7f585-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="7f585-113">Functies die momenteel niet aanwezig in Hallo Microsoft Cloud Duitsland:</span><span class="sxs-lookup"><span data-stu-id="7f585-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="7f585-114">**Azure AD Connect Health** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f585-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="7f585-115">**Automatische updates** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f585-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="7f585-116">**Wachtwoord terugschrijven** is beschikbaar voor het voorbeeld met Azure AD Connect versie 1.1.570.0 en na.</span><span class="sxs-lookup"><span data-stu-id="7f585-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="7f585-117">Andere Azure AD Premium-services zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f585-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="7f585-118">Microsoft Azure Government cloud</span><span class="sxs-lookup"><span data-stu-id="7f585-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="7f585-119">Hallo [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is een cloudservice voor de overheid.</span><span class="sxs-lookup"><span data-stu-id="7f585-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="7f585-120">Deze cloud werd ondersteund door eerdere releases van DirSync.</span><span class="sxs-lookup"><span data-stu-id="7f585-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="7f585-121">Vanaf build 1.1.180 van Azure AD Connect wordt Hallo volgende generatie Hallo cloud ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7f585-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="7f585-122">Deze generatie alleen VS gebaseerde eindpunten gebruikt en een andere lijst met URL's tooopen hebben in uw proxy-server.</span><span class="sxs-lookup"><span data-stu-id="7f585-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="7f585-123">URL's tooopen in proxyserver</span><span class="sxs-lookup"><span data-stu-id="7f585-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="7f585-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7f585-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="7f585-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="7f585-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="7f585-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7f585-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="7f585-127">+ Intrekkingslijsten voor certificaten</span><span class="sxs-lookup"><span data-stu-id="7f585-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="7f585-128">Kan geen Azure AD Connect tooautomatically detecteren dat uw Azure AD-tenant bevindt zich in de cloud van de overheid Hallo.</span><span class="sxs-lookup"><span data-stu-id="7f585-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="7f585-129">In plaats daarvan moet u tootake Hallo van de volgende activiteiten wanneer u Azure AD Connect installeert.</span><span class="sxs-lookup"><span data-stu-id="7f585-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="7f585-130">Hello Azure AD Connect-installatie start.</span><span class="sxs-lookup"><span data-stu-id="7f585-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="7f585-131">Wanneer er Hallo van de eerste pagina waar u gewoonlijk tooaccept Hallo overeenkomst, niet worden voortgezet, maar laat Hallo-installatiewizard uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7f585-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="7f585-132">Start regedit en wijzigt u de registersleutel Hallo `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello waarde `2`.</span><span class="sxs-lookup"><span data-stu-id="7f585-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="7f585-133">Ga terug toohello Azure AD Connect-installatiewizard, Hallo overeenkomst te accepteren en doorgaan.</span><span class="sxs-lookup"><span data-stu-id="7f585-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="7f585-134">Zorg ervoor dat toouse Hallo tijdens de installatie van **aangepaste configuratie** installatie pad (en niet de Express-installatie).</span><span class="sxs-lookup"><span data-stu-id="7f585-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="7f585-135">Ga vervolgens door gewoon Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="7f585-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="7f585-136">Functies die momenteel niet aanwezig in Hallo Microsoft Azure Government cloud:</span><span class="sxs-lookup"><span data-stu-id="7f585-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="7f585-137">**Azure AD Connect Health** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f585-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="7f585-138">**Automatische updates** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f585-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="7f585-139">**Wachtwoord terugschrijven** is beschikbaar voor het voorbeeld met Azure AD Connect versie 1.1.570.0 en na.</span><span class="sxs-lookup"><span data-stu-id="7f585-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="7f585-140">Andere Azure AD Premium-services zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f585-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f585-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f585-141">Next steps</span></span>
<span data-ttu-id="7f585-142">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="7f585-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
