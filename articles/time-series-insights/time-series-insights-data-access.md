---
title: aaaData-beleid in Azure Time Series Insights | Microsoft Docs
description: In deze zelfstudie leert u toomanage gegevenstoegangsbeleid in tijd reeks inzichten
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="21920-103">Data access tooa Time Series Insights-omgeving met Azure portal verlenen</span><span class="sxs-lookup"><span data-stu-id="21920-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="21920-104">Time Series Insights-omgevingen hebben twee onafhankelijke typen toegangsbeleid:</span><span class="sxs-lookup"><span data-stu-id="21920-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="21920-105">Beleid voor beheertoegang</span><span class="sxs-lookup"><span data-stu-id="21920-105">Management access policies</span></span>
* <span data-ttu-id="21920-106">Beleid voor gegevenstoegang</span><span class="sxs-lookup"><span data-stu-id="21920-106">Data access policies</span></span>

<span data-ttu-id="21920-107">Beide soorten beleid verlenen Azure Active Directory-principals (gebruikers en apps) verschillende machtigingen voor een specifieke omgeving.</span><span class="sxs-lookup"><span data-stu-id="21920-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="21920-108">Hallo principals (gebruikers en apps) moeten behoren toohello active directory (of 'Azure-tenant') die zijn gekoppeld aan het Hallo-abonnement met Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="21920-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="21920-109">Beheerbeleid toegang verlenen machtigingen gerelateerde toohello configuratie van Hallo-omgeving, zoals</span><span class="sxs-lookup"><span data-stu-id="21920-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="21920-110">Verwijzen naar gegevenssets, maken en verwijderen van Hallo-omgeving, bronnen van gebeurtenissen en</span><span class="sxs-lookup"><span data-stu-id="21920-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="21920-111">Beheer van Hallo gegevenstoegangsbeleid.</span><span class="sxs-lookup"><span data-stu-id="21920-111">Management of hello data access policies.</span></span>

<span data-ttu-id="21920-112">Gegevenstoegangsbeleid machtigingen verlenen gegevensquery's tooissue, referentiegegevens in Hallo omgeving bewerkt en opgeslagen query's en perspectieven die zijn gekoppeld aan de omgeving Hallo delen.</span><span class="sxs-lookup"><span data-stu-id="21920-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="21920-113">Hallo twee soorten beleid toestaan duidelijke scheiding tussen toohello toegangsbeheer van Hallo-omgeving en toegang tot toohello gegevens binnen Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="21920-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="21920-114">Het is bijvoorbeeld mogelijk toosetup een omgeving zodat Hallo eigenaar/maker van Hallo omgeving uit Hallo gegevenstoegang wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="21920-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="21920-115">En de gebruikers en services die zijn toegestaan tooread gegevens van Hallo-omgeving kan worden verleend geen toegang tot toohello configuratie van Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="21920-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="21920-116">Gegevenstoegang verlenen</span><span class="sxs-lookup"><span data-stu-id="21920-116">Grant data access</span></span>
<span data-ttu-id="21920-117">Hallo volgende stappen laten zien hoe toogrant toegang tot de gegevens voor de principal van een gebruiker:</span><span class="sxs-lookup"><span data-stu-id="21920-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="21920-118">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21920-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="21920-119">Klik op 'Alle resources' in hello menu aan de linkerkant Hallo Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="21920-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="21920-120">Selecteer uw Time Series Insights-omgeving.</span><span class="sxs-lookup"><span data-stu-id="21920-120">Select your Time Series Insights environment.</span></span>

  ![Beheren van Hallo Time Series Insights-bron - omgeving](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="21920-122">Selecteer Toegang gegevenslaag en klik op Toevoegen</span><span class="sxs-lookup"><span data-stu-id="21920-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Hallo Time Series Insights bron beheren: toevoegen](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="21920-124">Klik op Gebruiker selecteren.</span><span class="sxs-lookup"><span data-stu-id="21920-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="21920-125">Zoek en selecteer gebruiker via e-mail Hallo.</span><span class="sxs-lookup"><span data-stu-id="21920-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="21920-126">Klik op de blade Gebruiker selecteren op Selecteren.</span><span class="sxs-lookup"><span data-stu-id="21920-126">Click “Select” in “Select User” blade.</span></span>

  ![Hallo Time Series Insights-bron - Selecteer de gebruiker beheren](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="21920-128">Klik op Rol selecteren.</span><span class="sxs-lookup"><span data-stu-id="21920-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="21920-129">Selecteer 'Inzender' als u tooallow gebruiker toochange referentiegegevens wilt en opgeslagen query's en perspectieven met andere gebruikers van Hallo-omgeving delen.</span><span class="sxs-lookup"><span data-stu-id="21920-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="21920-130">Anders 'Lezer' tooallow gebruikersgegevens query selecteren in Hallo-omgeving en persoonlijke (niet-gedeelde) query's opslaan in Hallo-omgeving.</span><span class="sxs-lookup"><span data-stu-id="21920-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="21920-131">Klik op 'Ok' Hallo 'Rol selecteren' blade.</span><span class="sxs-lookup"><span data-stu-id="21920-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Hallo Time Series Insights-bron - Functieservices selecteren beheren](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="21920-133">Klik op 'Ok' Hallo 'Gebruikersrol selecteren' blade.</span><span class="sxs-lookup"><span data-stu-id="21920-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="21920-134">U ziet het volgende:</span><span class="sxs-lookup"><span data-stu-id="21920-134">You should see:</span></span>

  ![Hallo Time Series Insights-bron - resultaten beheren](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="21920-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="21920-136">Next steps</span></span>

* [<span data-ttu-id="21920-137">Een gebeurtenisbron maken</span><span class="sxs-lookup"><span data-stu-id="21920-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="21920-138">[Verzenden van gebeurtenissen](time-series-insights-send-events.md) toohello gebeurtenisbron</span><span class="sxs-lookup"><span data-stu-id="21920-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="21920-139">Uw omgeving bekijken in de [Time Series Insights-portal](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="21920-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
