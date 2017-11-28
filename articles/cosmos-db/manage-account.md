---
title: Beheren van een Azure DB die Cosmos-account via Azure Portal | Microsoft Docs
description: "Informatie over het beheren van uw Azure DB die Cosmos-account via Azure Portal. Een handleiding voor het gebruik van de Azure Portal weergeven, kopiëren, verwijderen en toegang tot accounts vinden."
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
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="b8d6b-105">Het beheren van een Azure DB die Cosmos-account</span><span class="sxs-lookup"><span data-stu-id="b8d6b-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="b8d6b-106">Informatie over het globale consistentie instellen, in combinatie met sleutels en verwijderen van een Azure DB die Cosmos-account in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="b8d6b-107"><a id="consistency"></a>Azure Cosmos DB consistentie instellingen beheren</span><span class="sxs-lookup"><span data-stu-id="b8d6b-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="b8d6b-108">Het consistentieniveau van de juiste te selecteren, is afhankelijk van de semantiek van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="b8d6b-109">U moet vertrouwd raken met de beschikbare consistentieniveaus in Azure Cosmos DB door te lezen [consistentieniveaus gebruiken om te maximaliseren, beschikbaarheid en prestaties in Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="b8d6b-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="b8d6b-110">Azure Cosmos DB biedt consistentie, beschikbaarheid en prestaties garanties, op elk consistentieniveau beschikbaar voor het account van uw database.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="b8d6b-111">Configureren van uw databaseaccount met een sterke consistentie vereist dat uw gegevens beperkt aan één Azure-regio en niet algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="b8d6b-112">Anderzijds, de beperkte consistentieniveaus - gebonden veroudering, session of uiteindelijke inschakelen u een willekeurig aantal Azure-regio's koppelen aan uw databaseaccount.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="b8d6b-113">De volgende eenvoudige stappen ziet u hoe u selecteert het standaardniveau voor consistentie voor het account van uw database.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="b8d6b-114">De standaardconsistentie voor een Azure DB die Cosmos-account opgeven</span><span class="sxs-lookup"><span data-stu-id="b8d6b-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="b8d6b-115">In de [Azure-portal](https://portal.azure.com/), toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="b8d6b-116">Klik op de accountblade **consistentie standaard**.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="b8d6b-117">In de **standaard consistentie** blade, selecteer de nieuwe consistentieniveau en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="b8d6b-118">![Standaard consistentie sessie][5]</span><span class="sxs-lookup"><span data-stu-id="b8d6b-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="b8d6b-119"><a id="keys"></a>Weergeven, kopiëren en opnieuw genereren toegangstoetsen</span><span class="sxs-lookup"><span data-stu-id="b8d6b-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="b8d6b-120">Wanneer u een Azure DB die Cosmos-account maakt, genereert de service twee master toegangstoetsen die kunnen worden gebruikt voor verificatie wanneer het account voor Azure Cosmos DB wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="b8d6b-121">Dankzij twee toegangssleutels, kunt u opnieuw genereren van de sleutels zonder onderbreking naar uw Azure DB die Cosmos-account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="b8d6b-122">In de [Azure-portal](https://portal.azure.com/), toegang tot de **sleutels** blade vanuit het menu van de resource op de **Azure DB die Cosmos-account** blade weergeven, kopiëren en opnieuw genereren van de sneltoetsen die worden gebruikt voor toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Azure Portal schermafdruk is de blade sleutels](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="b8d6b-124">De **sleutels** blade bevat ook de primaire en secundaire verbindingsreeksen die kunnen worden gebruikt voor verbinding met uw account uit de [hulpprogramma voor gegevensmigratie](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="b8d6b-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="b8d6b-125">Alleen-lezen sleutels zijn ook beschikbaar in deze blade.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="b8d6b-126">Lees- en query's zijn alleen-lezen-bewerkingen tijdens maakt, verwijderen, en vervangt niet.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="b8d6b-127">Kopieer een toegangssleutel in de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b8d6b-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="b8d6b-128">Op de **sleutels** blade, klikt u op de **kopie** knop aan de rechterkant van de sleutel die u wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Bekijken en kopiëren van een toegangssleutel in de Azure-Portal blade sleutels](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="b8d6b-130">Toegangstoetsen genereren</span><span class="sxs-lookup"><span data-stu-id="b8d6b-130">Regenerate access keys</span></span>
<span data-ttu-id="b8d6b-131">Aan uw account voor Azure Cosmos DB regelmatig om te voorkomen dat uw verbindingen beter te beveiligen, moet u de toegangssleutels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="b8d6b-132">Twee toegangssleutels zijn zodat u verbindingen met de Azure DB die Cosmos-account met behulp van één toegangssleutel terwijl u de toegangssleutel opnieuw genereert onderhouden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="b8d6b-133">Is van invloed op alle toepassingen die afhankelijk van de huidige sleutel zijn opnieuw genereren van uw toegangssleutels.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="b8d6b-134">Alle clients die gebruikmaken van de toegangssleutel voor toegang tot de Azure DB die Cosmos-account moeten worden bijgewerkt om de nieuwe sleutel te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="b8d6b-135">Als u toepassingen of cloudservices met de Azure DB die Cosmos-account hebt, wordt de verbinding verbroken als u opnieuw sleutels genereert, tenzij u uw sleutels rouleert.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="b8d6b-136">De volgende stappen wordt beschreven hoe die zijn betrokken bij het implementeren van uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="b8d6b-137">De toegangssleutel in uw toepassingscode om te verwijzen naar de secundaire toegangssleutel van het Azure DB die Cosmos-account bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="b8d6b-138">Opnieuw genereren van de primaire toegangssleutel voor uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="b8d6b-139">In de [Azure Portal](https://portal.azure.com/), toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="b8d6b-140">In de **Azure Cosmos-DB Account** blade, klikt u op **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="b8d6b-141">Op de **sleutels** blade, klik op de knop opnieuw genereren en klik vervolgens op **Ok** om te bevestigen dat u wilt een nieuwe sleutel te genereren.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="b8d6b-142">![Toegangstoetsen genereren](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="b8d6b-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="b8d6b-143">Nadat u hebt gecontroleerd dat de nieuwe sleutel beschikbaar voor gebruik (ongeveer 5 minuten na het opnieuw genereren is), worden de toegangssleutel in uw toepassingscode om te verwijzen naar de nieuwe primaire toegangssleutel bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="b8d6b-144">Genereer de secundaire toegangssleutel opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-144">Regenerate the secondary access key.</span></span>
   
    ![Toegangstoetsen genereren](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="b8d6b-146">Het kan enkele minuten duren voordat een zojuist gegenereerde sleutel kan worden gebruikt voor toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="b8d6b-147">De verbindingsreeks ophalen</span><span class="sxs-lookup"><span data-stu-id="b8d6b-147">Get the  connection string</span></span>
<span data-ttu-id="b8d6b-148">Voor het ophalen van de verbindingsreeks, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="b8d6b-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="b8d6b-149">In de [Azure-portal](https://portal.azure.com), toegang tot uw Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="b8d6b-150">Klik in het menu resource **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="b8d6b-151">Klik op de **kopie** naast de **primaire verbindingsreeks** of **secundaire verbindingsreeks** vak.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="b8d6b-152">Als u de verbindingsreeks in de [hulpprogramma voor migratie van Azure Cosmos DB Database](import-data.md), naam van de database toevoegen aan het einde van de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="b8d6b-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="b8d6b-154"><a id="delete"></a>Een Azure DB die Cosmos-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="b8d6b-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="b8d6b-155">Als u wilt verwijderen een Cosmos-DB Azure-account van de Azure Portal die u niet langer gebruikt, met de rechtermuisknop op de accountnaam en klik op **account verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Het verwijderen van een Azure DB die Cosmos-account in de Azure Portal](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="b8d6b-157">In de [Azure-portal](https://portal.azure.com/), toegang tot de Azure DB die Cosmos-account dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="b8d6b-158">Op de **Azure Cosmos DB account** blade met de rechtermuisknop op het account en klik vervolgens op **Account verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="b8d6b-159">Typ de naam van de Azure DB die Cosmos om te bevestigen dat u wilt verwijderen van het account op de blade resulterende bevestiging.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="b8d6b-160">Klik op de **verwijderen** knop.</span><span class="sxs-lookup"><span data-stu-id="b8d6b-160">Click the **Delete** button.</span></span>

![Het verwijderen van een Azure DB die Cosmos-account in de Azure Portal](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="b8d6b-162"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8d6b-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="b8d6b-163">Meer informatie over hoe [aan de slag met uw account voor Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="b8d6b-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
