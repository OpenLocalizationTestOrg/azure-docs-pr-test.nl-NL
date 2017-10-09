---
title: aaaAn toepassingsproxy-toepassing duurt te lang tooload | Microsoft Docs
description: Pagina load prestatieproblemen Hello Azure AD-toepassingsproxy oplossen
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="4d939-103">Een toepassing toepassingsproxy duurt te lang tooload</span><span class="sxs-lookup"><span data-stu-id="4d939-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="4d939-104">In dit artikel kunt u toounderstand waarom een Azure AD-toepassingsproxy-toepassing duurt een tooload lang en wat u kunt tooresolve doen dit probleem.</span><span class="sxs-lookup"><span data-stu-id="4d939-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="4d939-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4d939-105">Overview</span></span>
<span data-ttu-id="4d939-106">Als uw toepassingen werken, maar u een lange latentie ziet, mogelijk zijn er enkele kleine trucs in uw netwerktopologie die u, tooimprove Hallo snelheid overwegen kunt.</span><span class="sxs-lookup"><span data-stu-id="4d939-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="4d939-107">Zie voor een evaluatieversie van verschillende topologieën Hallo [netwerk overwegingen document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="4d939-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="4d939-108">Als deze overwegingen niet helpt, er zijn momenteel hebben helaas momenteel geen verdere aanbevelingen voor prestaties afstemmen.</span><span class="sxs-lookup"><span data-stu-id="4d939-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="4d939-109">U kunt toosee verbeterde latentie zoals Hallo service voor toepassingsproxy wordt toomore-datacenters die dichter tooyou kunnen worden uitgebreid, rechtstreeks starten.</span><span class="sxs-lookup"><span data-stu-id="4d939-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="4d939-110">toosee hello volledige lijst met Azure data centers, ziet u Hallo [latentie testpagina](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="4d939-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="4d939-111">Hallo datacenters met service voor toepassingsproxy Hallo vindt Hello [Connectorhulpprogramma poorten Test](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="4d939-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="4d939-112">Feedback over toepassingsproxy data center-locaties</span><span class="sxs-lookup"><span data-stu-id="4d939-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="4d939-113">Mogelijk zijn er Azure-datacenters die toepassingsproxy nog niet zijn maar zou leiden tooa geweldige latentie verbetering voor u.</span><span class="sxs-lookup"><span data-stu-id="4d939-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="4d939-114">Hallo-datacentrum locatie < aadapfeedback@microsoft.com > zodat we uw feedback tooplan gebruiken kunt als we uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="4d939-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="4d939-115">We werken aan enkele aanvullende mogelijkheden Hallo-latentie verbeteren voor tenants die momenteel Zie lang latenties en ervoor tooshare documentatie zodra deze beschikbaar worden.</span><span class="sxs-lookup"><span data-stu-id="4d939-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d939-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d939-116">Next steps</span></span>
[<span data-ttu-id="4d939-117">Werken met bestaande lokale proxyservers</span><span class="sxs-lookup"><span data-stu-id="4d939-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
