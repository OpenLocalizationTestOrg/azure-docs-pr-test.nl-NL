---
title: Beheren van DNS-recordsets en records met Azure DNS | Microsoft Docs
description: Azure DNS biedt de mogelijkheid voor het beheren van DNS-recordsets en records bij het hosten van uw domein.
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
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="9580f-103">Beheren van DNS-records en recordsets met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9580f-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9580f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9580f-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="9580f-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9580f-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="9580f-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9580f-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="9580f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9580f-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="9580f-108">In dit artikel laat zien hoe recordsets en records voor de DNS-zone beheren met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9580f-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="9580f-109">Het is belangrijk om het verschil tussen de DNS-recordsets en afzonderlijke DNS-records.</span><span class="sxs-lookup"><span data-stu-id="9580f-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="9580f-110">Een recordset is een verzameling van records in een zone die dezelfde naam hebben en hetzelfde type zijn.</span><span class="sxs-lookup"><span data-stu-id="9580f-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="9580f-111">Zie voor meer informatie [maken DNS-recordsets en records met behulp van de Azure-portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9580f-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="9580f-112">Een nieuwe recordset en record maken</span><span class="sxs-lookup"><span data-stu-id="9580f-112">Create a new record set and record</span></span>

<span data-ttu-id="9580f-113">Zie het maken van een record in de Azure-portal [maken DNS-records met behulp van de Azure-portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9580f-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="9580f-114">Een recordset weergeven</span><span class="sxs-lookup"><span data-stu-id="9580f-114">View a record set</span></span>

1. <span data-ttu-id="9580f-115">In de Azure portal, gaat u naar de **DNS-zone** blade.</span><span class="sxs-lookup"><span data-stu-id="9580f-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="9580f-116">De recordset zoekt en selecteert u deze.</span><span class="sxs-lookup"><span data-stu-id="9580f-116">Search for the record set and select it.</span></span> <span data-ttu-id="9580f-117">Hiermee opent u de eigenschappen van de recordset.</span><span class="sxs-lookup"><span data-stu-id="9580f-117">This opens the record set properties.</span></span>

    ![Zoeken naar een Recordset](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="9580f-119">Een nieuwe record toevoegen aan een Recordset</span><span class="sxs-lookup"><span data-stu-id="9580f-119">Add a new record to a record set</span></span>

<span data-ttu-id="9580f-120">U kunt maximaal 20 records toevoegen aan een recordset.</span><span class="sxs-lookup"><span data-stu-id="9580f-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="9580f-121">Een recordset mag niet twee identieke records.</span><span class="sxs-lookup"><span data-stu-id="9580f-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="9580f-122">Lege recordsets (met nul records) kunnen worden gemaakt, maar worden niet weergegeven op de Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="9580f-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="9580f-123">Recordsets van het type CNAME kunnen maximaal één record bevatten.</span><span class="sxs-lookup"><span data-stu-id="9580f-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="9580f-124">Op de **eigenschappen van de recordset** blade voor uw DNS-zone, klikt u op de recordset die u wilt toevoegen van een record.</span><span class="sxs-lookup"><span data-stu-id="9580f-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Selecteer een Recordset](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="9580f-126">Geef dat de eigenschappen van de recordset door in de velden te vullen.</span><span class="sxs-lookup"><span data-stu-id="9580f-126">Specify the record set properties by filling in the fields.</span></span>

    ![Een record toevoegen](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="9580f-128">Klik op **opslaan** boven aan de blade als u uw instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="9580f-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="9580f-129">Sluit de blade.</span><span class="sxs-lookup"><span data-stu-id="9580f-129">Then close the blade.</span></span>
4. <span data-ttu-id="9580f-130">In de hoek ziet u dat de record wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9580f-130">In the corner, you will see that the record is saving.</span></span>

    ![Recordset opslaan](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="9580f-132">Nadat de record is opgeslagen, de waarden op de **DNS-zone** blade geeft de nieuwe record.</span><span class="sxs-lookup"><span data-stu-id="9580f-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="9580f-133">Een record bijwerken</span><span class="sxs-lookup"><span data-stu-id="9580f-133">Update a record</span></span>

<span data-ttu-id="9580f-134">De velden die u kunt bijwerken wanneer u een record in een bestaande recordset bijwerkt, zijn afhankelijk van het type record waarmee u werkt.</span><span class="sxs-lookup"><span data-stu-id="9580f-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="9580f-135">Op de **eigenschappen van de recordset** blade voor uw recordset en zoekt u de record.</span><span class="sxs-lookup"><span data-stu-id="9580f-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="9580f-136">De record wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9580f-136">Modify the record.</span></span> <span data-ttu-id="9580f-137">Wanneer u een record wijzigt, kunt u de beschikbare instellingen voor de record.</span><span class="sxs-lookup"><span data-stu-id="9580f-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="9580f-138">In het volgende voorbeeld wordt de **IP-adres** hebt ingeschakeld, en het IP-adres is bezig te worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="9580f-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Een record wijzigen](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="9580f-140">Klik op **opslaan** boven aan de blade als u uw instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="9580f-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="9580f-141">In de rechterbovenhoek ziet u de melding dat de record is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9580f-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Recordset opgeslagen](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="9580f-143">Nadat de record is opgeslagen, de waarden voor de record moet worden ingesteld op de **DNS-zone** blade geeft de bijgewerkte record.</span><span class="sxs-lookup"><span data-stu-id="9580f-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="9580f-144">Een record verwijderen uit een Recordset</span><span class="sxs-lookup"><span data-stu-id="9580f-144">Remove a record from a record set</span></span>

<span data-ttu-id="9580f-145">U kunt de Azure-portal gebruiken om records te verwijderen van een recordset.</span><span class="sxs-lookup"><span data-stu-id="9580f-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="9580f-146">Houd er rekening mee dat de laatste record van een recordset niet de recordset verwijderen worden.</span><span class="sxs-lookup"><span data-stu-id="9580f-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="9580f-147">Op de **eigenschappen van de recordset** blade voor uw recordset en zoekt u de record.</span><span class="sxs-lookup"><span data-stu-id="9580f-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="9580f-148">Klik op de record die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9580f-148">Click the record that you want to remove.</span></span> <span data-ttu-id="9580f-149">Selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9580f-149">Then select **Remove**.</span></span>

    ![Een record verwijderen](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="9580f-151">Klik op **opslaan** boven aan de blade als u uw instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="9580f-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="9580f-152">Nadat de record is verwijderd, de waarden voor de record op de **DNS-zone** blade geeft de verwijzing wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9580f-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="9580f-153"><a name="delete"></a>Een recordset verwijderen</span><span class="sxs-lookup"><span data-stu-id="9580f-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="9580f-154">Op de **eigenschappen van de recordset** blade voor uw recordset en klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9580f-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Een recordset verwijderen](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="9580f-156">Er verschijnt een bericht waarin wordt gevraagd als u wilt verwijderen van de recordset.</span><span class="sxs-lookup"><span data-stu-id="9580f-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="9580f-157">Controleren of de naam overeenkomt met de recordset die u wilt verwijderen en klik vervolgens op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="9580f-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="9580f-158">Op de **DNS-zone** blade, Controleer of de recordset is niet meer zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="9580f-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="9580f-159">Werken met NS en SOA-records</span><span class="sxs-lookup"><span data-stu-id="9580f-159">Work with NS and SOA records</span></span>

<span data-ttu-id="9580f-160">NS en SOA-records die automatisch worden gemaakt, worden anders worden beheerd vanuit andere recordtypen.</span><span class="sxs-lookup"><span data-stu-id="9580f-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="9580f-161">SOA-records wijzigen</span><span class="sxs-lookup"><span data-stu-id="9580f-161">Modify SOA records</span></span>

<span data-ttu-id="9580f-162">U kunt toevoegen of verwijderen van records uit de automatisch gemaakte SOA-record is ingesteld in het toppunt van de zone (naam = ' @ ').</span><span class="sxs-lookup"><span data-stu-id="9580f-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="9580f-163">Echter, kunt u een van de parameters binnen de SOA-record (met uitzondering van de "Host") en de TTL-waarde van de recordset.</span><span class="sxs-lookup"><span data-stu-id="9580f-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="9580f-164">NS-records in het toppunt van de zone wijzigen</span><span class="sxs-lookup"><span data-stu-id="9580f-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="9580f-165">De NS-recordset in het toppunt van de zone wordt automatisch gemaakt met elke DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="9580f-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="9580f-166">Het bevat de namen van de Azure DNS-naamservers toegewezen aan de zone.</span><span class="sxs-lookup"><span data-stu-id="9580f-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="9580f-167">U kunt extra naam ingesteld van servers aan deze NS-record, ter ondersteuning van collega hosting domeinen met meer dan één DNS-provider toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9580f-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="9580f-168">U kunt ook de TTL-waarde en de metagegevens voor deze recordset wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9580f-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="9580f-169">U kan echter verwijderen of wijzigen van de vooraf ingestelde Azure DNS-naamservers.</span><span class="sxs-lookup"><span data-stu-id="9580f-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="9580f-170">Houd er rekening mee dat dit alleen voor de NS-recordset in het toppunt van de zone geldt.</span><span class="sxs-lookup"><span data-stu-id="9580f-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="9580f-171">Andere NS-recordsets in de zone (zoals gebruikt voor het delegeren van onderliggende zones) kunnen worden gewijzigd zonder beperking.</span><span class="sxs-lookup"><span data-stu-id="9580f-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="9580f-172">SOA- of NS recordsets verwijderen</span><span class="sxs-lookup"><span data-stu-id="9580f-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="9580f-173">U kunt de SOA niet verwijderen en NS-record wordt ingesteld in het toppunt van de zone (naam = ' @ ') die automatisch worden gemaakt wanneer de zone wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9580f-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="9580f-174">Ze worden automatisch verwijderd wanneer u de zone verwijdert.</span><span class="sxs-lookup"><span data-stu-id="9580f-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9580f-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9580f-175">Next steps</span></span>

* <span data-ttu-id="9580f-176">Zie voor meer informatie over Azure DNS de [Azure DNS-overzicht](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9580f-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="9580f-177">Zie voor meer informatie over het automatiseren van DNS [maken van DNS-zones en -recordsets met de .NET SDK](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9580f-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="9580f-178">Zie voor meer informatie over de reverse DNS-records [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9580f-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
