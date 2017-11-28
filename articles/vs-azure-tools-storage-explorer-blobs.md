---
title: aaaManage Azure Blob Storage-resources met Opslagverkenner (Preview) | Microsoft Docs
description: Azure Blob-Containers en Blobs met Opslagverkenner (Preview) beheren
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="87ce4-103">Azure Blob Storage-resources beheren met Opslagverkenner (Preview)</span><span class="sxs-lookup"><span data-stu-id="87ce4-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="87ce4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="87ce4-104">Overview</span></span>
<span data-ttu-id="87ce4-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="87ce4-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="87ce4-106">U kunt Blob storage-tooexpose gegevens openbaar toohello world of toostore toepassingsgegevens privé.</span><span class="sxs-lookup"><span data-stu-id="87ce4-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="87ce4-107">In dit artikel leert u hoe toouse Opslagverkenner (Preview) toowork met blob-containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="87ce4-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87ce4-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="87ce4-108">Prerequisites</span></span>
<span data-ttu-id="87ce4-109">toocomplete hello stappen in dit artikel, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="87ce4-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="87ce4-110">Opslagverkenner (preview) downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="87ce4-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="87ce4-111">Verbinding maken met tooa Azure storage-account of -service</span><span class="sxs-lookup"><span data-stu-id="87ce4-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="87ce4-112">Een blob-container maken</span><span class="sxs-lookup"><span data-stu-id="87ce4-112">Create a blob container</span></span>
<span data-ttu-id="87ce4-113">Alle blobs moeten zich bevinden in een blob-container gewoon een logische groepering van blobs is.</span><span class="sxs-lookup"><span data-stu-id="87ce4-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="87ce4-114">Een account kan een onbeperkt aantal containers bevatten en elke container kan een onbeperkt aantal blobs opslaan.</span><span class="sxs-lookup"><span data-stu-id="87ce4-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="87ce4-115">Hallo volgende stappen laten zien hoe toocreate een blobcontainer in Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="87ce4-116">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-117">Vouw in het linkerdeelvenster Hallo Hallo storage-account waarin u wenst dat toocreate Hallo blob-container.</span><span class="sxs-lookup"><span data-stu-id="87ce4-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="87ce4-118">Met de rechtermuisknop op **Blob-Containers**, en selecteer in het contextmenu Hallo - **Blob-Container maken**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![Contextmenu van blob-containers maken][0]
4. <span data-ttu-id="87ce4-120">Een tekstvak wordt weergegeven onder Hallo **Blob-Containers** map.</span><span class="sxs-lookup"><span data-stu-id="87ce4-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="87ce4-121">Hallo-naam voor uw blob-container opgeven.</span><span class="sxs-lookup"><span data-stu-id="87ce4-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="87ce4-122">Zie Hallo [Container naamgevingsregels](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sectie voor een lijst van regels en beperkingen voor de naamgeving van blob-containers.</span><span class="sxs-lookup"><span data-stu-id="87ce4-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Tekstvak voor Blob-Containers maken][1]
5. <span data-ttu-id="87ce4-124">Druk op **Enter** wanneer klaar toocreate Hallo blob-container of **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="87ce4-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="87ce4-125">Zodra het Hallo blob-container heeft gemaakt, die wordt weergegeven onder Hallo **Blob-Containers** map voor Hallo storage-account geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="87ce4-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![BLOB-Container gemaakt][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="87ce4-127">Een blob-container inhoud weergeven</span><span class="sxs-lookup"><span data-stu-id="87ce4-127">View a blob container's contents</span></span>
<span data-ttu-id="87ce4-128">BLOB-containers bevatten blobs en -mappen (die ook blobs kunnen bevatten).</span><span class="sxs-lookup"><span data-stu-id="87ce4-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="87ce4-129">Hallo volgende stappen laten zien hoe tooview Hallo inhoud van een blobcontainer in Opslagverkenner (Preview):</span><span class="sxs-lookup"><span data-stu-id="87ce4-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="87ce4-130">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-131">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van tooview met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="87ce4-132">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-133">Met de rechtermuisknop op Hallo blob-container u tooview wilt en - selecteer in het contextmenu Hallo - **Open Editor voor Blob-Container**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="87ce4-134">U kunt ook Hallo blob-container gewenst tooview dubbelklikken.</span><span class="sxs-lookup"><span data-stu-id="87ce4-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Open blob-container editor contextmenu][19]
5. <span data-ttu-id="87ce4-136">hoofdvenster Hello wordt Hallo blob-container van inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="87ce4-136">hello main pane will display hello blob container's contents.</span></span>

   ![Editor voor BLOB-container][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="87ce4-138">Verwijderen van een blob-container</span><span class="sxs-lookup"><span data-stu-id="87ce4-138">Delete a blob container</span></span>
<span data-ttu-id="87ce4-139">BLOB-containers kunnen eenvoudig worden gemaakt en verwijderd indien nodig.</span><span class="sxs-lookup"><span data-stu-id="87ce4-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="87ce4-140">(toosee hoe toodelete afzonderlijke blobs, Raadpleeg de sectie toohello [beheren blobs in een blobcontainer](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="87ce4-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="87ce4-141">Hallo volgende stappen laten zien hoe toodelete een blobcontainer in Opslagverkenner (Preview):</span><span class="sxs-lookup"><span data-stu-id="87ce4-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="87ce4-142">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-143">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van tooview met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="87ce4-144">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-145">Met de rechtermuisknop op Hallo blob-container u toodelete wilt en - selecteer in het contextmenu Hallo - **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="87ce4-146">U kunt ook op drukken **verwijderen** toodelete Hallo geselecteerde blob-container.</span><span class="sxs-lookup"><span data-stu-id="87ce4-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![Contextmenu van blob-container verwijderen][4]
5. <span data-ttu-id="87ce4-148">Selecteer **Ja** toohello bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="87ce4-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![Verwijderen van blob-Container bevestigen][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="87ce4-150">Kopiëren van een blob-container</span><span class="sxs-lookup"><span data-stu-id="87ce4-150">Copy a blob container</span></span>
<span data-ttu-id="87ce4-151">Opslagverkenner (Preview) kunt u toocopy een blob-container toohello Klembord en plak BLOB-container in een ander opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="87ce4-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="87ce4-152">(toosee hoe toocopy afzonderlijke blobs, Raadpleeg de sectie toohello [beheren blobs in een blobcontainer](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="87ce4-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="87ce4-153">Hallo stappen laten zien hoe een blob-container uit één opslag toocopy tooanother account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="87ce4-154">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-155">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van toocopy met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="87ce4-156">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-157">Met de rechtermuisknop op Hallo blob-container u toocopy wilt en - selecteer in het contextmenu Hallo - **kopie Blob-Container**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Kopiëren van blob-container contextmenu][6]
5. <span data-ttu-id="87ce4-159">Met de rechtermuisknop op de gewenste Hallo 'target' storage-account waarin u wilt toopaste Hallo blob-container en - selecteer in het contextmenu Hallo - **Blob-Container plakken**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Menu context blob-container plakken][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="87ce4-161">Hallo SAS ophalen voor een blob-container</span><span class="sxs-lookup"><span data-stu-id="87ce4-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="87ce4-162">Een [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) tooresources gedelegeerde toegang in uw opslagaccount biedt.</span><span class="sxs-lookup"><span data-stu-id="87ce4-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="87ce4-163">Dit betekent dat u een client beperkte machtigingen tooobjects in uw opslagaccount gedurende een bepaalde tijd en met een opgegeven set machtigingen, zonder dat voor het delen van de toegangssleutels van uw account kunt verlenen.</span><span class="sxs-lookup"><span data-stu-id="87ce4-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="87ce4-164">Hallo volgende stappen laten zien hoe toocreate een SAS voor een blob-container:</span><span class="sxs-lookup"><span data-stu-id="87ce4-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="87ce4-165">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-166">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container waarvoor tooget een SAS met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="87ce4-167">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-168">Met de rechtermuisknop op de gewenste blobcontainer hello, en selecteer in het contextmenu Hallo - **Shared Access Signature ophalen**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![Contextmenu SAS ophalen][8]
5. <span data-ttu-id="87ce4-170">In Hallo **Shared Access Signature** dialoogvenster Hallo-beleid, de begin- en verloopdatum datums, de tijdzone opgeven en toegangsniveaus voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="87ce4-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![Ophalen van SAS-opties][9]
6. <span data-ttu-id="87ce4-172">Wanneer u klaar bent Hallo SAS-opties op te geven, selecteert u **maken**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="87ce4-173">Een tweede **Shared Access Signature** dialoogvenster dat een lijst met blob-container samen met de URL Hallo Hallo en kunt u tooaccess QueryStrings Hallo storage resource vervolgens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="87ce4-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="87ce4-174">Selecteer **kopie** volgende toohello-URL die u wenst dat toocopy toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="87ce4-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![SAS-URL's kopiëren][10]
8. <span data-ttu-id="87ce4-176">Als u klaar bent, selecteert u **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="87ce4-177">-Beleid beheren voor een blob-container</span><span class="sxs-lookup"><span data-stu-id="87ce4-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="87ce4-178">Hallo volgende stappen laten zien hoe toomanage (toevoegen en verwijderen) toegangsbeleid voor een blob-container:</span><span class="sxs-lookup"><span data-stu-id="87ce4-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="87ce4-179">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-180">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container waarvan u wilt dat toomanage toegangsbeleid met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="87ce4-181">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-182">Selecteer de gewenste blobcontainer Hallo, en selecteer in het contextmenu Hallo - **toegangsbeleid beheren**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Contextmenu Toegangsbeleid beheren][11]
5. <span data-ttu-id="87ce4-184">Hallo **toegangsbeleid** dialoogvenster vermeldt alle beleidsregels voor toegang al is gemaakt voor Hallo geselecteerde blob-container.</span><span class="sxs-lookup"><span data-stu-id="87ce4-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Opties voor toegangsbeleid][12]        
6. <span data-ttu-id="87ce4-186">Volg deze stappen, afhankelijk van Hallo toegang beleid beheertaak:</span><span class="sxs-lookup"><span data-stu-id="87ce4-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="87ce4-187">**Een nieuw toegangsbeleid toevoegen**: selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="87ce4-188">Zodra gegenereerd, Hallo **toegangsbeleid** dialoogvenster wordt weergegeven Hallo toegevoegde toegangsbeleid (met de standaardinstellingen).</span><span class="sxs-lookup"><span data-stu-id="87ce4-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="87ce4-189">**Een toegangsbeleid bewerken** - eventueel wijzigingen doorvoeren en selecteer **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="87ce4-190">**Verwijderen van een toegangsbeleid** : Selecteer **verwijderen** volgende toohello toegangsbeleid gewenste tooremove.</span><span class="sxs-lookup"><span data-stu-id="87ce4-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="87ce4-191">Hallo openbare toegangsniveau instellen voor een blob-container</span><span class="sxs-lookup"><span data-stu-id="87ce4-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="87ce4-192">Standaard elke blob-container te ingesteld 'Geen openbare toegang'.</span><span class="sxs-lookup"><span data-stu-id="87ce4-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="87ce4-193">Hallo volgende stappen laten zien hoe toospecify dat door een openbare toegang tot niveau voor een blob-container.</span><span class="sxs-lookup"><span data-stu-id="87ce4-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="87ce4-194">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-195">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container waarvan u wilt dat toomanage toegangsbeleid met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="87ce4-196">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-197">Selecteer de gewenste blobcontainer Hallo, en selecteer in het contextmenu Hallo - **ingesteld openbare toegangsniveau**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Openbare toegang niveau contextmenu instellen][13]
5. <span data-ttu-id="87ce4-199">In Hallo **ingesteld Container openbaar toegangsniveau** dialoogvenster u Hallo gewenst toegangsniveau kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="87ce4-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Opties voor openbare toegang niveau instellen][14]
6. <span data-ttu-id="87ce4-201">Selecteer **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="87ce4-202">Blobs in een blobcontainer beheren</span><span class="sxs-lookup"><span data-stu-id="87ce4-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="87ce4-203">Als u een blob-container hebt gemaakt, kunt u een blob-container toothat blob uploaden, downloaden van een blob tooyour lokale computer, opent u een blob op uw lokale computer en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="87ce4-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="87ce4-204">Hallo stappen laten zien hoe toomanage BLOB's (en mappen) Hallo binnen een blob-container.</span><span class="sxs-lookup"><span data-stu-id="87ce4-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="87ce4-205">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="87ce4-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="87ce4-206">Vouw in het linkerdeelvenster Hallo HALLO hallo blob-container wilt van toomanage met storage-account.</span><span class="sxs-lookup"><span data-stu-id="87ce4-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="87ce4-207">Vouw Hallo storage account **Blob-Containers**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="87ce4-208">Dubbelklik op Hallo gewenst tooview blob-container.</span><span class="sxs-lookup"><span data-stu-id="87ce4-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="87ce4-209">hoofdvenster Hello wordt Hallo blob-container van inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="87ce4-209">hello main pane will display hello blob container's contents.</span></span>

   ![Weergave blob-container][3]
6. <span data-ttu-id="87ce4-211">hoofdvenster Hello wordt Hallo blob-container van inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="87ce4-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="87ce4-212">Volg deze dat stappen, afhankelijk van de taak Hallo gewenste tooperform:</span><span class="sxs-lookup"><span data-stu-id="87ce4-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="87ce4-213">**Uploaden van bestanden tooa blob-container**</span><span class="sxs-lookup"><span data-stu-id="87ce4-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="87ce4-214">Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **bestanden uploaden** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="87ce4-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Menu bestanden uploaden][15]
     2. <span data-ttu-id="87ce4-216">In Hallo **bestanden uploaden** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **bestanden** tekstvak tooselect Hallo op die u wenst dat tooupload.</span><span class="sxs-lookup"><span data-stu-id="87ce4-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Opties voor bestanden uploaden][16]
     3. <span data-ttu-id="87ce4-218">Geef Hallo type **Blob-type**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="87ce4-219">Hallo artikel [aan de slag met Azure Blob storage met .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) uitgelegd Hallo verschillen tussen Hallo diverse typen van de blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="87ce4-220">Geef desgewenst een pad van de map waarnaar u de geselecteerde bestanden hello wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="87ce4-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="87ce4-221">Als de doelmap Hallo niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="87ce4-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="87ce4-222">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-222">Select **Upload**.</span></span>
   * <span data-ttu-id="87ce4-223">**Uploaden van een map tooa blob-container**</span><span class="sxs-lookup"><span data-stu-id="87ce4-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="87ce4-224">Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **map uploaden** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="87ce4-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu voor uploaden van map][17]
     2. <span data-ttu-id="87ce4-226">In Hallo **map Upload** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **map** tekst vak tooselect Hallo map waarvan de gewenste tooupload inhoud.</span><span class="sxs-lookup"><span data-stu-id="87ce4-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Mapopties uploaden][18]
     3. <span data-ttu-id="87ce4-228">Geef Hallo type **Blob-type**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="87ce4-229">Hallo artikel [aan de slag met Azure Blob storage met .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) uitgelegd Hallo verschillen tussen Hallo diverse typen van de blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="87ce4-230">Geef desgewenst een doelmap in welke Hallo inhoud van de geselecteerde map wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="87ce4-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="87ce4-231">Als de doelmap Hallo niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="87ce4-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="87ce4-232">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-232">Select **Upload**.</span></span>
   * <span data-ttu-id="87ce4-233">**Een blob tooyour lokale computer downloaden**</span><span class="sxs-lookup"><span data-stu-id="87ce4-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="87ce4-234">Selecteer desgewenst toodownload Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="87ce4-235">Selecteer op de werkbalk Hallo hoofdvenster van **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="87ce4-236">In Hallo **opgeven waar toosave Hallo blob gedownload** dialoogvenster Geef Hallo-locatie waar u Hallo blob gedownload en naam die u wenst dat toogive Hallo deze.</span><span class="sxs-lookup"><span data-stu-id="87ce4-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="87ce4-237">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-237">Select **Save**.</span></span>
   * <span data-ttu-id="87ce4-238">**Open een blob op uw lokale computer**</span><span class="sxs-lookup"><span data-stu-id="87ce4-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="87ce4-239">Selecteer desgewenst tooopen Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="87ce4-240">Selecteer op de werkbalk Hallo hoofdvenster van **Open**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="87ce4-241">Hallo blob wordt gedownload en geopend met Hallo-toepassing die is gekoppeld aan de onderliggende bestandstype Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="87ce4-242">**Een blob toohello Klembord kopiëren**</span><span class="sxs-lookup"><span data-stu-id="87ce4-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="87ce4-243">Selecteer desgewenst toocopy Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="87ce4-244">Selecteer op de werkbalk Hallo hoofdvenster van **kopie**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="87ce4-245">Klik in het linkerdeelvenster Hallo Ga tooanother blob-container en dubbelklik erop tooview in het hoofdvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="87ce4-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="87ce4-246">Selecteer op de werkbalk Hallo hoofdvenster van **plakken** toocreate een kopie van het Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="87ce4-247">**Verwijderen van een blob**</span><span class="sxs-lookup"><span data-stu-id="87ce4-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="87ce4-248">Selecteer desgewenst toodelete Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="87ce4-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="87ce4-249">Selecteer op de werkbalk Hallo hoofdvenster van **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="87ce4-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="87ce4-250">Selecteer **Ja** toohello bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="87ce4-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87ce4-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87ce4-251">Next steps</span></span>
* <span data-ttu-id="87ce4-252">Weergave Hallo [meest recente release-opmerkingen Opslagverkenner (Preview) en video's](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="87ce4-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="87ce4-253">Meer informatie over hoe te[maken van toepassingen met Azure blobs, tabellen, wachtrijen en bestanden](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="87ce4-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
