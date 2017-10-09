---
title: aaaCreate een StorSimple 8000 series ondersteuningspakket | Microsoft Docs
description: Ontdek hoe toocreate, ontsleutelen en bewerken van een ondersteuningspakket voor uw StorSimple 8000 serie-apparaat.
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="50d70-103">Maken en beheren van een ondersteuningspakket voor StorSimple 8000-serie</span><span class="sxs-lookup"><span data-stu-id="50d70-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="50d70-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="50d70-104">Overview</span></span>

<span data-ttu-id="50d70-105">Een StorSimple-ondersteuningspakket is een mechanisme voor eenvoudig te gebruiken dat alle relevante logboeken tooassist Microsoft Support verzamelt bij het oplossen van eventuele problemen StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="50d70-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="50d70-106">Hallo zijn verzamelde logboeken versleuteld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="50d70-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="50d70-107">Deze zelfstudie bevat stapsgewijze instructies toocreate en Hallo support-pakket voor uw StorSimple 8000 series apparaat beheren.</span><span class="sxs-lookup"><span data-stu-id="50d70-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="50d70-108">Als u met een virtueel StorSimple-matrix werkt, gaat u verder te[genereren van een pakket logboek](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="50d70-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="50d70-109">Een ondersteuningspakket maken</span><span class="sxs-lookup"><span data-stu-id="50d70-109">Create a support package</span></span>

<span data-ttu-id="50d70-110">In sommige gevallen moet u toomanually Hallo ondersteuningspakket via Windows PowerShell voor StorSimple maken.</span><span class="sxs-lookup"><span data-stu-id="50d70-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="50d70-111">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="50d70-111">For example:</span></span>

