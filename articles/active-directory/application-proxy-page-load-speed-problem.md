---
title: Een toepassing toepassingsproxy duurt te lang laden | Microsoft Docs
description: Pagina load prestatieproblemen met de Azure AD-toepassingsproxy oplossen
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
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="5970b-103">Een toepassing toepassingsproxy duurt te lang om te laden</span><span class="sxs-lookup"><span data-stu-id="5970b-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="5970b-104">In dit artikel helpt u bij het begrijpen waarom een Azure AD-toepassingsproxy-toepassing kan lang duren om te laden en wat u kunt doen om dit probleem te verhelpen.</span><span class="sxs-lookup"><span data-stu-id="5970b-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="5970b-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5970b-105">Overview</span></span>
<span data-ttu-id="5970b-106">Als uw toepassingen werken, maar u een lange latentie ziet, mogelijk zijn er enkele kleine trucs in uw netwerktopologie die u overwegen kunt de snelheid verhogen.</span><span class="sxs-lookup"><span data-stu-id="5970b-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="5970b-107">Zie voor een evaluatie van verschillende topologieën, de [netwerk overwegingen document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="5970b-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="5970b-108">Als deze overwegingen niet helpt, er zijn momenteel hebben helaas momenteel geen verdere aanbevelingen voor prestaties afstemmen.</span><span class="sxs-lookup"><span data-stu-id="5970b-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="5970b-109">Als de service voor toepassingsproxy wordt uitgebreid naar meer datacenters die mogelijk dichter bij u, kunt u gaan Zie verbeterde latentie rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="5970b-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="5970b-110">De volledige lijst van Azure-datacenters wilt bekijken, ziet u de [latentie testpagina](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="5970b-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="5970b-111">De datacenters met de service voor toepassingsproxy kunnen gevonden met de [Connectorhulpprogramma poorten Test](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="5970b-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="5970b-112">Feedback over toepassingsproxy data center-locaties</span><span class="sxs-lookup"><span data-stu-id="5970b-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="5970b-113">Mogelijk zijn er Azure-datacenters die toepassingsproxy nog niet zijn maar zou leiden tot een verbetering geweldige latentie voor u.</span><span class="sxs-lookup"><span data-stu-id="5970b-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="5970b-114">De locatie van het datacentrum < aadapfeedback@microsoft.com > zodat we uw feedback als we vouw plannen kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5970b-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="5970b-115">We werken aan enkele aanvullende mogelijkheden die de latentie verbeteren voor tenants die momenteel Zie lang latenties en zorg ervoor dat voor het delen van documentatie zodra deze beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="5970b-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5970b-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5970b-116">Next steps</span></span>
[<span data-ttu-id="5970b-117">Werken met bestaande lokale proxyservers</span><span class="sxs-lookup"><span data-stu-id="5970b-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
