---
title: Maken van een StorSimple-ondersteuningspakket | Microsoft Docs
description: Informatie over het maken, te ontsleutelen en te bewerken van een ondersteuningspakket voor uw StorSimple-apparaat.
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
ms.openlocfilehash: 32d20e7a8adcfc646c592213fe7395b87a93c985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="7a3d6-103">Maken en beheren van een pakket StorSimple-ondersteuning</span><span class="sxs-lookup"><span data-stu-id="7a3d6-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="7a3d6-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7a3d6-104">Overview</span></span>
<span data-ttu-id="7a3d6-105">Een StorSimple-ondersteuningspakket is een mechanisme voor eenvoudig te gebruiken dat alle relevante Logboeken om te helpen bij het oplossen van eventuele problemen StorSimple-apparaat met Microsoft Support verzamelt.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="7a3d6-106">De logboeken van de verzamelde zijn versleuteld en gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="7a3d6-107">Deze zelfstudie bevat stapsgewijze instructies voor het maken en beheren van het ondersteuningspakket.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-107">This tutorial includes step-by-step instructions to create and manage the support package.</span></span>

## <a name="create-and-upload-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="7a3d6-108">Maken en uploaden van een ondersteuningspakket in de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="7a3d6-108">Create and upload a support package in the Azure classic portal</span></span>
<span data-ttu-id="7a3d6-109">U kunt maken en een ondersteuningspakket uploaden naar de website van Microsoft Support via de **onderhoud** pagina van de service in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-109">You can create and upload a support package to the Microsoft Support site through the **Maintenance** page of the service in the Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7a3d6-110">Het uploaden is een sleutel ondersteuning vereist.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-110">The upload requires a support passkey.</span></span> <span data-ttu-id="7a3d6-111">De ondersteuningstechnicus dient dit voor u in een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-111">Your support engineer should provide this to you in an email.</span></span>
> 
> 

<span data-ttu-id="7a3d6-112">Een versleutelde en gecomprimeerde support-pakket (.cab-bestand) is gemaakt en geüpload naar de site ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-112">An encrypted and compressed support package (.cab file) is created and uploaded to the Support site.</span></span> <span data-ttu-id="7a3d6-113">Vervolgens kan de ondersteuningstechnicus van dit pakket opgehaald van de site ondersteuning voor het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-113">The support engineer can then retrieve this package from the Support site for troubleshooting the issue.</span></span>

<span data-ttu-id="7a3d6-114">Voer de volgende stappen uit in de klassieke portal een ondersteuningspakket maken.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-114">Perform the following steps in the classic portal to create a support package.</span></span>

