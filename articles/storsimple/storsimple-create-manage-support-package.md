---
title: een StorSimple-ondersteuningspakket aaaCreate | Microsoft Docs
description: Ontdek hoe toocreate, ontsleutelen en bewerken van een ondersteuningspakket voor uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="4133a-103">Maken en beheren van een pakket StorSimple-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="4133a-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="4133a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4133a-104">Overview</span></span>
<span data-ttu-id="4133a-105">Een StorSimple-ondersteuningspakket is een mechanisme voor eenvoudig te gebruiken dat alle relevante logboeken tooassist Microsoft Support verzamelt bij het oplossen van eventuele problemen StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="4133a-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="4133a-106">Hallo zijn verzamelde logboeken versleuteld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="4133a-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="4133a-107">Deze zelfstudie bevat stapsgewijze instructies toocreate en Hallo ondersteuningspakket beheren.</span><span class="sxs-lookup"><span data-stu-id="4133a-107">This tutorial includes step-by-step instructions toocreate and manage hello support package.</span></span>

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="4133a-108">Maken en uploaden van een ondersteuningspakket in Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4133a-108">Create and upload a support package in hello Azure classic portal</span></span>
<span data-ttu-id="4133a-109">U kunt maken en uploaden van een site ondersteuning pakket toohello Microsoft Support via Hallo **onderhoud** pagina van de service Hallo in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4133a-109">You can create and upload a support package toohello Microsoft Support site through hello **Maintenance** page of hello service in hello Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4133a-110">Hallo uploaden vereist een sleutel voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="4133a-110">hello upload requires a support passkey.</span></span> <span data-ttu-id="4133a-111">De ondersteuningstechnicus dient dit tooyou in een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="4133a-111">Your support engineer should provide this tooyou in an email.</span></span>
> 
> 

<span data-ttu-id="4133a-112">Een versleutelde en gecomprimeerde support-pakket (.cab-bestand) is gemaakt en geüploade toohello ondersteuningssite.</span><span class="sxs-lookup"><span data-stu-id="4133a-112">An encrypted and compressed support package (.cab file) is created and uploaded toohello Support site.</span></span> <span data-ttu-id="4133a-113">Hallo ondersteuningstechnicus kan vervolgens dit pakket ophalen van Hallo ondersteuningssite voor Hallo probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="4133a-113">hello support engineer can then retrieve this package from hello Support site for troubleshooting hello issue.</span></span>

