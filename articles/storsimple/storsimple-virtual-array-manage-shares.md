---
title: aaaManage virtuele StorSimple-matrix deelt | Microsoft Docs
description: Beschrijving van Hallo StorSimple Apparaatbeheer en wordt uitgelegd hoe toouse het toomanage shares op uw virtuele StorSimple-matrix.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="fb142-103">Hallo Apparaatbeheer StorSimple-service toomanage shares op Hallo virtuele StorSimple-matrix gebruiken</span><span class="sxs-lookup"><span data-stu-id="fb142-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="fb142-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fb142-104">Overview</span></span>

<span data-ttu-id="fb142-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheren van shares op uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="fb142-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="fb142-106">Hallo StorSimple-apparaat Manager-service is een uitbreiding in hello Azure-portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface.</span><span class="sxs-lookup"><span data-stu-id="fb142-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="fb142-107">In toevoeging toomanaging shares en -volumes, kunt u Hallo Apparaatbeheer StorSimple-service tooview gebruiken en beheren van apparaten, waarschuwingen weergeven, back-upbeleid beheren en Hallo back-catalogus beheren.</span><span class="sxs-lookup"><span data-stu-id="fb142-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="fb142-108">Typen delen</span><span class="sxs-lookup"><span data-stu-id="fb142-108">Share Types</span></span>

<span data-ttu-id="fb142-109">StorSimple-shares zijn:</span><span class="sxs-lookup"><span data-stu-id="fb142-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="fb142-110">**Lokaal vastgemaakt**: gegevens in deze shares op Hallo matrix te allen tijde blijft en heeft geen toohello cloud worden gelekt.</span><span class="sxs-lookup"><span data-stu-id="fb142-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="fb142-111">**Gelaagde**: gegevens in deze shares kunt toohello cloud worden gelekt.</span><span class="sxs-lookup"><span data-stu-id="fb142-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="fb142-112">Bij het maken van een gelaagde share ongeveer 10% van Hallo ruimte is ingericht op de lokale laag Hallo en 90% van Hallo ruimte in de cloud Hallo is ingericht.</span><span class="sxs-lookup"><span data-stu-id="fb142-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="fb142-113">Hallo bijvoorbeeld gegevenslagen op als u een share 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte Hallo en 900 GB wordt gebruikt in de cloud Hallo wanneer.</span><span class="sxs-lookup"><span data-stu-id="fb142-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="fb142-114">Dit wordt op zijn beurt betekent dat als u geen alle Hallo lokale ruimte meer op Hallo apparaat uitvoeren, u kunt geen een gelaagde share inrichten (omdat Hallo 10% op Hallo lokale laag niet meer beschikbaar vereist).</span><span class="sxs-lookup"><span data-stu-id="fb142-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="fb142-115">Ingerichte capaciteit</span><span class="sxs-lookup"><span data-stu-id="fb142-115">Provisioned capacity</span></span>

<span data-ttu-id="fb142-116">Raadpleeg de volgende tabel voor maximale ingerichte capaciteit voor elk sharetype toohello.</span><span class="sxs-lookup"><span data-stu-id="fb142-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="fb142-117">**Limiet-ID**</span><span class="sxs-lookup"><span data-stu-id="fb142-117">**Limit identifier**</span></span> | <span data-ttu-id="fb142-118">**Limiet**</span><span class="sxs-lookup"><span data-stu-id="fb142-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="fb142-119">Minimale grootte van een gelaagde share</span><span class="sxs-lookup"><span data-stu-id="fb142-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="fb142-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="fb142-120">500 GB</span></span> |
| <span data-ttu-id="fb142-121">Maximale grootte van een gelaagde share</span><span class="sxs-lookup"><span data-stu-id="fb142-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="fb142-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="fb142-122">20 TB</span></span> |
| <span data-ttu-id="fb142-123">Minimale grootte van een lokaal vastgemaakt share</span><span class="sxs-lookup"><span data-stu-id="fb142-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="fb142-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="fb142-124">50 GB</span></span> |
| <span data-ttu-id="fb142-125">Maximale grootte van een lokaal vastgemaakt share</span><span class="sxs-lookup"><span data-stu-id="fb142-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="fb142-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="fb142-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="fb142-127">Hallo Shares blade</span><span class="sxs-lookup"><span data-stu-id="fb142-127">hello Shares blade</span></span>

