---
title: Toepassingspagina niet correct weergegeven voor een toepassing toepassingsproxy | Microsoft Docs
description: "Richtlijnen wanneer de pagina is niet correct in een toepassing Proxy-toepassing weergegeven hebt geïntegreerd met Azure AD"
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="e2847-103">Toepassingspagina weergegeven niet correct voor een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="e2847-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="e2847-104">In dit artikel helpt u bij het oplossen van problemen met Azure Active Directory-toepassingsproxy toepassingen wanneer u naar de pagina navigeren, maar er op de pagina ziet er niet juist.</span><span class="sxs-lookup"><span data-stu-id="e2847-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="e2847-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e2847-105">Overview</span></span>
<span data-ttu-id="e2847-106">Wanneer u een toepassingsproxy-app publiceert, zijn alleen pagina's in uw hoofdmap toegankelijk bij het openen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2847-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="e2847-107">Als de pagina is niet correct weergegeven, kan de interne basis-URL voor de toepassing gebruikt enkele pagina resources ontbreken.</span><span class="sxs-lookup"><span data-stu-id="e2847-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="e2847-108">Om op te lossen, zorg ervoor dat u hebt gepubliceerd *alle* de resources voor de pagina als onderdeel van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2847-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="e2847-109">U kunt controleren of dit het probleem is door het openen van het beheer van uw netwerk (zoals Fiddler of F12 extra in Internet Explorer/Edge), de pagina te laden en zoekt 404-fouten.</span><span class="sxs-lookup"><span data-stu-id="e2847-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="e2847-110">Die aangeeft dat de pagina's die momenteel is niet gevonden en kunnen nog steeds moeten worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="e2847-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="e2847-111">Als een voorbeeld van deze aanvraag, wordt ervan uitgegaan hebt u een toepassing kosten op basis van een interne URL van gepubliceerd <http://myapps/expenses>, maar de app gebruikmaakt van het opmaakmodel <http://myapps/style.css>.</span><span class="sxs-lookup"><span data-stu-id="e2847-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="e2847-112">Het opmaakmodel is in dit geval niet gepubliceerd in uw toepassing, zodat u een 404-fout tijdens het laden van style.css bij het laden van de app uitgaven genereert.</span><span class="sxs-lookup"><span data-stu-id="e2847-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="e2847-113">In dit voorbeeld zou het probleem worden opgelost door de toepassing met een interne URL publiceert <http://myapp/> in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="e2847-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="e2847-114">Problemen met de publicatie als één toepassing</span><span class="sxs-lookup"><span data-stu-id="e2847-114">Problems with publishing as one application</span></span>

<span data-ttu-id="e2847-115">Als het niet mogelijk om alle bronnen binnen dezelfde toepassing te publiceren, moet u meerdere toepassingen publiceren en koppelingen tussen deze twee inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e2847-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="e2847-116">Om dit te doen, wordt u aangeraden de [aangepaste domeinen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) oplossing.</span><span class="sxs-lookup"><span data-stu-id="e2847-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="e2847-117">Deze oplossing vereist echter dat de eigenaar van het certificaat voor uw domein en uw toepassingen volledig gekwalificeerde domeinnamen (FQDN's) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2847-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="e2847-118">Zie voor andere opties, de [verbroken koppelingen documentatie oplossen](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span><span class="sxs-lookup"><span data-stu-id="e2847-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2847-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2847-119">Next steps</span></span>
[<span data-ttu-id="e2847-120">Toepassingen publiceren met Azure AD-toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="e2847-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
