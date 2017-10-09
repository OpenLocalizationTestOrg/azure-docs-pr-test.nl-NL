---
title: aaaAzure RemoteApp netwerkbandbreedte - algemene richtlijnen | Microsoft Docs
description: Sommige Basisnetwerk bandbreedte richtlijnen voor uw Azure RemoteApp-collecties en apps te begrijpen.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Azure RemoteApp netwerkbandbreedte - algemene richtlijnen (als u niet kunt uw eigen testen)
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Als u nog geen Hallo tijd of mogelijkheid toorun hello [netwerk bandbreedte tests](remoteapp-bandwidthtests.md) voor Azure RemoteApp Hier volgen enkele tamelijk algemene richtlijnen kunt u schatten netwerkbandbreedte per gebruiker.

Als u een combinatie van deze scenario's hebt, wordt niet aanbevolen iets kleiner zijn dan (of gelijk zijn aan) 10 MB/s zoals Hallo minimale netwerkbandbreedte voor moderne apps met Internet verbonden in een externe omgeving. (Hoewel zoals besproken, dit wordt niet gegarandeerd dat een beter dan gemiddelde gebruikerservaring.)

## <a name="complex-powerpoint-simple-powerpoint"></a>Complexe PowerPoint, eenvoudige PowerPoint
Azure RemoteApp komt het beste op 100 MB LAN. Hallo op 10 MB/s-netwerkprofiel wanneer jitter hoger dan 120 ms meer dan 5% Hallo gebruiker is ziet een gemiddelde ervaring. 1 MB/s Hallo verschillende is ongeautomatiseerde verwerking - bijvoorbeeld in een diavoorstelling, Hallo gebruiker ziet mogelijk ook geen bewegende overgangen helemaal omdat frames worden overgeslagen.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, gemengde PDF-, PDF, tekst
10 MB/s-netwerkprofiel is sluiten tooLAN in de meeste aspecten. 1 MB/s biedt een OK-ervaring, hoewel er mogelijk nog enkele jitter wanneer een gebruiker terwijl er installatiekopieën op het welkomstscherm zijn.

## <a name="flash-video-youtube"></a>Flash-video (YouTube)
100 MB/s LAN biedt de beste ervaring Hallo terwijl 10 MB/s acceptabel (dat wil zeggen we blijven is van het Hallo-framesnelheid maar jitter toeneemt). Jitter is 1 MB/s, zeer hoge en merkbare.

## <a name="word-typing-word-remote-input"></a>Word-typen (Word externe invoer)
Dit is een lage bandbreedte gebruiksscenario. Om 256 KB/s bieden we een ervaring als LAN goed.

## <a name="learn-more"></a>Meer informatie
* [Gebruik van netwerkbandbreedte Azure RemoteApp schatten](remoteapp-bandwidth.md)
* [Azure RemoteApp - hoe doet netwerkbandbreedte en de kwaliteit van zich werk samen?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp - tseting uw gebruik van netwerkbandbreedte met enkele algemene scenario's](remoteapp-bandwidthtests.md)

