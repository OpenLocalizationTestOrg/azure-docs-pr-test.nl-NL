---
title: Access control records beheren voor virtuele StorSimple-matrix | Microsoft Docs
description: Beschrijft hoe access control records (ACRs) om te bepalen welke hosts kunnen verbinding maken met een volume op de virtuele StorSimple-matrix te beheren.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="df314-103">Het StorSimple-Apparaatbeheer gebruiken voor het beheren van access control records voor virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="df314-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="df314-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="df314-104">Overview</span></span>

<span data-ttu-id="df314-105">Access control-records (ACRs) kunnen u opgeven welke hosts kunnen verbinding maken met een volume op de virtuele StorSimple-matrix (ook wel bekend als de StorSimple on-premises virtuele apparaat).</span><span class="sxs-lookup"><span data-stu-id="df314-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="df314-106">ACRs zijn ingesteld op een bepaald volume en de iSCSI-gekwalificeerde namen bevatten (IQN's de gebruikershandleiding) van de hosts.</span><span class="sxs-lookup"><span data-stu-id="df314-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="df314-107">Wanneer een host probeert verbinding maken met een volume, het apparaat de ACR die zijn gekoppeld aan dat volume voor de naam IQN controleert en als er een overeenkomst, klikt u vervolgens de verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="df314-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="df314-108">De **Access control records** blade binnen de **configuratie** sectie van uw service Apparaatbeheer vindt u alle access control records met de bijbehorende IQN's de gebruikershandleiding van de hosts.</span><span class="sxs-lookup"><span data-stu-id="df314-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![Access control records beheren](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="df314-110">Deze zelfstudie wordt uitgelegd hoe de volgende algemene ACR-gerelateerde taken:</span><span class="sxs-lookup"><span data-stu-id="df314-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="df314-111">Het IQN ophalen</span><span class="sxs-lookup"><span data-stu-id="df314-111">Get the IQN</span></span>
* <span data-ttu-id="df314-112">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="df314-112">Add an access control record</span></span>
* <span data-ttu-id="df314-113">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="df314-113">Edit an access control record</span></span>
* <span data-ttu-id="df314-114">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="df314-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="df314-115">Wanneer u een ACR toewijst aan een volume, ervoor te zorgen dat het volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan het volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="df314-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="df314-116">Wanneer u een ACR verwijdert van een volume, zorg dat de bijbehorende host geen toegang heeft tot het volume omdat de verwijdering tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="df314-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="df314-117">Het IQN ophalen</span><span class="sxs-lookup"><span data-stu-id="df314-117">Get the IQN</span></span>

<span data-ttu-id="df314-118">De volgende stappen uitvoeren om te het IQN ophalen van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="df314-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="df314-119">Een ACR toevoegen</span><span class="sxs-lookup"><span data-stu-id="df314-119">Add an ACR</span></span>

<span data-ttu-id="df314-120">U gebruikt **Access control records** blade binnen de **configuratie** gedeelte van uw StorSimple-apparaat Manager service ACRs toevoegen.</span><span class="sxs-lookup"><span data-stu-id="df314-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="df314-121">Normaal gesproken koppelt u een ACR aan één volume.</span><span class="sxs-lookup"><span data-stu-id="df314-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="df314-122">Ga voor informatie over het koppelen van een ACR met een volume naar [toevoegen van een volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="df314-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="df314-123">Wanneer u een ACR toewijst aan een volume, ervoor te zorgen dat het volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan het volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="df314-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="df314-124">Voer de volgende stappen uit om toe te voegen een ACR.</span><span class="sxs-lookup"><span data-stu-id="df314-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="df314-125">Een ACR toevoegen</span><span class="sxs-lookup"><span data-stu-id="df314-125">To add an ACR</span></span>

1. <span data-ttu-id="df314-126">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik vervolgens in de **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="df314-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="df314-127">In de **Access control records** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="df314-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="df314-128">In de **ACR toevoegen** blade het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="df314-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="df314-129">Geef een **naam** voor uw ACR op.</span><span class="sxs-lookup"><span data-stu-id="df314-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="df314-130">Onder **iSCSI-initiatornaam**, geef de naam van het IQN van uw Windows-host.</span><span class="sxs-lookup"><span data-stu-id="df314-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="df314-131">Als u het IQN van uw Windows Server-host, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="df314-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="df314-132">Start de Microsoft iSCSI-initiator op uw Windows-host.</span><span class="sxs-lookup"><span data-stu-id="df314-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="df314-133">In het venster van de iSCSI-Initiator-eigenschappen, op de **configuratie** tabblad Selecteer en kopieer de tekenreeks van de **initiatornaam** veld.</span><span class="sxs-lookup"><span data-stu-id="df314-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="df314-134">Plak deze tekenreeks in de **IQN** veld in de **ACR toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="df314-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="df314-135">Klik op **toevoegen** de ACR toevoegen.</span><span class="sxs-lookup"><span data-stu-id="df314-135">Click **Add** to add the ACR.</span></span>  
   
        ![Access control records toevoegen](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="df314-137">In de lijst in tabelvorm is bijgewerkt, zodat deze toevoeging.</span><span class="sxs-lookup"><span data-stu-id="df314-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="df314-138">Een ACR bewerken</span><span class="sxs-lookup"><span data-stu-id="df314-138">Edit an ACR</span></span>

<span data-ttu-id="df314-139">U gebruikt de **Access control records** blade binnen de **configuratie** gedeelte van uw service Apparaatbeheer in de Azure portal ACRs bewerken.</span><span class="sxs-lookup"><span data-stu-id="df314-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="df314-140">U moet een ACR die momenteel in gebruik is niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="df314-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="df314-141">Als u wilt bewerken een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, moet u het volume eerst offline halen.</span><span class="sxs-lookup"><span data-stu-id="df314-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="df314-142">De volgende stappen uitvoeren om te bewerken van een ACR.</span><span class="sxs-lookup"><span data-stu-id="df314-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="df314-143">Een ACR bewerken</span><span class="sxs-lookup"><span data-stu-id="df314-143">To edit an ACR</span></span>

1. <span data-ttu-id="df314-144">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik vervolgens in de **configuratie** sectie **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="df314-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="df314-145">In de **Access control records** blade in de lijst in tabelvorm van de access control records, dubbelklikt u op de ACR die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="df314-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="df314-146">In de **bewerken access control records** blade het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="df314-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="df314-147">Het IQN opgeven voor de ACR.</span><span class="sxs-lookup"><span data-stu-id="df314-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="df314-148">Klik op **opslaan** boven aan de blade om op te slaan van het gewijzigde ACR.</span><span class="sxs-lookup"><span data-stu-id="df314-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="df314-149">U ziet het volgende bevestigingsbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="df314-149">You see the following confirmation message:</span></span>
   
        ![Access control records bewerken](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="df314-151">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="df314-151">Delete an access control record</span></span>

<span data-ttu-id="df314-152">U gebruikt de **configuratie** pagina in de Azure portal ACRs verwijderen.</span><span class="sxs-lookup"><span data-stu-id="df314-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="df314-153">U moet een ACR die momenteel in gebruik is niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="df314-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="df314-154">Als u wilt verwijderen een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, moet u het volume eerst offline halen.</span><span class="sxs-lookup"><span data-stu-id="df314-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="df314-155">Wanneer u een ACR verwijdert van een volume, zorg dat de bijbehorende host geen toegang heeft tot het volume omdat de verwijdering tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="df314-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="df314-156">Voer de volgende stappen uit als u wilt verwijderen van een record voor toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="df314-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="df314-157">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="df314-157">To delete an access control record</span></span>

1. <span data-ttu-id="df314-158">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik vervolgens in de **configuratie** sectie **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="df314-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="df314-159">In de **Access control records** blade in de lijst in tabelvorm van de access control records, dubbelklikt u op de ACR die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="df314-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="df314-160">Klik op de blade bewerken access control records **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="df314-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![ACRS verwijderen](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="df314-162">Wanneer u om bevestiging gevraagd, klikt u op **verwijderen** om door te gaan met het verwijderen.</span><span class="sxs-lookup"><span data-stu-id="df314-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="df314-163">In de lijst in tabelvorm is bijgewerkt met de verwijdering.</span><span class="sxs-lookup"><span data-stu-id="df314-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![Waarschuwingsbericht](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="df314-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df314-165">Next steps</span></span>

* <span data-ttu-id="df314-166">Meer informatie over [volumes toevoegen en configureren van ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="df314-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

