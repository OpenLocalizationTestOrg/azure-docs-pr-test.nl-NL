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
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="360ba-104">Een Apache Cordova-app maken</span><span class="sxs-lookup"><span data-stu-id="360ba-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="360ba-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="360ba-105">Overview</span></span>
<span data-ttu-id="360ba-106">Deze zelfstudie leert u hoe tooadd back-end van een cloud-gebaseerde mobiele tooan Apache Cordova-app service met behulp van een back-end voor mobiele Apps van Azure.</span><span class="sxs-lookup"><span data-stu-id="360ba-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="360ba-107">U maakt zowel een nieuwe back-end voor een mobiele app als een eenvoudige Apache Cordova-app voor *takenlijsten* die app-gegevens opslaat in Azure.</span><span class="sxs-lookup"><span data-stu-id="360ba-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="360ba-108">Voltooien van deze zelfstudie is een vereiste voor alle andere Apache Cordova-zelfstudies over het gebruik van de functie Mobile Apps Hallo in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="360ba-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="360ba-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="360ba-109">Prerequisites</span></span>
<span data-ttu-id="360ba-110">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="360ba-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="360ba-111">Een pc met [Visual Studio Community 2017] of hoger.</span><span class="sxs-lookup"><span data-stu-id="360ba-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="360ba-112">[Visual Studio Tools for Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="360ba-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="360ba-113">Een [actief Azure-account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="360ba-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="360ba-114">U kunt ook Visual Studio overslaan en Hallo Apache Cordova-opdrachtregel rechtstreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="360ba-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="360ba-115">Via de opdrachtregel Hallo is handig bij het voltooien van de zelfstudie Hallo op een Mac-computer.</span><span class="sxs-lookup"><span data-stu-id="360ba-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="360ba-116">Compileren van Apache Cordova-clienttoepassingen via de opdrachtregel Hallo niet wordt gedekt door deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="360ba-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="360ba-117">Een back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="360ba-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="360ba-118">Bekijk een video van vergelijkbare stappen</span><span class="sxs-lookup"><span data-stu-id="360ba-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="360ba-119">Hallo serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="360ba-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="360ba-120">Hallo Apache Cordova-app downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="360ba-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="360ba-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="360ba-121">Next Steps</span></span>
<span data-ttu-id="360ba-122">Nu dat u deze zelfstudie hebt voltooid, verplaatst u op tooone Hallo volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="360ba-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="360ba-123">[Offline gegevens toe te voegen](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="360ba-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="360ba-124">[Verificatie toevoegen](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="360ba-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="360ba-125">[Pushmeldingen toevoegen](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova-app.</span><span class="sxs-lookup"><span data-stu-id="360ba-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="360ba-126">Meer informatie over belangrijke concepten met Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="360ba-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="360ba-127">[Offlinegegevens]</span><span class="sxs-lookup"><span data-stu-id="360ba-127">[Offline Data]</span></span>
* <span data-ttu-id="360ba-128">[Verificatie]</span><span class="sxs-lookup"><span data-stu-id="360ba-128">[Authentication]</span></span>
* <span data-ttu-id="360ba-129">[Pushmeldingen]</span><span class="sxs-lookup"><span data-stu-id="360ba-129">[Push Notifications]</span></span>

<span data-ttu-id="360ba-130">Meer informatie over hoe toouse Hallo SDK's.</span><span class="sxs-lookup"><span data-stu-id="360ba-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="360ba-131">[Apache Cordova SDK]</span><span class="sxs-lookup"><span data-stu-id="360ba-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="360ba-132">[ASP.NET Server SDK]</span><span class="sxs-lookup"><span data-stu-id="360ba-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="360ba-133">[Node.js Server SDK]</span><span class="sxs-lookup"><span data-stu-id="360ba-133">[Node.js Server SDK]</span></span>

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