<span data-ttu-id="4133a-114">Hallo stappen te volgen in Hallo klassieke portal toocreate ondersteuningspakket uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4133a-114">Perform hello following steps in hello classic portal toocreate a support package.</span></span>

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="4133a-115">toocreate ondersteuningspakket in Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4133a-115">toocreate a support package in hello Azure classic portal</span></span>
1. <span data-ttu-id="4133a-116">Selecteer **apparaten** > **onderhoud**.</span><span class="sxs-lookup"><span data-stu-id="4133a-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="4133a-117">In Hallo **ondersteuningspakket** sectie **ondersteuningspakket maken en uploaden**.</span><span class="sxs-lookup"><span data-stu-id="4133a-117">In hello **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="4133a-118">In Hallo **ondersteuningspakket maken en uploaden** dialoogvenster vak, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="4133a-118">In hello **Create and upload support package** dialog box, do hello following:</span></span>
   
    ![Ondersteuningspakket maken](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="4133a-120">In Hallo **ondersteuning sleutel** tekst Voer Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="4133a-120">In hello **Support Passkey** text box, enter hello passkey.</span></span> <span data-ttu-id="4133a-121">De ondersteuningstechnicus van Microsoft het beste deze sleutel tooyou in e-mailbericht verzenden.</span><span class="sxs-lookup"><span data-stu-id="4133a-121">Your Microsoft support engineer should send this passkey tooyou in email.</span></span>
   * <span data-ttu-id="4133a-122">Selecteer Hallo selectievakje tooprovide toestemming tooautomatically uploaden Hallo ondersteuning pakket toohello Microsoft Support-site.</span><span class="sxs-lookup"><span data-stu-id="4133a-122">Select hello check box tooprovide consent tooautomatically upload hello support package toohello Microsoft Support site.</span></span>
   * <span data-ttu-id="4133a-123">Klik op het vinkje Hallo</span><span class="sxs-lookup"><span data-stu-id="4133a-123">Click hello check icon</span></span> ![Vinkje](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="4133a-125">.</span><span class="sxs-lookup"><span data-stu-id="4133a-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="4133a-126">Handmatig een ondersteuningspakket maken</span><span class="sxs-lookup"><span data-stu-id="4133a-126">Manually create a support package</span></span>
<span data-ttu-id="4133a-127">In sommige gevallen moet u toomanually Hallo ondersteuningspakket via Windows PowerShell voor StorSimple maken.</span><span class="sxs-lookup"><span data-stu-id="4133a-127">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="4133a-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4133a-128">For example:</span></span>

* <span data-ttu-id="4133a-129">Als u tooremove gevoelige informatie van uw logboek bestanden voorafgaande toosharing met Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="4133a-129">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="4133a-130">Als u problemen bij het uploaden van Hallo pakket vanwege tooconnectivity problemen ondervindt.</span><span class="sxs-lookup"><span data-stu-id="4133a-130">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="4133a-131">U kunt uw handmatig gegenereerde ondersteuningspakket delen met Microsoft Support via e-mail.</span><span class="sxs-lookup"><span data-stu-id="4133a-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="4133a-132">Volgende stappen toocreate ondersteuningspakket in Windows PowerShell voor StorSimple Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4133a-132">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="4133a-133">toocreate ondersteuningspakket in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="4133a-133">toocreate a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="4133a-134">toostart een Windows PowerShell-sessie als administrator op Hallo externe computer die is gebruikt tooconnect tooyour StorSimple-apparaat, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4133a-134">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="4133a-135">In de Windows PowerShell-sessie Hallo verbinden toohello SSAdmin Console van uw apparaat:</span><span class="sxs-lookup"><span data-stu-id="4133a-135">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="4133a-136">Voer het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="4133a-136">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="4133a-137">Voer het beheerderswachtwoord van uw apparaat Hallo in het dialoogvenster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4133a-137">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="4133a-138">Hallo standaardwachtwoord is:</span><span class="sxs-lookup"><span data-stu-id="4133a-138">hello default password is:</span></span>
     
      `Password1`
     
      ![In het dialoogvenster van PowerShell-referentie](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="4133a-140">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="4133a-140">Select **OK**.</span></span>
   * <span data-ttu-id="4133a-141">Voer het volgende achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="4133a-141">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="4133a-142">Voer de juiste opdracht Hallo in Hallo-sessie die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4133a-142">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="4133a-143">Voer voor netwerkshares die beveiligd met een wachtwoord zijn:</span><span class="sxs-lookup"><span data-stu-id="4133a-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="4133a-144">U wordt gevraagd om een wachtwoord, een pad toohello gedeelde netwerkmap en een wachtwoordzin voor versleuteling (omdat het ondersteuningspakket Hallo is versleuteld).</span><span class="sxs-lookup"><span data-stu-id="4133a-144">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="4133a-145">Een ondersteuningspakket wordt vervolgens gemaakt in de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="4133a-145">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="4133a-146">Voor shares die niet beveiligd met een wachtwoord zijn, hoeft u niet Hallo `-Credential` parameter.</span><span class="sxs-lookup"><span data-stu-id="4133a-146">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="4133a-147">Voer de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4133a-147">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="4133a-148">Hallo ondersteuningspakket is gemaakt voor beide domeincontrollers in Hallo opgegeven gedeelde netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="4133a-148">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="4133a-149">Het is een versleutelde, gecomprimeerd bestand dat kan worden verzonden tooMicrosoft ondersteuning voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="4133a-149">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="4133a-150">Zie voor meer informatie [contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="4133a-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="4133a-151">Hallo Export HcsSupportPackage cmdlet-parameters</span><span class="sxs-lookup"><span data-stu-id="4133a-151">hello Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="4133a-152">U kunt Hallo na Hallo Export HcsSupportPackage cmdlet-parameters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4133a-152">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="4133a-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="4133a-153">Parameter</span></span> | <span data-ttu-id="4133a-154">Vereiste/optionele</span><span class="sxs-lookup"><span data-stu-id="4133a-154">Required/Optional</span></span> | <span data-ttu-id="4133a-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4133a-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="4133a-156">Vereist</span><span class="sxs-lookup"><span data-stu-id="4133a-156">Required</span></span> |<span data-ttu-id="4133a-157">Gebruik tooprovide Hallo locatie van Hallo gedeelde netwerkmap in welke Hallo ondersteuningspakket wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="4133a-157">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="4133a-158">Vereist</span><span class="sxs-lookup"><span data-stu-id="4133a-158">Required</span></span> |<span data-ttu-id="4133a-159">Gebruik tooprovide een wachtwoordzin toohelp Hallo ondersteuningspakket versleutelen.</span><span class="sxs-lookup"><span data-stu-id="4133a-159">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="4133a-160">Optioneel</span><span class="sxs-lookup"><span data-stu-id="4133a-160">Optional</span></span> |<span data-ttu-id="4133a-161">Gebruik toosupply toegangsreferenties voor Hallo gedeelde netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="4133a-161">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="4133a-162">Optioneel</span><span class="sxs-lookup"><span data-stu-id="4133a-162">Optional</span></span> |<span data-ttu-id="4133a-163">Gebruik tooskip Hallo versleuteling wachtwoordzin bevestigen.</span><span class="sxs-lookup"><span data-stu-id="4133a-163">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="4133a-164">Optioneel</span><span class="sxs-lookup"><span data-stu-id="4133a-164">Optional</span></span> |<span data-ttu-id="4133a-165">Gebruik toospecify een map onder *pad* in welke ondersteuning Hallo pakket wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="4133a-165">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="4133a-166">Hallo standaard is [apparaatnaam]-[huidige datum en time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="4133a-166">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="4133a-167">Optioneel</span><span class="sxs-lookup"><span data-stu-id="4133a-167">Optional</span></span> |<span data-ttu-id="4133a-168">Geef als **Cluster** (standaard) toocreate ondersteuningspakket voor beide domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="4133a-168">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="4133a-169">Geef desgewenst kunt u een pakket toocreate alleen voor de huidige controller Hallo **Controller**.</span><span class="sxs-lookup"><span data-stu-id="4133a-169">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="4133a-170">Een ondersteuningspakket bewerken</span><span class="sxs-lookup"><span data-stu-id="4133a-170">Edit a support package</span></span>
<span data-ttu-id="4133a-171">Nadat u een ondersteuningspakket hebt gegenereerd, moet u mogelijk tooedit Hallo pakket tooremove gevoelige informatie.</span><span class="sxs-lookup"><span data-stu-id="4133a-171">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="4133a-172">Dit kunnen bijvoorbeeld volumenamen, IP-adressen van apparaten en back-namen uit Hallo-logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="4133a-172">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4133a-173">U kunt alleen een ondersteuningspakket die is gegenereerd via Windows PowerShell voor StorSimple bewerken.</span><span class="sxs-lookup"><span data-stu-id="4133a-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="4133a-174">U kunt een pakket gemaakt in de klassieke Azure-portal met de StorSimple Manager-service Hallo niet bewerken.</span><span class="sxs-lookup"><span data-stu-id="4133a-174">You can't edit a package created in hello Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="4133a-175">tooedit ondersteuningspakket voordat u dit uploadt op Hallo van Microsoft Support-site, eerst ontsleutelen ondersteuningspakket Hallo Hallo bestanden bewerken en vervolgens opnieuw versleutelen.</span><span class="sxs-lookup"><span data-stu-id="4133a-175">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="4133a-176">Hallo stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4133a-176">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="4133a-177">tooedit ondersteuningspakket in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="4133a-177">tooedit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="4133a-178">Genereren van een ondersteuningspakket zoals is beschreven, worden eerder in [toocreate ondersteuningspakket in Windows PowerShell voor StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="4133a-178">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="4133a-179">[Hallo script downloaden](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokaal op de client.</span><span class="sxs-lookup"><span data-stu-id="4133a-179">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="4133a-180">Hallo Windows PowerShell-module importeren.</span><span class="sxs-lookup"><span data-stu-id="4133a-180">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="4133a-181">Geef Hallo pad toohello lokale map waarin u Hallo script hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="4133a-181">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="4133a-182">tooimport hello module invoeren:</span><span class="sxs-lookup"><span data-stu-id="4133a-182">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="4133a-183">Alle Hallo-bestanden zijn *.aes* bestanden die worden gecomprimeerd en versleuteld.</span><span class="sxs-lookup"><span data-stu-id="4133a-183">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="4133a-184">Voer in toodecompress en ontsleutelen-bestanden:</span><span class="sxs-lookup"><span data-stu-id="4133a-184">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="4133a-185">Houd er rekening mee Hallo werkelijke bestandsextensies worden nu weergegeven voor alle Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="4133a-185">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="4133a-187">Wanneer u wordt gevraagd om de wachtwoordzin voor versleuteling hello, voert u Hallo wachtwoordzin op die u hebt gebruikt toen Hallo ondersteuningspakket is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4133a-187">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="4133a-188">Blader toohello-map met logboekbestanden Hallo.</span><span class="sxs-lookup"><span data-stu-id="4133a-188">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="4133a-189">Omdat het Hallo-logboekbestanden zijn nu gedecomprimeerd en ontsleuteld, wordt deze oorspronkelijke bestandsextensies hebben.</span><span class="sxs-lookup"><span data-stu-id="4133a-189">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="4133a-190">Deze bestanden tooremove eventuele klantspecifieke informatie, zoals volumenamen en IP-adressen van apparaten, wijzigen en Hallo bestanden op te slaan.</span><span class="sxs-lookup"><span data-stu-id="4133a-190">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="4133a-191">Sluit Hallo bestanden toocompress ze met gzip en versleuteld met AES-256.</span><span class="sxs-lookup"><span data-stu-id="4133a-191">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="4133a-192">Dit is van de snelheid en beveiliging bij het overbrengen van Hallo ondersteuningspakket via een netwerk.</span><span class="sxs-lookup"><span data-stu-id="4133a-192">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="4133a-193">toocompress en bestanden te versleutelen, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4133a-193">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="4133a-195">Geef desgevraagd een wachtwoordzin voor versleuteling voor de gewijzigde ondersteuningspakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="4133a-195">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="4133a-196">Noteer de nieuwe wachtwoordzin hello, zodat u het met Microsoft Support delen kunt wanneer dit wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="4133a-196">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="4133a-197">Voorbeeld: Bestanden in een ondersteuningspakket op een wachtwoord beveiligde share bewerken</span><span class="sxs-lookup"><span data-stu-id="4133a-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="4133a-198">Hallo volgende voorbeeld ziet u hoe toodecrypt, bewerken en opnieuw versleutelen een ondersteuningspakket.</span><span class="sxs-lookup"><span data-stu-id="4133a-198">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4133a-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4133a-199">Next steps</span></span>
* <span data-ttu-id="4133a-200">Meer informatie over hoe te[gebruik ondersteuningspakketten en apparaat logboeken tootroubleshoot de implementatie van uw apparaten](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="4133a-200">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="4133a-201">Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4133a-201">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

