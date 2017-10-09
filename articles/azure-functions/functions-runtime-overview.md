---
title: Overzicht van de Runtime Functions aaaAzure | Microsoft Docs
description: Overzicht van hello Azure Functions-Runtime-Preview
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Overzicht van Azure Functions-Runtime

Hello Azure Functions-Runtime biedt een nieuwe manier voor u tootake profiteren van Hallo eenvoud en flexibiliteit van hello Azure Functions programming model lokale. Gebouwd op Hallo dezelfde bron hoofdmappen zoals Azure Functions, Azure Functions-Runtime geïmplementeerde lokale tooprovide een bijna identiek ontwikkeling optreden als Hallo-cloudservice is geopend.

![Preview-Portal voor Azure Functions-Runtime][1]

Hello Azure Functions-Runtime biedt een manier voor u tooexperience Azure Functions alvorens toohello cloud toe te wijzen. Op deze manier kunnen Hallo code activa die u bouwt vervolgens worden uitgevoerd met u toohello cloud wanneer u migreert.  Hallo runtime worden ook nieuwe opties voor u, zoals het gebruik van Hallo spare rekencapaciteit van uw lokale computers toorun batchprocessen nacht geopend. U kunt apparaten binnen uw organisatie tooconditionally verzenden tooother gegevenssystemen, zowel on-premises en in Hallo cloud.

Hello Azure Functions-Runtime bestaat uit twee onderdelen:
* Beheer van Azure Functions-Runtimerol
* Azure Functions-Runtime-Werkrol

## <a name="azure-functions-management-role"></a>Azure Functions Beheerrol

Hallo Beheerrol van Azure Functions biedt een host voor het Hallo-beheer van uw functies on-premises. Deze rol voert Hallo taken te volgen:

* Hosting van Azure Functions-beheerportal, Hallo HALLO hallo dezelfde is als die u in Hallo ziet [Azure-portal](https://portal.azure.com). Deze kunt ontwikkelen van uw functies in Hallo dezelfde manier als in hello Azure-portal.
* Functies over meerdere functies werknemers verdeeld.
* Levert een publishing eindpunt zodat u uw functies direct vanuit Microsoft Visual Studio kunt publiceren.

## <a name="azure-functions-worker-role"></a>Azure Functions-Werkrol

Hello Azure Functions-werkrollen zijn geïmplementeerd in Windows-Containers en dit is waar uw functiecode wordt uitgevoerd.  U kunt meerdere werkrollen implementeren binnen uw organisatie en is een belangrijke manier waarin klanten kunnen maken gebruik van ongebruikte rekenkracht.

## <a name="minimum-requirements"></a>Minimale vereisten

tooget Hello Azure Functions-Runtime moet u een machine met hebben gestart **Windows Server 2016 of Windows 10 auteurs Update** met toegang tooa **SQL Server** exemplaar.

## <a name="next-steps"></a>Volgende stappen

Hallo installeren [Azure Functions-Runtime-preview](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
