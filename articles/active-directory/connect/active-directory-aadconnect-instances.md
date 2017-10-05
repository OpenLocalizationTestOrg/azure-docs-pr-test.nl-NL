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
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="72723-103">Azure AD Connect: Speciale overwegingen voor exemplaren</span><span class="sxs-lookup"><span data-stu-id="72723-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="72723-104">Azure AD Connect wordt meestal gebruikt met het wereldwijde exemplaar van Azure AD en Office 365.</span><span class="sxs-lookup"><span data-stu-id="72723-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="72723-105">Maar er zijn ook andere exemplaren en deze hebben verschillende vereisten voor de URL's en andere speciale overwegingen.</span><span class="sxs-lookup"><span data-stu-id="72723-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="72723-106">Microsoft Cloud Duitsland</span><span class="sxs-lookup"><span data-stu-id="72723-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="72723-107">De [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) is een soevereine cloud beheerd door een beheerder Duitse gegevens.</span><span class="sxs-lookup"><span data-stu-id="72723-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="72723-108">URL's openen in de proxyserver</span><span class="sxs-lookup"><span data-stu-id="72723-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="72723-109">\*. microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="72723-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="72723-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="72723-110">\*.windows.net</span></span> |
| <span data-ttu-id="72723-111">+ Intrekkingslijsten voor certificaten</span><span class="sxs-lookup"><span data-stu-id="72723-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="72723-112">Wanneer u zich bij uw Azure AD-tenant aanmelden, moet u een account in het domein onmicrosoft.de gebruiken.</span><span class="sxs-lookup"><span data-stu-id="72723-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="72723-113">Functies die momenteel niet aanwezig in de Microsoft Cloud-Duitsland:</span><span class="sxs-lookup"><span data-stu-id="72723-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="72723-114">**Azure AD Connect Health** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72723-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="72723-115">**Automatische updates** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72723-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="72723-116">**Wachtwoord terugschrijven** is beschikbaar voor het voorbeeld met Azure AD Connect versie 1.1.570.0 en na.</span><span class="sxs-lookup"><span data-stu-id="72723-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="72723-117">Andere Azure AD Premium-services zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72723-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="72723-118">Microsoft Azure Government cloud</span><span class="sxs-lookup"><span data-stu-id="72723-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="72723-119">De [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is een cloudservice voor de overheid.</span><span class="sxs-lookup"><span data-stu-id="72723-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="72723-120">Deze cloud werd ondersteund door eerdere releases van DirSync.</span><span class="sxs-lookup"><span data-stu-id="72723-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="72723-121">Vanaf build 1.1.180 van Azure AD Connect, zijn de volgende generatie van de cloud wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="72723-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="72723-122">Deze generatie alleen VS gebaseerde eindpunten gebruikt en een andere lijst met URL's openen in uw proxy-server hebben.</span><span class="sxs-lookup"><span data-stu-id="72723-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="72723-123">URL's openen in de proxyserver</span><span class="sxs-lookup"><span data-stu-id="72723-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="72723-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="72723-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="72723-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="72723-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="72723-126">\*. gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="72723-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="72723-127">+ Intrekkingslijsten voor certificaten</span><span class="sxs-lookup"><span data-stu-id="72723-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="72723-128">Azure AD Connect kan niet automatisch detecteren dat uw Azure AD-tenant bevindt zich in de cloud van de overheid.</span><span class="sxs-lookup"><span data-stu-id="72723-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="72723-129">In plaats daarvan moet u de volgende acties uitvoeren als u Azure AD Connect installeert.</span><span class="sxs-lookup"><span data-stu-id="72723-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="72723-130">Start de installatie van Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="72723-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="72723-131">Wanneer u de eerste pagina waar u gewoonlijk accepteer de gebruiksrechtovereenkomst ziet, niet worden voortgezet, maar laat u de installatiewizard uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="72723-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="72723-132">Start regedit en wijzigt u de registersleutel `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` op de waarde `2`.</span><span class="sxs-lookup"><span data-stu-id="72723-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="72723-133">Ga terug naar de Azure AD Connect-installatiewizard, accepteer de gebruiksrechtovereenkomst en doorgaan.</span><span class="sxs-lookup"><span data-stu-id="72723-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="72723-134">Controleer of u tijdens de installatie van de **aangepaste configuratie** installatie pad (en niet de Express-installatie).</span><span class="sxs-lookup"><span data-stu-id="72723-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="72723-135">Ga vervolgens door gewoon de installatie.</span><span class="sxs-lookup"><span data-stu-id="72723-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="72723-136">Functies die momenteel niet aanwezig in de Microsoft Azure Government cloud:</span><span class="sxs-lookup"><span data-stu-id="72723-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="72723-137">**Azure AD Connect Health** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72723-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="72723-138">**Automatische updates** is niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72723-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="72723-139">**Wachtwoord terugschrijven** is beschikbaar voor het voorbeeld met Azure AD Connect versie 1.1.570.0 en na.</span><span class="sxs-lookup"><span data-stu-id="72723-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="72723-140">Andere Azure AD Premium-services zijn niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="72723-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72723-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72723-141">Next steps</span></span>
<span data-ttu-id="72723-142">Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="72723-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
