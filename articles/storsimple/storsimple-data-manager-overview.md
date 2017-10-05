---
title: Overzicht van Microsoft Azure StorSimple Data Manager | Microsoft Docs
description: Biedt een overzicht van de StorSimple Data Manager-service (afgeschermd voorbeeld)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: aedb44610fe57055851538b9dbdb810e66e58d73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="38596-103">Overzicht van StorSimple Data Manager (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="38596-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="38596-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="38596-104">Overview</span></span>

<span data-ttu-id="38596-105">Microsoft Azure StorSimple is een hybride cloud-opslagoplossing die zijn gericht op de complexiteit van niet-gestructureerde gegevens die betrekking hebben op bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="38596-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="38596-106">StorSimple maakt gebruik van cloud-opslag als een uitbreiding van de on-premises oplossing en automatisch lagen gegevens voor de lokale opslag- en cloud-opslag.</span><span class="sxs-lookup"><span data-stu-id="38596-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="38596-107">Gegevensbescherming, geïntegreerd met lokale en cloud worden opgeslagen, hoeft u voor een weids opslaginfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="38596-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="38596-108">Er is ook het archiveren en herstel na noodgevallen naadloze aan de cloud die fungeert als een externe locatie.</span><span class="sxs-lookup"><span data-stu-id="38596-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span></span>

<span data-ttu-id="38596-109">De service voor de transformatie van gegevens die worden geïntroduceerd in dit document, kunt u naadloos toegang krijgen tot de StorSimple-gegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="38596-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span></span> <span data-ttu-id="38596-110">Deze service biedt API's om de gegevens ophalen uit de StorSimple en deze voor andere Azure-services in een indeling die gemakkelijk kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38596-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="38596-111">De indelingen ondersteund in dit voorbeeld zijn Azure-blobs en activa Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="38596-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="38596-112">Deze transformatie kunt u eenvoudig wire-services zoals Azure Media Services, Azure HDInsight Azure Machine Learning en Azure Search gegevens op StorSimple 8000 series on-premises apparaat werken.</span><span class="sxs-lookup"><span data-stu-id="38596-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="38596-113">Een hoog niveau diagram ter illustratie van deze worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="38596-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagram op hoog niveau](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="38596-115">Dit document wordt uitgelegd hoe u zich kunt aanmelden voor een persoonlijke voorbeeld van deze service.</span><span class="sxs-lookup"><span data-stu-id="38596-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="38596-116">Ook wordt uitgelegd hoe u deze service om toepassingen die gebruikmaken van StorSimple-gegevens te schrijven en andere Azure-services kunt gebruiken in de cloud.</span><span class="sxs-lookup"><span data-stu-id="38596-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="38596-117">Aanmelden voor de preview van Data Manager</span><span class="sxs-lookup"><span data-stu-id="38596-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="38596-118">Voordat u zich registreert voor de service Manager gegevens, controleert u de volgende vereisten.</span><span class="sxs-lookup"><span data-stu-id="38596-118">Before you sign up for the Data Manager service, review the following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="38596-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="38596-119">Prerequisites</span></span>

<span data-ttu-id="38596-120">In deze oefening wordt ervan uitgegaan dat u hebt</span><span class="sxs-lookup"><span data-stu-id="38596-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="38596-121">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="38596-121">an active Azure subscription.</span></span>
* <span data-ttu-id="38596-122">toegang tot een geregistreerd StorSimple 8000 series apparaat</span><span class="sxs-lookup"><span data-stu-id="38596-122">access to a registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="38596-123">alle sleutels die zijn gekoppeld aan het apparaat van de serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="38596-123">all the keys associated with the StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="38596-124">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="38596-124">Sign up</span></span>

<span data-ttu-id="38596-125">De StorSimple Data Manager is private preview.</span><span class="sxs-lookup"><span data-stu-id="38596-125">The StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="38596-126">Voer de volgende stappen voor het aanmelden voor een persoonlijke voorbeeld van deze service:</span><span class="sxs-lookup"><span data-stu-id="38596-126">Perform the following steps to sign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="38596-127">Meld u aan bij de Azure-portal met de extensie StorSimple Data Manager op: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="38596-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="38596-128">Uw Azure-referenties gebruiken om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="38596-128">Use your Azure credentials to log in.</span></span>

2.  <span data-ttu-id="38596-129">Klik op de  **+**  pictogram om een service te maken.</span><span class="sxs-lookup"><span data-stu-id="38596-129">Click the **+** icon to create a service.</span></span> <span data-ttu-id="38596-130">Klik op **opslag** en klik vervolgens op **alle Zie** in de blade die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="38596-130">Click **Storage** and then click **See All** in the blade that opens up.</span></span>

    ![Pictogram voor StorSimple Manager gegevens zoeken](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="38596-132">U ziet het pictogram StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="38596-132">You see the StorSimple Data Manager icon.</span></span>

    ![Selecteer de gegevens van de StorSimple Manager-pictogram](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="38596-134">Klik op het pictogram StorSimple Data Manager en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="38596-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="38596-135">Selecteer het abonnement dat u wilt inschakelen voor de private preview en klik vervolgens op **inschrijven!**</span><span class="sxs-lookup"><span data-stu-id="38596-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span></span>

    ![Inschrijven](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="38596-137">Dit wordt een aanvraag verzonden naar vrijgeven u.</span><span class="sxs-lookup"><span data-stu-id="38596-137">This sends a request to onboard you.</span></span> <span data-ttu-id="38596-138">We zullen we u zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="38596-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="38596-139">Nadat uw abonnement is ingeschakeld, kunt u een StorSimple Data Manager-service.</span><span class="sxs-lookup"><span data-stu-id="38596-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="38596-140">Voor eenvoudig toegang tot de StorSimple Data Manager-service, klikt u op het sterpictogram op vastmaken aan uw Favorieten.</span><span class="sxs-lookup"><span data-stu-id="38596-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span></span>

    ![Toegang tot gegevens van de StorSimple Managers](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="38596-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38596-142">Next steps</span></span>

<span data-ttu-id="38596-143">[Gebruik StorSimple Data Manager UI om uw gegevens te transformeren](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="38596-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>