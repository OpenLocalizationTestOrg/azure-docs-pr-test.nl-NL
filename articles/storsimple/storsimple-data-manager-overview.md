---
title: overzicht van de Azure StorSimple Data Manager aaaMicrosoft | Microsoft Docs
description: Biedt een overzicht van Hallo StorSimple Data Manager-service (afgeschermd voorbeeld)
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
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="e2b9f-103">Overzicht van StorSimple Data Manager (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="e2b9f-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="e2b9f-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e2b9f-104">Overview</span></span>

<span data-ttu-id="e2b9f-105">Microsoft Azure StorSimple is een hybride cloud-opslagoplossing die adressen Hallo complexiteit van niet-gestructureerde gegevens die betrekking hebben op bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="e2b9f-106">StorSimple maakt gebruik van cloud-opslag als een uitbreiding van Hallo on-premises-oplossing en automatisch gegevens over Hallo lokale opslag en cloud-opslag lagen.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="e2b9f-107">Gegevensbescherming, geïntegreerd met lokale en cloud worden opgeslagen, niet meer nodig voor een weids opslaginfrastructuur Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="e2b9f-108">Het archiveren en herstel na noodgevallen is ook naadloos met Hallo cloud fungeert als een externe locatie.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="e2b9f-109">Hallo transformatie gegevensservice die worden geïntroduceerd in dit document, kunt u tooseamlessly toegang Hallo StorSimple-gegevens in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="e2b9f-110">Deze service biedt API's tooextract gegevens van StorSimple, en het tooother Azure-services in de indelingen die gemakkelijk kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="e2b9f-111">Hallo-indelingen ondersteund in dit voorbeeld zijn Azure blobs en activa Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="e2b9f-112">Deze transformatie kunt u tooeasily kabel van services zoals Azure Media Services, Azure HDInsight Azure Machine Learning en Azure Search toooperate gegevens op StorSimple 8000 series on-premises-apparaat.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="e2b9f-113">Een hoog niveau diagram ter illustratie van deze worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-113">A high-level block diagram illustrating this is shown below.</span></span>

![Diagram op hoog niveau](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="e2b9f-115">Dit document wordt uitgelegd hoe u zich kunt aanmelden voor een persoonlijke voorbeeld van deze service.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="e2b9f-116">Ook wordt uitgelegd hoe u deze service toowrite toepassingen die gebruikmaken van StorSimple-gegevens en andere Azure-services in de cloud Hallo kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="e2b9f-117">Aanmelden voor de preview van Data Manager</span><span class="sxs-lookup"><span data-stu-id="e2b9f-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="e2b9f-118">Voordat u zich aanmeldt voor Data Manager-service Hallo, bekijk Hallo vereisten te volgen.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e2b9f-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2b9f-119">Prerequisites</span></span>

<span data-ttu-id="e2b9f-120">In deze oefening wordt ervan uitgegaan dat u hebt</span><span class="sxs-lookup"><span data-stu-id="e2b9f-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="e2b9f-121">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-121">an active Azure subscription.</span></span>
* <span data-ttu-id="e2b9f-122">toegang tooa geregistreerd StorSimple 8000 serie-apparaat</span><span class="sxs-lookup"><span data-stu-id="e2b9f-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="e2b9f-123">alle Hallo sleutels die zijn gekoppeld aan Hallo StorSimple 8000 series apparaat.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="e2b9f-124">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="e2b9f-124">Sign up</span></span>

<span data-ttu-id="e2b9f-125">Hallo StorSimple Data Manager is private preview.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="e2b9f-126">Voer Hallo toosign voor een persoonlijke evaluatieversie van deze service stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e2b9f-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="e2b9f-127">Meld u aan bij hello Azure-portal met de extensie van de Hallo StorSimple Data Manager op: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="e2b9f-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="e2b9f-128">Gebruik de toolog van uw Azure-referenties in.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="e2b9f-129">Klik op Hallo  **+**  pictogram toocreate een service.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="e2b9f-130">Klik op **opslag** en klik vervolgens op **alle Zie** Hallo-blade die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Pictogram voor StorSimple Manager gegevens zoeken](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="e2b9f-132">U ziet Hallo StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-132">You see hello StorSimple Data Manager icon.</span></span>

    ![Selecteer de gegevens van de StorSimple Manager-pictogram](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="e2b9f-134">Klik op het pictogram StorSimple Data Manager en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="e2b9f-135">Kies Hallo-abonnement dat u tooenable voor private preview Hallo wilt en klik vervolgens op **inschrijven!**</span><span class="sxs-lookup"><span data-stu-id="e2b9f-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Inschrijven](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="e2b9f-137">Hiermee verzendt u een aanvraag tooonboard u.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="e2b9f-138">We zullen we u zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="e2b9f-139">Nadat uw abonnement is ingeschakeld, kunt u een StorSimple Data Manager-service.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="e2b9f-140">tooeasily hello StorSimple Data Manager-service te openen, klikt u op Hallo sterpictogram toopin het tooyour Favorieten.</span><span class="sxs-lookup"><span data-stu-id="e2b9f-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Toegang tot gegevens van de StorSimple Managers](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="e2b9f-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2b9f-142">Next steps</span></span>

<span data-ttu-id="e2b9f-143">[Uw gegevens StorSimple Data Manager UI tootransform gebruiken](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="e2b9f-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
