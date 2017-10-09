---
title: aaaManage DNS-record sets en records met Azure DNS | Microsoft Docs
description: Azure DNS biedt Hallo mogelijkheid toomanage DNS-record wordt ingesteld en registreert bij het hosten van uw domein.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="5962a-103">DNS-records en recordsets beheren met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5962a-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5962a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5962a-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="5962a-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5962a-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="5962a-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5962a-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="5962a-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5962a-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="5962a-108">Dit artikel laat zien hoe Hallo toomanage recordsets en records voor uw DNS-zone met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5962a-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="5962a-109">Het is belangrijk toounderstand Hallo verschil tussen de DNS-recordsets en afzonderlijke DNS-records.</span><span class="sxs-lookup"><span data-stu-id="5962a-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="5962a-110">Een recordset is een verzameling van records in een zone die Hallo dezelfde naam en zijn Hallo hetzelfde type hebben.</span><span class="sxs-lookup"><span data-stu-id="5962a-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="5962a-111">Zie voor meer informatie [maken DNS-recordsets en records met behulp van Azure-portal Hallo](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5962a-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="5962a-112">Een nieuwe recordset en record maken</span><span class="sxs-lookup"><span data-stu-id="5962a-112">Create a new record set and record</span></span>

<span data-ttu-id="5962a-113">een record in hello Azure-portal toocreate Zie [maken DNS-records met behulp van Azure-portal Hallo](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5962a-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="5962a-114">Een recordset weergeven</span><span class="sxs-lookup"><span data-stu-id="5962a-114">View a record set</span></span>

1. <span data-ttu-id="5962a-115">Ga in de Azure-portal hello, toohello **DNS-zone** blade.</span><span class="sxs-lookup"><span data-stu-id="5962a-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="5962a-116">Hallo-Recordset zoekt en selecteert u deze.</span><span class="sxs-lookup"><span data-stu-id="5962a-116">Search for hello record set and select it.</span></span> <span data-ttu-id="5962a-117">Hiermee opent u de eigenschappen van Hallo Recordset.</span><span class="sxs-lookup"><span data-stu-id="5962a-117">This opens hello record set properties.</span></span>

    ![Zoeken naar een Recordset](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="5962a-119">Voeg een nieuwe record tooa-Recordset</span><span class="sxs-lookup"><span data-stu-id="5962a-119">Add a new record tooa record set</span></span>

<span data-ttu-id="5962a-120">U kunt toevoegen, too20 records tooany Recordset.</span><span class="sxs-lookup"><span data-stu-id="5962a-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="5962a-121">Een recordset mag niet twee identieke records.</span><span class="sxs-lookup"><span data-stu-id="5962a-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="5962a-122">Lege recordsets (met nul records) kunnen worden gemaakt, maar worden niet weergegeven op Hallo Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="5962a-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="5962a-123">Recordsets van het type CNAME kunnen maximaal één record bevatten.</span><span class="sxs-lookup"><span data-stu-id="5962a-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="5962a-124">Op Hallo **eigenschappen van de recordset** blade voor uw DNS-zone, klikt u op Hallo-record dat u tooadd een record wilt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5962a-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Selecteer een Recordset](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="5962a-126">Geef Hallo Recordset eigenschappen Hallo velden.</span><span class="sxs-lookup"><span data-stu-id="5962a-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Een record toevoegen](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="5962a-128">Klik op **opslaan** op Hallo Hallo blade toosave bovenaan uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="5962a-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="5962a-129">Sluit de blade Hallo.</span><span class="sxs-lookup"><span data-stu-id="5962a-129">Then close hello blade.</span></span>
4. <span data-ttu-id="5962a-130">In de hoek hello ziet u dat Hallo-record wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5962a-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Recordset opslaan](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="5962a-132">Nadat het Hallo-record is opgeslagen, waarden op Hallo Hallo **DNS-zone** blade Hallo nieuwe record wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5962a-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="5962a-133">Een record bijwerken</span><span class="sxs-lookup"><span data-stu-id="5962a-133">Update a record</span></span>

<span data-ttu-id="5962a-134">Hallo-velden die u kunt bijwerken wanneer u een record in een bestaande recordset bijwerkt, zijn afhankelijk van Hallo type record waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="5962a-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="5962a-135">Op Hallo **eigenschappen van de recordset** blade voor uw recordset en zoeken naar Hallo record.</span><span class="sxs-lookup"><span data-stu-id="5962a-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="5962a-136">Hallo record wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5962a-136">Modify hello record.</span></span> <span data-ttu-id="5962a-137">Wanneer u een record wijzigt, kunt u de beschikbare instellingen voor de record Hallo Hallo kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5962a-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="5962a-138">Hallo in Hallo voorbeeld te volgen, **IP-adres** veld is geselecteerd en Hallo IP-adres wordt Hallo proces wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5962a-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Een record wijzigen](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="5962a-140">Klik op **opslaan** op Hallo Hallo blade toosave bovenaan uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="5962a-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="5962a-141">In de rechterbovenhoek Hallo ziet u Hallo melding dat Hallo-record is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5962a-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Recordset opgeslagen](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="5962a-143">Nadat het Hallo-record is opgeslagen, Hallo waarden voor Hallo record moet worden ingesteld op Hallo **DNS-zone** blade Hallo bijgewerkt record bevatten.</span><span class="sxs-lookup"><span data-stu-id="5962a-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="5962a-144">Een record verwijderen uit een Recordset</span><span class="sxs-lookup"><span data-stu-id="5962a-144">Remove a record from a record set</span></span>

<span data-ttu-id="5962a-145">U kunt hello Azure portal tooremove records uit een recordset.</span><span class="sxs-lookup"><span data-stu-id="5962a-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="5962a-146">Houd er rekening mee dat Hallo laatste record van een recordset niet Hallo Recordset verwijderen worden.</span><span class="sxs-lookup"><span data-stu-id="5962a-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="5962a-147">Op Hallo **eigenschappen van de recordset** blade voor uw recordset en zoeken naar Hallo record.</span><span class="sxs-lookup"><span data-stu-id="5962a-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="5962a-148">Klik op Hallo-record dat u wilt dat tooremove.</span><span class="sxs-lookup"><span data-stu-id="5962a-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="5962a-149">Selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5962a-149">Then select **Remove**.</span></span>

    ![Een record verwijderen](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="5962a-151">Klik op **opslaan** op Hallo Hallo blade toosave bovenaan uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="5962a-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="5962a-152">Nadat het Hallo-record is verwijderd, de waarden voor de record Hallo op Hallo Hallo **DNS-zone** blade nieuwe Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5962a-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="5962a-153"><a name="delete"></a>Een recordset verwijderen</span><span class="sxs-lookup"><span data-stu-id="5962a-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="5962a-154">Op Hallo **eigenschappen van de recordset** blade voor uw recordset en klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5962a-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Een recordset verwijderen](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="5962a-156">Er verschijnt een bericht waarin wordt gevraagd als u wilt dat toodelete Hallo-Recordset.</span><span class="sxs-lookup"><span data-stu-id="5962a-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="5962a-157">Controleer of Hallo naam komt overeen met Hallo record ingesteld dat u toodelete wilt en klik vervolgens op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="5962a-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="5962a-158">Op Hallo **DNS-zone** blade controleren Hallo recordset is niet meer zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="5962a-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="5962a-159">Werken met NS en SOA-records</span><span class="sxs-lookup"><span data-stu-id="5962a-159">Work with NS and SOA records</span></span>

<span data-ttu-id="5962a-160">NS en SOA-records die automatisch worden gemaakt, worden anders worden beheerd vanuit andere recordtypen.</span><span class="sxs-lookup"><span data-stu-id="5962a-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="5962a-161">SOA-records wijzigen</span><span class="sxs-lookup"><span data-stu-id="5962a-161">Modify SOA records</span></span>

<span data-ttu-id="5962a-162">U kunt toevoegen of verwijderen van records uit Hallo automatisch gemaakt SOA-record is ingesteld in het toppunt Hallo zone (naam = ' @ ').</span><span class="sxs-lookup"><span data-stu-id="5962a-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="5962a-163">Echter kunt u een van de parameters Hallo binnen Hallo SOA-record (met uitzondering van de "Host") en de TTL van de recordset Hallo.</span><span class="sxs-lookup"><span data-stu-id="5962a-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="5962a-164">NS-records in het toppunt zone Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="5962a-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="5962a-165">Hallo NS-recordset in het toppunt Hallo zone wordt automatisch gemaakt met elke DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="5962a-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="5962a-166">Het bevat Hallo-namen van hello Azure DNS-naam servers toegewezen toohello zone.</span><span class="sxs-lookup"><span data-stu-id="5962a-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="5962a-167">U kunt de naam van de aanvullende servers toothis NS-recordset, toosupport CO domeinen met meer dan één DNS-provider host toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5962a-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="5962a-168">U kunt ook wijzigen Hallo TTL en metagegevens voor deze recordset.</span><span class="sxs-lookup"><span data-stu-id="5962a-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="5962a-169">U kan echter verwijderen of wijzigen Hallo vooraf ingestelde Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="5962a-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="5962a-170">Houd er rekening mee dat dit alleen toohello NS recordset in het toppunt zone Hallo geldt.</span><span class="sxs-lookup"><span data-stu-id="5962a-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="5962a-171">Andere NS recordsets in de zone (als gebruikte toodelegate onderliggende zones) kunnen worden gewijzigd zonder beperking.</span><span class="sxs-lookup"><span data-stu-id="5962a-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="5962a-172">SOA- of NS recordsets verwijderen</span><span class="sxs-lookup"><span data-stu-id="5962a-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="5962a-173">U kunt geen Hallo SOA- en NS-recordsets in het toppunt Hallo zone verwijderen (naam = ' @ ') die automatisch worden gemaakt wanneer het Hallo-zone wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5962a-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="5962a-174">Ze worden automatisch verwijderd wanneer u Hallo zone verwijdert.</span><span class="sxs-lookup"><span data-stu-id="5962a-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5962a-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5962a-175">Next steps</span></span>

* <span data-ttu-id="5962a-176">Zie voor meer informatie over Azure DNS Hallo [Azure DNS-overzicht](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5962a-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="5962a-177">Zie voor meer informatie over het automatiseren van DNS [maken van DNS-zones en -recordsets met .NET SDK Hallo](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5962a-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="5962a-178">Zie voor meer informatie over de reverse DNS-records [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5962a-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
