---
title: Access control records in StorSimple beheren | Microsoft Docs
description: Beschrijft hoe access control-records (ACRs) gebruiken om te bepalen welke hosts kunnen verbinding maken met een volume op het StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="4d3d0-103">De StorSimple Manager-service gebruiken om de access control records beheren</span><span class="sxs-lookup"><span data-stu-id="4d3d0-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="4d3d0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4d3d0-104">Overview</span></span>
<span data-ttu-id="4d3d0-105">Access control-records (ACRs) kunnen u opgeven welke hosts kunnen verbinding maken met een volume op het StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="4d3d0-106">ACRs zijn ingesteld op een bepaald volume en de iSCSI-gekwalificeerde namen bevatten (IQN's de gebruikershandleiding) van de hosts.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="4d3d0-107">Wanneer een host probeert verbinding maken met een volume bevindt, controleert het apparaat de ACR die zijn gekoppeld aan dat volume voor de naam IQN en als er een overeenkomst, klikt u vervolgens de verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="4d3d0-108">Het toegangsbeheer sectie registreert op de **configureren** pagina wordt weergegeven voor alle access control records met de bijbehorende IQN's de gebruikershandleiding van de hosts.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="4d3d0-109">Deze zelfstudie wordt uitgelegd hoe de volgende algemene ACR-gerelateerde taken:</span><span class="sxs-lookup"><span data-stu-id="4d3d0-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="4d3d0-110">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-110">Add an access control record</span></span> 
* <span data-ttu-id="4d3d0-111">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="4d3d0-111">Edit an access control record</span></span> 
* <span data-ttu-id="4d3d0-112">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="4d3d0-113">Wanneer u een ACR toewijst aan een volume, ervoor te zorgen dat het volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan het volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="4d3d0-114">Wanneer u een ACR verwijdert van een volume, zorg dat de bijbehorende host geen toegang heeft tot het volume omdat de verwijdering tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="4d3d0-115">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-115">Add an access control record</span></span>
<span data-ttu-id="4d3d0-116">Gebruik van de StorSimple Manager-service **configureren** pagina ACRs toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="4d3d0-117">U koppelt doorgaans één ACR met één volume.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="4d3d0-118">Voer de volgende stappen uit om toe te voegen een ACR.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="4d3d0-119">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-119">To add an access control record</span></span>
1. <span data-ttu-id="4d3d0-120">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik op de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="4d3d0-121">In de lijst in tabelvorm onder **Access control records**, supply een **naam** voor uw ACR.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="4d3d0-122">Geef de naam van het IQN van uw Windows-host onder **iSCSI-initiatornaam**.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="4d3d0-123">Als u het IQN van uw Windows Server-host, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="4d3d0-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="4d3d0-124">Start de Microsoft iSCSI-initiator op uw Windows-host.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="4d3d0-125">Selecteer en kopieer in het venster **Eigenschappen iSCSI-initiator** op het tabblad **Configuratie** de tekenreeks in het veld **Naam van initiator**.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="4d3d0-126">Plak deze tekenreeks in de **iSCSI-initiatornaam** op de tabel ACRs in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="4d3d0-127">Klik op **opslaan** de zojuist gemaakte ACR opslaan.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="4d3d0-128">In de lijst in tabelvorm worden bijgewerkt naar aanleiding van deze toevoeging.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="4d3d0-129">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="4d3d0-129">Edit an access control record</span></span>
<span data-ttu-id="4d3d0-130">U gebruikt de **configureren** pagina in de klassieke Azure portal ACRs bewerken.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d3d0-131">U kunt alleen deze ACRs die zich momenteel niet in gebruik wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4d3d0-132">Als u wilt bewerken een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, moet u het volume eerst offline halen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="4d3d0-133">De volgende stappen uitvoeren om te bewerken van een ACR.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="4d3d0-134">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="4d3d0-134">To edit an access control record</span></span>
1. <span data-ttu-id="4d3d0-135">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik op de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="4d3d0-136">In de lijst in tabelvorm van de access control-records de muisaanwijzer op de ACR die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="4d3d0-137">Geef een nieuwe naam en/of IQN voor de ACR.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="4d3d0-138">Klik op **opslaan** de gewijzigde ACR opslaan.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="4d3d0-139">In de lijst in tabelvorm worden bijgewerkt om deze wijziging weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="4d3d0-140">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-140">Delete an access control record</span></span>
<span data-ttu-id="4d3d0-141">U gebruikt de **configureren** pagina in de klassieke Azure portal ACRs verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d3d0-142">U kunt alleen deze ACRs die zich momenteel niet in gebruik verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="4d3d0-143">Als u wilt verwijderen een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, moet u het volume eerst offline halen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="4d3d0-144">Voer de volgende stappen uit als u wilt verwijderen van een record voor toegangscontrole.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="4d3d0-145">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-145">To delete an access control record</span></span>
1. <span data-ttu-id="4d3d0-146">Selecteer uw service op de startpagina van de service, dubbelklikt u op de servicenaam en klik op de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="4d3d0-147">In de lijst in tabelvorm access control records (ACRs), de muisaanwijzer op de ACR die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="4d3d0-148">Een verwijderpictogram (**x**) wordt weergegeven in de rechterkolom extreme voor de ACR die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="4d3d0-149">Klik op de **x** pictogram de ACR verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="4d3d0-150">Wanneer u om bevestiging gevraagd, klikt u op **Ja** om door te gaan met het verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="4d3d0-151">In de lijst in tabelvorm worden bijgewerkt naar aanleiding van de verwijdering.</span><span class="sxs-lookup"><span data-stu-id="4d3d0-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d3d0-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d3d0-152">Next steps</span></span>
* <span data-ttu-id="4d3d0-153">Meer informatie over [StorSimple-volumes beheren](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="4d3d0-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="4d3d0-154">Meer informatie over [de StorSimple Manager-service gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4d3d0-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

