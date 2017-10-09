---
title: aaaUsing Opslagverkenner (Preview) met Azure File storage | Microsoft Docs
description: Meer informatie over hoe meer informatie over hoe toouse Opslagverkenner (Preview) toowork met bestand deelt en bestanden.
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="e8857-103">Opslagverkenner (preview) gebruiken met Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="e8857-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="e8857-104">Azure File storage is een service die bestand aanbiedt deelt in de cloud met behulp van Hallo Hallo standaard Server Message Block (SMB)-Protocol.</span><span class="sxs-lookup"><span data-stu-id="e8857-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="e8857-105">Zowel SMB 2.1 als SMB 3.0 wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e8857-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="e8857-106">Met Azure File storage, kunt u oudere toepassingen die afhankelijk van bestandsshares tooAzure snel en zonder kostbare regeneraties zijn te migreren.</span><span class="sxs-lookup"><span data-stu-id="e8857-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="e8857-107">Kunt u bestandsgegevens opslag tooexpose openbaar toohello world of toostore toepassingsgegevens privé.</span><span class="sxs-lookup"><span data-stu-id="e8857-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="e8857-108">In dit artikel leert u hoe toouse Opslagverkenner (Preview) toowork met bestand deelt, en bestanden.</span><span class="sxs-lookup"><span data-stu-id="e8857-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8857-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e8857-109">Prerequisites</span></span>

<span data-ttu-id="e8857-110">toocomplete hello stappen in dit artikel, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e8857-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="e8857-111">Opslagverkenner (preview) downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="e8857-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="e8857-112">Verbinding maken met tooa Azure storage-account of -service</span><span class="sxs-lookup"><span data-stu-id="e8857-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="e8857-113">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="e8857-113">Create a File Share</span></span>

