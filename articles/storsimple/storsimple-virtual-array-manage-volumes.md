---
title: aaaManage volumes op de virtuele StorSimple-matrix | Microsoft Docs
description: Beschrijving van Hallo StorSimple Apparaatbeheer en wordt uitgelegd hoe toouse het toomanage volumes op uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="2d948-103">Gebruik StorSimple Apparaatbeheer service toomanage volumes op Hallo virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="2d948-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="2d948-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="2d948-104">Overview</span></span>

<span data-ttu-id="2d948-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheren van volumes op uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="2d948-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="2d948-106">Hallo StorSimple-apparaat Manager-service is een uitbreiding in hello Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface.</span><span class="sxs-lookup"><span data-stu-id="2d948-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="2d948-107">In toevoeging toomanaging shares en -volumes, kunt u Hallo Apparaatbeheer StorSimple-service tooview gebruiken en beheren van apparaten, waarschuwingen, weergeven en weergeven en beheren back-upbeleid en back-upcatalogus Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d948-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="2d948-108">Volumetypen</span><span class="sxs-lookup"><span data-stu-id="2d948-108">Volume Types</span></span>

<span data-ttu-id="2d948-109">StorSimple-volumes kunnen zijn:</span><span class="sxs-lookup"><span data-stu-id="2d948-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="2d948-110">**Lokaal vastgemaakt**: gegevens op deze volumes op Hallo matrix te allen tijde blijft en heeft geen toohello cloud worden gelekt.</span><span class="sxs-lookup"><span data-stu-id="2d948-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="2d948-111">**Gelaagde**: gegevens in deze volumes kunnen toohello cloud worden gelekt.</span><span class="sxs-lookup"><span data-stu-id="2d948-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="2d948-112">Wanneer u een gelaagd volume maakt, wordt ongeveer 10% van Hallo ruimte is ingericht op de lokale laag Hallo en 90% van Hallo ruimte in de cloud Hallo is ingericht.</span><span class="sxs-lookup"><span data-stu-id="2d948-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="2d948-113">Hallo bijvoorbeeld gegevenslagen op als u een volume 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte Hallo en 900 GB wordt gebruikt in de cloud Hallo wanneer.</span><span class="sxs-lookup"><span data-stu-id="2d948-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="2d948-114">Dit wordt op zijn beurt betekent dat als u geen alle Hallo lokale ruimte meer op Hallo apparaat uitvoeren, u kunt geen een gelaagd volume inrichten (omdat Hallo 10% op Hallo lokale laag niet meer beschikbaar vereist).</span><span class="sxs-lookup"><span data-stu-id="2d948-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="2d948-115">Ingerichte capaciteit</span><span class="sxs-lookup"><span data-stu-id="2d948-115">Provisioned capacity</span></span>
<span data-ttu-id="2d948-116">Raadpleeg de volgende tabel voor maximale ingerichte capaciteit voor elk volumetype toohello.</span><span class="sxs-lookup"><span data-stu-id="2d948-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="2d948-117">**Limiet-ID**</span><span class="sxs-lookup"><span data-stu-id="2d948-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="2d948-118">**Limiet**</span><span class="sxs-lookup"><span data-stu-id="2d948-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="2d948-119">Minimale grootte van een gelaagd volume</span><span class="sxs-lookup"><span data-stu-id="2d948-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="2d948-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="2d948-120">500 GB</span></span>        |
| <span data-ttu-id="2d948-121">Maximale grootte van een gelaagd volume</span><span class="sxs-lookup"><span data-stu-id="2d948-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="2d948-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="2d948-122">5 TB</span></span>          |
| <span data-ttu-id="2d948-123">Minimale grootte van een lokaal vastgemaakt volume</span><span class="sxs-lookup"><span data-stu-id="2d948-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="2d948-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="2d948-124">50 GB</span></span>         |
| <span data-ttu-id="2d948-125">Maximale grootte van een lokaal vastgemaakt volume</span><span class="sxs-lookup"><span data-stu-id="2d948-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="2d948-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="2d948-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="2d948-127">Hallo Volumes blade</span><span class="sxs-lookup"><span data-stu-id="2d948-127">hello Volumes blade</span></span>
<span data-ttu-id="2d948-128">Hallo **Volumes** menu op de blade voor een overzicht van het StorSimple-service Hallo lijst weergeven met opslagvolumes op een gegeven StorSimple-matrix en kunt u toomanage ze.</span><span class="sxs-lookup"><span data-stu-id="2d948-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Blade volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="2d948-130">Een volume bestaat uit een reeks van kenmerken:</span><span class="sxs-lookup"><span data-stu-id="2d948-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="2d948-131">**Volumenaam** – een beschrijvende naam moet uniek zijn en kan Hallo volume geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="2d948-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="2d948-132">**Status** – online of offline kan zijn.</span><span class="sxs-lookup"><span data-stu-id="2d948-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="2d948-133">Als een volume offline is, maar het is niet zichtbaar tooinitiators (servers) die toegang toouse Hallo volume zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2d948-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="2d948-134">**Type** – Hiermee wordt aangegeven of Hallo volume **tiers verdeelde** (Hallo standaard) of **lokaal vastgemaakt**.</span><span class="sxs-lookup"><span data-stu-id="2d948-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="2d948-135">**Capaciteit** – geeft Hallo hoeveelheid gegevens die worden gebruikt als vergeleken toohello totale hoeveelheid gegevens die kunnen worden opgeslagen door Hallo initiator (server).</span><span class="sxs-lookup"><span data-stu-id="2d948-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="2d948-136">**Back-** – voor het geval van Hallo virtuele StorSimple-matrix, worden alle volumes automatisch ingeschakeld voor back-up.</span><span class="sxs-lookup"><span data-stu-id="2d948-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="2d948-137">**Verbonden hosts** – Hiermee geeft u op Hallo initiators (servers) die toegang toothis volume zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2d948-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Details van de volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="2d948-139">Gebruik Hallo-instructies in deze zelfstudie tooperform Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d948-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="2d948-140">Een volume toevoegen</span><span class="sxs-lookup"><span data-stu-id="2d948-140">Add a volume</span></span>
* <span data-ttu-id="2d948-141">Een volume wijzigen</span><span class="sxs-lookup"><span data-stu-id="2d948-141">Modify a volume</span></span>
* <span data-ttu-id="2d948-142">Een volume offline zetten</span><span class="sxs-lookup"><span data-stu-id="2d948-142">Take a volume offline</span></span>
* <span data-ttu-id="2d948-143">Een volume verwijderen</span><span class="sxs-lookup"><span data-stu-id="2d948-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="2d948-144">Een volume toevoegen</span><span class="sxs-lookup"><span data-stu-id="2d948-144">Add a volume</span></span>

