---
title: aaaManage access control-records in StorSimple | Microsoft Docs
description: Hierin wordt beschreven hoe toouse toegangsbeheer (ACRs) toodetermine welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen registreert.
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="43148-103">Hallo StorSimple Manager-service toomanage access control records gebruiken</span><span class="sxs-lookup"><span data-stu-id="43148-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="43148-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="43148-104">Overview</span></span>
<span data-ttu-id="43148-105">Access control-records (ACRs) kunnen u toospecify welke hosts verbinding van volume tooa op Hallo StorSimple-apparaat maken kunnen.</span><span class="sxs-lookup"><span data-stu-id="43148-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="43148-106">ACRs tooa specifieke volume worden ingesteld en bevatten Hallo iSCSI gekwalificeerde namen (IQN's de gebruikershandleiding) Hallo-hosts.</span><span class="sxs-lookup"><span data-stu-id="43148-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="43148-107">Wanneer een host tooconnect tooa volume probeert, controleert Hallo apparaat Hallo ACR die zijn gekoppeld aan dat volume voor Hallo IQN naam en als er een overeenkomst is, wordt hello verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="43148-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="43148-108">access control-records in Hallo Hallo **configuratie** sectie van de blade van uw StorSimple Device Manager-service alle Hallo access control records weergeven met Hallo IQN's de gebruikershandleiding Hallo hosts overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="43148-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="43148-109">Deze zelfstudie wordt uitgelegd hoe Hallo algemene ACR-gerelateerde taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="43148-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="43148-110">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="43148-110">Add an access control record</span></span>
* <span data-ttu-id="43148-111">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="43148-111">Edit an access control record</span></span>
* <span data-ttu-id="43148-112">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="43148-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="43148-113">Bij het toewijzen van een volume van de tooa ACR zorgt dat Hallo volume niet gelijktijdig toegankelijk is door meer dan één niet-geclusterde host omdat dit kan Hallo volume beschadigd.</span><span class="sxs-lookup"><span data-stu-id="43148-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="43148-114">Wanneer u een ACR verwijdert van een volume, zorg er dan voor dat die Hallo bijbehorende host geen toegang heeft tot Hallo volume omdat Hallo verwijderen tot een onderbreking van de alleen-lezen leiden kan.</span><span class="sxs-lookup"><span data-stu-id="43148-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="43148-115">Hallo IQN ophalen</span><span class="sxs-lookup"><span data-stu-id="43148-115">Get hello IQN</span></span>

<span data-ttu-id="43148-116">Hallo te volgen stappen tooget Hallo IQN van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="43148-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="43148-117">Een record voor toegangscontrole toevoegen</span><span class="sxs-lookup"><span data-stu-id="43148-117">Add an access control record</span></span>
<span data-ttu-id="43148-118">Gebruik van Hallo **configuratie** sectie in Hallo StorSimple Apparaatbeheer service blade tooadd ACRs.</span><span class="sxs-lookup"><span data-stu-id="43148-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="43148-119">U koppelt doorgaans één ACR met één volume.</span><span class="sxs-lookup"><span data-stu-id="43148-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="43148-120">Volgende stappen tooadd een ACR Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43148-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="43148-121">een ACR tooadd</span><span class="sxs-lookup"><span data-stu-id="43148-121">tooadd an ACR</span></span>