<span data-ttu-id="fb142-128">Hallo **Shares** menu op de blade voor een overzicht van het StorSimple-service Hallo lijst weergeven met storage-shares op een gegeven StorSimple-matrix en kunt u toomanage ze.</span><span class="sxs-lookup"><span data-stu-id="fb142-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Blade shares](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="fb142-130">Een share bestaat uit een reeks van kenmerken:</span><span class="sxs-lookup"><span data-stu-id="fb142-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="fb142-131">**Sharenaam** – een beschrijvende naam moet uniek zijn en kan Hallo share geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="fb142-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="fb142-132">**Status** – online of offline kan zijn.</span><span class="sxs-lookup"><span data-stu-id="fb142-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="fb142-133">Als een share offline is, gebruikers van de share Hallo tooaccess kunnen niet worden deze.</span><span class="sxs-lookup"><span data-stu-id="fb142-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="fb142-134">**Type** – Hiermee wordt aangegeven of de share Hallo **tiers verdeelde** (Hallo standaard) of **lokaal vastgemaakt**.</span><span class="sxs-lookup"><span data-stu-id="fb142-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="fb142-135">**Capaciteit** – Hiermee geeft u de hoeveelheid gegevens die worden gebruikt als de totale hoeveelheid gegevens die kunnen worden opgeslagen op Hallo share vergeleken toohello Hallo.</span><span class="sxs-lookup"><span data-stu-id="fb142-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="fb142-136">**Beschrijving** : een optionele instelling waarmee Hallo share beschrijven.</span><span class="sxs-lookup"><span data-stu-id="fb142-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="fb142-137">**Machtigingen** -Hallo NTFS-machtigingen toohello share die kan worden beheerd via de Windows Verkenner.</span><span class="sxs-lookup"><span data-stu-id="fb142-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="fb142-138">**Back-** – voor het geval van Hallo virtuele StorSimple-matrix, alle shares automatisch ingeschakeld voor back-up.</span><span class="sxs-lookup"><span data-stu-id="fb142-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Shares details](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="fb142-140">Gebruik Hallo-instructies in deze zelfstudie tooperform Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb142-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="fb142-141">Share toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb142-141">Add a share</span></span>
* <span data-ttu-id="fb142-142">Een share wijzigen</span><span class="sxs-lookup"><span data-stu-id="fb142-142">Modify a share</span></span>
* <span data-ttu-id="fb142-143">Een share offline zetten</span><span class="sxs-lookup"><span data-stu-id="fb142-143">Take a share offline</span></span>
* <span data-ttu-id="fb142-144">Een share verwijderen</span><span class="sxs-lookup"><span data-stu-id="fb142-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="fb142-145">Share toevoegen</span><span class="sxs-lookup"><span data-stu-id="fb142-145">Add a share</span></span>

1. <span data-ttu-id="fb142-146">Hallo StorSimple-service samenvatting blade, klikt u op **+ bestandsshare toevoegen** uit Hallo opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="fb142-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="fb142-147">Hiermee opent u up Hallo **toevoegen share** blade.</span><span class="sxs-lookup"><span data-stu-id="fb142-147">This opens up hello **Add share** blade.</span></span>

    ![Share toevoegen](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="fb142-149">In Hallo **toevoegen share** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="fb142-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="fb142-150">In Hallo **sharenaam** en voer een unieke naam voor de share.</span><span class="sxs-lookup"><span data-stu-id="fb142-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="fb142-151">Hallo-naam moet een tekenreeks die 3 too127 tekens bevat.</span><span class="sxs-lookup"><span data-stu-id="fb142-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="fb142-152">Een optionele **beschrijving** voor Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="fb142-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="fb142-153">Hallo beschrijving kunt identificeren Hallo eigenaren van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="fb142-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="fb142-154">In Hallo **Type** dropdown lijst, opgeven of toocreate een **tiers verdeelde** of **lokaal vastgemaakt** delen.</span><span class="sxs-lookup"><span data-stu-id="fb142-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="fb142-155">Selecteer voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, **lokaal vastgemaakt share**.</span><span class="sxs-lookup"><span data-stu-id="fb142-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="fb142-156">Voor alle overige gegevens selecteert **tiers verdeelde** delen.</span><span class="sxs-lookup"><span data-stu-id="fb142-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="fb142-157">In Hallo **capaciteit** veld, Hallo grootte van Hallo share opgeven.</span><span class="sxs-lookup"><span data-stu-id="fb142-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="fb142-158">Een gelaagde share moet tussen 500 GB en 20 TB en een lokaal vastgemaakt share moet tussen 50 GB en 2 TB.</span><span class="sxs-lookup"><span data-stu-id="fb142-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="fb142-159">In Hallo **standaard volledige machtigingen ingesteld op** veld, Hallo machtigingen toohello gebruiker of groep Hallo die toegang heeft tot deze share toewijzen.</span><span class="sxs-lookup"><span data-stu-id="fb142-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="fb142-160">Hallo naam opgeven van Hallo-gebruiker of groep in Hallo  _john@contoso.com_  indeling.</span><span class="sxs-lookup"><span data-stu-id="fb142-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="fb142-161">Het is raadzaam dat u een gebruiker groep (in plaats van een enkele gebruiker) tooallow admin bevoegdheden tooaccess deze shares.</span><span class="sxs-lookup"><span data-stu-id="fb142-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="fb142-162">Nadat u hier Hallo machtigingen hebt toegewezen, klikt u vervolgens kunt u Windows Verkenner toomodify deze machtigingen.</span><span class="sxs-lookup"><span data-stu-id="fb142-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="fb142-163">Wanneer u klaar bent met het configureren van de share, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="fb142-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="fb142-164">Een share wordt gemaakt met de opgegeven Hallo instellingen en u ziet een melding.</span><span class="sxs-lookup"><span data-stu-id="fb142-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="fb142-165">Standaard wordt de back-up worden ingeschakeld voor Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="fb142-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="fb142-166">tooconfirm die share Hallo is is gemaakt, gaat u toohello **Shares** blade.</span><span class="sxs-lookup"><span data-stu-id="fb142-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="fb142-167">U ziet Hallo vermelde delen.</span><span class="sxs-lookup"><span data-stu-id="fb142-167">You should see hello share listed.</span></span>
   
    ![Share maken geslaagd](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="fb142-169">Een share wijzigen</span><span class="sxs-lookup"><span data-stu-id="fb142-169">Modify a share</span></span>

<span data-ttu-id="fb142-170">Een share wijzigen wanneer u toochange Hallo beschrijving van de Hallo share nodig.</span><span class="sxs-lookup"><span data-stu-id="fb142-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="fb142-171">Er zijn geen andere eigenschappen van de share kunnen worden gewijzigd zodra de share Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fb142-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="fb142-172">toomodify een share</span><span class="sxs-lookup"><span data-stu-id="fb142-172">toomodify a share</span></span>

1. <span data-ttu-id="fb142-173">Van Hallo **Shares** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo share die u wenst dat u toomodify zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="fb142-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="fb142-174">**Selecteer** Hallo share tooview Hallo huidige beschrijving en te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fb142-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="fb142-175">Sla de wijzigingen door te klikken op Hallo **opslaan** opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="fb142-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="fb142-176">De opgegeven instellingen worden toegepast en u ziet een melding.</span><span class="sxs-lookup"><span data-stu-id="fb142-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="fb142-177">Share bewerken</span><span class="sxs-lookup"><span data-stu-id="fb142-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="fb142-178">Een share offline zetten</span><span class="sxs-lookup"><span data-stu-id="fb142-178">Take a share offline</span></span>

<span data-ttu-id="fb142-179">Mogelijk moet u een share offline tootake wanneer u van plan bent toomodify of verwijderen deze.</span><span class="sxs-lookup"><span data-stu-id="fb142-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="fb142-180">Als een share offline is, is het niet beschikbaar voor lees-/ schrijftoegang.</span><span class="sxs-lookup"><span data-stu-id="fb142-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="fb142-181">U moet tootake Hallo share offline op host hello, evenals op Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="fb142-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="fb142-182">tootake een share offline</span><span class="sxs-lookup"><span data-stu-id="fb142-182">tootake a share offline</span></span>

1. <span data-ttu-id="fb142-183">Zorg ervoor dat de dat betreffende Hallo share wordt niet gebruikt voordat deze offline wordt gezet.</span><span class="sxs-lookup"><span data-stu-id="fb142-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="fb142-184">Hallo-share op Hallo matrix offline nemen door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="fb142-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="fb142-185">Van Hallo **Shares** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke Hallo share die u wenst dat u offline tootake zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="fb142-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="fb142-186">**Selecteer** Hallo share en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **offline zetten**.</span><span class="sxs-lookup"><span data-stu-id="fb142-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Offline share](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="fb142-188">Lees de informatie Hallo in Hallo **offline zetten** blade en Bevestig de bevestiging van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="fb142-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="fb142-189">Klik op **offline zetten** offline tootake Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="fb142-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="fb142-190">U ziet een melding van Hallo-bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fb142-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="fb142-191">tooconfirm die share Hallo is offline, gaat u toohello is gehaald **Shares** blade.</span><span class="sxs-lookup"><span data-stu-id="fb142-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="fb142-192">U ziet Hallo status als offline Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="fb142-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="fb142-193">Een share verwijderen</span><span class="sxs-lookup"><span data-stu-id="fb142-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb142-194">U kunt een share alleen verwijderen als deze offline is.</span><span class="sxs-lookup"><span data-stu-id="fb142-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="fb142-195">Volgende stappen toodelete een share Hallo voltooien.</span><span class="sxs-lookup"><span data-stu-id="fb142-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="fb142-196">toodelete een share</span><span class="sxs-lookup"><span data-stu-id="fb142-196">toodelete a share</span></span>

1. <span data-ttu-id="fb142-197">Van Hallo **Shares** instellen op Hallo StorSimple-service samenvatting blade, selecteer Hallo virtuele matrix op welke share Hallo gewenst toodelete zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="fb142-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="fb142-198">**Selecteer** Hallo share en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="fb142-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Share verwijderen](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="fb142-200">Controleer de status van Hallo Hallo-share die u wilt toodelete.</span><span class="sxs-lookup"><span data-stu-id="fb142-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="fb142-201">Als u wilt dat toodelete Hallo-share niet offline is, het offline halen eerst.</span><span class="sxs-lookup"><span data-stu-id="fb142-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="fb142-202">Volg de stappen Hallo in [offline zetten van een share](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="fb142-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="fb142-203">Als u wordt gevraagd om bevestiging in Hallo **verwijderen** blade accepteer Hallo bevestiging en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="fb142-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="fb142-204">Hallo-share wordt nu verwijderd en Hallo **Shares** blade ziet u Hallo bijgewerkt lijst met shares binnen Hallo virtuele matrix.</span><span class="sxs-lookup"><span data-stu-id="fb142-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb142-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb142-205">Next steps</span></span>
<span data-ttu-id="fb142-206">Meer informatie over hoe te[klonen van een StorSimple-share](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="fb142-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

