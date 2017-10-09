---
title: aaaCreate een Cordova-app in Azure App Service Mobile Apps | Microsoft Docs
description: Volg deze zelfstudie tooget gestart met behulp van back-ends voor mobiele Apps van Azure voor Apache Cordova-ontwikkeling
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova,javascript,mobiel,client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Een Apache Cordova-app maken
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe tooadd back-end van een cloud-gebaseerde mobiele tooan Apache Cordova-app service met behulp van een back-end voor mobiele Apps van Azure.  U maakt zowel een nieuwe back-end voor een mobiele app als een eenvoudige Apache Cordova-app voor *takenlijsten* die app-gegevens opslaat in Azure.

Voltooien van deze zelfstudie is een vereiste voor alle andere Apache Cordova-zelfstudies over het gebruik van de functie Mobile Apps Hallo in Azure App Service.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

* Een pc met [Visual Studio Community 2017] of hoger.
* [Visual Studio Tools for Apache Cordova].
* Een [actief Azure-account](https://azure.microsoft.com/pricing/free-trial/).

U kunt ook Visual Studio overslaan en Hallo Apache Cordova-opdrachtregel rechtstreeks gebruiken.  Via de opdrachtregel Hallo is handig bij het voltooien van de zelfstudie Hallo op een Mac-computer.  Compileren van Apache Cordova-clienttoepassingen via de opdrachtregel Hallo niet wordt gedekt door deze zelfstudie.

## <a name="create-an-azure-mobile-app-backend"></a>Een back-end voor mobiele apps van Azure maken
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Bekijk een video van vergelijkbare stappen](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Hallo serverproject configureren
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Hallo Apache Cordova-app downloaden en uitvoeren
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Volgende stappen
Nu dat u deze zelfstudie hebt voltooid, verplaatst u op tooone Hallo volgende zelfstudies:

* [Offline gegevens toe te voegen](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova-app.
* [Verificatie toevoegen](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova-app.
* [Pushmeldingen toevoegen](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova-app.

Meer informatie over belangrijke concepten met Azure App Service.

* [Offlinegegevens]
* [Verificatie]
* [Pushmeldingen]

Meer informatie over hoe toouse Hallo SDK's.

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Offlinegegevens]: app-service-mobile-offline-data-sync.md
[Verificatie]: app-service-mobile-auth.md
[Pushmeldingen]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