1. <span data-ttu-id="43148-122">Ga tooyour Apparaatbeheer StorSimple-service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="43148-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="43148-123">In Hallo **Access control records** blade, klikt u op **+ toevoegen ACR**.</span><span class="sxs-lookup"><span data-stu-id="43148-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="43148-125">In Hallo **ACR toevoegen** blade Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="43148-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="43148-126">Geef een naam voor uw ACR.</span><span class="sxs-lookup"><span data-stu-id="43148-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="43148-127">Hallo IQN naam van uw Windows Server-host onder **iSCSI-Initiator Name (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="43148-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="43148-128">Klik op **toevoegen** toocreate hello ACR.</span><span class="sxs-lookup"><span data-stu-id="43148-128">Click **Add** toocreate hello ACR.</span></span>

        ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="43148-130">Hallo toegevoegde dat ACR in tabelvorm aanbieding Hallo van ACRs wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="43148-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Klik op toevoegen ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="43148-132">Een record voor toegangscontrole bewerken</span><span class="sxs-lookup"><span data-stu-id="43148-132">Edit an access control record</span></span>
<span data-ttu-id="43148-133">Gebruik van Hallo **configuratie** sectie in Hallo StorSimple Apparaatbeheer service blade tooedit ACRs.</span><span class="sxs-lookup"><span data-stu-id="43148-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="43148-134">Het is raadzaam dat u alleen deze ACRs die zich momenteel niet in gebruik.</span><span class="sxs-lookup"><span data-stu-id="43148-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="43148-135">tooedit een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.</span><span class="sxs-lookup"><span data-stu-id="43148-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="43148-136">Volgende stappen tooedit een ACR Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43148-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="43148-137">een record voor toegangscontrole tooedit</span><span class="sxs-lookup"><span data-stu-id="43148-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="43148-138">Ga tooyour Apparaatbeheer StorSimple-service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="43148-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="43148-140">In tabelvorm aanbieding Hallo Hallo access control records, op en selecteer Hallo ACR gewenste toomodify.</span><span class="sxs-lookup"><span data-stu-id="43148-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="43148-142">In Hallo **record voor toegangscontrole bewerken** blade, Geef een andere IQN bijbehorende tooanother host.</span><span class="sxs-lookup"><span data-stu-id="43148-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="43148-144">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="43148-144">Click **Save**.</span></span> <span data-ttu-id="43148-145">Klik op **Ja** als u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="43148-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Access control records bewerken](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="43148-147">U wordt gewaarschuwd wanneer Hallo ACR wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="43148-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="43148-148">in de lijst in tabelvorm Hallo werkt ook tooreflect Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="43148-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="43148-149">Een record voor toegangscontrole verwijderen</span><span class="sxs-lookup"><span data-stu-id="43148-149">Delete an access control record</span></span>
<span data-ttu-id="43148-150">Gebruik van Hallo **configuratie** sectie in Hallo StorSimple Apparaatbeheer service blade toodelete ACRs.</span><span class="sxs-lookup"><span data-stu-id="43148-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="43148-151">U kunt alleen deze ACRs die zich momenteel niet in gebruik verwijderen.</span><span class="sxs-lookup"><span data-stu-id="43148-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="43148-152">toodelete een ACR die zijn gekoppeld aan een volume dat wordt gebruikt, u moet eerst Hallo volume offline halen.</span><span class="sxs-lookup"><span data-stu-id="43148-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="43148-153">Volgende stappen toodelete een record voor toegangscontrole Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="43148-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="43148-154">een record voor toegangscontrole toodelete</span><span class="sxs-lookup"><span data-stu-id="43148-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="43148-155">Ga tooyour Apparaatbeheer StorSimple-service, dubbelklikt u op Hallo servicenaam en klik vervolgens in Hallo **configuratie** sectie, klikt u op **Access control records**.</span><span class="sxs-lookup"><span data-stu-id="43148-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="43148-157">In tabelvorm aanbieding Hallo Hallo access control records, op en selecteer Hallo ACR gewenste toodelete.</span><span class="sxs-lookup"><span data-stu-id="43148-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="43148-159">Met de rechtermuisknop op tooinvoke Hallo contextmenu en selecteer **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="43148-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="43148-161">Als u wordt gevraagd om bevestiging, Hallo informatie bekijken en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="43148-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="43148-163">U wordt gewaarschuwd wanneer Hallo verwijdering is voltooid.</span><span class="sxs-lookup"><span data-stu-id="43148-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="43148-164">Hallo in tabelvorm aanbieding is bijgewerkte tooreflect Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="43148-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Ga tooaccess records beheren](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="43148-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43148-166">Next steps</span></span>
* <span data-ttu-id="43148-167">Meer informatie over [StorSimple-volumes beheren](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="43148-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="43148-168">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="43148-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

