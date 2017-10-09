---
title: aaaHow tooopen Hallo firewallpoorten die nodig zijn voor een toepassing toepassingsproxy | Microsoft Docs
description: Ontdek welke poorten tooopen voor hello Azure AD-toepassingsproxy toowork correct
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="3ea92-103">Hoe tooopen firewallpoorten die nodig zijn voor een toepassing toepassingsproxy Hallo</span><span class="sxs-lookup"><span data-stu-id="3ea92-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="3ea92-104">een volledige lijst met poorten Hallo vereist en de Hallo-functie van elke poort toosee Zie Hallo vereisten sectie Hallo [toepassingsproxy documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="3ea92-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="3ea92-105">Houd er rekening mee dat toepassingsproxy alleen uitgaande poorten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3ea92-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="3ea92-106">U kunt ook controleren of u beschikt over alle vereiste Hallo poorten openen door Hallo openen [Connectorhulpprogramma poorten Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) vanuit uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="3ea92-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="3ea92-107">Meer een groen vinkje betekent groter tolerantie.</span><span class="sxs-lookup"><span data-stu-id="3ea92-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="3ea92-108">Toepassingsproxy van regio 's</span><span class="sxs-lookup"><span data-stu-id="3ea92-108">App Proxy regions</span></span>

<span data-ttu-id="3ea92-109">We werken op een manier die u weet welke van deze gebieden toolet toobe groen voor u moet.</span><span class="sxs-lookup"><span data-stu-id="3ea92-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="3ea92-110">Zorg dat ze allemaal zijn op dit moment.</span><span class="sxs-lookup"><span data-stu-id="3ea92-110">For now, make sure they all are.</span></span> <span data-ttu-id="3ea92-111">VS-midden is ook vereist, ongeacht welke regio in.</span><span class="sxs-lookup"><span data-stu-id="3ea92-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="3ea92-112">toomake ervoor Hallo hulpprogramma biedt u de juiste resultaten Hallo moet:</span><span class="sxs-lookup"><span data-stu-id="3ea92-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="3ea92-113">Hallo-hulpprogramma op een browser openen vanuit Hallo server waar u Hallo Connector hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3ea92-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="3ea92-114">Zorg ervoor dat alle proxy's en firewalls toepasselijk tooyour Connector zijn ook toothis pagina toegepast.</span><span class="sxs-lookup"><span data-stu-id="3ea92-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="3ea92-115">Dit kan worden gedaan in Internet Explorer door te gaan**instellingen**  - &gt; **Internetopties**  - &gt; **verbindingen**  - &gt; **Lan-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="3ea92-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="3ea92-116">Op deze pagina ziet u Hallo veld 'Gebruik een Proxy-Server voor uw LAN'.</span><span class="sxs-lookup"><span data-stu-id="3ea92-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="3ea92-117">Schakel dit selectievakje in en Hallo proxyadres in Hallo 'Adres' veld geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3ea92-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ea92-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3ea92-118">Next steps</span></span>
[<span data-ttu-id="3ea92-119">Azure AD-toepassingsproxy connectors begrijpen</span><span class="sxs-lookup"><span data-stu-id="3ea92-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
