---
title: Extensies app - Azure AD B2C | Microsoft Docs
description: Hallo b2c-uitbreidingen-app herstellen
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a><span data-ttu-id="b7051-103">Azure AD B2C: Extensies app</span><span class="sxs-lookup"><span data-stu-id="b7051-103">Azure AD B2C: Extensions app</span></span>

<span data-ttu-id="b7051-104">Als een Azure AD B2C-directory is gemaakt, wordt aangeroepen door een app `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` automatisch wordt gemaakt in de nieuwe map Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7051-104">When an Azure AD B2C directory is created, an app called `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` is automatically created inside hello new directory.</span></span> <span data-ttu-id="b7051-105">Deze app op, waarnaar wordt verwezen tooas hello **b2c-uitbreidingen-app**, zichtbaar is in *App registraties*.</span><span class="sxs-lookup"><span data-stu-id="b7051-105">This app, referred tooas hello **b2c-extensions-app**, is visible in *App registrations*.</span></span> <span data-ttu-id="b7051-106">Deze wordt gebruikt door hello Azure AD B2C-service toostore informatie over gebruikers en aangepaste kenmerken.</span><span class="sxs-lookup"><span data-stu-id="b7051-106">It is used by hello Azure AD B2C service toostore information about users and custom attributes.</span></span> <span data-ttu-id="b7051-107">Hallo-app wordt verwijderd, Azure AD B2C niet naar behoren als uw productieomgeving worden beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="b7051-107">If hello app is deleted, Azure AD B2C will not function correctly and your production environment will be affected.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7051-108">Verwijder Hallo b2c-uitbreidingen-app niet tenzij u van plan bent tooimmediately verwijderen uw tenant.</span><span class="sxs-lookup"><span data-stu-id="b7051-108">Do not delete hello b2c-extensions-app unless you are planning tooimmediately delete your tenant.</span></span> <span data-ttu-id="b7051-109">Als het Hallo-app blijft gedurende meer dan 30 dagen verwijderd, worden gebruikersgegevens permanent verloren.</span><span class="sxs-lookup"><span data-stu-id="b7051-109">If hello app remains deleted for more than 30 days, user information will be permanently lost.</span></span>

## <a name="verifying-that-hello-extensions-app-is-present"></a><span data-ttu-id="b7051-110">Controleren die Hallo extensies app aanwezig is</span><span class="sxs-lookup"><span data-stu-id="b7051-110">Verifying that hello extensions app is present</span></span>

<span data-ttu-id="b7051-111">tooverify die Hallo b2c-uitbreidingen-app is aanwezig:</span><span class="sxs-lookup"><span data-stu-id="b7051-111">tooverify that hello b2c-extensions-app is present:</span></span>

1. <span data-ttu-id="b7051-112">Binnen uw Azure AD B2C-tenant, klikt u op **meer services** in Hallo links navigatiemenu.</span><span class="sxs-lookup"><span data-stu-id="b7051-112">Inside your Azure AD B2C tenant, click on **More services** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="b7051-113">Zoeken en openen **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="b7051-113">Search for and open **App registrations**.</span></span>
1. <span data-ttu-id="b7051-114">Een app die met begint zoeken **b2c-uitbreidingen-app**</span><span class="sxs-lookup"><span data-stu-id="b7051-114">Look for an app that begins with **b2c-extensions-app**</span></span>

## <a name="recover-hello-extensions-app"></a><span data-ttu-id="b7051-115">Hallo-extensies app herstellen</span><span class="sxs-lookup"><span data-stu-id="b7051-115">Recover hello extensions app</span></span>

<span data-ttu-id="b7051-116">Als u per ongeluk Hallo b2c-uitbreidingen-app hebt verwijderd, hebt u 30 dagen toorecover deze.</span><span class="sxs-lookup"><span data-stu-id="b7051-116">If you accidentally deleted hello b2c-extensions-app, you have 30 days toorecover it.</span></span> <span data-ttu-id="b7051-117">Hallo-app met behulp van Hallo Graph API kunt u herstellen:</span><span class="sxs-lookup"><span data-stu-id="b7051-117">You can restore hello app using hello Graph API:</span></span>

1. <span data-ttu-id="b7051-118">Te bladeren[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span><span class="sxs-lookup"><span data-stu-id="b7051-118">Browse too[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).</span></span>
1. <span data-ttu-id="b7051-119">Toohello site aanmelden als globale beheerder voor hello Azure AD B2C-directory die u wilt dat toorestore Hallo verwijderd-app voor.</span><span class="sxs-lookup"><span data-stu-id="b7051-119">Log in toohello site as a global administrator for hello Azure AD B2C directory that you want toorestore hello deleted app for.</span></span>
1. <span data-ttu-id="b7051-120">Uitgeven van een HTTP GET tegen Hallo URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` = met api-versie 1.6.</span><span class="sxs-lookup"><span data-stu-id="b7051-120">Issue an HTTP GET against hello URL `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` with api-version=1.6.</span></span> <span data-ttu-id="b7051-121">Zorg ervoor dat tooreplace `{tenantName}` met de tenantnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="b7051-121">Make sure tooreplace `{tenantName}` with your tenant name.</span></span> <span data-ttu-id="b7051-122">Deze bewerking wordt een lijst alle Hallo-toepassingen die zijn verwijderd binnen Hallo afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="b7051-122">This operation will list all of hello applications that have been deleted within hello past 30 days.</span></span>
1. <span data-ttu-id="b7051-123">Hallo toepassing zoeken in Hallo lijst waarbij Hallo naam met 'b2c-extensie-app' en kopieer begint de `objectid` eigenschapswaarde.</span><span class="sxs-lookup"><span data-stu-id="b7051-123">Find hello application in hello list where hello name begins with 'b2c-extension-app’ and copy its `objectid` property value.</span></span>
1. <span data-ttu-id="b7051-124">Uitgeven van een HTTP POST tegen Hallo URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span><span class="sxs-lookup"><span data-stu-id="b7051-124">Issue an HTTP POST against hello URL `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`.</span></span> <span data-ttu-id="b7051-125">Vervang Hallo `{OBJECTID}` deel van de URL Hallo Hello `objectid` uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7051-125">Replace hello `{OBJECTID}` portion of hello URL with hello `objectid` from hello previous step.</span></span> 

<span data-ttu-id="b7051-126">U moet nu mogelijk te[Zie Hallo hersteld app](#verifying-that-the-extensions-app-is-present) in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b7051-126">You should now be able too[see hello restored app](#verifying-that-the-extensions-app-is-present) in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b7051-127">Een toepassing kan alleen worden hersteld als deze is verwijderd binnen Hallo afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="b7051-127">An application can only be restored if it has been deleted within hello last 30 days.</span></span> <span data-ttu-id="b7051-128">Als het meer dan 30 dagen is, worden gegevens permanent verloren.</span><span class="sxs-lookup"><span data-stu-id="b7051-128">If it has been more than 30 days, data will be permanently lost.</span></span> <span data-ttu-id="b7051-129">Het bestand een ondersteuningsticket voor verdere ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="b7051-129">For more assistance, file a support ticket.</span></span>
