---
title: aaaManage access control-records in StorSimple | Microsoft Docs
description: Hierin wordt beschreven hoe toouse toegangsbeheer (ACRs) toodetermine welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen registreert.
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
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="1c6d0-103">Hallo StorSimple Manager-service toomanage access control records gebruiken</span><span class="sxs-lookup"><span data-stu-id="1c6d0-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="1c6d0-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1c6d0-104">Overview</span></span>
<span data-ttu-id="1c6d0-105">Access control-records (ACRs) kunnen u toospecify welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="1c6d0-106">ACRs tooa specifieke volume worden ingesteld en bevatten Hallo iSCSI gekwalificeerde namen (IQN's de gebruikershandleiding) Hallo-hosts.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="1c6d0-107">Wanneer een host tooconnect tooa volume probeert, controleert Hallo apparaat Hallo ACR die zijn gekoppeld aan dat volume voor Hallo IQN naam en als er een overeenkomst is, wordt hello verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="1c6d0-108">Hallo-toegangsbeheer registreert sectie op Hallo **configureren** pagina alle Hallo access control records wordt weergegeven met Hallo IQN's de gebruikershandleiding Hallo hosts overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="1c6d0-109">Deze zelfstudie wordt uitgelegd hoe Hallo algemene ACR-gerelateerde taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c6d0-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="1c6d0-110">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c6d0-110">Add an access control record</span></span> 
* <span data-ttu-id="1c6d0-111">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="1c6d0-111">Edit an access control record</span></span> 
* <span data-ttu-id="1c6d0-112">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="1c6d0-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="1c6d0-113">Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="1c6d0-114">Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="1c6d0-115">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c6d0-115">Add an access control record</span></span>
<span data-ttu-id="1c6d0-116">Gebruik van de StorSimple Manager-service Hallo **configureren** tooadd ACRs pagina.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="1c6d0-117">U koppelt doorgaans één ACR met één volume.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="1c6d0-118">Volgende stappen tooadd een ACR Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="1c6d0-119">een record voor toegangscontrole tooadd</span><span class="sxs-lookup"><span data-stu-id="1c6d0-119">tooadd an access control record</span></span>
1. <span data-ttu-id="1c6d0-120">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="1c6d0-121">In Hallo in tabelvorm aanbieding onder **Access control records**, supply een **naam** voor uw ACR.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="1c6d0-122">Hallo IQN naam van uw Windows-host onder **iSCSI-initiatornaam**.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="1c6d0-123">tooget hello IQN van Windows Server-host Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="1c6d0-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="1c6d0-124">Start Hallo Microsoft iSCSI-initiator op uw Windows-host.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="1c6d0-125">In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **configuratie** tabblad Selecteer en kopieer Hallo tekenreeks van Hallo **initiatornaam** veld.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="1c6d0-126">Plak deze tekenreeks in Hallo **iSCSI-initiatornaam** op Hallo ACRs tabel in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="1c6d0-127">Klik op **opslaan** toosave hello ACR van een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="1c6d0-128">Hallo in tabelvorm aanbieding zal worden bijgewerkte tooreflect deze toevoeging.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="1c6d0-129">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="1c6d0-129">Edit an access control record</span></span>
<span data-ttu-id="1c6d0-130">Gebruik van Hallo **configureren** pagina in hello Azure classic portal tooedit ACRs.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="1c6d0-131">U kunt alleen deze ACRs die zich momenteel niet in gebruik wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="1c6d0-132">tooedit een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="1c6d0-133">Volgende stappen tooedit een ACR Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="1c6d0-134">een record voor toegangscontrole tooedit</span><span class="sxs-lookup"><span data-stu-id="1c6d0-134">tooedit an access control record</span></span>
1. <span data-ttu-id="1c6d0-135">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="1c6d0-136">In tabelvorm aanbieding Hallo Hallo access control records, de muisaanwijzer op Hallo ACR gewenste toomodify.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="1c6d0-137">Geef een nieuwe naam en/of IQN voor Hallo ACR.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="1c6d0-138">Klik op **opslaan** toosave hello ACR gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="1c6d0-139">Hallo in tabelvorm aanbieding zal worden bijgewerkte tooreflect deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="1c6d0-140">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="1c6d0-140">Delete an access control record</span></span>
<span data-ttu-id="1c6d0-141">Gebruik van Hallo **configureren** pagina in hello Azure classic portal toodelete ACRs.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="1c6d0-142">U kunt alleen deze ACRs die zich momenteel niet in gebruik verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="1c6d0-143">toodelete een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="1c6d0-144">Volgende stappen toodelete een record voor toegangscontrole Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="1c6d0-145">een record voor toegangscontrole toodelete</span><span class="sxs-lookup"><span data-stu-id="1c6d0-145">toodelete an access control record</span></span>
1. <span data-ttu-id="1c6d0-146">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="1c6d0-147">In tabelvorm aanbieding Hallo van Hallo access control-records (ACRs), de muisaanwijzer op Hallo ACR gewenste toodelete.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="1c6d0-148">Een verwijderpictogram (**x**) wordt weergegeven in Hallo extreme rechterkolom voor Hallo ACR die u selecteert.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="1c6d0-149">Klik op Hallo **x** pictogram toodelete hello ACR.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="1c6d0-150">Wanneer u om bevestiging gevraagd, klikt u op **Ja** toocontinue met Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="1c6d0-151">in de lijst in tabelvorm Hallo worden bijgewerkte tooreflect Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1c6d0-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c6d0-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c6d0-152">Next steps</span></span>
* <span data-ttu-id="1c6d0-153">Meer informatie over [StorSimple-volumes beheren](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="1c6d0-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="1c6d0-154">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1c6d0-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

