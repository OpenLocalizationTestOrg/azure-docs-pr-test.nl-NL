---
title: Het openen van de firewall-poorten die vereist zijn voor een toepassing toepassingsproxy | Microsoft Docs
description: Uitzoeken wat poorten te openen voor de Azure AD-toepassingsproxy correct te laten werken
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="90d93-103">Het openen van de firewall-poorten die vereist zijn voor een toepassing toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="90d93-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="90d93-104">Een volledige lijst met de vereiste poorten en de functie van elke poort, Zie de sectie vereisten van de [toepassingsproxy documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="90d93-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="90d93-105">Houd er rekening mee dat toepassingsproxy alleen uitgaande poorten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="90d93-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="90d93-106">U kunt ook controleren of u beschikt over alle vereiste poorten via openen de [Connectorhulpprogramma poorten Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) vanuit uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="90d93-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="90d93-107">Meer een groen vinkje betekent groter tolerantie.</span><span class="sxs-lookup"><span data-stu-id="90d93-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="90d93-108">Toepassingsproxy van regio 's</span><span class="sxs-lookup"><span data-stu-id="90d93-108">App Proxy regions</span></span>

<span data-ttu-id="90d93-109">We werken op een manier om te laten u weten welke van deze gebieden moet groen voor u.</span><span class="sxs-lookup"><span data-stu-id="90d93-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="90d93-110">Zorg dat ze allemaal zijn op dit moment.</span><span class="sxs-lookup"><span data-stu-id="90d93-110">For now, make sure they all are.</span></span> <span data-ttu-id="90d93-111">VS-midden is ook vereist, ongeacht welke regio in.</span><span class="sxs-lookup"><span data-stu-id="90d93-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="90d93-112">Om te zorgen dat het hulpprogramma kunt u de juiste resultaten, moet u:</span><span class="sxs-lookup"><span data-stu-id="90d93-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="90d93-113">Open het hulpprogramma op een browser van de server waar u de Connector hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="90d93-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="90d93-114">Zorg ervoor dat alle proxy's of de van toepassing op uw Connector firewalls ook worden toegepast op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="90d93-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="90d93-115">Dit kan worden gedaan in Internet Explorer door te gaan naar **instellingen**  - &gt; **Internetopties**  - &gt; **verbindingen**  - &gt; **Lan-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="90d93-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="90d93-116">Op deze pagina ziet u het veld 'Gebruik een Proxy-Server voor uw LAN'.</span><span class="sxs-lookup"><span data-stu-id="90d93-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="90d93-117">Schakel dit in en adres voor de proxyserver in het veld 'Adres' geplaatst.</span><span class="sxs-lookup"><span data-stu-id="90d93-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90d93-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90d93-118">Next steps</span></span>
[<span data-ttu-id="90d93-119">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="90d93-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
