---
title: een Azure DB die Cosmos-account via Azure Portal Hallo aaaManage | Microsoft Docs
description: "Meer informatie over hoe toomanage uw Cosmos Azure DB account via hello Azure-Portal. Een handleiding voor het gebruik van hello Azure Portal tooview, kopiëren, verwijderen en toegang tot accounts vinden."
keywords: Azure-Portal, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="64359-105">Hoe toomanage een Cosmos-DB Azure-account</span><span class="sxs-lookup"><span data-stu-id="64359-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="64359-106">Meer informatie over hoe tooset globale consistentie, in combinatie met sleutels en verwijderen van een Azure DB die Cosmos-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="64359-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="64359-107"><a id="consistency"></a>Azure Cosmos DB consistentie instellingen beheren</span><span class="sxs-lookup"><span data-stu-id="64359-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="64359-108">Hallo rechts consistentieniveau selecteren, is afhankelijk van Hallo semantiek van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="64359-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="64359-109">U moet vertrouwd raken met Hallo beschikbaar consistentieniveaus in Azure Cosmos DB door te lezen [met behulp van de consistentie niveaus toomaximize beschikbaarheid en prestaties in Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="64359-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="64359-110">Azure Cosmos DB biedt consistentie, beschikbaarheid en prestaties garanties, op elk consistentieniveau beschikbaar voor het account van uw database.</span><span class="sxs-lookup"><span data-stu-id="64359-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="64359-111">Configureren van uw databaseaccount met een sterke consistentie vereist dat uw gegevens beperkt tooa één Azure-regio is en niet algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="64359-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="64359-112">Op Hallo daarentegen, beperkte consistentieniveaus - gebonden veroudering, session of uiteindelijke inschakelen Hallo tooassociate u een willekeurig aantal Azure-regio's aan uw databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="64359-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="64359-113">Hallo eenvoudige stappen ziet u hoe tooselect Hallo consistentie standaardniveau voor het account van uw database.</span><span class="sxs-lookup"><span data-stu-id="64359-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="64359-114">toospecify hello standaardconsistentie voor een Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="64359-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="64359-115">In Hallo [Azure-portal](https://portal.azure.com/), toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="64359-116">Klik op Hallo accountblade **consistentie standaard**.</span><span class="sxs-lookup"><span data-stu-id="64359-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="64359-117">In Hallo **standaard consistentie** blade, selecteer Hallo nieuwe consistentieniveau en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="64359-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="64359-118">![Standaard consistentie sessie][5]</span><span class="sxs-lookup"><span data-stu-id="64359-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="64359-119"><a id="keys"></a>Weergeven, kopiëren en opnieuw genereren toegangstoetsen</span><span class="sxs-lookup"><span data-stu-id="64359-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="64359-120">Wanneer u een Azure DB die Cosmos-account maakt, genereert Hallo service twee master toegangstoetsen die kunnen worden gebruikt voor verificatie wanneer hello Azure DB die Cosmos-account wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="64359-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="64359-121">Dankzij twee toegangssleutels, kunnen Azure Cosmos DB tooregenerate Hallo sleutels met niets onderbreking tooyour Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="64359-122">In Hallo [Azure-portal](https://portal.azure.com/), toegang Hallo **sleutels** blade vanuit Hallo resource-menu op Hallo **Azure Cosmos DB account** blade tooview, kopiëren en opnieuw genereren Hallo toegangstoetsen die gebruikte tooaccess zijn uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Azure Portal schermafdruk is de blade sleutels](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="64359-124">Hallo **sleutels** blade bevat primaire en secundaire verbindingsreeksen die gebruikt tooconnect tooyour worden kunnen rekening van Hallo [hulpprogramma voor gegevensmigratie](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="64359-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="64359-125">Alleen-lezen sleutels zijn ook beschikbaar in deze blade.</span><span class="sxs-lookup"><span data-stu-id="64359-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="64359-126">Lees- en query's zijn alleen-lezen-bewerkingen tijdens maakt, verwijderen, en vervangt niet.</span><span class="sxs-lookup"><span data-stu-id="64359-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="64359-127">Kopieer een toegangssleutel in hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="64359-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="64359-128">Op Hallo **sleutels** blade, klikt u op Hallo **kopie** knop toohello rechts van de sleutel Hallo gewenste toocopy.</span><span class="sxs-lookup"><span data-stu-id="64359-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Bekijken en kopiëren van een toegangssleutel in hello Azure-Portal blade sleutels](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="64359-130">Toegangstoetsen genereren</span><span class="sxs-lookup"><span data-stu-id="64359-130">Regenerate access keys</span></span>
<span data-ttu-id="64359-131">Hallo sleutels tooyour Azure Cosmos DB toegangsaccount moet u regelmatig toohelp beter te beveiligen uw verbindingen.</span><span class="sxs-lookup"><span data-stu-id="64359-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="64359-132">Twee toegangssleutels toegewezen tooenable u toomaintain verbindingen toohello Azure DB die Cosmos-account met behulp van één toegangssleutel terwijl u genereren Hallo andere toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="64359-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="64359-133">Opnieuw genereren van uw toegangssleutels is van invloed op alle toepassingen die afhankelijk van de huidige sleutel Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="64359-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="64359-134">Alle clients die gebruikmaken van Hallo sleutel tooaccess hello Azure Cosmos DB toegangsaccount moet bijgewerkte toouse Hallo nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="64359-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="64359-135">Als u toepassingen of cloudservices met behulp van hello Azure DB die Cosmos-account hebt, wordt u Hallo verbinding verbroken als u opnieuw sleutels genereert, tenzij u uw sleutels rouleert.</span><span class="sxs-lookup"><span data-stu-id="64359-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="64359-136">Hallo volgende stappen wordt uitgelegd Hallo-proces voor het implementeren van uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="64359-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="64359-137">Hallo-toegangssleutel in uw toepassing code tooreference Hallo secundaire toegangssleutel van hello Azure DB die Cosmos-account bijwerken.</span><span class="sxs-lookup"><span data-stu-id="64359-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="64359-138">Opnieuw genereren Hallo primaire toegangssleutel voor uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="64359-139">In Hallo [Azure Portal](https://portal.azure.com/), toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="64359-140">In Hallo **Azure Cosmos-DB Account** blade, klikt u op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="64359-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="64359-141">Op Hallo **sleutels** blade, klikt u op Hallo opnieuw genereren en klik vervolgens op **Ok** tooconfirm dat u wilt dat een nieuwe sleutel toogenerate.</span><span class="sxs-lookup"><span data-stu-id="64359-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="64359-142">![Toegangstoetsen genereren](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="64359-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="64359-143">Zodra u hebt gecontroleerd dat nieuwe Hallo-sleutel is beschikbaar voor gebruik bijwerken (ongeveer 5 minuten na het opnieuw genereren), Hallo toegangssleutel in uw toepassing code tooreference Hallo nieuwe primaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="64359-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="64359-144">Genereer de secundaire toegangssleutel Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="64359-144">Regenerate hello secondary access key.</span></span>
   
    ![Toegangstoetsen genereren](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="64359-146">Het kan enkele minuten duren voordat een zojuist gegenereerde sleutel gebruikt tooaccess worden kan uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="64359-147">Hallo-verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="64359-147">Get hello  connection string</span></span>
<span data-ttu-id="64359-148">tooretrieve uw verbinding tekenreeks, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="64359-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="64359-149">In Hallo [Azure-portal](https://portal.azure.com), toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="64359-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="64359-150">Hallo resource menu en klik op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="64359-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="64359-151">Klik op Hallo **kopie** knop volgende toohello **primaire verbindingsreeks** of **secundaire verbindingsreeks** vak.</span><span class="sxs-lookup"><span data-stu-id="64359-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="64359-152">Als u de verbindingsreeks Hallo in Hallo [hulpprogramma voor migratie van Azure Cosmos DB Database](import-data.md), Hallo database naam toohello einde van de verbindingsreeks Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="64359-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="64359-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="64359-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="64359-154"><a id="delete"></a>Een Azure DB die Cosmos-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="64359-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="64359-155">een Cosmos Azure DB tooremove account uit hello Azure-Portal die u niet langer gebruikt, klik met de rechtermuisknop Hallo accountnaam, en klik op **account verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="64359-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Hoe een Cosmos Azure DB toodelete account in Azure Portal Hallo](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="64359-157">In Hallo [Azure-portal](https://portal.azure.com/), toegang tot hello Azure Cosmos DB account u wilt dat toodelete.</span><span class="sxs-lookup"><span data-stu-id="64359-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="64359-158">Op Hallo **Azure Cosmos DB account** blade met de rechtermuisknop op het Hallo-account en klik vervolgens op **Account verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="64359-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="64359-159">Typ op de resulterende bevestiging blade Hallo hello Azure Cosmos DB account naam tooconfirm gewenste toodelete Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="64359-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="64359-160">Klik op Hallo **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="64359-160">Click hello **Delete** button.</span></span>

![Hoe een Cosmos Azure DB toodelete account in Azure Portal Hallo](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="64359-162"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64359-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="64359-163">Meer informatie over hoe te[aan de slag met uw account voor Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="64359-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
