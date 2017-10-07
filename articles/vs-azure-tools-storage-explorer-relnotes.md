---
title: Opmerkingen bij de release van de aaaMicrosoft Azure Opslagverkenner (Preview) | Microsoft Docs
description: Releaseopmerkingen voor Microsoft Azure Opslagverkenner (Preview)
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="ff768-103">Opmerkingen bij de release van Microsoft Azure Opslagverkenner (Preview)</span><span class="sxs-lookup"><span data-stu-id="ff768-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="ff768-104">Dit artikel bevat Hallo release-opmerkingen voor Azure Storage Explorer 0.8.16 (Preview), evenals release-opmerkingen voor eerdere versies vrijgeven.</span><span class="sxs-lookup"><span data-stu-id="ff768-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="ff768-105">[Microsoft Azure Opslagverkenner (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is een zelfstandige app waarmee u tooeasily werken met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="ff768-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="ff768-106">Versie 0.8.16 (Preview)</span><span class="sxs-lookup"><span data-stu-id="ff768-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="ff768-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="ff768-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="ff768-108">Azure Storage Explorer 0.8.16 (Preview) downloaden</span><span class="sxs-lookup"><span data-stu-id="ff768-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="ff768-109">Azure Opslagverkenner (Preview) 0.8.16 voor Windows</span><span class="sxs-lookup"><span data-stu-id="ff768-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="ff768-110">Azure Opslagverkenner (Preview) 0.8.16 voor Mac</span><span class="sxs-lookup"><span data-stu-id="ff768-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="ff768-111">Azure Opslagverkenner (Preview) 0.8.16 voor Linux</span><span class="sxs-lookup"><span data-stu-id="ff768-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="ff768-112">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-112">New</span></span>
* <span data-ttu-id="ff768-113">Wanneer u een blob opent, wordt Opslagverkenner u gevraagd tooupload Hallo gedownload bestand als een wijziging wordt gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="ff768-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="ff768-114">Verbeterde Azure Stack-aanmeldingservaring aanpast</span><span class="sxs-lookup"><span data-stu-id="ff768-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="ff768-115">Hallo verbeterde prestaties van uploaden/downloaden van veel kleine bestanden op Hallo dezelfde tijd</span><span class="sxs-lookup"><span data-stu-id="ff768-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="ff768-116">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-116">Fixes</span></span>
* <span data-ttu-id="ff768-117">Voor bepaalde typen blob zou kiezen te "vervangen" tijdens een upload-conflict soms leiden tot Hallo uploaden wordt opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="ff768-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="ff768-118">In versie 0.8.15, zou soms uploads achterstallige voor 99%.</span><span class="sxs-lookup"><span data-stu-id="ff768-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="ff768-119">Tijdens het uploaden van bestanden tooa bestandsshare, als u hebt gekozen tooupload tooa directory, die nog niet bestaat, mislukt het uploaden.</span><span class="sxs-lookup"><span data-stu-id="ff768-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="ff768-120">Opslagverkenner is niet juist genereren van tijdstempels voor handtekeningen voor gedeelde toegang en tabel query's.</span><span class="sxs-lookup"><span data-stu-id="ff768-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="ff768-121">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-121">Known Issues</span></span>
* <span data-ttu-id="ff768-122">Met behulp van een naam en sleutel verbindingsreeks werkt momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="ff768-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="ff768-123">Het wordt opgelost in de volgende release Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff768-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="ff768-124">Tot die tijd kunt u met de naam en sleutel koppelen.</span><span class="sxs-lookup"><span data-stu-id="ff768-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="ff768-125">Als u een bestand met een ongeldige naam van de Windows-bestand tooopen probeert, resulteren Hallo downloaden in een bestand niet gevonden fout.</span><span class="sxs-lookup"><span data-stu-id="ff768-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="ff768-126">Wanneer u op 'Annuleren' voor een taak, duurt het even voor die taak toocancel.</span><span class="sxs-lookup"><span data-stu-id="ff768-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="ff768-127">Dit is een beperking van hello Azure Opslagknooppunt bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="ff768-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="ff768-128">Nadat het uploaden van een blob wordt Hallo tabblad die Hallo uploaden gestart vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="ff768-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="ff768-129">Dit is een wijziging ten opzichte van vorige gedrag en ook wordt u toobe genomen terug toohello hoofdmap van Hallo-container in.</span><span class="sxs-lookup"><span data-stu-id="ff768-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="ff768-130">Als u ervoor kiest verkeerde PINCODE/smartcardcertificaat hello, moet u toorestart in volgorde toohave vergeet Opslagverkenner dat besluit.</span><span class="sxs-lookup"><span data-stu-id="ff768-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="ff768-131">paneel met toepassingsinstellingen Hallo-account kan worden weergegeven dat u nodig hebt tooreenter referenties toofilter abonnementen.</span><span class="sxs-lookup"><span data-stu-id="ff768-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="ff768-132">Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="ff768-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="ff768-133">Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ff768-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="ff768-134">Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account.</span><span class="sxs-lookup"><span data-stu-id="ff768-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="ff768-135">Voor gebruikers op Ubuntu 14.04, moet u tooensure GCC toodate is-kunt u dit doen door het uitvoeren van Hallo opdrachten te volgen en de computer opnieuw te starten:</span><span class="sxs-lookup"><span data-stu-id="ff768-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="ff768-136">Voor gebruikers op Ubuntu 17.04, moet u tooinstall GConf - kunt dit doen door Hallo de volgende opdrachten en opnieuw starten van de computer uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ff768-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="ff768-137">Versie 0.8.14 (Preview)</span><span class="sxs-lookup"><span data-stu-id="ff768-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="ff768-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="ff768-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="ff768-139">Azure Storage Explorer 0.8.14 (Preview) downloaden</span><span class="sxs-lookup"><span data-stu-id="ff768-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="ff768-140">Download de Azure Opslagverkenner (Preview) 0.8.14 voor Windows</span><span class="sxs-lookup"><span data-stu-id="ff768-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="ff768-141">Download de Azure Opslagverkenner (Preview) 0.8.14 voor Mac</span><span class="sxs-lookup"><span data-stu-id="ff768-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="ff768-142">Azure Opslagverkenner (Preview) 0.8.14 voor Linux downloaden</span><span class="sxs-lookup"><span data-stu-id="ff768-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="ff768-143">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-143">New</span></span>

* <span data-ttu-id="ff768-144">Bijgewerkte Electron versie too1.7.2 in volgorde tootake profiteren van verschillende essentiële updates</span><span class="sxs-lookup"><span data-stu-id="ff768-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="ff768-145">U kunt nu snel toegang tot Hallo online probleemoplossingsgids van Hallo help-menu</span><span class="sxs-lookup"><span data-stu-id="ff768-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="ff768-146">Opslagverkenner probleemoplossing [handleiding][2]</span><span class="sxs-lookup"><span data-stu-id="ff768-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="ff768-147">[Instructies] [ 3] voor het verbinden van tooan Stack Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="ff768-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="ff768-148">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-148">Known Issues</span></span>

* <span data-ttu-id="ff768-149">Knoppen op het Hallo-dialoogvenster voor bevestiging van verwijderen-map registreren niet bij Hallo muisklikken op Linux.</span><span class="sxs-lookup"><span data-stu-id="ff768-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="ff768-150">Tijdelijke oplossing is toouse Hallo Enter-toets</span><span class="sxs-lookup"><span data-stu-id="ff768-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="ff768-151">Als u ervoor kiest verkeerde PINCODE/smartcardcertificaat hello, moet u toorestart in volgorde toohave Opslagverkenner vergeet Hallo besluit</span><span class="sxs-lookup"><span data-stu-id="ff768-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="ff768-152">Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken</span><span class="sxs-lookup"><span data-stu-id="ff768-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="ff768-153">paneel met toepassingsinstellingen Hallo-account kan tonen, moet u referenties tooreenter in volgorde toofilter abonnementen</span><span class="sxs-lookup"><span data-stu-id="ff768-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="ff768-154">Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="ff768-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="ff768-155">Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ff768-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="ff768-156">Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account.</span><span class="sxs-lookup"><span data-stu-id="ff768-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="ff768-157">Ubuntu 14.04 installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="ff768-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="ff768-158">Eerdere versies</span><span class="sxs-lookup"><span data-stu-id="ff768-158">Previous releases</span></span>

* [<span data-ttu-id="ff768-159">Versie 0.8.13</span><span class="sxs-lookup"><span data-stu-id="ff768-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="ff768-160">Versie 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="ff768-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="ff768-161">Versie 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="ff768-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="ff768-162">Versie 0.8.7</span><span class="sxs-lookup"><span data-stu-id="ff768-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="ff768-163">Versie 0.8.6</span><span class="sxs-lookup"><span data-stu-id="ff768-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="ff768-164">Versie 0.8.5</span><span class="sxs-lookup"><span data-stu-id="ff768-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="ff768-165">Versie 0.8.4</span><span class="sxs-lookup"><span data-stu-id="ff768-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="ff768-166">Versie 0.8.3</span><span class="sxs-lookup"><span data-stu-id="ff768-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="ff768-167">Versie 0.8.2</span><span class="sxs-lookup"><span data-stu-id="ff768-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="ff768-168">Versie 0.8.0</span><span class="sxs-lookup"><span data-stu-id="ff768-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="ff768-169">Versie 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="ff768-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="ff768-170">Versie 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="ff768-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="ff768-171">Versie 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="ff768-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="ff768-172">Versie 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="ff768-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="ff768-173">Versie 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="ff768-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="ff768-174">Versie 0.8.13</span><span class="sxs-lookup"><span data-stu-id="ff768-174">Version 0.8.13</span></span>
<span data-ttu-id="ff768-175">12/05/2017</span><span class="sxs-lookup"><span data-stu-id="ff768-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-176">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-176">New</span></span>

* <span data-ttu-id="ff768-177">Opslagverkenner probleemoplossing [handleiding][2]</span><span class="sxs-lookup"><span data-stu-id="ff768-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="ff768-178">[Instructies] [ 3] voor het verbinden van tooan Stack Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="ff768-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-179">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-179">Fixes</span></span>

* <span data-ttu-id="ff768-180">Vaste: Uploaden bestand heeft een hoog risico dat een out-of geheugenfout</span><span class="sxs-lookup"><span data-stu-id="ff768-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="ff768-181">Vaste: U kunt nu aanmelden met PINCODE/Smartcard</span><span class="sxs-lookup"><span data-stu-id="ff768-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="ff768-182">Vaste: Open in de Portal nu werkt met Azure China, Duitse Azure, Azure US Government en Azure-Stack</span><span class="sxs-lookup"><span data-stu-id="ff768-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="ff768-183">Vaste: Tijdens het uploaden van een map tooa blob-container 'Ongeldige bewerking' zou soms treedt er een fout</span><span class="sxs-lookup"><span data-stu-id="ff768-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="ff768-184">Vaste: Alles selecteren is uitgeschakeld terwijl het beheer van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="ff768-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="ff768-185">Vaste: Hallo metagegevens van Hallo base blob mogelijk overschreven na het Hallo-eigenschappen van de momentopnamen weer te geven</span><span class="sxs-lookup"><span data-stu-id="ff768-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-186">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-186">Known Issues</span></span>

* <span data-ttu-id="ff768-187">Als u ervoor kiest verkeerde PINCODE/smartcardcertificaat hello, moet u toorestart in volgorde toohave Opslagverkenner vergeet Hallo besluit</span><span class="sxs-lookup"><span data-stu-id="ff768-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="ff768-188">Tijdens het in- of uitzoomen op schaal, opnieuw Hallo zoomniveau tijdelijk worden toohello standaardniveau</span><span class="sxs-lookup"><span data-stu-id="ff768-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="ff768-189">Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken</span><span class="sxs-lookup"><span data-stu-id="ff768-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="ff768-190">paneel met toepassingsinstellingen Hallo-account kan tonen, moet u referenties tooreenter in volgorde toofilter abonnementen</span><span class="sxs-lookup"><span data-stu-id="ff768-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="ff768-191">Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="ff768-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="ff768-192">Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ff768-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="ff768-193">Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account.</span><span class="sxs-lookup"><span data-stu-id="ff768-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="ff768-194">Ubuntu 14.04 installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="ff768-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="ff768-195">Versie 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="ff768-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="ff768-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="ff768-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-197">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-197">New</span></span>

* <span data-ttu-id="ff768-198">Opslagverkenner wordt nu automatisch gesloten wanneer u een update vanaf Hallo updatebericht installeert</span><span class="sxs-lookup"><span data-stu-id="ff768-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="ff768-199">In-place snelle toegang biedt een verbeterde ervaring voor het werken met uw vaak gebruikte resources</span><span class="sxs-lookup"><span data-stu-id="ff768-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="ff768-200">In de Blob-Container-editor Hallo nu ziet u welke virtuele machine een geleaste blob behoort</span><span class="sxs-lookup"><span data-stu-id="ff768-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="ff768-201">U kunt nu Hallo linkerkant Configuratiescherm samenvouwen</span><span class="sxs-lookup"><span data-stu-id="ff768-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="ff768-202">Detectie nu wordt uitgevoerd op Hallo dezelfde tijd als download</span><span class="sxs-lookup"><span data-stu-id="ff768-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="ff768-203">Gebruik maken van statistieken in Hallo Blob-Container, bestandsshare en tabel editors toosee Hallo grootte van de resource of selectie</span><span class="sxs-lookup"><span data-stu-id="ff768-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="ff768-204">U kunt nu aanmelden tooAzure Active Directory (AAD) op basis van Azure-Stack-accounts.</span><span class="sxs-lookup"><span data-stu-id="ff768-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="ff768-205">U kunt nu uploaden meer dan 32 MB tooPremium storage-accounts archiefbestanden</span><span class="sxs-lookup"><span data-stu-id="ff768-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="ff768-206">Verbeterde Toegankelijkheidsondersteuning voor</span><span class="sxs-lookup"><span data-stu-id="ff768-206">Improved accessibility support</span></span>
* <span data-ttu-id="ff768-207">U kunt nu toevoegen vertrouwde Base64-gecodeerd x.509-SSL-certificaten gaat tooEdit -&gt; SSL-certificaten -&gt; certificaten importeren</span><span class="sxs-lookup"><span data-stu-id="ff768-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-208">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-208">Fixes</span></span>

* <span data-ttu-id="ff768-209">Vaste: na het vernieuwen van een account referenties Hallo structuurweergave zou soms niet automatisch vernieuwd</span><span class="sxs-lookup"><span data-stu-id="ff768-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="ff768-210">Vaste: genereren van een SAS voor emulator wachtrijen en tabellen zou leiden tot een ongeldige URL</span><span class="sxs-lookup"><span data-stu-id="ff768-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="ff768-211">Vaste: premium storage-accounts kunnen nu worden uitgebreid terwijl een proxy is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="ff768-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="ff768-212">Vaste: Hallo knop toepassen op Hallo accounts management-pagina werkt niet als u had 1 of 0 accounts die zijn geselecteerd</span><span class="sxs-lookup"><span data-stu-id="ff768-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="ff768-213">Vaste: het uploaden van BLOB's waarvoor oplossingen mislukken - 0.8.11, vast</span><span class="sxs-lookup"><span data-stu-id="ff768-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="ff768-214">Vaste: feedback sturen is onderverdeeld in 0.8.11 - 0.8.12, vast</span><span class="sxs-lookup"><span data-stu-id="ff768-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="ff768-215">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-215">Known Issues</span></span>

* <span data-ttu-id="ff768-216">Na de upgrade too0.8.10, moet u toorefresh alle uw referenties.</span><span class="sxs-lookup"><span data-stu-id="ff768-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="ff768-217">Terwijl het in- of uitzoomen op schaal, Hallo zoomniveau kan tijdelijk worden opnieuw ingesteld toohello standaardniveau.</span><span class="sxs-lookup"><span data-stu-id="ff768-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="ff768-218">Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="ff768-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="ff768-219">paneel met toepassingsinstellingen Hallo-account kan worden weergegeven dat u referenties tooreenter in volgorde toofilter abonnementen moet.</span><span class="sxs-lookup"><span data-stu-id="ff768-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="ff768-220">Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="ff768-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="ff768-221">Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ff768-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="ff768-222">Hoewel Azure Stack momenteel geen bestandsshares ondersteunt, wordt een knooppunt bestandsshares nog steeds wordt weergegeven onder een gekoppelde Azure-Stack storage-account.</span><span class="sxs-lookup"><span data-stu-id="ff768-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="ff768-223">Ubuntu 14.04 installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="ff768-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="ff768-224">Versie 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="ff768-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="ff768-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="ff768-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="ff768-226">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-226">New</span></span>

* <span data-ttu-id="ff768-227">Opslagverkenner 0.8.9 downloadt automatisch de meest recente versie Hallo voor updates.</span><span class="sxs-lookup"><span data-stu-id="ff768-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="ff768-228">Hotfix: met behulp van een portal SAS-URI tooattach die een opslagaccount tot een fout leiden zou gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ff768-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="ff768-229">U kunt nu maken, beheren en blob momentopnamen promoveren.</span><span class="sxs-lookup"><span data-stu-id="ff768-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="ff768-230">U kunt nu tooAzure China, Duitse Azure en Azure US Government accounts aanmelden.</span><span class="sxs-lookup"><span data-stu-id="ff768-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="ff768-231">U kunt nu Hallo zoomniveau wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ff768-231">You can now change hello zoom level.</span></span> <span data-ttu-id="ff768-232">Hallo-opties in Hallo weergave menu tooZoom In uitzoomen en zoomen opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff768-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="ff768-233">Unicode-tekens worden nu ondersteund in de metagegevens van de gebruiker voor blobs en bestanden.</span><span class="sxs-lookup"><span data-stu-id="ff768-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="ff768-234">Toegankelijkheid is verbeterd.</span><span class="sxs-lookup"><span data-stu-id="ff768-234">Accessibility improvements.</span></span>
* <span data-ttu-id="ff768-235">Opmerkingen bij de release van Hallo volgende versie kunnen worden bekeken in Hallo updatebericht.</span><span class="sxs-lookup"><span data-stu-id="ff768-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="ff768-236">U kunt ook de huidige release-opmerkingen Hallo van Hallo Help-menu weergeven.</span><span class="sxs-lookup"><span data-stu-id="ff768-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-237">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-237">Fixes</span></span>

* <span data-ttu-id="ff768-238">Vaste: Hallo versienummer nu juist wordt weergegeven in het Configuratiescherm in Windows</span><span class="sxs-lookup"><span data-stu-id="ff768-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="ff768-239">Vaste: search is niet langer beperkt too50, 000 knooppunten</span><span class="sxs-lookup"><span data-stu-id="ff768-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="ff768-240">Vaste: bestandsshare voor het uploaden van tooa ingezet permanent verloren als doelmap Hallo al niet bestaat</span><span class="sxs-lookup"><span data-stu-id="ff768-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="ff768-241">Vaste: verbeterde stabiliteit voor lange uploaden en downloaden</span><span class="sxs-lookup"><span data-stu-id="ff768-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-242">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-242">Known Issues</span></span>

* <span data-ttu-id="ff768-243">Terwijl het in- of uitzoomen op schaal, Hallo zoomniveau kan tijdelijk worden opnieuw ingesteld toohello standaardniveau.</span><span class="sxs-lookup"><span data-stu-id="ff768-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="ff768-244">Snelle toegang werkt alleen met een abonnement op basis van items.</span><span class="sxs-lookup"><span data-stu-id="ff768-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="ff768-245">Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release.</span><span class="sxs-lookup"><span data-stu-id="ff768-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="ff768-246">Het duurt een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt Snelweergavetoegang.</span><span class="sxs-lookup"><span data-stu-id="ff768-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="ff768-247">Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="ff768-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="ff768-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="ff768-249">Versie 0.8.7</span><span class="sxs-lookup"><span data-stu-id="ff768-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="ff768-250">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-250">New</span></span>

* <span data-ttu-id="ff768-251">U kunt kiezen hoe tooresolve conflicten op Hallo begin van een update downloaden of sessie in Hallo activiteiten venster kopiëren</span><span class="sxs-lookup"><span data-stu-id="ff768-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="ff768-252">Beweeg de muisaanwijzer over een tabblad toosee Hallo volledig pad van Hallo storage resource</span><span class="sxs-lookup"><span data-stu-id="ff768-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="ff768-253">Wanneer u op een tabblad klikt, synchroniseert het met de locatie in het navigatiedeelvenster van Hallo linkerkant</span><span class="sxs-lookup"><span data-stu-id="ff768-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-254">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-254">Fixes</span></span>

* <span data-ttu-id="ff768-255">Vaste: Opslagverkenner is nu een vertrouwd app op Mac</span><span class="sxs-lookup"><span data-stu-id="ff768-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="ff768-256">Vaste: Ubuntu 14.04 wordt opnieuw ondersteund</span><span class="sxs-lookup"><span data-stu-id="ff768-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="ff768-257">Vaste: Soms Hallo-account toevoegen UI knippert bij het laden van abonnementen</span><span class="sxs-lookup"><span data-stu-id="ff768-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="ff768-258">Vaste: Soms niet alle opslagbronnen zijn vermeld in Hallo linkerkant navigatiedeelvenster</span><span class="sxs-lookup"><span data-stu-id="ff768-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="ff768-259">Vaste: Hallo actievenster soms weergegeven leeg acties</span><span class="sxs-lookup"><span data-stu-id="ff768-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="ff768-260">Vaste: venstergrootte Hallo van Hallo laatste gesloten sessie wordt nu bewaard</span><span class="sxs-lookup"><span data-stu-id="ff768-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="ff768-261">Vaste: U kunt openen meerdere tabbladen voor Hallo dezelfde resource met Hallo contextmenu</span><span class="sxs-lookup"><span data-stu-id="ff768-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-262">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-262">Known Issues</span></span>

* <span data-ttu-id="ff768-263">Snelle toegang werkt alleen met een abonnement op basis van items.</span><span class="sxs-lookup"><span data-stu-id="ff768-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="ff768-264">Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release</span><span class="sxs-lookup"><span data-stu-id="ff768-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="ff768-265">Het kan een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt duren voor Snelweergavetoegang</span><span class="sxs-lookup"><span data-stu-id="ff768-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="ff768-266">Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken</span><span class="sxs-lookup"><span data-stu-id="ff768-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="ff768-267">Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna prestaties kan van invloed zijn of niet-verwerkte uitzondering veroorzaken</span><span class="sxs-lookup"><span data-stu-id="ff768-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="ff768-268">Voor Hallo eerst met Hallo Opslagverkenner op Mac OS, ziet u mogelijk meerdere prompts van de gebruiker toestemming tooaccess sleutelhanger daarvoor.</span><span class="sxs-lookup"><span data-stu-id="ff768-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="ff768-269">We raden dat u altijd toestaan selecteren zodat het Hallo-prompt opnieuw niet weergegeven</span><span class="sxs-lookup"><span data-stu-id="ff768-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="ff768-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="ff768-271">Versie 0.8.6</span><span class="sxs-lookup"><span data-stu-id="ff768-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-272">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-272">New</span></span>

* <span data-ttu-id="ff768-273">U kunt nu services toohello Snelweergavetoegang pincode doorgaans voor eenvoudige navigatie gebruikt</span><span class="sxs-lookup"><span data-stu-id="ff768-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="ff768-274">U kunt nu meerdere editors openen in andere tabbladen.</span><span class="sxs-lookup"><span data-stu-id="ff768-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="ff768-275">Een tijdelijke tabblad; tooopen met één klik Dubbelklik tooopen een permanente tabblad. U kunt ook klikken op Hallo tijdelijke tabblad toomake dit een permanente tabblad</span><span class="sxs-lookup"><span data-stu-id="ff768-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="ff768-276">We hebben aangebracht merkbare prestaties en stabiliteitsverbeteringen voor uploadt en downloads, met name voor grote bestanden op snelle machines</span><span class="sxs-lookup"><span data-stu-id="ff768-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="ff768-277">Lege 'virtuele' mappen kunnen nu worden gemaakt in de blob-containers</span><span class="sxs-lookup"><span data-stu-id="ff768-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="ff768-278">We hebben afgebakende zoekopdracht met onze nieuwe verbeterde subtekenreeks search, zodat u nu twee opties voor het zoeken hebt opnieuw zijn geïntroduceerd:</span><span class="sxs-lookup"><span data-stu-id="ff768-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="ff768-279">Globale zoeken: Geef een zoekterm in het Zoektekstvak Hallo</span><span class="sxs-lookup"><span data-stu-id="ff768-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="ff768-280">Afgebakende zoekopdracht - Hallo Vergrootglas pictogram volgende tooa knooppunt, klik op vervolgens het einde van een zoekopdracht term toohello van Hallo-pad toevoegen of met de rechtermuisknop op en selecteer 'Zoeken vanaf hier'</span><span class="sxs-lookup"><span data-stu-id="ff768-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="ff768-281">We hebben verschillende thema's toegevoegd: licht (standaard), donker, Hoog Contrast zwart en Hoog Contrast wit.</span><span class="sxs-lookup"><span data-stu-id="ff768-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="ff768-282">Ga tooEdit -&gt; thema's toochange uw voorkeur thema's</span><span class="sxs-lookup"><span data-stu-id="ff768-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="ff768-283">U kunt eigenschappen van Blob en de bestandsnaam wijzigen</span><span class="sxs-lookup"><span data-stu-id="ff768-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="ff768-284">Er wordt nu ondersteuning gecodeerde (base64) en ongecodeerde Wachtrijberichten</span><span class="sxs-lookup"><span data-stu-id="ff768-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="ff768-285">Op Linux, een 64-bits besturingssysteem is nu vereist.</span><span class="sxs-lookup"><span data-stu-id="ff768-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="ff768-286">Voor deze release wordt alleen ondersteund 64-bits Ubuntu 16.04.1 TNS</span><span class="sxs-lookup"><span data-stu-id="ff768-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="ff768-287">We hebben onze logo bijgewerkt!</span><span class="sxs-lookup"><span data-stu-id="ff768-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-288">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-288">Fixes</span></span>

* <span data-ttu-id="ff768-289">Opgelost: Blokkering problemen scherm</span><span class="sxs-lookup"><span data-stu-id="ff768-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="ff768-290">Vaste: Verbeterde beveiliging</span><span class="sxs-lookup"><span data-stu-id="ff768-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="ff768-291">Vaste: Soms dubbele gekoppelde accounts kunnen worden weergegeven</span><span class="sxs-lookup"><span data-stu-id="ff768-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="ff768-292">Vaste: Een blob met een niet-gedefinieerde type inhoud kan genereren een uitzondering</span><span class="sxs-lookup"><span data-stu-id="ff768-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="ff768-293">Vaste: Openen Hallo deelvenster van de Query op een lege tabel was het niet mogelijk</span><span class="sxs-lookup"><span data-stu-id="ff768-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="ff768-294">Vaste: Varieert fouten in de zoekopdracht</span><span class="sxs-lookup"><span data-stu-id="ff768-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="ff768-295">Vaste: Het aantal resources die worden geladen vanuit 50 too100 wanneer te klikken op 'Meer Load' Hallo verhoogd</span><span class="sxs-lookup"><span data-stu-id="ff768-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="ff768-296">Vaste: Op de eerste keer uitvoert als een account is aangemeld, we nu alle abonnementen voor dat account standaard selecteren</span><span class="sxs-lookup"><span data-stu-id="ff768-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="ff768-297">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-297">Known Issues</span></span>

* <span data-ttu-id="ff768-298">Deze release van Hallo Opslagverkenner kan niet worden uitgevoerd op Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="ff768-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="ff768-299">tooopen meerdere tabbladen voor dezelfde resource, komen niet continu klikt u op Hallo Hallo dezelfde resource.</span><span class="sxs-lookup"><span data-stu-id="ff768-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="ff768-300">Klik op een andere resource en vervolgens terug en klik vervolgens op de oorspronkelijke bron tooopen Hallo deze opnieuw in een ander tabblad</span><span class="sxs-lookup"><span data-stu-id="ff768-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="ff768-301">Snelle toegang werkt alleen met een abonnement op basis van items.</span><span class="sxs-lookup"><span data-stu-id="ff768-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="ff768-302">Lokale resources of resources via de sleutel- of SAS-token is gekoppeld, worden niet ondersteund in deze release</span><span class="sxs-lookup"><span data-stu-id="ff768-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="ff768-303">Het kan een paar seconden toonavigate toohello doelresource, afhankelijk van hoeveel resources die u hebt duren voor Snelweergavetoegang</span><span class="sxs-lookup"><span data-stu-id="ff768-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="ff768-304">Als meer dan 3 groepen van blobs of bestanden uploaden op Hallo van dezelfde kan tijd fouten veroorzaken</span><span class="sxs-lookup"><span data-stu-id="ff768-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="ff768-305">Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna prestaties kan van invloed zijn of niet-verwerkte uitzondering veroorzaken</span><span class="sxs-lookup"><span data-stu-id="ff768-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="ff768-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="ff768-307">Versie 0.8.5</span><span class="sxs-lookup"><span data-stu-id="ff768-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-308">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-308">New</span></span>

* <span data-ttu-id="ff768-309">Kan zich nu gebruik Portal gegenereerde SAS-codes tooattach tooStorage Accounts en resources</span><span class="sxs-lookup"><span data-stu-id="ff768-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-310">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-310">Fixes</span></span>

* <span data-ttu-id="ff768-311">Vaste: race condition tijdens de zoekopdracht soms veroorzaakt knooppunten toobecome niet uitbreidbaar</span><span class="sxs-lookup"><span data-stu-id="ff768-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="ff768-312">Vaste: 'HTTP gebruiken' werkt niet bij het verbinden van tooStorage Accounts met de naam en sleutel</span><span class="sxs-lookup"><span data-stu-id="ff768-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="ff768-313">Vaste: SAS-sleutels (die speciaal Portal gegenereerde) retourneren een foutmelding 'afsluitende slash'</span><span class="sxs-lookup"><span data-stu-id="ff768-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="ff768-314">Vaste: tabel importeren problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="ff768-315">Soms zijn partitiesleutel en de rijsleutel teruggedraaid</span><span class="sxs-lookup"><span data-stu-id="ff768-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="ff768-316">Kan geen tooread 'null' partitiesleutels</span><span class="sxs-lookup"><span data-stu-id="ff768-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-317">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-317">Known Issues</span></span>

* <span data-ttu-id="ff768-318">Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna gevolgen voor de prestaties</span><span class="sxs-lookup"><span data-stu-id="ff768-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="ff768-319">Azure Stack ondersteunt momenteel geen bestanden, zodat tooexpand bestanden bij een fout wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="ff768-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="ff768-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="ff768-321">Versie 0.8.4</span><span class="sxs-lookup"><span data-stu-id="ff768-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="ff768-322">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-322">New</span></span>

* <span data-ttu-id="ff768-323">Genereren, directe koppelingen toostorage accounts, containers, wachtrijen, tabellen, of bestandsshares voor delen en eenvoudig toegang krijgen tot bronnen tooyour - Windows en Mac OS-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="ff768-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="ff768-324">Zoeken naar de blob-containers, tabellen, wachtrijen, bestandsshares of storage-accounts in het zoekvak Hallo</span><span class="sxs-lookup"><span data-stu-id="ff768-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="ff768-325">U kunt nu componenten in de opbouwfunctie voor query's Hallo tabel groeperen</span><span class="sxs-lookup"><span data-stu-id="ff768-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="ff768-326">Wijzig de naam en de blob-containers, bestandsshares, tabellen, blobs, blob-mappen, bestanden en mappen uit binnen SAS gekoppelde accounts en containers kopiëren en plakken</span><span class="sxs-lookup"><span data-stu-id="ff768-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="ff768-327">Naam en het kopiëren van blob-containers en bestandsshares nu behouden eigenschappen en metagegevens</span><span class="sxs-lookup"><span data-stu-id="ff768-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-328">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-328">Fixes</span></span>

* <span data-ttu-id="ff768-329">Vaste: kan niet worden bewerkt tabelentiteiten als ze Booleaanse of binaire eigenschappen bevatten</span><span class="sxs-lookup"><span data-stu-id="ff768-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-330">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-330">Known Issues</span></span>

* <span data-ttu-id="ff768-331">Zoeken ingangen zoeken over ongeveer 50.000 knooppunten - hierna gevolgen voor de prestaties</span><span class="sxs-lookup"><span data-stu-id="ff768-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="ff768-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="ff768-333">Versie 0.8.3</span><span class="sxs-lookup"><span data-stu-id="ff768-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="ff768-334">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-334">New</span></span>

* <span data-ttu-id="ff768-335">Wijzig de naam van containers, tabellen, bestandsshares</span><span class="sxs-lookup"><span data-stu-id="ff768-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="ff768-336">Verbeterde ervaring voor de opbouwfunctie voor Query</span><span class="sxs-lookup"><span data-stu-id="ff768-336">Improved Query builder experience</span></span>
* <span data-ttu-id="ff768-337">Mogelijkheid toosave en de belasting query 's</span><span class="sxs-lookup"><span data-stu-id="ff768-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="ff768-338">Directe koppelingen toostorage accounts of containers, wachtrijen, tabellen of bestandsshares voor het delen en eenvoudige toegang tot uw resources (alleen Windows - Mac OS ondersteunen binnenkort beschikbaar.)</span><span class="sxs-lookup"><span data-stu-id="ff768-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="ff768-339">Mogelijkheid toomanage en CORS-regels configureren</span><span class="sxs-lookup"><span data-stu-id="ff768-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-340">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-340">Fixes</span></span>

* <span data-ttu-id="ff768-341">Vaste: Microsoft-Accounts hernieuwde verificatie vereist is om de 8-12 uur</span><span class="sxs-lookup"><span data-stu-id="ff768-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-342">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-342">Known Issues</span></span>

* <span data-ttu-id="ff768-343">Soms hello UI lijkt bevroren - maximaliseren Hallo venster helpt dit probleem oplossen</span><span class="sxs-lookup"><span data-stu-id="ff768-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="ff768-344">Mac OS-installatie mogelijk verhoogde machtigingen</span><span class="sxs-lookup"><span data-stu-id="ff768-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="ff768-345">Paneel met toepassingsinstellingen account kan tonen, moet u referenties tooreenter in volgorde toofilter abonnementen</span><span class="sxs-lookup"><span data-stu-id="ff768-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="ff768-346">Naamswijzigingen bestandsshares, blob-containers en tabellen blijven niet behouden metagegevens of andere eigenschappen van het Hallo-container, zoals het quotum voor de bestandsshare, openbare toegangsniveau of beleidsregels voor toegang</span><span class="sxs-lookup"><span data-stu-id="ff768-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="ff768-347">Naam van de BLOB's (afzonderlijk of in een nieuwe naam blob-container) behoudt niet momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="ff768-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="ff768-348">Alle andere eigenschappen en metagegevens voor blobs, bestanden en entiteiten blijven behouden tijdens een naam wijzigen</span><span class="sxs-lookup"><span data-stu-id="ff768-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="ff768-349">Kopiëren of verwijderen van resources werkt niet in SAS gekoppelde accounts</span><span class="sxs-lookup"><span data-stu-id="ff768-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="ff768-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="ff768-351">Versie 0.8.2</span><span class="sxs-lookup"><span data-stu-id="ff768-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="ff768-352">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-352">New</span></span>

* <span data-ttu-id="ff768-353">Storage-Accounts zijn gegroepeerd op abonnementen. opslag van de ontwikkeling en resources die zijn aangesloten via een sleutel- of SAS worden weergegeven onder het knooppunt (lokaal en bijlage)</span><span class="sxs-lookup"><span data-stu-id="ff768-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="ff768-354">Afmelden bij accounts in Configuratiescherm van de 'Azure Accountinstellingen'</span><span class="sxs-lookup"><span data-stu-id="ff768-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="ff768-355">Proxy-instellingen tooenable configureren en beheren van aanmeldingspagina</span><span class="sxs-lookup"><span data-stu-id="ff768-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="ff768-356">Maken en de blob-leases opsplitsen</span><span class="sxs-lookup"><span data-stu-id="ff768-356">Create and break blob leases</span></span>
* <span data-ttu-id="ff768-357">Open blob-containers, wachtrijen, tabellen en bestanden met één klik</span><span class="sxs-lookup"><span data-stu-id="ff768-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-358">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-358">Fixes</span></span>

* <span data-ttu-id="ff768-359">Vaste: Wachtrijberichten ingevoegd met .NET of Java-bibliotheken zijn niet goed gedecodeerd van base64</span><span class="sxs-lookup"><span data-stu-id="ff768-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="ff768-360">Vaste: $metrics tabellen worden niet weergegeven voor Blob Storage-accounts</span><span class="sxs-lookup"><span data-stu-id="ff768-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="ff768-361">Vaste: tabellen knooppunt werkt niet voor lokale opslag van (ontwikkeling)</span><span class="sxs-lookup"><span data-stu-id="ff768-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-362">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-362">Known Issues</span></span>

* <span data-ttu-id="ff768-363">Mac OS-installatie mogelijk verhoogde machtigingen</span><span class="sxs-lookup"><span data-stu-id="ff768-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="ff768-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="ff768-365">Versie 0.8.0</span><span class="sxs-lookup"><span data-stu-id="ff768-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="ff768-366">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-366">New</span></span>

* <span data-ttu-id="ff768-367">Share-ondersteuning: weergeven, uploaden, downloaden, kopiëren van bestanden en mappen, SAS URI's (maken en verbinding maken)</span><span class="sxs-lookup"><span data-stu-id="ff768-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="ff768-368">Verbeterde gebruikerservaring voor tooStorage verbinden met SAS URI's of toegangscodes</span><span class="sxs-lookup"><span data-stu-id="ff768-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="ff768-369">De resultaten van de query exporteren</span><span class="sxs-lookup"><span data-stu-id="ff768-369">Export table query results</span></span>
* <span data-ttu-id="ff768-370">De tabel kolom volgorde en aanpassen</span><span class="sxs-lookup"><span data-stu-id="ff768-370">Table column reordering and customization</span></span>
* <span data-ttu-id="ff768-371">$Logs blob-containers en $metrics tabellen bekijken voor Storage-Accounts met ingeschakelde metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="ff768-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="ff768-372">Verbeterde exporteren en importeren van gedrag, bevat nu het soort waarde</span><span class="sxs-lookup"><span data-stu-id="ff768-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-373">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-373">Fixes</span></span>

* <span data-ttu-id="ff768-374">Vaste: uploaden of grote blobs downloaden kan leiden tot onvolledige uploads/downloads</span><span class="sxs-lookup"><span data-stu-id="ff768-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="ff768-375">Vaste: bewerken, toevoegen of importeren van een entity met een numerieke waarde ('1') wordt converteren toodouble</span><span class="sxs-lookup"><span data-stu-id="ff768-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="ff768-376">Vaste: Kan geen tooexpand Hallo tabelknooppunt in de lokale ontwikkelingsomgeving Hallo</span><span class="sxs-lookup"><span data-stu-id="ff768-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-377">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-377">Known Issues</span></span>

* <span data-ttu-id="ff768-378">$metrics tabellen zijn niet zichtbaar voor Blob Storage-accounts</span><span class="sxs-lookup"><span data-stu-id="ff768-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="ff768-379">Berichten in wachtrij plaatsen toegevoegd via een programma mogelijk niet correct weergegeven als het Hallo-berichten moeten worden gecodeerd met Base64-codering</span><span class="sxs-lookup"><span data-stu-id="ff768-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="ff768-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="ff768-381">Versie 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="ff768-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-382">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-382">New</span></span>

* <span data-ttu-id="ff768-383">Betere foutafhandeling voor de app vastloopt</span><span class="sxs-lookup"><span data-stu-id="ff768-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-384">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-384">Fixes</span></span>

* <span data-ttu-id="ff768-385">Vaste bug waar informatiebalk berichten soms worden niet weergegeven als aanmeldingsreferenties vereist zijn</span><span class="sxs-lookup"><span data-stu-id="ff768-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-386">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-386">Known Issues</span></span>

* <span data-ttu-id="ff768-387">Tabellen: Toevoegen, bewerken of importeren van een entiteit die een eigenschap met een ambiguously numerieke waarde, zoals "1" of "1.0 heeft" en gebruiker probeert toosend Hallo als een `Edm.String`, Hallo waarde wordt terugkeren via Hallo client-API als een Edm.Double</span><span class="sxs-lookup"><span data-stu-id="ff768-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="ff768-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="ff768-389">Versie 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="ff768-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="ff768-390">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-390">New</span></span>

* <span data-ttu-id="ff768-391">Tabel ondersteuning: weergeven, query, export, importeren en CRUD-bewerkingen voor entiteiten</span><span class="sxs-lookup"><span data-stu-id="ff768-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="ff768-392">Wachtrij-ondersteuning: bekijken, toe te voegen, dequeueing berichten</span><span class="sxs-lookup"><span data-stu-id="ff768-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="ff768-393">Genereren van SAS-URI's voor Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="ff768-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="ff768-394">TooStorage Accounts verbinden met SAS URI 's</span><span class="sxs-lookup"><span data-stu-id="ff768-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="ff768-395">Meldingen voor toekomstige updates tooStorage Explorer updates</span><span class="sxs-lookup"><span data-stu-id="ff768-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="ff768-396">Bijgewerkte uiterlijk</span><span class="sxs-lookup"><span data-stu-id="ff768-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-397">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-397">Fixes</span></span>

* <span data-ttu-id="ff768-398">Verbeteringen in prestaties en betrouwbaarheid</span><span class="sxs-lookup"><span data-stu-id="ff768-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="ff768-399">Bekende problemen &amp; oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="ff768-400">Downloaden van bestanden van de grote blob werkt niet correct - wordt u aangeraden AzCopy terwijl we dit probleem op te lossen</span><span class="sxs-lookup"><span data-stu-id="ff768-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="ff768-401">Accountreferenties wordt niet opgehaald of in de cache opgeslagen als basismap Hallo kan niet worden gevonden of kan niet naar worden geschreven</span><span class="sxs-lookup"><span data-stu-id="ff768-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="ff768-402">Als we zijn toevoegen, bewerken of importeren van een entiteit die een eigenschap met een ambiguously numerieke waarde, zoals "1" of "1.0 heeft" en Hallo gebruiker toosend probeert als een `Edm.String`, Hallo waarde wordt terugkeren via Hallo client-API als een Edm.Double</span><span class="sxs-lookup"><span data-stu-id="ff768-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="ff768-403">Bij het importeren van CSV-bestanden met meerdere regels records kunnen Hallo gegevens ophalen afgekapt of versleuteld</span><span class="sxs-lookup"><span data-stu-id="ff768-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="ff768-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="ff768-405">Versie 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="ff768-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-406">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-406">Fixes</span></span>

* <span data-ttu-id="ff768-407">Verbeterde prestaties bij het uploaden, downloaden en blobs kopiëren</span><span class="sxs-lookup"><span data-stu-id="ff768-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="ff768-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="ff768-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="ff768-409">Versie 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="ff768-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-410">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-410">New</span></span>

* <span data-ttu-id="ff768-411">Linux-ondersteuning (pariteit functies tooOSX)</span><span class="sxs-lookup"><span data-stu-id="ff768-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="ff768-412">Blob-containers met Shared Access Signatures (SAS)-sleutel niet toevoegen</span><span class="sxs-lookup"><span data-stu-id="ff768-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="ff768-413">Storage-Accounts voor Azure China toevoegen</span><span class="sxs-lookup"><span data-stu-id="ff768-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="ff768-414">Storage-Accounts met aangepaste eindpunten toevoegen</span><span class="sxs-lookup"><span data-stu-id="ff768-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="ff768-415">Openen en bekijken Hallo inhoud tekst en afbeeldingen blobs</span><span class="sxs-lookup"><span data-stu-id="ff768-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="ff768-416">Blob-eigenschappen en metagegevens weergeven en bewerken</span><span class="sxs-lookup"><span data-stu-id="ff768-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="ff768-417">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="ff768-417">Fixes</span></span>

* <span data-ttu-id="ff768-418">Vaste: uploaden of downloaden van een groot aantal blobs (500 +) soms mogelijk Hallo app toohave een wit scherm</span><span class="sxs-lookup"><span data-stu-id="ff768-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="ff768-419">Vaste: bij het instellen van blob-container openbaar toegangsniveau Hallo nieuwe waarde is niet bijgewerkt totdat u Hallo focus op Hallo container opnieuw instelt.</span><span class="sxs-lookup"><span data-stu-id="ff768-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="ff768-420">Bovendien Hallo dialoogvenster standaard altijd te 'geen enkele openbare toegang' en niet Hallo werkelijke huidige waarde.</span><span class="sxs-lookup"><span data-stu-id="ff768-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="ff768-421">Ondersteuning voor betere algehele toetsenbord toegankelijkheid en -gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="ff768-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="ff768-422">Breadcrumbs tekstomloop geschiedenis wanneer het lang met witruimte</span><span class="sxs-lookup"><span data-stu-id="ff768-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="ff768-423">Dialoogvenster SAS ondersteunt validatie voor invoer</span><span class="sxs-lookup"><span data-stu-id="ff768-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="ff768-424">Lokale opslag blijft toobe beschikbaar, zelfs als de gebruikersreferenties zijn verlopen</span><span class="sxs-lookup"><span data-stu-id="ff768-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="ff768-425">Wanneer een geopende blob-container wordt verwijderd, is Hallo blob explorer aan de rechterkant Hallo gesloten</span><span class="sxs-lookup"><span data-stu-id="ff768-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-426">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-426">Known Issues</span></span>

* <span data-ttu-id="ff768-427">Linux installeren behoeften gcc versie bijwerken of bijgewerkt – stappen tooupgrade zijn hieronder:</span><span class="sxs-lookup"><span data-stu-id="ff768-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="ff768-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="ff768-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="ff768-429">Versie 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="ff768-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="ff768-430">Nieuw</span><span class="sxs-lookup"><span data-stu-id="ff768-430">New</span></span>

* <span data-ttu-id="ff768-431">Mac OS en Windows-versies</span><span class="sxs-lookup"><span data-stu-id="ff768-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="ff768-432">Tooview aanmelden met uw Storage-Accounts: gebruik uw Org-Account, Microsoft-Account, 2FA, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ff768-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="ff768-433">Opslag voor lokale ontwikkeling (opslagemulator, gebruiken alleen-Windows)</span><span class="sxs-lookup"><span data-stu-id="ff768-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="ff768-434">Ondersteuning voor Azure Resource Manager en Classic resource</span><span class="sxs-lookup"><span data-stu-id="ff768-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="ff768-435">Maken en verwijderen van blobs, wachtrijen of tabellen</span><span class="sxs-lookup"><span data-stu-id="ff768-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="ff768-436">Zoeken naar specifieke blobs, wachtrijen of tabellen</span><span class="sxs-lookup"><span data-stu-id="ff768-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="ff768-437">Bekijk de inhoud Hallo van blob-containers</span><span class="sxs-lookup"><span data-stu-id="ff768-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="ff768-438">Navigeren door mappen</span><span class="sxs-lookup"><span data-stu-id="ff768-438">View and navigate through directories</span></span>
* <span data-ttu-id="ff768-439">Uploaden, downloaden en verwijderen van blobs en mappen</span><span class="sxs-lookup"><span data-stu-id="ff768-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="ff768-440">Blob-eigenschappen en metagegevens weergeven en bewerken</span><span class="sxs-lookup"><span data-stu-id="ff768-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="ff768-441">SAS sleutels genereren</span><span class="sxs-lookup"><span data-stu-id="ff768-441">Generate SAS keys</span></span>
* <span data-ttu-id="ff768-442">Beheren en opgeslagen toegang beleid (SAP) maken</span><span class="sxs-lookup"><span data-stu-id="ff768-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="ff768-443">Blobs op voorvoegsel zoeken</span><span class="sxs-lookup"><span data-stu-id="ff768-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="ff768-444">Sleep n neerzetten van bestanden tooupload of downloaden</span><span class="sxs-lookup"><span data-stu-id="ff768-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ff768-445">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="ff768-445">Known Issues</span></span>

* <span data-ttu-id="ff768-446">Bij het instellen van blob-container openbaar toegangsniveau wordt Hallo nieuwe waarde pas bijgewerkt wanneer u Hallo focus op Hallo container opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="ff768-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="ff768-447">Wanneer u Hallo dialoogvenster tooset Hallo openbare toegangsniveau opent, bevat wordt altijd 'Geen openbare toegang' hello standaard en niet Hallo werkelijke huidige waarde</span><span class="sxs-lookup"><span data-stu-id="ff768-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="ff768-448">Gedownloade blobs hernoemen niet</span><span class="sxs-lookup"><span data-stu-id="ff768-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="ff768-449">Logboekvermeldingen activiteit wordt soms 'hangen' een onderhanden status wanneer er een fout optreedt en het Hallo-fout niet wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="ff768-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="ff768-450">Soms crashes of schakelt volledig wit wanneer u probeert tooupload of een groot aantal blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="ff768-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="ff768-451">Soms annuleren van een kopieerbewerking werkt niet</span><span class="sxs-lookup"><span data-stu-id="ff768-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="ff768-452">Tijdens het maken van een container (wachtrij-blob/tabelnaam) als u een ongeldige naam invoeren en doorgaan toocreate andere onder een andere containertype u kan niet de focus instelt op het nieuwe type Hallo</span><span class="sxs-lookup"><span data-stu-id="ff768-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="ff768-453">Kan geen nieuwe map maken of wijzig de map</span><span class="sxs-lookup"><span data-stu-id="ff768-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md