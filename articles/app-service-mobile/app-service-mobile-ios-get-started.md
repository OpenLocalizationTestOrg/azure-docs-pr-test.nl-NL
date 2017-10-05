---
title: Een iOS-app maken in Azure App Service Mobile Apps| Microsoft Docs
description: Volg deze zelfstudie om aan de slag te gaan met back-ends voor mobiele apps van Azure voor iOs-ontwikkeling in Objective-C of Swift.
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 6461a899-9340-42dd-b118-ffc5ba00e846
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 36936ae66c458fcbedeec95cfa2f573a40c8af53
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-ios-app"></a><span data-ttu-id="f7d76-103">Een iOS-app maken</span><span class="sxs-lookup"><span data-stu-id="f7d76-103">Create an iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="f7d76-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f7d76-104">Overview</span></span>
<span data-ttu-id="f7d76-105">Deze zelfstudie laat zien hoe u [Azure Mobile Apps](app-service-mobile-value-prop.md), een back-endservice in de cloud, toevoegt aan een iOs-app.</span><span class="sxs-lookup"><span data-stu-id="f7d76-105">This tutorial shows how to add [Azure Mobile Apps](app-service-mobile-value-prop.md), a cloud backend service, to an iOS app.</span></span> <span data-ttu-id="f7d76-106">Eerst maakt u een nieuwe mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="f7d76-106">We'll first create a new mobile backend.</span></span> <span data-ttu-id="f7d76-107">Vervolgens gebruiken we een eenvoudige iOS-app voor een *takenlijst* voor het opslaan van gegevens in Azure.</span><span class="sxs-lookup"><span data-stu-id="f7d76-107">Then, we'll use a simple *Todo list* iOS app to store data in Azure.</span></span>

<span data-ttu-id="f7d76-108">Voor het uitvoeren van deze zelfstudie hebt u een Mac en [een Azure-account](https://azure.microsoft.com/pricing/free-trial/) nodig</span><span class="sxs-lookup"><span data-stu-id="f7d76-108">To complete this tutorial, you need a Mac and [an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>

## <a name="step-i-create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="f7d76-109">Stap 1: een nieuwe back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="f7d76-109">Step I: Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="step-ii-configure-the-backend-project"></a><span data-ttu-id="f7d76-110">Stap II: het back-endproject configureren</span><span class="sxs-lookup"><span data-stu-id="f7d76-110">Step II: Configure the backend project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="step-iii-download-and-run-the-ios-app"></a><span data-ttu-id="f7d76-111">Stap III: de iOS-app downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f7d76-111">Step III: Download and run the iOS app</span></span>
[!INCLUDE [app-service-mobile-ios-run-app](../../includes/app-service-mobile-ios-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