* <span data-ttu-id="50d70-112">Als u tooremove gevoelige informatie van uw logboek bestanden voorafgaande toosharing met Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="50d70-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="50d70-113">Als u problemen bij het uploaden van Hallo pakket vanwege tooconnectivity problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="50d70-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="50d70-114">U kunt uw handmatig gegenereerde ondersteuningspakket delen met Microsoft Support via e-mail.</span><span class="sxs-lookup"><span data-stu-id="50d70-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="50d70-115">Volgende stappen toocreate ondersteuningspakket in Windows PowerShell voor StorSimple Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="50d70-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="50d70-116">toocreate ondersteuningspakket in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="50d70-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="50d70-117">toostart een Windows PowerShell-sessie als administrator op Hallo externe computer die is gebruikt tooconnect tooyour StorSimple-apparaat, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="50d70-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="50d70-118">In de Windows PowerShell-sessie Hallo verbinden toohello SSAdmin Console van uw apparaat:</span><span class="sxs-lookup"><span data-stu-id="50d70-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="50d70-119">Voer het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="50d70-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="50d70-120">Voer het beheerderswachtwoord van uw apparaat Hallo in het dialoogvenster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="50d70-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="50d70-121">is het standaardwachtwoord Hallo _Wachtwoord1_.</span><span class="sxs-lookup"><span data-stu-id="50d70-121">hello default password is _Password1_.</span></span>
     
      ![In het dialoogvenster van PowerShell-referentie](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="50d70-123">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="50d70-123">Select **OK**.</span></span>
   4. <span data-ttu-id="50d70-124">Voer het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="50d70-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="50d70-125">Voer de juiste opdracht Hallo in Hallo-sessie die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="50d70-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="50d70-126">Voer voor netwerkshares die beveiligd met een wachtwoord zijn:</span><span class="sxs-lookup"><span data-stu-id="50d70-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="50d70-127">U wordt gevraagd om een wachtwoord, een pad toohello gedeelde netwerkmap en een wachtwoordzin voor versleuteling (omdat het ondersteuningspakket Hallo is versleuteld).</span><span class="sxs-lookup"><span data-stu-id="50d70-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="50d70-128">Een ondersteuningspakket wordt vervolgens gemaakt in de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d70-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="50d70-129">Voor shares die niet beveiligd met een wachtwoord zijn, hoeft u niet Hallo `-Credential` parameter.</span><span class="sxs-lookup"><span data-stu-id="50d70-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="50d70-130">Voer de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="50d70-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="50d70-131">Hallo ondersteuningspakket is gemaakt voor beide domeincontrollers in Hallo opgegeven gedeelde netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="50d70-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="50d70-132">Het is een versleutelde, gecomprimeerd bestand dat kan worden verzonden tooMicrosoft ondersteuning voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="50d70-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="50d70-133">Zie voor meer informatie [contact opnemen met Microsoft ondersteuning](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="50d70-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="50d70-134">Hallo Export HcsSupportPackage cmdlet-parameters</span><span class="sxs-lookup"><span data-stu-id="50d70-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="50d70-135">U kunt Hallo na Hallo Export HcsSupportPackage cmdlet-parameters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50d70-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="50d70-136">Parameter</span><span class="sxs-lookup"><span data-stu-id="50d70-136">Parameter</span></span> | <span data-ttu-id="50d70-137">Vereiste/optionele</span><span class="sxs-lookup"><span data-stu-id="50d70-137">Required/Optional</span></span> | <span data-ttu-id="50d70-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="50d70-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="50d70-139">Vereist</span><span class="sxs-lookup"><span data-stu-id="50d70-139">Required</span></span> |<span data-ttu-id="50d70-140">Gebruik tooprovide Hallo locatie van Hallo gedeelde netwerkmap in welke Hallo ondersteuningspakket wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="50d70-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="50d70-141">Vereist</span><span class="sxs-lookup"><span data-stu-id="50d70-141">Required</span></span> |<span data-ttu-id="50d70-142">Gebruik tooprovide een wachtwoordzin toohelp Hallo ondersteuningspakket versleutelen.</span><span class="sxs-lookup"><span data-stu-id="50d70-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="50d70-143">Optioneel</span><span class="sxs-lookup"><span data-stu-id="50d70-143">Optional</span></span> |<span data-ttu-id="50d70-144">Gebruik toosupply toegangsreferenties voor Hallo gedeelde netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="50d70-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="50d70-145">Optioneel</span><span class="sxs-lookup"><span data-stu-id="50d70-145">Optional</span></span> |<span data-ttu-id="50d70-146">Gebruik tooskip Hallo versleuteling wachtwoordzin bevestigen.</span><span class="sxs-lookup"><span data-stu-id="50d70-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="50d70-147">Optioneel</span><span class="sxs-lookup"><span data-stu-id="50d70-147">Optional</span></span> |<span data-ttu-id="50d70-148">Gebruik toospecify een map onder *pad* in welke ondersteuning Hallo pakket wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="50d70-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="50d70-149">Hallo standaard is [apparaatnaam]-[huidige datum en time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="50d70-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="50d70-150">Optioneel</span><span class="sxs-lookup"><span data-stu-id="50d70-150">Optional</span></span> |<span data-ttu-id="50d70-151">Geef als **Cluster** (standaard) toocreate ondersteuningspakket voor beide domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="50d70-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="50d70-152">Geef desgewenst kunt u een pakket toocreate alleen voor de huidige controller Hallo **Controller**.</span><span class="sxs-lookup"><span data-stu-id="50d70-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="50d70-153">Een ondersteuningspakket bewerken</span><span class="sxs-lookup"><span data-stu-id="50d70-153">Edit a support package</span></span>

<span data-ttu-id="50d70-154">Nadat u een ondersteuningspakket hebt gegenereerd, moet u mogelijk tooedit Hallo pakket tooremove gevoelige informatie.</span><span class="sxs-lookup"><span data-stu-id="50d70-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="50d70-155">Dit kunnen bijvoorbeeld volumenamen, IP-adressen van apparaten en back-namen uit Hallo-logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="50d70-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50d70-156">U kunt alleen een ondersteuningspakket die is gegenereerd via Windows PowerShell voor StorSimple bewerken.</span><span class="sxs-lookup"><span data-stu-id="50d70-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="50d70-157">U kunt een pakket gemaakt in hello Azure-portal met Apparaatbeheer StorSimple-service niet bewerken.</span><span class="sxs-lookup"><span data-stu-id="50d70-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="50d70-158">tooedit ondersteuningspakket voordat u dit uploadt op Hallo van Microsoft Support-site, eerst ontsleutelen ondersteuningspakket Hallo Hallo bestanden bewerken en vervolgens opnieuw versleutelen.</span><span class="sxs-lookup"><span data-stu-id="50d70-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="50d70-159">Hallo stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="50d70-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="50d70-160">tooedit ondersteuningspakket in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="50d70-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="50d70-161">Genereren van een ondersteuningspakket zoals is beschreven, worden eerder in [toocreate ondersteuningspakket in Windows PowerShell voor StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="50d70-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="50d70-162">[Hallo script downloaden](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokaal op de client.</span><span class="sxs-lookup"><span data-stu-id="50d70-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="50d70-163">Hallo Windows PowerShell-module importeren.</span><span class="sxs-lookup"><span data-stu-id="50d70-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="50d70-164">Geef Hallo pad toohello lokale map waarin u Hallo script hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="50d70-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="50d70-165">tooimport hello module invoeren:</span><span class="sxs-lookup"><span data-stu-id="50d70-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="50d70-166">Alle Hallo-bestanden zijn *.aes* bestanden die worden gecomprimeerd en versleuteld.</span><span class="sxs-lookup"><span data-stu-id="50d70-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="50d70-167">Voer in toodecompress en ontsleutelen-bestanden:</span><span class="sxs-lookup"><span data-stu-id="50d70-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="50d70-168">Houd er rekening mee Hallo werkelijke bestandsextensies worden nu weergegeven voor alle Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="50d70-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="50d70-170">Wanneer u wordt gevraagd om de wachtwoordzin voor versleuteling hello, voert u Hallo wachtwoordzin op die u hebt gebruikt toen Hallo ondersteuningspakket is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50d70-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="50d70-171">Blader toohello-map met logboekbestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d70-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="50d70-172">Omdat het Hallo-logboekbestanden zijn nu gedecomprimeerd en ontsleuteld, wordt deze oorspronkelijke bestandsextensies hebben.</span><span class="sxs-lookup"><span data-stu-id="50d70-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="50d70-173">Deze bestanden tooremove eventuele klantspecifieke informatie, zoals volumenamen en IP-adressen van apparaten, wijzigen en Hallo bestanden op te slaan.</span><span class="sxs-lookup"><span data-stu-id="50d70-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="50d70-174">Sluit Hallo bestanden toocompress ze met gzip en versleuteld met AES-256.</span><span class="sxs-lookup"><span data-stu-id="50d70-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="50d70-175">Dit is van de snelheid en beveiliging bij het overbrengen van Hallo ondersteuningspakket via een netwerk.</span><span class="sxs-lookup"><span data-stu-id="50d70-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="50d70-176">toocompress en bestanden te versleutelen, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="50d70-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="50d70-178">Geef desgevraagd een wachtwoordzin voor versleuteling voor de gewijzigde ondersteuningspakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="50d70-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="50d70-179">Noteer de nieuwe wachtwoordzin hello, zodat u het met Microsoft Support delen kunt wanneer dit wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="50d70-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="50d70-180">Voorbeeld: Bestanden in een ondersteuningspakket op een wachtwoord beveiligde share bewerken</span><span class="sxs-lookup"><span data-stu-id="50d70-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="50d70-181">Hallo volgende voorbeeld ziet u hoe toodecrypt, bewerken en opnieuw versleutelen een ondersteuningspakket.</span><span class="sxs-lookup"><span data-stu-id="50d70-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="50d70-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50d70-182">Next steps</span></span>

* <span data-ttu-id="50d70-183">Meer informatie over Hallo [informatie verzameld in Hallo Support-pakket](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="50d70-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="50d70-184">Meer informatie over hoe te[gebruik ondersteuningspakketten en apparaat logboeken tootroubleshoot de implementatie van uw apparaten](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="50d70-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="50d70-185">Meer informatie over hoe te[gebruik Hallo StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="50d70-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

