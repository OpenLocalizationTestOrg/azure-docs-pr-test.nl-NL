---
title: aaaOptions voor het opsporen van Azure-cloudservices | Microsoft Docs
description: Foutopsporing van Azure-cloudservices
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Meer informatie over verschillende manieren Hallo toodebug een Azure cloudservice
Dit artikel vindt u koppelingen toohello verschillende manieren toodebug een Azure-cloudservice. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Foutopsporing van een Azure-cloud-service in Visual Studio
U kunt opslaan tijd en geld met behulp van hello Azure compute-emulator toodebug uw cloudservice op een lokale computer. U kunt door foutopsporing lokaal een service in voordat u deze implementeert, betrouwbaarheid en prestaties verbeteren zonder te betalen voor compute-tijd. Echter een aantal fouten optreden alleen wanneer u een cloudservice in Azure uitvoert. Fouten die optreden alleen wanneer u een cloudservice in Azure uitvoeren kunnen fouten worden opgespoord door in te schakelen foutopsporing op afstand wanneer u uw service publiceert en vervolgens Hallo foutopsporingsprogramma tooa rolinstantie koppelen. Zie voor meer informatie [fouten opsporen in uw cloudservice op de lokale computer](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Met behulp van Azure Diagnostics 
U kunt Azure Diagnostics toolog gedetailleerde informatie in rollen, code wordt uitgevoerd of Hallo functies worden uitgevoerd in de ontwikkelomgeving Hallo of in Azure. Zie voor meer informatie [Azure Diagnostics inschakelen in Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Met behulp van IntelliTrace 
Als u Visual Studio Enterprise toowrite rollen gericht .NET Framework 4.5, kunt u IntelliTrace inschakelen op Hallo tijdstip dat u een Azure-cloudservice implementeren vanuit Visual Studio. IntelliTrace voorziet in een logboek die u met Visual Studio toodebug uw toepassing gebruiken kunt als in Azure werd uitgevoerd. Zie voor meer informatie [foutopsporing van een gepubliceerde cloudservice met IntelliTrace en Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Foutopsporing op afstand 
Foutopsporing op afstand op uw cloudservices op Hallo tijdstip wanneer u de cloudservice Hallo vanuit Visual Studio implementeert, kunt u inschakelen. Als u foutopsporing op afstand voor een implementatie tooenable kiest, is externe foutopsporing services zijn geïnstalleerd op Hallo virtuele machines met elk rolexemplaar. Deze services - zoals `msvsmon.exe` - geen invloed hebben op prestaties of leiden tot extra kosten. Zie voor meer informatie [fouten opsporen in een cloudservice in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Volgende stappen
- [Een Azure-cloudservice of virtuele machine in Visual Studio-foutopsporing](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -informatie Hallo hoe toodebug Azure-cloudservices.
