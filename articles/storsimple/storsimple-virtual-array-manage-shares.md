---
title: Virtuele StorSimple-matrix shares kunt beheren | Microsoft Docs
description: Worden Apparaatbeheer StorSimple beschreven en wordt uitgelegd hoe u deze voor het beheren van shares op uw virtuele StorSimple-matrix.
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
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="c3db7-103">De service Manager voor StorSimple-apparaat gebruiken voor het beheren van shares op de virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="c3db7-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="c3db7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c3db7-104">Overview</span></span>

<span data-ttu-id="c3db7-105">Deze zelfstudie wordt uitgelegd hoe u met de service Manager voor StorSimple-apparaat maken en beheren van shares op uw virtuele StorSimple-matrix.</span><span class="sxs-lookup"><span data-stu-id="c3db7-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="c3db7-106">De service Manager voor StorSimple-apparaat is een uitbreiding in de Azure portal waarmee u uw StorSimple-oplossing beheren via een enkel webinterface.</span><span class="sxs-lookup"><span data-stu-id="c3db7-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="c3db7-107">Naast het beheren van bestandsshares en volumes, kunt u de service Manager voor StorSimple-apparaat om te bekijken en beheren van apparaten, waarschuwingen weergeven back-upbeleid beheren en de back-catalogus beheren.</span><span class="sxs-lookup"><span data-stu-id="c3db7-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="c3db7-108">Typen delen</span><span class="sxs-lookup"><span data-stu-id="c3db7-108">Share Types</span></span>

<span data-ttu-id="c3db7-109">StorSimple-shares zijn:</span><span class="sxs-lookup"><span data-stu-id="c3db7-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="c3db7-110">**Lokaal vastgemaakt**: gegevens in deze shares blijft op de matrix te allen tijde en komt niet in de cloud worden gelekt.</span><span class="sxs-lookup"><span data-stu-id="c3db7-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="c3db7-111">**Gelaagde**: gegevens in deze shares kunnen worden gelekt naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="c3db7-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="c3db7-112">Bij het maken van een gelaagde share ongeveer 10% van de ruimte is ingericht op de lokale laag en 90% van de ruimte in de cloud is ingericht.</span><span class="sxs-lookup"><span data-stu-id="c3db7-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="c3db7-113">Bijvoorbeeld: als u een share 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte en 900 GB in de cloud moet worden gebruikt wanneer de gegevenslagen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="c3db7-114">Dit wordt op zijn beurt betekent dat als u buiten de lokale ruimte op het apparaat uitvoeren, u kunt geen een gelaagde share inrichten (omdat de 10% vereist op de lokale laag niet meer beschikbaar).</span><span class="sxs-lookup"><span data-stu-id="c3db7-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="c3db7-115">Ingerichte capaciteit</span><span class="sxs-lookup"><span data-stu-id="c3db7-115">Provisioned capacity</span></span>

<span data-ttu-id="c3db7-116">Raadpleeg de volgende tabel voor maximale ingerichte capaciteit voor elk sharetype.</span><span class="sxs-lookup"><span data-stu-id="c3db7-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="c3db7-117">**Limiet-ID**</span><span class="sxs-lookup"><span data-stu-id="c3db7-117">**Limit identifier**</span></span> | <span data-ttu-id="c3db7-118">**Limiet**</span><span class="sxs-lookup"><span data-stu-id="c3db7-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="c3db7-119">Minimale grootte van een gelaagde share</span><span class="sxs-lookup"><span data-stu-id="c3db7-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="c3db7-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="c3db7-120">500 GB</span></span> |
| <span data-ttu-id="c3db7-121">Maximale grootte van een gelaagde share</span><span class="sxs-lookup"><span data-stu-id="c3db7-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="c3db7-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="c3db7-122">20 TB</span></span> |
| <span data-ttu-id="c3db7-123">Minimale grootte van een lokaal vastgemaakt share</span><span class="sxs-lookup"><span data-stu-id="c3db7-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="c3db7-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="c3db7-124">50 GB</span></span> |
| <span data-ttu-id="c3db7-125">Maximale grootte van een lokaal vastgemaakt share</span><span class="sxs-lookup"><span data-stu-id="c3db7-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="c3db7-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="c3db7-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="c3db7-127">De blade Shares</span><span class="sxs-lookup"><span data-stu-id="c3db7-127">The Shares blade</span></span>

