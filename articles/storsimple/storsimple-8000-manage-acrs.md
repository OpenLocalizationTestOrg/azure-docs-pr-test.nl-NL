---
title: Access control records in StorSimple beheren | Microsoft Docs
description: Beschrijft hoe access control-records (ACRs) gebruiken om te bepalen welke hosts kunnen verbinding maken met een volume op het StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="44748-103">De StorSimple Manager-service gebruiken om de access control records beheren</span><span class="sxs-lookup"><span data-stu-id="44748-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="44748-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="44748-104">Overview</span></span>
<span data-ttu-id="44748-105">Access control-records (ACRs) kunnen u opgeven welke hosts kunnen verbinding maken met een volume op het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="44748-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="44748-106">ACRs zijn ingesteld op een bepaald volume en de iSCSI-gekwalificeerde namen bevatten (IQN's de gebruikershandleiding) van de hosts.</span><span class="sxs-lookup"><span data-stu-id="44748-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="44748-107">Wanneer een host probeert verbinding maken met een volume bevindt, controleert het apparaat de ACR die zijn gekoppeld aan dat volume voor de naam IQN en als er een overeenkomst, klikt u vervolgens de verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="44748-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="44748-108">Het toegangsbeheer registreert in de **configuratie** sectie van de blade van uw StorSimple Device Manager-service alle access control records met de bijbehorende IQN's de gebruikershandleiding van de hosts weergeven.</span><span class="sxs-lookup"><span data-stu-id="44748-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="44748-109">Deze zelfstudie wordt uitgelegd hoe de volgende algemene ACR-gerelateerde taken:</span><span class="sxs-lookup"><span data-stu-id="44748-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="44748-110">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="44748-110">Add an access control record</span></span>
* <span data-ttu-id="44748-111">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="44748-111">Edit an access control record</span></span>
* <span data-ttu-id="44748-112">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="44748-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="44748-113">Wanneer u een ACR toewijst aan een volume, ervoor te zorgen dat het volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan het volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="44748-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="44748-114">Wanneer u een ACR verwijdert van een volume, zorg dat de bijbehorende host geen toegang heeft tot het volume omdat de verwijdering tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="44748-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="44748-115">Het IQN ophalen</span><span class="sxs-lookup"><span data-stu-id="44748-115">Get the IQN</span></span>

<span data-ttu-id="44748-116">De volgende stappen uitvoeren om te het IQN ophalen van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="44748-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="44748-117">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="44748-117">Add an access control record</span></span>
<span data-ttu-id="44748-118">U gebruikt de **configuratie** sectie in de blade van de service Manager voor StorSimple-apparaat ACRs toevoegen.</span><span class="sxs-lookup"><span data-stu-id="44748-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="44748-119">U koppelt doorgaans één ACR met één volume.</span><span class="sxs-lookup"><span data-stu-id="44748-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="44748-120">Voer de volgende stappen uit om toe te voegen een ACR.</span><span class="sxs-lookup"><span data-stu-id="44748-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="44748-121">Een ACR toevoegen</span><span class="sxs-lookup"><span data-stu-id="44748-121">To add an ACR</span></span>

1. <span data-ttu-id="44748-122">Ga naar uw StorSimple-apparaat Manager-service, dubbelklikt u op de servicenaam en klik vervolgens in de **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="44748-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="44748-123">In de **Access control records** blade, klikt u op **+ toevoegen ACR**.</span><span class="sxs-lookup"><span data-stu-id="44748-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="44748-125">In de **ACR toevoegen** blade, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="44748-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="44748-126">Geef een naam voor uw ACR.</span><span class="sxs-lookup"><span data-stu-id="44748-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="44748-127">Geef de naam van het IQN van uw Windows Server-host onder **iSCSI-Initiator Name (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="44748-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="44748-128">Klik op **toevoegen** de ACR maken.</span><span class="sxs-lookup"><span data-stu-id="44748-128">Click **Add** to create the ACR.</span></span>

        ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="44748-130">De toegevoegde ACR wordt weergegeven in de lijst in tabelvorm van ACRs.</span><span class="sxs-lookup"><span data-stu-id="44748-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="44748-132">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="44748-132">Edit an access control record</span></span>
<span data-ttu-id="44748-133">U gebruikt de **configuratie** sectie in de blade van de service Manager voor StorSimple-apparaat ACRs bewerken.</span><span class="sxs-lookup"><span data-stu-id="44748-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="44748-134">Het is raadzaam dat u alleen deze ACRs die zich momenteel niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="44748-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="44748-135">Als u wilt bewerken een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, moet u het volume eerst offline halen.</span><span class="sxs-lookup"><span data-stu-id="44748-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="44748-136">De volgende stappen uitvoeren om te bewerken van een ACR.</span><span class="sxs-lookup"><span data-stu-id="44748-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="44748-137">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="44748-137">To edit an access control record</span></span>
1.  <span data-ttu-id="44748-138">Ga naar uw StorSimple-apparaat Manager-service, dubbelklikt u op de servicenaam en klik vervolgens in de **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="44748-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Ga naar de access control-records](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="44748-140">Klik in de lijst in tabelvorm access control records en selecteert u de ACR die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44748-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="44748-142">In de **record voor toegangscontrole bewerken** blade, Geef een andere IQN overeenkomt met een andere host.</span><span class="sxs-lookup"><span data-stu-id="44748-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="44748-144">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="44748-144">Click **Save**.</span></span> <span data-ttu-id="44748-145">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="44748-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="44748-147">U wordt gewaarschuwd wanneer de ACR wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="44748-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="44748-148">De in tabelvorm aanbieding ook bijgewerkt zodat de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="44748-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="44748-149">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="44748-149">Delete an access control record</span></span>
<span data-ttu-id="44748-150">U gebruikt de **configuratie** sectie in de blade van de service Manager voor StorSimple-apparaat ACRs verwijderen.</span><span class="sxs-lookup"><span data-stu-id="44748-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="44748-151">U kunt alleen deze ACRs die zich momenteel niet in gebruik verwijderen.</span><span class="sxs-lookup"><span data-stu-id="44748-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="44748-152">Als u wilt verwijderen een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, moet u het volume eerst offline halen.</span><span class="sxs-lookup"><span data-stu-id="44748-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="44748-153">Voer de volgende stappen uit als u wilt verwijderen van een record voor toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="44748-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="44748-154">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="44748-154">To delete an access control record</span></span>
1.  <span data-ttu-id="44748-155">Ga naar uw StorSimple-apparaat Manager-service, dubbelklikt u op de servicenaam en klik vervolgens in de **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="44748-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Ga naar de access control-records](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="44748-157">Klik in de lijst in tabelvorm access control records en selecteert u de ACR die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="44748-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Ga naar de access control-records](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="44748-159">Klik met de rechtermuisknop het contextmenu aanroepen en selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="44748-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Ga naar de access control-records](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="44748-161">Als u wordt gevraagd om bevestiging, lees de informatie en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="44748-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Ga naar de access control-records](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="44748-163">U wordt gewaarschuwd wanneer de verwijdering is voltooid.</span><span class="sxs-lookup"><span data-stu-id="44748-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="44748-164">In de lijst in tabelvorm is bijgewerkt met de verwijdering.</span><span class="sxs-lookup"><span data-stu-id="44748-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Ga naar de access control-records](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="44748-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44748-166">Next steps</span></span>
* <span data-ttu-id="44748-167">Meer informatie over [StorSimple-volumes beheren](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="44748-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="44748-168">Meer informatie over [de StorSimple Manager-service gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="44748-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