#### <a name="to-create-a-support-package-in-the-azure-classic-portal"></a><span data-ttu-id="7a3d6-115">Een ondersteuningspakket maken in de klassieke Azure portal</span><span class="sxs-lookup"><span data-stu-id="7a3d6-115">To create a support package in the Azure classic portal</span></span>
1. <span data-ttu-id="7a3d6-116">Selecteer **apparaten** > **onderhoud**.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="7a3d6-117">In de **ondersteuningspakket** sectie **ondersteuningspakket maken en uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-117">In the **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="7a3d6-118">In de **ondersteuningspakket maken en uploaden** dialoogvenster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-118">In the **Create and upload support package** dialog box, do the following:</span></span>
   
    ![Ondersteuningspakket maken](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="7a3d6-120">In de **ondersteuning sleutel** tekst en voer de sleutel.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-120">In the **Support Passkey** text box, enter the passkey.</span></span> <span data-ttu-id="7a3d6-121">De ondersteuningstechnicus Microsoft moet deze sleutel naar u verzenden via e-mail.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-121">Your Microsoft support engineer should send this passkey to you in email.</span></span>
   * <span data-ttu-id="7a3d6-122">Schakel het selectievakje in als u toestemming geven om automatisch de support-pakket te uploaden naar de website van Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-122">Select the check box to provide consent to automatically upload the support package to the Microsoft Support site.</span></span>
   * <span data-ttu-id="7a3d6-123">Klik op het vinkje</span><span class="sxs-lookup"><span data-stu-id="7a3d6-123">Click the check icon</span></span> ![Vinkje](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="7a3d6-125">.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="7a3d6-126">Handmatig een ondersteuningspakket maken</span><span class="sxs-lookup"><span data-stu-id="7a3d6-126">Manually create a support package</span></span>
<span data-ttu-id="7a3d6-127">In sommige gevallen moet u handmatig maken van het ondersteuningspakket via Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-127">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7a3d6-128">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-128">For example:</span></span>

* <span data-ttu-id="7a3d6-129">Als u wilt dat gevoelige gegevens verwijderen uit uw logboekbestanden vóór delen met Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-129">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="7a3d6-130">Als u problemen bij het uploaden van het pakket vanwege problemen met de netwerkverbinding ondervindt.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-130">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="7a3d6-131">U kunt uw handmatig gegenereerde ondersteuningspakket delen met Microsoft Support via e-mail.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="7a3d6-132">Voer de volgende stappen uit om een ondersteuningspakket maken in Windows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-132">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7a3d6-133">Een ondersteuningspakket maken in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="7a3d6-133">To create a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7a3d6-134">Voor het starten van een Windows PowerShell-sessie als een beheerder op de externe computer die verbinding maken met uw StorSimple-apparaat wordt gebruikt, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-134">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="7a3d6-135">Verbinding maken met de SSAdmin Console van uw apparaat in de Windows PowerShell-sessie:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-135">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="7a3d6-136">Voer het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-136">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="7a3d6-137">Voer het beheerderswachtwoord van uw apparaat in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-137">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="7a3d6-138">Het standaardwachtwoord is:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-138">The default password is:</span></span>
     
      `Password1`
     
      ![In het dialoogvenster van PowerShell-referentie](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="7a3d6-140">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-140">Select **OK**.</span></span>
   * <span data-ttu-id="7a3d6-141">Voer het volgende achter de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-141">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="7a3d6-142">Voer de juiste opdracht in de sessie wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-142">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="7a3d6-143">Voer voor netwerkshares die beveiligd met een wachtwoord zijn:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="7a3d6-144">U wordt gevraagd een wachtwoord, een pad naar de gedeelde netwerkmap en een wachtwoordzin voor versleuteling (omdat het ondersteuningspakket is versleuteld).</span><span class="sxs-lookup"><span data-stu-id="7a3d6-144">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="7a3d6-145">Een ondersteuningspakket wordt vervolgens in de opgegeven map gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-145">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="7a3d6-146">Voor shares die niet beveiligd met een wachtwoord zijn, hoeft u niet de `-Credential` parameter.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-146">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="7a3d6-147">Voer het volgende:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-147">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="7a3d6-148">Het ondersteuningspakket wordt gemaakt voor beide domeincontrollers in de opgegeven gedeelde netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-148">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="7a3d6-149">Het is een versleutelde, gecomprimeerd bestand dat kan worden verzonden naar Microsoft Support voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-149">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="7a3d6-150">Zie voor meer informatie [contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="7a3d6-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="7a3d6-151">De parameters van de cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="7a3d6-151">The Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="7a3d6-152">Met de cmdlet Export-HcsSupportPackage kunt u de volgende parameters.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-152">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="7a3d6-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="7a3d6-153">Parameter</span></span> | <span data-ttu-id="7a3d6-154">Vereiste/optionele</span><span class="sxs-lookup"><span data-stu-id="7a3d6-154">Required/Optional</span></span> | <span data-ttu-id="7a3d6-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7a3d6-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="7a3d6-156">Vereist</span><span class="sxs-lookup"><span data-stu-id="7a3d6-156">Required</span></span> |<span data-ttu-id="7a3d6-157">Gebruiken voor de locatie van de gedeelde netwerkmap waarin het ondersteuningspakket wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-157">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="7a3d6-158">Vereist</span><span class="sxs-lookup"><span data-stu-id="7a3d6-158">Required</span></span> |<span data-ttu-id="7a3d6-159">Gebruiken voor een wachtwoordzin in om u te helpen bij het versleutelen van het ondersteuningspakket.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-159">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="7a3d6-160">Optioneel</span><span class="sxs-lookup"><span data-stu-id="7a3d6-160">Optional</span></span> |<span data-ttu-id="7a3d6-161">Gebruik te voorzien van referenties voor toegang voor de gedeelde netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-161">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="7a3d6-162">Optioneel</span><span class="sxs-lookup"><span data-stu-id="7a3d6-162">Optional</span></span> |<span data-ttu-id="7a3d6-163">Gebruik voor de versleuteling wachtwoordzin bevestigingsstap overslaan.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-163">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="7a3d6-164">Optioneel</span><span class="sxs-lookup"><span data-stu-id="7a3d6-164">Optional</span></span> |<span data-ttu-id="7a3d6-165">Gebruiken om op te geven van een map onder *pad* in het ondersteuningspakket wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-165">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="7a3d6-166">De standaardwaarde is [apparaatnaam]-[huidige datum en time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="7a3d6-166">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="7a3d6-167">Optioneel</span><span class="sxs-lookup"><span data-stu-id="7a3d6-167">Optional</span></span> |<span data-ttu-id="7a3d6-168">Geef als **Cluster** (standaard) voor het maken van een ondersteuningspakket voor beide domeincontrollers.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-168">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="7a3d6-169">Als u maken van een pakket alleen voor de huidige controller wilt, geeft u **Controller**.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-169">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="7a3d6-170">Een ondersteuningspakket bewerken</span><span class="sxs-lookup"><span data-stu-id="7a3d6-170">Edit a support package</span></span>
<span data-ttu-id="7a3d6-171">Nadat u een ondersteuningspakket hebt gegenereerd, moet u mogelijk om te bewerken van het pakket om gevoelige informatie te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-171">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="7a3d6-172">Dit kunnen bijvoorbeeld volumenamen apparaat IP-adressen en namen van back-up van de logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-172">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a3d6-173">U kunt alleen een ondersteuningspakket die is gegenereerd via Windows PowerShell voor StorSimple bewerken.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="7a3d6-174">U kunt een pakket gemaakt in de klassieke Azure portal met de StorSimple Manager-service niet bewerken.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-174">You can't edit a package created in the Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="7a3d6-175">Ondersteuningspakket bewerken voordat u dit uploadt op de website Microsoft Support, het ondersteuningspakket met voor het eerst ontsleutelen, de bestanden bewerken en vervolgens opnieuw versleutelen.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-175">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="7a3d6-176">De volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-176">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7a3d6-177">Het bewerken van een ondersteuningspakket in Windows PowerShell voor StorSimple</span><span class="sxs-lookup"><span data-stu-id="7a3d6-177">To edit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7a3d6-178">Genereren van een ondersteuningspakket zoals is beschreven, worden eerder in [een ondersteuningspakket maken in Windows PowerShell voor StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="7a3d6-178">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="7a3d6-179">[Het script downloaden](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokaal op de client.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-179">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="7a3d6-180">Importeer de module Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-180">Import the Windows PowerShell module.</span></span> <span data-ttu-id="7a3d6-181">Geef het pad naar de lokale map waarin u het script hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-181">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="7a3d6-182">Geef voor het importeren van de module:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-182">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="7a3d6-183">Alle bestanden zijn *.aes* bestanden die worden gecomprimeerd en versleuteld.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-183">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="7a3d6-184">Decomprimeren en bestanden ontsleutelen, geeft u op:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-184">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="7a3d6-185">Houd er rekening mee dat de werkelijke bestandsextensies nu worden weergegeven voor alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-185">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="7a3d6-187">Wanneer u wordt gevraagd om de wachtwoordzin voor versleuteling, voert u de wachtwoordzin op die u hebt gebruikt toen u het ondersteuningspakket is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-187">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="7a3d6-188">Blader naar de map waarin de logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-188">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="7a3d6-189">Omdat de logboekbestanden worden nu gecomprimeerd en ontsleuteld, wordt deze oorspronkelijke bestandsextensies hebben.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-189">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="7a3d6-190">Deze bestanden wijzigt om klantspecifieke informatie, zoals volumenamen en IP-adressen van apparaten, verwijderen en de bestanden op te slaan.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-190">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="7a3d6-191">Sluit de bestanden om ze met gzip wordt gecomprimeerd en versleuteld met AES-256.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-191">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="7a3d6-192">Dit is van de snelheid en beveiliging bij het overbrengen van het ondersteuningspakket via een netwerk.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-192">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="7a3d6-193">Als u wilt comprimeren en bestanden te versleutelen, voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="7a3d6-193">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="7a3d6-195">Geef desgevraagd een wachtwoordzin voor versleuteling voor het ondersteuningspakket gewijzigde.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-195">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="7a3d6-196">Noteer de nieuwe wachtwoordzin, zodat u het met Microsoft Support delen kunt wanneer dit wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-196">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="7a3d6-197">Voorbeeld: Bestanden in een ondersteuningspakket op een wachtwoord beveiligde share bewerken</span><span class="sxs-lookup"><span data-stu-id="7a3d6-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="7a3d6-198">Het volgende voorbeeld laat zien hoe ontsleutelen, bewerken en opnieuw versleutelen een ondersteuningspakket.</span><span class="sxs-lookup"><span data-stu-id="7a3d6-198">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="7a3d6-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a3d6-199">Next steps</span></span>
* <span data-ttu-id="7a3d6-200">Meer informatie over hoe [ondersteuningspakketten en apparaatlogboeken gebruiken om op te lossen de implementatie van uw apparaten](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7a3d6-200">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="7a3d6-201">Meer informatie over hoe [de StorSimple Manager-service gebruiken voor het beheren van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="7a3d6-201">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

