---
title: aaaApplication pagina niet correct weergegeven voor een toepassing toepassingsproxy | Microsoft Docs
description: "Hulp bij het Hallo-pagina is niet correct weergegeven in een toepassing Proxy-toepassing hebt geïntegreerd met Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="c9ee0-103">Toepassingspagina weergegeven niet correct voor een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="c9ee0-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="c9ee0-104">In dit artikel kunt u tootroubleshoot problemen met Azure Active Directory-toepassingsproxy toepassingen wanneer u toohello pagina navigeert, maar er op de pagina Hallo ziet er niet juist.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="c9ee0-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c9ee0-105">Overview</span></span>
<span data-ttu-id="c9ee0-106">Wanneer u een toepassingsproxy-app publiceert, zijn alleen pagina's in uw hoofdmap toegankelijk wanneer toegang tot de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="c9ee0-107">Als het Hallo-pagina is niet correct weergegeven, ontbreekt Hallo hoofdmap interne URL die wordt gebruikt voor de toepassing hello enkele informatiebronnen die pagina.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="c9ee0-108">tooresolve, zorg ervoor dat u hebt gepubliceerd *alle* Hallo resources voor Hallo pagina als onderdeel van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="c9ee0-109">U kunt controleren of dit Hallo probleem is door het openen van het beheer van uw netwerk (zoals Fiddler of F12 extra in Internet Explorer/Edge), Hallo pagina te laden en zoekt u 404-fouten.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="c9ee0-110">Die Hallo-pagina's die momenteel is niet gevonden en moeten nog steeds gepubliceerd toobe aangeeft.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="c9ee0-111">Als een voorbeeld van deze aanvraag, wordt ervan uitgegaan hebt u een toepassing kosten op basis van een interne URL van gepubliceerd <http://myapps/expenses>, maar Hallo app gebruikmaakt van Hallo opmaakmodel <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="c9ee0-112">Hallo opmaakmodel is in dit geval niet gepubliceerd in uw toepassing, zodat u een 404-fout bij poging tooload style.css laden Hallo uitgaven app genereert.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="c9ee0-113">In dit voorbeeld zou Hallo probleem worden opgelost door het publiceren van de toepassing hello met een interne URL <http://myapp/> in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="c9ee0-114">Problemen met de publicatie als één toepassing</span><span class="sxs-lookup"><span data-stu-id="c9ee0-114">Problems with publishing as one application</span></span>

<span data-ttu-id="c9ee0-115">Als het niet mogelijk toopublish alle resources binnen dezelfde toepassing hello, u moet toopublish meerdere toepassingen en koppelingen tussen deze twee inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="c9ee0-116">toodo geval is, wordt u aangeraden Hallo [aangepaste domeinen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) oplossing.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="c9ee0-117">Deze oplossing vereist echter dat u Hallo-certificaat voor uw domein bezit en uw toepassingen volledig gekwalificeerde domeinnamen (FQDN's) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9ee0-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="c9ee0-118">Zie voor andere opties Hallo [verbroken koppelingen documentatie oplossen](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="c9ee0-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9ee0-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c9ee0-119">Next steps</span></span>
[<span data-ttu-id="c9ee0-120">Toepassingen publiceren met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="c9ee0-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
