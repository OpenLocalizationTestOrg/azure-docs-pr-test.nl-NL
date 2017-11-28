---
title: aaaCreate een Android-app in Azure App Service Mobile Apps | Microsoft Docs
description: Volg deze zelfstudie tooget gestart met behulp van back-ends voor mobiele Apps van Azure voor Android-ontwikkeling
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 355f0959-aa7f-472c-a6c7-9eecea3a34a9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 0af85a3a4de9fc265976bbe3f34d73effc3807df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-android-app"></a><span data-ttu-id="fddad-103">Een Android-app maken</span><span class="sxs-lookup"><span data-stu-id="fddad-103">Create an Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="fddad-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fddad-104">Overview</span></span>
<span data-ttu-id="fddad-105">Deze zelfstudie laat zien hoe een cloud-gebaseerde back-end tooadd tooan mobiele Android-app service met behulp van een back-end voor mobiele Apps van Azure.</span><span class="sxs-lookup"><span data-stu-id="fddad-105">This tutorial shows you how tooadd a cloud-based backend service tooan Android mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="fddad-106">U maakt zowel een nieuwe back-end voor een mobiele app als een eenvoudige Android-app voor *takenlijsten* die app-gegevens opslaat in Azure.</span><span class="sxs-lookup"><span data-stu-id="fddad-106">You will create both a new mobile app backend and a simple *Todo list* Android app that stores app data in Azure.</span></span>

<span data-ttu-id="fddad-107">Voltooien van deze zelfstudie is een vereiste voor alle andere Android-zelfstudies over het gebruik van de functie Mobile Apps Hallo in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="fddad-107">Completing this tutorial is a prerequisite for all other Android tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fddad-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fddad-108">Prerequisites</span></span>
<span data-ttu-id="fddad-109">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="fddad-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="fddad-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), waaronder Hallo Android Studio geïntegreerde ontwikkelomgeving en Hallo meest recente Android-platform.</span><span class="sxs-lookup"><span data-stu-id="fddad-110">[Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>
* <span data-ttu-id="fddad-111">Azure Mobile Android SDK, die automatisch wordt verwezen als onderdeel van Hallo Quick Start-project downloaden.</span><span class="sxs-lookup"><span data-stu-id="fddad-111">Azure Mobile Android SDK, which is automatically referenced as part of hello quickstart project you download.</span></span>
* <span data-ttu-id="fddad-112">Een [actief Azure-account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fddad-112">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="fddad-113">Een nieuwe back-end voor mobiele apps van Azure maken</span><span class="sxs-lookup"><span data-stu-id="fddad-113">Create a new Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="fddad-114">Hallo serverproject configureren</span><span class="sxs-lookup"><span data-stu-id="fddad-114">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-android-app"></a><span data-ttu-id="fddad-115">Hallo Android-app downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="fddad-115">Download and run hello Android app</span></span>
[!INCLUDE [app-service-mobile-android-run-app](../../includes/app-service-mobile-android-run-app.md)]

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2013]: https://go.microsoft.com/fwLink/p/?LinkID=534203
