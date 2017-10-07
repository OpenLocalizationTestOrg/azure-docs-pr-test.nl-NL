---
title: aaaMicrosoft Azure StorSimple Data Manager UI | Microsoft Docs
description: Hierin wordt beschreven hoe toouse StorSimple Data Manager service UI (afgeschermd voorbeeld)
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
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="6b39e-103">Beheren met behulp van Hallo StorSimple Data Manager service UI (afgeschermd voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="6b39e-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="6b39e-104">Dit artikel wordt uitgelegd hoe u Hallo StorSimple Data Manager UI tooperform gegevenstransformatie kunt gebruiken voor gegevens die zich op apparaten Hallo StorSimple 8000-serie.</span><span class="sxs-lookup"><span data-stu-id="6b39e-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="6b39e-105">Hallo kunnen getransformeerde gegevens vervolgens worden gebruikt door andere Azure-services zoals Azure Media Services, Azure HDInsight Azure Machine Learning en Azure Search.</span><span class="sxs-lookup"><span data-stu-id="6b39e-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="6b39e-106">StorSimple gegevenstransformatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="6b39e-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="6b39e-107">Hallo StorSimple Data Manager is Hallo resource waarbinnen gegevenstransformatie kan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6b39e-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="6b39e-108">Hallo Data Transformation service kunt u gegevens van uw StorSimple lokale apparaat tooblobs in Azure-opslag verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="6b39e-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="6b39e-109">Daarom in de werkstroom moet u toospecify Hallo details over uw StorSimple-apparaat en Hallo gegevens van belang dat u wilt dat toomove toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="6b39e-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="6b39e-110">Een StorSimple Data Manager-service maken</span><span class="sxs-lookup"><span data-stu-id="6b39e-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="6b39e-111">Hallo te volgen stappen toocreate een StorSimple Data Manager-service uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6b39e-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="6b39e-112">toocreate StorSimple Data Manager-service te gaan[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="6b39e-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="6b39e-113">Klik op Hallo  **+**  pictogram en de zoekcriteria voor StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="6b39e-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="6b39e-114">Klik op uw StorSimple Data Manager-service en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="6b39e-115">Als uw abonnement voor het maken van deze service is ingeschakeld, ziet u Hallo blade te volgen.</span><span class="sxs-lookup"><span data-stu-id="6b39e-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![Maak een resource StorSimple gegevens Managers](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="6b39e-117">Voer Hallo invoer en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="6b39e-118">Hallo opgegeven locatie moet Hallo een met uw storage-accounts en uw StorSimple Manager-service.</span><span class="sxs-lookup"><span data-stu-id="6b39e-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="6b39e-119">Op dit moment worden alleen VS-West en West-Europa regio's ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6b39e-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="6b39e-120">Daarom gekoppelde uw StorSimple Manager-service, Data Manager-service en Hallo storage-account moet worden in Hallo voorgaande ondersteunde regio's.</span><span class="sxs-lookup"><span data-stu-id="6b39e-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="6b39e-121">Het duurt een minuut toocreate Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="6b39e-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="6b39e-122">Een definitie van de transformatie-taak maken</span><span class="sxs-lookup"><span data-stu-id="6b39e-122">Create a data transformation job definition</span></span>

<span data-ttu-id="6b39e-123">Binnen een StorSimple Data Manager-service moet u toocreate een taakdefinitie voor transformatie van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6b39e-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="6b39e-124">De taakdefinitie van een geeft details over Hallo gegevens dat u geïnteresseerd bent in het verplaatsen naar een opslagaccount in systeemeigen Hallo-indeling.</span><span class="sxs-lookup"><span data-stu-id="6b39e-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="6b39e-125">Hallo na toocreate stappen een nieuwe data transformation taakdefinitie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6b39e-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="6b39e-126">Navigeer toohello-service die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6b39e-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="6b39e-127">Klik op **+ taak definitie**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-127">Click **+ Job Definition**.</span></span>

    ![Klik op + taakdefinitie](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="6b39e-129">Hallo nieuwe definitie taakblade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="6b39e-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="6b39e-130">Geef een naam op voor de taakdefinitie van de en klik op **bron**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="6b39e-131">In Hallo **gegevensbron configureren** blade Geef details op Hallo van uw StorSimple-apparaat en Hallo van gegevens van belang.</span><span class="sxs-lookup"><span data-stu-id="6b39e-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![Taakdefinitie maken](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="6b39e-133">Aangezien dit een nieuwe Data Manager-service, worden geen gegevens opslagplaatsen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6b39e-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="6b39e-134">Klik op tooadd uw StorSimple Manager als een gegevensopslagplaats **nieuwe toevoegen** in Hallo gegevens opslagplaats vervolgkeuzelijst en klik vervolgens op **gegevensopslagplaats toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="6b39e-135">Kies **StorSimple 8000-serie Manager** als Hallo-opslagplaats te typen eigenschappen van Hallo en uw **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="6b39e-136">Voor Hallo **Resource-Id** veld, moet u tooenter Hallo nummer voordat Hallo **:** in de registratiesleutel Hallo van uw StorSimple manager.</span><span class="sxs-lookup"><span data-stu-id="6b39e-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![Gegevensbron maken](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="6b39e-138">Klik op **OK** wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="6b39e-138">Click **OK** when done.</span></span> <span data-ttu-id="6b39e-139">Hiermee slaat u de gegevensopslagplaats van uw en deze StorSimple Manager in andere taakdefinities zonder opnieuw invoeren van deze parameters kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6b39e-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="6b39e-140">Het duurt enkele seconden nadat u op **OK** voor Hallo StorSimple Manager tooshow up Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="6b39e-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="6b39e-141">In Hallo **gegevensbron configureren** blade Voer Hallo apparaatnaam en Hallo volumenaam met uw gegevens van belang.</span><span class="sxs-lookup"><span data-stu-id="6b39e-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="6b39e-142">In Hallo **Filter** subsectie, voert u Hallo-hoofdmap waarin de gegevens van belang (dit veld moet beginnen met een `\`).</span><span class="sxs-lookup"><span data-stu-id="6b39e-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="6b39e-143">U kunt ook een bestandsfilters hier toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6b39e-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="6b39e-144">Hallo data transformation-service werkt op Hallo-gegevens die wordt doorgeschoven up toohello Azure via momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="6b39e-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="6b39e-145">Wanneer deze taak wordt uitgevoerd, kunt u tootake een back-up elke keer dat deze taak wordt uitgevoerd (toowork op de meest recente gegevens) of toouse laatste bestaande back-up in de cloud Hallo Hallo (als u werkt op sommige gearchiveerde gegevens).</span><span class="sxs-lookup"><span data-stu-id="6b39e-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![Nieuwe details van gegevensbron](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="6b39e-147">Vervolgens moeten Hallo-doelinstellingen toobe geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="6b39e-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="6b39e-148">Er zijn 2 soorten ondersteunde doelen – Azure Storage-accounts en Azure Media Services-accounts.</span><span class="sxs-lookup"><span data-stu-id="6b39e-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="6b39e-149">Storage-accounts tooput-bestanden in BLOB's in het account kiezen.</span><span class="sxs-lookup"><span data-stu-id="6b39e-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="6b39e-150">Media services-account tooput-bestanden in de activa in het account kiezen.</span><span class="sxs-lookup"><span data-stu-id="6b39e-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="6b39e-151">Opnieuw, moeten we tooadd een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6b39e-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="6b39e-152">Selecteer in de vervolgkeuzelijst Hallo **nieuwe toevoegen** en vervolgens **configureren**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Gegevens sink maken](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="6b39e-154">Hier kunt u Hallo-type van de opslagplaats die u wilt dat tooadd en Hallo andere parameters die zijn gekoppeld aan het Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="6b39e-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="6b39e-155">In beide gevallen worden de storage-wachtrij wordt gemaakt wanneer Hallo-taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6b39e-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="6b39e-156">Deze wachtrij wordt gevuld met berichten over getransformeerde blobs wanneer deze gereed zijn.</span><span class="sxs-lookup"><span data-stu-id="6b39e-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="6b39e-157">Hallo-naam van deze wachtrij is hetzelfde als de naam van de taakdefinitie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="6b39e-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="6b39e-158">Als u selecteert **Media Services** als type Hallo-opslagplaats, vervolgens kunt u ook opgeven opslagaccountreferenties waar Hallo wachtrij wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6b39e-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![Nieuwe gegevens sink-details](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="6b39e-160">Na het toevoegen van Hallo data opslagplaats (die duurt een paar seconden) vindt u Hallo-opslagplaats in de vervolgkeuzelijst Hallo in Hallo **doel-accountnaam**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="6b39e-161">Kies Hallo doelmap die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="6b39e-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="6b39e-162">Klik op **OK** toocreate Hallo taakdefinitie.</span><span class="sxs-lookup"><span data-stu-id="6b39e-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="6b39e-163">De taakdefinitie van de is nu ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6b39e-163">Your job definition is now set up.</span></span> <span data-ttu-id="6b39e-164">U kunt deze taakdefinitie meerdere keren via Hallo gebruikersinterface gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6b39e-164">You can use this job definition multiple times via hello UI.</span></span>

    ![Nieuwe taakdefinitie toevoegen](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="6b39e-166">Hallo taakdefinitie uitvoeren</span><span class="sxs-lookup"><span data-stu-id="6b39e-166">Run hello job definition</span></span>

<span data-ttu-id="6b39e-167">Als u toomove gegevens van StorSimple toohello storage-account dat u hebt opgegeven in de taakdefinitie hello moet, moet u tooinvoke deze.</span><span class="sxs-lookup"><span data-stu-id="6b39e-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="6b39e-168">Er is enige flexibiliteit in Hallo parameters wijzigen telkens wanneer u Hallo taak aanroept.</span><span class="sxs-lookup"><span data-stu-id="6b39e-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="6b39e-169">Hallo stappen zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="6b39e-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="6b39e-170">Selecteer uw StorSimple Data Manager-service en ga te**bewaking**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="6b39e-171">Klik op **nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="6b39e-171">Click **Run Now**.</span></span>

    ![De definitie van de trigger](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="6b39e-173">Hallo taakdefinitie kiezen dat u wilt dat toorun.</span><span class="sxs-lookup"><span data-stu-id="6b39e-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="6b39e-174">Klik op **instellingen uitvoeren** toomodify alle instellingen die u toochange voor deze taak uitvoeren wilt mogelijk.</span><span class="sxs-lookup"><span data-stu-id="6b39e-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![Taakinstellingen uitvoeren](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="6b39e-176">Klik op **OK** en klik vervolgens op **uitvoeren** toolaunch uw taak.</span><span class="sxs-lookup"><span data-stu-id="6b39e-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="6b39e-177">toomonitor deze taak, Ga toohello **taken** pagina in uw StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="6b39e-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Takenlijst met en status](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="6b39e-179">In aanvulling toomonitoring in Hallo **taken** blade, u kunt ook luisteren op Hallo opslagwachtrij waar een bericht telkens wanneer een bestand wordt verplaatst van StorSimple toohello storage-account is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6b39e-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6b39e-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b39e-180">Next steps</span></span>

<span data-ttu-id="6b39e-181">[Gebruik de .NET SDK toolaunch StorSimple Data Manager taken](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="6b39e-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
