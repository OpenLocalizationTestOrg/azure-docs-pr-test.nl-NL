---
title: aaaManage access control-records voor virtuele StorSimple-matrix | Microsoft Docs
description: Hierin wordt beschreven hoe toomanage toegangsbeheer (ACRs) toodetermine welke hosts verbinding van tooa volume op Hallo virtuele StorSimple-matrix maken kunnen registreert.
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
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="f89d3-103">Gebruik StorSimple Apparaatbeheer toomanage access control-records voor virtuele StorSimple-matrix</span><span class="sxs-lookup"><span data-stu-id="f89d3-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f89d3-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f89d3-104">Overview</span></span>

<span data-ttu-id="f89d3-105">Access control-records (ACRs) kunnen u toospecify welke hosts verbinding van tooa volume op Hallo virtuele StorSimple-matrix (ook wel bekend als Hallo StorSimple on-premises virtuele apparaat maken kunnen).</span><span class="sxs-lookup"><span data-stu-id="f89d3-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="f89d3-106">ACRs tooa specifieke volume worden ingesteld en bevatten Hallo iSCSI gekwalificeerde namen (IQN's de gebruikershandleiding) Hallo-hosts.</span><span class="sxs-lookup"><span data-stu-id="f89d3-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="f89d3-107">Wanneer een host tooconnect tooa volume probeert, Hallo apparaat Hallo ACR die zijn gekoppeld aan dat volume voor de naam van de IQN Hallo controleert en als er een overeenkomst, klikt u vervolgens Hallo-verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="f89d3-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="f89d3-108">Hallo **Access control records** blade binnen Hallo **configuratie** sectie van uw service Apparaatbeheer vindt u alle Hallo access control records Hello IQN's de gebruikershandleiding Hallo hosts overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="f89d3-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Access control records beheren](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="f89d3-110">Deze zelfstudie wordt uitgelegd hoe Hallo algemene ACR-gerelateerde taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="f89d3-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="f89d3-111">Hallo IQN ophalen</span><span class="sxs-lookup"><span data-stu-id="f89d3-111">Get hello IQN</span></span>
* <span data-ttu-id="f89d3-112">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="f89d3-112">Add an access control record</span></span>
* <span data-ttu-id="f89d3-113">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="f89d3-113">Edit an access control record</span></span>
* <span data-ttu-id="f89d3-114">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="f89d3-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="f89d3-115">Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="f89d3-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="f89d3-116">Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="f89d3-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="f89d3-117">Hallo IQN ophalen</span><span class="sxs-lookup"><span data-stu-id="f89d3-117">Get hello IQN</span></span>

<span data-ttu-id="f89d3-118">Hallo te volgen stappen tooget Hallo IQN van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f89d3-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="f89d3-119">Een ACR toevoegen</span><span class="sxs-lookup"><span data-stu-id="f89d3-119">Add an ACR</span></span>

<span data-ttu-id="f89d3-120">U gebruikt **Access control records** blade binnen Hallo **configuratie** gedeelte van uw StorSimple-apparaat Manager service tooadd ACRs.</span><span class="sxs-lookup"><span data-stu-id="f89d3-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="f89d3-121">Normaal gesproken koppelt u een ACR aan één volume.</span><span class="sxs-lookup"><span data-stu-id="f89d3-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="f89d3-122">Voor informatie over het koppelen van een ACR met een volume gaat te[toevoegen van een volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="f89d3-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f89d3-123">Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="f89d3-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="f89d3-124">Volgende stappen tooadd een ACR Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f89d3-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="f89d3-125">een ACR tooadd</span><span class="sxs-lookup"><span data-stu-id="f89d3-125">tooadd an ACR</span></span>

1. <span data-ttu-id="f89d3-126">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="f89d3-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="f89d3-127">In Hallo **Access control records** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f89d3-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="f89d3-128">In Hallo **ACR toevoegen** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f89d3-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="f89d3-129">Geef een **naam** voor uw ACR op.</span><span class="sxs-lookup"><span data-stu-id="f89d3-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="f89d3-130">Onder **iSCSI-initiatornaam**, Hallo IQN naam van uw Windows-host.</span><span class="sxs-lookup"><span data-stu-id="f89d3-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="f89d3-131">tooget hello IQN van Windows Server-host Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f89d3-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="f89d3-132">Start Hallo Microsoft iSCSI-initiator op uw Windows-host.</span><span class="sxs-lookup"><span data-stu-id="f89d3-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="f89d3-133">Hallo iSCSI-Initiator venster Eigenschappen op Hallo **configuratie** tabblad Selecteer en kopieer Hallo tekenreeks van Hallo **initiatornaam** veld.</span><span class="sxs-lookup"><span data-stu-id="f89d3-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="f89d3-134">Plak deze tekenreeks in Hallo **IQN** veld Hallo **ACR toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="f89d3-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="f89d3-135">Klik op **toevoegen** tooadd hello ACR.</span><span class="sxs-lookup"><span data-stu-id="f89d3-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Access control records toevoegen](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="f89d3-137">in de lijst in tabelvorm Hallo bijgewerkte tooreflect is deze aanvulling.</span><span class="sxs-lookup"><span data-stu-id="f89d3-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="f89d3-138">Een ACR bewerken</span><span class="sxs-lookup"><span data-stu-id="f89d3-138">Edit an ACR</span></span>

<span data-ttu-id="f89d3-139">Gebruik van Hallo **Access control records** blade binnen Hallo **configuratie** gedeelte van uw service Apparaatbeheer in Azure portal tooedit ACRs Hallo.</span><span class="sxs-lookup"><span data-stu-id="f89d3-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="f89d3-140">U moet een ACR die momenteel in gebruik is niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f89d3-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="f89d3-141">tooedit een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.</span><span class="sxs-lookup"><span data-stu-id="f89d3-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="f89d3-142">Volgende stappen tooedit een ACR Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f89d3-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="f89d3-143">een ACR tooedit</span><span class="sxs-lookup"><span data-stu-id="f89d3-143">tooedit an ACR</span></span>

1. <span data-ttu-id="f89d3-144">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="f89d3-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="f89d3-145">In Hallo **Access control records** blade uit in tabelvorm aanbieding Hallo Hallo access control records, dubbelklikt u op Hallo ACR gewenste toomodify.</span><span class="sxs-lookup"><span data-stu-id="f89d3-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="f89d3-146">In Hallo **bewerken access control records** blade Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f89d3-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="f89d3-147">Hallo IQN voor Hallo ACR op te geven.</span><span class="sxs-lookup"><span data-stu-id="f89d3-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="f89d3-148">Klik op **opslaan** bovenaan Hallo Hallo blade toosave hello ACR gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f89d3-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="f89d3-149">Hallo volgende bevestigingsbericht wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="f89d3-149">You see hello following confirmation message:</span></span>
   
        ![Access control records bewerken](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="f89d3-151">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="f89d3-151">Delete an access control record</span></span>

<span data-ttu-id="f89d3-152">Gebruik van Hallo **configuratie** pagina in Azure portal toodelete ACRs Hallo.</span><span class="sxs-lookup"><span data-stu-id="f89d3-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="f89d3-153">U moet een ACR die momenteel in gebruik is niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f89d3-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="f89d3-154">toodelete een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.</span><span class="sxs-lookup"><span data-stu-id="f89d3-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="f89d3-155">Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="f89d3-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="f89d3-156">Volgende stappen toodelete een record voor toegangscontrole Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f89d3-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="f89d3-157">een record voor toegangscontrole toodelete</span><span class="sxs-lookup"><span data-stu-id="f89d3-157">toodelete an access control record</span></span>

1. <span data-ttu-id="f89d3-158">Op de startpagina van Hallo-service, selecteer uw service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="f89d3-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="f89d3-159">In Hallo **Access control records** blade uit in tabelvorm aanbieding Hallo Hallo access control records, dubbelklikt u op Hallo ACR gewenste toodelete.</span><span class="sxs-lookup"><span data-stu-id="f89d3-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="f89d3-160">Klik op Hallo bewerken access control records blade **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="f89d3-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![ACRS verwijderen](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="f89d3-162">Wanneer u om bevestiging gevraagd, klikt u op **verwijderen** toocontinue met Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f89d3-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="f89d3-163">Hallo in tabelvorm aanbieding is bijgewerkte tooreflect Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f89d3-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Waarschuwingsbericht](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="f89d3-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f89d3-165">Next steps</span></span>

* <span data-ttu-id="f89d3-166">Meer informatie over [volumes toevoegen en configureren van ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="f89d3-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