<span data-ttu-id="c3db7-128">De **Shares** menu op de blade voor een overzicht van het StorSimple-service geeft een lijst met storage-shares op een gegeven StorSimple-matrix en kunt u ze kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="c3db7-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![Blade shares](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="c3db7-130">Een share bestaat uit een reeks van kenmerken:</span><span class="sxs-lookup"><span data-stu-id="c3db7-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="c3db7-131">**Sharenaam** – een beschrijvende naam die moet uniek en kunt u de share te identificeren.</span><span class="sxs-lookup"><span data-stu-id="c3db7-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="c3db7-132">**Status** – online of offline kan zijn.</span><span class="sxs-lookup"><span data-stu-id="c3db7-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="c3db7-133">Als een share offline is, wordt gebruikers van de share niet mogelijk om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="c3db7-134">**Type** – Hiermee wordt aangegeven of de share **tiers verdeelde** (de standaardinstelling) of **lokaal vastgemaakt**.</span><span class="sxs-lookup"><span data-stu-id="c3db7-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="c3db7-135">**Capaciteit** – geeft de hoeveelheid gegevens die worden gebruikt in vergelijking met de totale hoeveelheid gegevens die kunnen worden opgeslagen op de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="c3db7-136">**Beschrijving** : een optionele instelling waarmee de share te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="c3db7-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="c3db7-137">**Machtigingen** -het NTFS-machtigingen voor de share die kunnen worden beheerd via de Windows Verkenner.</span><span class="sxs-lookup"><span data-stu-id="c3db7-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="c3db7-138">**Back-** – voor het geval van de virtuele StorSimple-matrix, alle shares automatisch ingeschakeld voor back-up.</span><span class="sxs-lookup"><span data-stu-id="c3db7-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Shares details](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="c3db7-140">Volg de instructies in deze zelfstudie aan de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c3db7-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="c3db7-141">Share toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3db7-141">Add a share</span></span>
* <span data-ttu-id="c3db7-142">Een share wijzigen</span><span class="sxs-lookup"><span data-stu-id="c3db7-142">Modify a share</span></span>
* <span data-ttu-id="c3db7-143">Een share offline zetten</span><span class="sxs-lookup"><span data-stu-id="c3db7-143">Take a share offline</span></span>
* <span data-ttu-id="c3db7-144">Een share verwijderen</span><span class="sxs-lookup"><span data-stu-id="c3db7-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="c3db7-145">Share toevoegen</span><span class="sxs-lookup"><span data-stu-id="c3db7-145">Add a share</span></span>

1. <span data-ttu-id="c3db7-146">Klik op de StorSimple-service samenvatting blade **+ bestandsshare toevoegen** uit de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="c3db7-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="c3db7-147">Hiermee opent u de **toevoegen share** blade.</span><span class="sxs-lookup"><span data-stu-id="c3db7-147">This opens up the **Add share** blade.</span></span>

    ![Share toevoegen](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="c3db7-149">In de **toevoegen share** blade het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c3db7-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="c3db7-150">In de **sharenaam** en voer een unieke naam voor de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="c3db7-151">De naam moet een tekenreeks met 3 tot en met 127 tekens.</span><span class="sxs-lookup"><span data-stu-id="c3db7-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="c3db7-152">Een optionele **beschrijving** voor de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-152">An optional **Description** for the share.</span></span> <span data-ttu-id="c3db7-153">De beschrijving kunt identificeren de eigenaren van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="c3db7-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="c3db7-154">In de **Type** dropdown lijst, opgeven of maken van een **tiers verdeelde** of **lokaal vastgemaakt** delen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="c3db7-155">Selecteer voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, **lokaal vastgemaakt share**.</span><span class="sxs-lookup"><span data-stu-id="c3db7-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="c3db7-156">Voor alle overige gegevens selecteert **tiers verdeelde** delen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="c3db7-157">In de **capaciteit** veld, geeft u de grootte van de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="c3db7-158">Een gelaagde share moet tussen 500 GB en 20 TB en een lokaal vastgemaakt share moet tussen 50 GB en 2 TB.</span><span class="sxs-lookup"><span data-stu-id="c3db7-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="c3db7-159">In de **standaard volledige machtigingen ingesteld op** veld, machtigingen toewijzen aan de gebruiker of de groep die toegang heeft tot deze share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="c3db7-160">Geef de naam van de gebruiker of de gebruikersgroep in  _john@contoso.com_  indeling.</span><span class="sxs-lookup"><span data-stu-id="c3db7-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="c3db7-161">Het is raadzaam dat u een gebruikersgroep (in plaats van een enkele gebruiker) om toe te staan beheerdersbevoegdheden voor toegang tot deze shares.</span><span class="sxs-lookup"><span data-stu-id="c3db7-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="c3db7-162">Nadat u hier de machtigingen hebt toegewezen, kunt u Windows Verkenner vervolgens gebruiken om deze machtigingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="c3db7-163">Wanneer u klaar bent met het configureren van de share, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="c3db7-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="c3db7-164">Een share met de opgegeven instellingen wordt gemaakt en u ziet een melding.</span><span class="sxs-lookup"><span data-stu-id="c3db7-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="c3db7-165">Standaard wordt de back-up worden ingeschakeld voor de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="c3db7-166">Om te bevestigen dat de share is gemaakt, gaat u naar de **Shares** blade.</span><span class="sxs-lookup"><span data-stu-id="c3db7-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="c3db7-167">Hier ziet u de share die wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="c3db7-167">You should see the share listed.</span></span>
   
    ![Share maken geslaagd](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="c3db7-169">Een share wijzigen</span><span class="sxs-lookup"><span data-stu-id="c3db7-169">Modify a share</span></span>

<span data-ttu-id="c3db7-170">Een share wijzigen als u wilt wijzigen, de beschrijving van de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="c3db7-171">Er zijn geen andere eigenschappen van de share kunnen worden gewijzigd zodra de share is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c3db7-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="c3db7-172">Wijzigen van een share</span><span class="sxs-lookup"><span data-stu-id="c3db7-172">To modify a share</span></span>

1. <span data-ttu-id="c3db7-173">Van de **Shares** instellen op de blade van StorSimple-service-samenvatting, de virtuele matrix selecteren waarop de share die u wenst te maken van zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="c3db7-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="c3db7-174">**Selecteer** de share bij de huidige beschrijving bekijken en wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="c3db7-175">Sla de wijzigingen door te klikken op de **opslaan** opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="c3db7-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="c3db7-176">De opgegeven instellingen worden toegepast en u ziet een melding.</span><span class="sxs-lookup"><span data-stu-id="c3db7-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="c3db7-177">Share bewerken</span><span class="sxs-lookup"><span data-stu-id="c3db7-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="c3db7-178">Een share offline zetten</span><span class="sxs-lookup"><span data-stu-id="c3db7-178">Take a share offline</span></span>

<span data-ttu-id="c3db7-179">Mogelijk moet u een share offline zetten wanneer u van plan bent om te wijzigen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="c3db7-180">Als een share offline is, is het niet beschikbaar voor lees-/ schrijftoegang.</span><span class="sxs-lookup"><span data-stu-id="c3db7-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="c3db7-181">U moet de share offline nemen op de host, evenals op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="c3db7-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="c3db7-182">Offline te nemen een share</span><span class="sxs-lookup"><span data-stu-id="c3db7-182">To take a share offline</span></span>

1. <span data-ttu-id="c3db7-183">Zorg ervoor dat de betreffende share niet gebruikt wordt voordat deze offline wordt gezet.</span><span class="sxs-lookup"><span data-stu-id="c3db7-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="c3db7-184">De share op de matrix offline nemen door de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="c3db7-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="c3db7-185">Van de **Shares** instellen op de blade van StorSimple-service-samenvatting, de virtuele matrix selecteren waarop de share die u wenst dat u offline te halen zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="c3db7-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="c3db7-186">**Selecteer** de share en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu **offline zetten**.</span><span class="sxs-lookup"><span data-stu-id="c3db7-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Offline share](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="c3db7-188">Lees de informatie in de **offline zetten** blade en de bevestiging van de bewerking te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="c3db7-189">Klik op **offline zetten** offline te nemen de share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="c3db7-190">U ziet een melding van de bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3db7-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="c3db7-191">Om te bevestigen dat de share is offline is gehaald, gaat u naar de **Shares** blade.</span><span class="sxs-lookup"><span data-stu-id="c3db7-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="c3db7-192">U ziet de status van de share als offline.</span><span class="sxs-lookup"><span data-stu-id="c3db7-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="c3db7-193">Een share verwijderen</span><span class="sxs-lookup"><span data-stu-id="c3db7-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3db7-194">U kunt een share alleen verwijderen als deze offline is.</span><span class="sxs-lookup"><span data-stu-id="c3db7-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="c3db7-195">De volgende stappen voor het verwijderen van een share.</span><span class="sxs-lookup"><span data-stu-id="c3db7-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="c3db7-196">Verwijderen van een share</span><span class="sxs-lookup"><span data-stu-id="c3db7-196">To delete a share</span></span>

1. <span data-ttu-id="c3db7-197">Van de **Shares** instellen op de blade van StorSimple-service-samenvatting, de virtuele matrix selecteren waarop de share die u wilt verwijderen zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="c3db7-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="c3db7-198">**Selecteer** de share en klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c3db7-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Share verwijderen](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="c3db7-200">Controleer de status van de share die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c3db7-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="c3db7-201">Als de share die u wilt verwijderen niet offline is, het offline halen eerst.</span><span class="sxs-lookup"><span data-stu-id="c3db7-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="c3db7-202">Volg de stappen in [offline zetten van een share](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="c3db7-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="c3db7-203">Als u wordt gevraagd om bevestiging in de **verwijderen** blade, accepteer de bevestiging en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c3db7-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="c3db7-204">De share wordt nu verwijderd en de **Shares** blade ziet u de bijgewerkte lijst met shares binnen de virtuele-matrix.</span><span class="sxs-lookup"><span data-stu-id="c3db7-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3db7-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3db7-205">Next steps</span></span>
<span data-ttu-id="c3db7-206">Meer informatie over hoe [klonen van een StorSimple-share](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="c3db7-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

