---
title: WebJobs in Azure App Service
description: Informatie over het bouwen van WebJobs achtergrond tests uitvoeren, communiceren met services zoals opslag en Service Bus en geplande taken maken.
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a>WebJobs in Azure App Service gebruiken
Dit artikel bevat koppelingen naar documentatie over het gebruik van Azure WebJobs en de Azure WebJobs SDK. Azure WebJobs bieden een eenvoudige manier om het uitvoeren van scripts of programma's als achtergrondprocessen op [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). U kunt uploaden en uitvoeren van een uitvoerbaar bestand zoals als cmd bat, exe (.NET) ps1, servicel, php, py, js en jar. Deze programma's uitvoeren als WebJobs volgens een schema (cron) of continu.

De WebJobs SDK kunt gemakkelijker Azure Storage gebruiken. De WebJobs SDK is een binding en de trigger-systeem dat met Microsoft Azure Storage-Blobs, wachtrijen en tabellen, evenals Service Bus-wachtrijen werkt.

Maken, implementeren en beheren van WebJobs is naadloos met geïntegreerde tooling in Visual Studio. WebJobs van sjablonen maken, publiceren en beheren (uitvoeren/stop/monitor/debug) ze.

Het WebJobs-dashboard in de Azure portal biedt krachtige beheermogelijkheden die u volledige controle over de uitvoering van WebJobs zodat, inclusief de mogelijkheid om aan te roepen afzonderlijke functies binnen WebJobs. Het dashboard worden bovendien de functie runtimes en logboekregistratie uitvoer weergegeven.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