<span data-ttu-id="e8857-114">Alle bestanden moeten zich bevinden in een bestandsshare, wat in feite niets meer is dan een logische groepering van bestanden.</span><span class="sxs-lookup"><span data-stu-id="e8857-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="e8857-115">Een account kan een onbeperkt aantal bestandsshares bevatten en elke share kan een onbeperkt aantal bestanden bevatten.</span><span class="sxs-lookup"><span data-stu-id="e8857-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="e8857-116">Hallo stappen laten zien hoe toocreate een bestandsshare in Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="e8857-117">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="e8857-118">Vouw in het linkerdeelvenster Hallo Hallo waarbinnen u wenst dat toocreate Hallo File Share storage-account</span><span class="sxs-lookup"><span data-stu-id="e8857-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="e8857-119">Met de rechtermuisknop op **bestandsshares**, en selecteer in het contextmenu Hallo - **bestandsshare maken**.</span><span class="sxs-lookup"><span data-stu-id="e8857-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Bestandsshare maken](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="e8857-121">Een tekstvak wordt weergegeven onder Hallo **bestandsshares** map.</span><span class="sxs-lookup"><span data-stu-id="e8857-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="e8857-122">Voer Hallo-naam voor de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="e8857-122">Enter hello name for your file share.</span></span> <span data-ttu-id="e8857-123">Zie Hallo [delen naamgevingsregels](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sectie voor een lijst van regels en beperkingen voor de naamgeving van bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="e8857-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Naamgeving Hallo-share](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="e8857-125">Druk op **Enter** wanneer gereed toocreate Hallo bestandsshare, of **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="e8857-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="e8857-126">Zodra het Hallo-bestandsshare is gemaakt, die wordt weergegeven onder Hallo **bestandsshares** map voor Hallo storage-account geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e8857-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![Hallo nieuwe share](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="e8857-128">De inhoud van een bestandsshare weergeven</span><span class="sxs-lookup"><span data-stu-id="e8857-128">View a file share's contents</span></span>

<span data-ttu-id="e8857-129">Bestandsshares bevatten bestanden en mappen (die ook weer bestanden kunnen bevatten).</span><span class="sxs-lookup"><span data-stu-id="e8857-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="e8857-130">Hallo volgende stappen laten zien hoe tooview Hallo inhoud van een bestand delen in Opslagverkenner (Preview): +</span><span class="sxs-lookup"><span data-stu-id="e8857-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="e8857-131">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="e8857-132">Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat tooview met storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8857-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="e8857-133">Vouw Hallo storage account **bestandsshares**.</span><span class="sxs-lookup"><span data-stu-id="e8857-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="e8857-134">Klik met de rechtermuisknop Hallo bestandsshare u tooview wilt, en - selecteer in het contextmenu Hallo - **Open**.</span><span class="sxs-lookup"><span data-stu-id="e8857-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="e8857-135">U kunt ook Hallo-bestandsshare die u wenst dat tooview dubbelklikken.</span><span class="sxs-lookup"><span data-stu-id="e8857-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Share openen](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="e8857-137">hoofdvenster Hello wordt Hallo van de bestandsshare inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8857-137">hello main pane will display hello file share's contents.</span></span>
    
    ![Hallo delen van inhoud](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="e8857-139">Een bestandsshare verwijderen</span><span class="sxs-lookup"><span data-stu-id="e8857-139">Delete a file share</span></span>

<span data-ttu-id="e8857-140">U kunt op ieder moment bestandsshares toevoegen en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e8857-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="e8857-141">(toosee hoe toodelete afzonderlijke bestanden, Raadpleeg de sectie toohello [beheren van bestanden in een bestandsshare](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="e8857-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="e8857-142">Hallo stappen laten zien hoe toodelete een bestandsshare in Opslagverkenner (Preview):</span><span class="sxs-lookup"><span data-stu-id="e8857-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="e8857-143">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="e8857-144">Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat tooview met storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8857-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="e8857-145">Vouw Hallo storage account **bestandsshares**.</span><span class="sxs-lookup"><span data-stu-id="e8857-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="e8857-146">Klik met de rechtermuisknop Hallo bestandsshare u toodelete wilt, en - selecteer in het contextmenu Hallo - **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e8857-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="e8857-147">U kunt ook op drukken **verwijderen** toodelete Hallo geselecteerde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="e8857-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Verwijderen](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="e8857-149">Selecteer **Ja** toohello bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="e8857-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Bevestigingsvenster](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="e8857-151">Een bestandsshare kopiëren</span><span class="sxs-lookup"><span data-stu-id="e8857-151">Copy a file share</span></span>

<span data-ttu-id="e8857-152">Opslagverkenner (Preview) kunt u toocopy file share toohello Klembord en plak vervolgens of de bestandsshare in een ander opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e8857-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="e8857-153">(toosee hoe toocopy afzonderlijke bestanden, Raadpleeg de sectie toohello [beheren van bestanden in een bestandsshare](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="e8857-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="e8857-154">Hallo stappen laten zien hoe toocopy een bestand van een storage account tooanother delen.</span><span class="sxs-lookup"><span data-stu-id="e8857-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="e8857-155">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="e8857-156">Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat toocopy met storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8857-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="e8857-157">Vouw Hallo storage account **bestandsshares**.</span><span class="sxs-lookup"><span data-stu-id="e8857-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="e8857-158">Klik met de rechtermuisknop Hallo bestandsshare u toocopy wilt, en - selecteer in het contextmenu Hallo - **kopie-bestandsshare**.</span><span class="sxs-lookup"><span data-stu-id="e8857-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Bestandsshare kopiëren](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="e8857-160">Met de rechtermuisknop op de gewenste Hallo 'target' storage-account waarin u wilt toopaste Hallo-bestandsshare en - selecteer in het contextmenu Hallo - **plakken bestandsshare**.</span><span class="sxs-lookup"><span data-stu-id="e8857-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Bestandsshare plakken](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="e8857-162">Hallo SAS ophalen voor een bestandsshare</span><span class="sxs-lookup"><span data-stu-id="e8857-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="e8857-163">Een [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) tooresources gedelegeerde toegang in uw opslagaccount biedt.</span><span class="sxs-lookup"><span data-stu-id="e8857-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="e8857-164">Dit betekent dat u een client beperkte machtigingen tooobjects in uw storage-account gedurende een bepaalde tijd en met een opgegeven set machtigingen, zonder tooshare de toegangssleutels van uw account kunt verlenen.</span><span class="sxs-lookup"><span data-stu-id="e8857-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="e8857-165">Hallo volgende stappen laten zien hoe toocreate een SAS voor een bestand delen: +</span><span class="sxs-lookup"><span data-stu-id="e8857-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="e8857-166">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="e8857-167">Vouw in het linkerdeelvenster Hallo HALLO hallo bestandsshare waarvoor tooget een SAS met storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8857-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="e8857-168">Vouw Hallo storage account **bestandsshares**.</span><span class="sxs-lookup"><span data-stu-id="e8857-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="e8857-169">Met de rechtermuisknop op de gewenste bestandsshare hello, en selecteer in het contextmenu Hallo - **Shared Access Signature ophalen**.</span><span class="sxs-lookup"><span data-stu-id="e8857-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Handtekening voor gedeelde toegang ophalen](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="e8857-171">In Hallo **Shared Access Signature** dialoogvenster Hallo-beleid, de begin- en verloopdatum datums, de tijdzone opgeven en toegangsniveaus voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="e8857-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![SAS-dialoogvenster](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="e8857-173">Wanneer u klaar bent Hallo SAS-opties op te geven, selecteert u **maken**.</span><span class="sxs-lookup"><span data-stu-id="e8857-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="e8857-174">Een tweede **Shared Access Signature** dialoogvenster dat lijsten Hallo bestandsshare samen met de Hallo-URL en kunt u tooaccess QueryStrings Hallo storage resource vervolgens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8857-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="e8857-175">Selecteer **kopie** volgende toohello-URL die u wenst dat toocopy toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="e8857-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![Tweede SAS-dialoogvenster](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="e8857-177">Als u klaar bent, selecteert u **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="e8857-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="e8857-178">Toegangsbeleid voor een bestandsshare beheren</span><span class="sxs-lookup"><span data-stu-id="e8857-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="e8857-179">Hallo volgende stappen laten zien hoe toomanage (toevoegen en verwijderen) toegangsbeleid voor een bestandsshare: +.</span><span class="sxs-lookup"><span data-stu-id="e8857-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="e8857-180">Hallo-beleid wordt gebruikt voor het maken van SAS-URL's via welke mensen tooaccess Hallo opslagbestand resource gedurende een bepaalde tijd kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e8857-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="e8857-181">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="e8857-182">Vouw in het linkerdeelvenster Hallo HALLO hallo bestandsshare waarvan u wilt dat toomanage toegangsbeleid met storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8857-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="e8857-183">Vouw Hallo storage account **bestandsshares**.</span><span class="sxs-lookup"><span data-stu-id="e8857-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="e8857-184">Selecteer de gewenste bestandsshare Hallo, en selecteer in het contextmenu Hallo - **toegangsbeleid beheren**.</span><span class="sxs-lookup"><span data-stu-id="e8857-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Contextmenu Toegangsbeleid beheren](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="e8857-186">Hallo **toegangsbeleid** dialoogvenster vermeldt alle beleidsregels voor toegang al is gemaakt voor de geselecteerde Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="e8857-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Toegangsbeleid](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="e8857-188">Volg deze stappen, afhankelijk van Hallo toegang beleid beheertaak:</span><span class="sxs-lookup"><span data-stu-id="e8857-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="e8857-189">**Een nieuw toegangsbeleid toevoegen**: selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e8857-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="e8857-190">Zodra gegenereerd, Hallo **toegangsbeleid** dialoogvenster wordt weergegeven Hallo toegevoegde toegangsbeleid (met de standaardinstellingen).</span><span class="sxs-lookup"><span data-stu-id="e8857-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="e8857-191">**Een toegangsbeleid bewerken**: breng de gewenste wijzigingen aan en selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e8857-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="e8857-192">**Verwijderen van een toegangsbeleid** : Selecteer **verwijderen** volgende toohello toegangsbeleid gewenste tooremove.</span><span class="sxs-lookup"><span data-stu-id="e8857-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="e8857-193">Maak een nieuwe SAS-URL met Hallo toegangsbeleid dat u eerder hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="e8857-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![SAS ophalen](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Naam en eigenschappen va SAS](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="e8857-196">Bestanden in een bestandsshare beheren</span><span class="sxs-lookup"><span data-stu-id="e8857-196">Managing files in a file share</span></span>

<span data-ttu-id="e8857-197">Als u een bestandsshare hebt gemaakt, kunt u een bestandsshare toothat-bestand uploaden, downloaden van een bestand tooyour lokale computer, opent u een bestand op uw lokale computer en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="e8857-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="e8857-198">Hallo volgende stappen laten zien hoe toomanage Hallo-bestanden (en mappen) in een bestand delen.</span><span class="sxs-lookup"><span data-stu-id="e8857-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="e8857-199">Open Opslagverkenner (Preview).</span><span class="sxs-lookup"><span data-stu-id="e8857-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="e8857-200">Vouw in het linkerdeelvenster Hallo HALLO hallo-bestandsshare die u wenst dat toomanage met storage-account.</span><span class="sxs-lookup"><span data-stu-id="e8857-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="e8857-201">Vouw Hallo storage account **bestandsshares**.</span><span class="sxs-lookup"><span data-stu-id="e8857-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="e8857-202">Dubbelklik op Hallo-bestandsshare die u wenst dat tooview.</span><span class="sxs-lookup"><span data-stu-id="e8857-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="e8857-203">hoofdvenster Hello wordt Hallo van de bestandsshare inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8857-203">hello main pane will display hello file share's contents.</span></span>

    ![Hallo delen van inhoud](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="e8857-205">hoofdvenster Hello wordt Hallo van de bestandsshare inhoud weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8857-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="e8857-206">Volg deze dat stappen, afhankelijk van de taak Hallo gewenste tooperform:</span><span class="sxs-lookup"><span data-stu-id="e8857-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="e8857-207">**Uploaden van bestanden tooa bestandsshare**</span><span class="sxs-lookup"><span data-stu-id="e8857-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="e8857-208">a.</span><span class="sxs-lookup"><span data-stu-id="e8857-208">a.</span></span>  <span data-ttu-id="e8857-209">Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **bestanden uploaden** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8857-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Bestanden uploaden](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="e8857-211">b.</span><span class="sxs-lookup"><span data-stu-id="e8857-211">b.</span></span> <span data-ttu-id="e8857-212">In Hallo **bestanden uploaden** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **bestanden** tekstvak tooselect Hallo op die u wenst dat tooupload.</span><span class="sxs-lookup"><span data-stu-id="e8857-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Bestanden toevoegen](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="e8857-214">c.</span><span class="sxs-lookup"><span data-stu-id="e8857-214">c.</span></span> <span data-ttu-id="e8857-215">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="e8857-215">Select **Upload**.</span></span>

    - <span data-ttu-id="e8857-216">**Een bestandsshare van de map tooa uploaden**</span><span class="sxs-lookup"><span data-stu-id="e8857-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="e8857-217">a.</span><span class="sxs-lookup"><span data-stu-id="e8857-217">a.</span></span> <span data-ttu-id="e8857-218">Selecteer op de werkbalk Hallo hoofdvenster van **uploaden**, en vervolgens **map uploaden** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8857-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Menu voor uploaden van map](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="e8857-220">b.</span><span class="sxs-lookup"><span data-stu-id="e8857-220">b.</span></span> <span data-ttu-id="e8857-221">In Hallo **map Upload** dialoogvenster, selecteer Hallo weglatingsteken (**...** ) knop aan de rechterkant Hallo Hallo **map** tekst vak tooselect Hallo map waarvan de gewenste tooupload inhoud.</span><span class="sxs-lookup"><span data-stu-id="e8857-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="e8857-222">c.</span><span class="sxs-lookup"><span data-stu-id="e8857-222">c.</span></span> <span data-ttu-id="e8857-223">Geef desgewenst een doelmap in welke Hallo inhoud van de geselecteerde map wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="e8857-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="e8857-224">Als de doelmap Hallo niet bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8857-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="e8857-225">d.</span><span class="sxs-lookup"><span data-stu-id="e8857-225">d.</span></span> <span data-ttu-id="e8857-226">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="e8857-226">Select **Upload**.</span></span>

    - <span data-ttu-id="e8857-227">**Een bestand tooyour lokale computer downloaden**</span><span class="sxs-lookup"><span data-stu-id="e8857-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="e8857-228">a.</span><span class="sxs-lookup"><span data-stu-id="e8857-228">a.</span></span> <span data-ttu-id="e8857-229">Selecteer desgewenst toodownload Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="e8857-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="e8857-230">b.</span><span class="sxs-lookup"><span data-stu-id="e8857-230">b.</span></span> <span data-ttu-id="e8857-231">Selecteer op de werkbalk Hallo hoofdvenster van **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="e8857-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="e8857-232">c.</span><span class="sxs-lookup"><span data-stu-id="e8857-232">c.</span></span> <span data-ttu-id="e8857-233">In Hallo **opgeven waar toosave Hallo bestand hebt gedownload** dialoogvenster Hallo-locatie waar u gedownloade Hallo-bestand wilt opgeven en naam die u wenst dat toogive Hallo deze.</span><span class="sxs-lookup"><span data-stu-id="e8857-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="e8857-234">d.</span><span class="sxs-lookup"><span data-stu-id="e8857-234">d.</span></span> <span data-ttu-id="e8857-235">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e8857-235">Select **Save**.</span></span>

    - <span data-ttu-id="e8857-236">**Een bestand op de lokale computer openen**</span><span class="sxs-lookup"><span data-stu-id="e8857-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="e8857-237">a.</span><span class="sxs-lookup"><span data-stu-id="e8857-237">a.</span></span>  <span data-ttu-id="e8857-238">Selecteer desgewenst tooopen Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="e8857-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="e8857-239">b.</span><span class="sxs-lookup"><span data-stu-id="e8857-239">b.</span></span>  <span data-ttu-id="e8857-240">Selecteer op de werkbalk Hallo hoofdvenster van **Open**.</span><span class="sxs-lookup"><span data-stu-id="e8857-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="e8857-241">c.</span><span class="sxs-lookup"><span data-stu-id="e8857-241">c.</span></span>  <span data-ttu-id="e8857-242">Hallo-bestand wordt gedownload en Hallo-toepassing die is gekoppeld aan de onderliggende bestandstype Hallo-bestand geopend.</span><span class="sxs-lookup"><span data-stu-id="e8857-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="e8857-243">**Een bestand toohello Klembord kopiëren**</span><span class="sxs-lookup"><span data-stu-id="e8857-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="e8857-244">a.</span><span class="sxs-lookup"><span data-stu-id="e8857-244">a.</span></span> <span data-ttu-id="e8857-245">Selecteer desgewenst toocopy Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="e8857-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="e8857-246">b.</span><span class="sxs-lookup"><span data-stu-id="e8857-246">b.</span></span> <span data-ttu-id="e8857-247">Selecteer op de werkbalk Hallo hoofdvenster van **kopie**.</span><span class="sxs-lookup"><span data-stu-id="e8857-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="e8857-248">c.</span><span class="sxs-lookup"><span data-stu-id="e8857-248">c.</span></span> <span data-ttu-id="e8857-249">Klik in het linkerdeelvenster Hallo Ga tooanother bestandsshare en dubbelklik erop tooview in het hoofdvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="e8857-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="e8857-250">d.</span><span class="sxs-lookup"><span data-stu-id="e8857-250">d.</span></span> <span data-ttu-id="e8857-251">Selecteer op de werkbalk Hallo hoofdvenster van **plakken** toocreate een kopie van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="e8857-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="e8857-252">**Een bestand verwijderen**</span><span class="sxs-lookup"><span data-stu-id="e8857-252">**Delete a file**</span></span>

        <span data-ttu-id="e8857-253">a.</span><span class="sxs-lookup"><span data-stu-id="e8857-253">a.</span></span> <span data-ttu-id="e8857-254">Selecteer desgewenst toodelete Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="e8857-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="e8857-255">b.</span><span class="sxs-lookup"><span data-stu-id="e8857-255">b.</span></span> <span data-ttu-id="e8857-256">Selecteer op de werkbalk Hallo hoofdvenster van **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e8857-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="e8857-257">c.</span><span class="sxs-lookup"><span data-stu-id="e8857-257">c.</span></span> <span data-ttu-id="e8857-258">Selecteer **Ja** toohello bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="e8857-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8857-259">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8857-259">Next steps</span></span>

- <span data-ttu-id="e8857-260">Weergave Hallo [meest recente release-opmerkingen Opslagverkenner (Preview) en video's](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e8857-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="e8857-261">Meer informatie over hoe te[maken van toepassingen met Azure blobs, tabellen, wachtrijen en bestanden](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="e8857-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