1. <span data-ttu-id="2d948-145">Hallo StorSimple-service samenvatting blade, klikt u op **+ volume toevoegen** uit Hallo opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="2d948-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="2d948-146">Hiermee opent u up Hallo **volume toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="2d948-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Volume toevoegen](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="2d948-148">In Hallo **volume toevoegen** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d948-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="2d948-149">In Hallo **volumenaam** en voer een unieke naam voor het volume.</span><span class="sxs-lookup"><span data-stu-id="2d948-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="2d948-150">Hallo-naam moet een tekenreeks die 3 too127 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="2d948-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="2d948-151">In Hallo **Type** dropdown lijst, opgeven of toocreate een **tiers verdeelde** of **lokaal vastgemaakt** volume.</span><span class="sxs-lookup"><span data-stu-id="2d948-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="2d948-152">Selecteer voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, **lokaal vastgemaakt volume**.</span><span class="sxs-lookup"><span data-stu-id="2d948-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="2d948-153">Voor alle overige gegevens selecteert **tiers verdeelde** volume.</span><span class="sxs-lookup"><span data-stu-id="2d948-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="2d948-154">In Hallo **capaciteit** veld, Hallo grootte van Hallo volume opgeven.</span><span class="sxs-lookup"><span data-stu-id="2d948-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="2d948-155">Een gelaagd volume moet liggen tussen 500 GB en 5 TB en een lokaal vastgemaakt volume moet tussen 50 en 500 GB.</span><span class="sxs-lookup"><span data-stu-id="2d948-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="2d948-156">Klik op **verbonden hosts**, selecteert u een access control record (ACR) bijbehorende toohello iSCSI-initiator wilt tooconnect toothis volume en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="2d948-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="2d948-157">tooadd nieuwe verbonden host, klikt u op **nieuwe toevoegen**, voer een naam voor het Hallo-host en de iSCSI Qualified Name (IQN) en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2d948-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Volume toevoegen](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="2d948-159">Wanneer u klaar bent met het configureren van het volume, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="2d948-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="2d948-160">Een volume wordt gemaakt met de opgegeven Hallo instellingen en u ziet een melding op Hallo gemaakt Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="2d948-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="2d948-161">Standaard worden back-up voor Hallo volume ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2d948-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="2d948-162">tooconfirm die Hallo volume is gemaakt, gaat u toohello is **Volumes** blade.</span><span class="sxs-lookup"><span data-stu-id="2d948-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="2d948-163">U ziet Hallo volume dat wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="2d948-163">You should see hello volume listed.</span></span>
   
    ![Volume maken geslaagd](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="2d948-165">Een volume wijzigen</span><span class="sxs-lookup"><span data-stu-id="2d948-165">Modify a volume</span></span>

<span data-ttu-id="2d948-166">Een volume wijzigen als u nodig hebt toochange Hallo hosts die toegang tot het Hallo-volume.</span><span class="sxs-lookup"><span data-stu-id="2d948-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="2d948-167">worden Hallo overige kenmerken van een volume kunnen niet gewijzigd zodra Hallo volume is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2d948-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="2d948-168">een volume toomodify</span><span class="sxs-lookup"><span data-stu-id="2d948-168">toomodify a volume</span></span>

1. <span data-ttu-id="2d948-169">Van Hallo **Volumes** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo volume dat u wenst dat u toomodify zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="2d948-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="2d948-170">**Selecteer** Hallo volume en klik op **verbonden hosts** tooview Hallo momenteel verbonden host en de andere server tooa te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2d948-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Volume bewerken](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="2d948-172">Sla de wijzigingen door te klikken op Hallo **opslaan** opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="2d948-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="2d948-173">De opgegeven instellingen worden toegepast en u ziet een melding.</span><span class="sxs-lookup"><span data-stu-id="2d948-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="2d948-174">Een volume offline zetten</span><span class="sxs-lookup"><span data-stu-id="2d948-174">Take a volume offline</span></span>

<span data-ttu-id="2d948-175">Mogelijk moet u een volume offline tootake wanneer u van plan bent toomodify of verwijderen deze.</span><span class="sxs-lookup"><span data-stu-id="2d948-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="2d948-176">Als een volume offline is, is het niet beschikbaar voor lees-/ schrijftoegang.</span><span class="sxs-lookup"><span data-stu-id="2d948-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="2d948-177">U moet tootake Hallo volume offline op host hello, evenals op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="2d948-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="2d948-178">een volume offline tootake</span><span class="sxs-lookup"><span data-stu-id="2d948-178">tootake a volume offline</span></span>

1. <span data-ttu-id="2d948-179">Zorg ervoor dat de betreffende Hallo volume is niet in gebruik voordat deze offline wordt gezet.</span><span class="sxs-lookup"><span data-stu-id="2d948-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="2d948-180">Hallo volume offline op host Hallo eerste duren.</span><span class="sxs-lookup"><span data-stu-id="2d948-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="2d948-181">Hierdoor wordt een potentieel risico van gegevensbeschadiging op Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="2d948-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="2d948-182">Raadpleeg voor specifieke stappen toohello instructies voor het besturingssysteem van de host.</span><span class="sxs-lookup"><span data-stu-id="2d948-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="2d948-183">Nadat het Hallo-volume op Hallo host offline is, ondernemen Hallo volume offline Hallo-matrix door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2d948-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="2d948-184">Van Hallo **Volumes** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo volume dat u wenst dat u offline tootake zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="2d948-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="2d948-185">**Selecteer** Hallo volume en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **offline zetten**.</span><span class="sxs-lookup"><span data-stu-id="2d948-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Offline volume](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="2d948-187">Lees de informatie Hallo in Hallo **offline zetten** blade en Bevestig de bevestiging van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="2d948-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="2d948-188">Klik op **offline zetten** tootake Hallo volume offline.</span><span class="sxs-lookup"><span data-stu-id="2d948-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="2d948-189">U ziet een melding van Hallo-bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2d948-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="2d948-190">tooconfirm die Hallo volume is offline gehaald, gaat u toohello **Volumes** blade.</span><span class="sxs-lookup"><span data-stu-id="2d948-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="2d948-191">U ziet Hallo-status van Hallo volume als offline.</span><span class="sxs-lookup"><span data-stu-id="2d948-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Offline volume bevestigen](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="2d948-193">Een volume verwijderen</span><span class="sxs-lookup"><span data-stu-id="2d948-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d948-194">U kunt een volume alleen verwijderen als deze offline is.</span><span class="sxs-lookup"><span data-stu-id="2d948-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="2d948-195">Volgende stappen toodelete een volume Hallo voltooien.</span><span class="sxs-lookup"><span data-stu-id="2d948-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="2d948-196">een volume toodelete</span><span class="sxs-lookup"><span data-stu-id="2d948-196">toodelete a volume</span></span>

1. <span data-ttu-id="2d948-197">Van Hallo **Volumes** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo volume dat u wenst dat u toodelete zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="2d948-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="2d948-198">**Selecteer** Hallo volume en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2d948-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Volume verwijderen](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="2d948-200">Controleer de status van Hallo Hallo volume dat u wilt dat toodelete.</span><span class="sxs-lookup"><span data-stu-id="2d948-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="2d948-201">Als de gewenste toodelete Hallo-volume niet offline is, het Hallo voor offline eerste, de volgende stappen uitvoeren [offline zetten van een volume](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="2d948-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="2d948-202">Als u wordt gevraagd om bevestiging in Hallo **verwijderen** blade accepteer Hallo bevestiging en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2d948-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="2d948-203">Hallo-volume wordt nu verwijderd en Hallo **Volumes** blade ziet Hallo bijgewerkt lijst van volumes in een virtuele Hallo-matrix.</span><span class="sxs-lookup"><span data-stu-id="2d948-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d948-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d948-204">Next steps</span></span>

<span data-ttu-id="2d948-205">Meer informatie over hoe te[klonen van een StorSimple-volume](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="2d948-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

