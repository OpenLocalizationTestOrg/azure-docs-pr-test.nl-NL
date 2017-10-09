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
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Een toepassing toepassingsproxy duurt te lang tooload

In dit artikel kunt u toounderstand waarom een Azure AD-toepassingsproxy-toepassing duurt een tooload lang en wat u kunt tooresolve doen dit probleem.

## <a name="overview"></a>Overzicht
Als uw toepassingen werken, maar u een lange latentie ziet, mogelijk zijn er enkele kleine trucs in uw netwerktopologie die u, tooimprove Hallo snelheid overwegen kunt. Zie voor een evaluatieversie van verschillende topologieën Hallo [netwerk overwegingen document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Als deze overwegingen niet helpt, er zijn momenteel hebben helaas momenteel geen verdere aanbevelingen voor prestaties afstemmen. U kunt toosee verbeterde latentie zoals Hallo service voor toepassingsproxy wordt toomore-datacenters die dichter tooyou kunnen worden uitgebreid, rechtstreeks starten. toosee hello volledige lijst met Azure data centers, ziet u Hallo [latentie testpagina](http://www.azurespeed.com/Azure/Latency). 

Hallo datacenters met service voor toepassingsproxy Hallo vindt Hello [Connectorhulpprogramma poorten Test](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Feedback over toepassingsproxy data center-locaties 
Mogelijk zijn er Azure-datacenters die toepassingsproxy nog niet zijn maar zou leiden tooa geweldige latentie verbetering voor u. Hallo-datacentrum locatie < aadapfeedback@microsoft.com > zodat we uw feedback tooplan gebruiken kunt als we uitbreiden.

We werken aan enkele aanvullende mogelijkheden Hallo-latentie verbeteren voor tenants die momenteel Zie lang latenties en ervoor tooshare documentatie zodra deze beschikbaar worden.

## <a name="next-steps"></a>Volgende stappen
[Werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md)
