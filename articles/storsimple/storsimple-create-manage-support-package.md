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
# <a name="create-and-manage-a-storsimple-support-package"></a>Maken en beheren van een pakket StorSimple-ondersteuning
## <a name="overview"></a>Overzicht
Een StorSimple-ondersteuningspakket is een mechanisme voor eenvoudig te gebruiken dat alle relevante logboeken tooassist Microsoft Support verzamelt bij het oplossen van eventuele problemen StorSimple-apparaat. Hallo zijn verzamelde logboeken versleuteld en gecomprimeerd.

Deze zelfstudie bevat stapsgewijze instructies toocreate en Hallo ondersteuningspakket beheren.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Maken en uploaden van een ondersteuningspakket in Hallo klassieke Azure-portal
U kunt maken en uploaden van een site ondersteuning pakket toohello Microsoft Support via Hallo **onderhoud** pagina van de service Hallo in Hallo klassieke Azure-portal.

> [!NOTE]
> Hallo uploaden vereist een sleutel voor ondersteuning. De ondersteuningstechnicus dient dit tooyou in een e-mailbericht.
> 
> 

Een versleutelde en gecomprimeerde support-pakket (.cab-bestand) is gemaakt en geüploade toohello ondersteuningssite. Hallo ondersteuningstechnicus kan vervolgens dit pakket ophalen van Hallo ondersteuningssite voor Hallo probleem op te lossen.

Hallo stappen te volgen in Hallo klassieke portal toocreate ondersteuningspakket uitvoeren.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate ondersteuningspakket in Hallo klassieke Azure-portal
1. Selecteer **apparaten** > **onderhoud**.
2. In Hallo **ondersteuningspakket** sectie **ondersteuningspakket maken en uploaden**.
3. In Hallo **ondersteuningspakket maken en uploaden** dialoogvenster vak, Hallo te volgen:
   
    ![Ondersteuningspakket maken](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * In Hallo **ondersteuning sleutel** tekst Voer Hallo-sleutel. De ondersteuningstechnicus van Microsoft het beste deze sleutel tooyou in e-mailbericht verzenden.
   * Selecteer Hallo selectievakje tooprovide toestemming tooautomatically uploaden Hallo ondersteuning pakket toohello Microsoft Support-site.
   * Klik op het vinkje Hallo ![Vinkje](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Handmatig een ondersteuningspakket maken
In sommige gevallen moet u toomanually Hallo ondersteuningspakket via Windows PowerShell voor StorSimple maken. Bijvoorbeeld:

* Als u tooremove gevoelige informatie van uw logboek bestanden voorafgaande toosharing met Microsoft Support.
* Als u problemen bij het uploaden van Hallo pakket vanwege tooconnectivity problemen ondervindt.

U kunt uw handmatig gegenereerde ondersteuningspakket delen met Microsoft Support via e-mail. Volgende stappen toocreate ondersteuningspakket in Windows PowerShell voor StorSimple Hallo uitvoeren.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate ondersteuningspakket in Windows PowerShell voor StorSimple
1. toostart een Windows PowerShell-sessie als administrator op Hallo externe computer die is gebruikt tooconnect tooyour StorSimple-apparaat, Voer Hallo volgende opdracht:
   
    `Start PowerShell`
2. In de Windows PowerShell-sessie Hallo verbinden toohello SSAdmin Console van uw apparaat:
   
   * Voer het volgende achter de opdrachtprompt Hallo:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * Voer het beheerderswachtwoord van uw apparaat Hallo in het dialoogvenster dat wordt geopend. Hallo standaardwachtwoord is:
     
      `Password1`
     
      ![In het dialoogvenster van PowerShell-referentie](./media/storsimple-create-manage-support-package/IC740962.png)
   * Selecteer **OK**.
   * Voer het volgende achter de opdrachtprompt Hallo:
     
      `Enter-PSSession $MS`
3. Voer de juiste opdracht Hallo in Hallo-sessie die wordt geopend.
   
   * Voer voor netwerkshares die beveiligd met een wachtwoord zijn:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       U wordt gevraagd om een wachtwoord, een pad toohello gedeelde netwerkmap en een wachtwoordzin voor versleuteling (omdat het ondersteuningspakket Hallo is versleuteld). Een ondersteuningspakket wordt vervolgens gemaakt in de opgegeven map Hallo.
   * Voor shares die niet beveiligd met een wachtwoord zijn, hoeft u niet Hallo `-Credential` parameter. Voer de volgende Hallo:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       Hallo ondersteuningspakket is gemaakt voor beide domeincontrollers in Hallo opgegeven gedeelde netwerkmap. Het is een versleutelde, gecomprimeerd bestand dat kan worden verzonden tooMicrosoft ondersteuning voor het oplossen van problemen. Zie voor meer informatie [contact opnemen met Microsoft ondersteuning](storsimple-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>Hallo Export HcsSupportPackage cmdlet-parameters
U kunt Hallo na Hallo Export HcsSupportPackage cmdlet-parameters gebruiken.

| Parameter | Vereiste/optionele | Beschrijving |
| --- | --- | --- |
| `-Path` |Vereist |Gebruik tooprovide Hallo locatie van Hallo gedeelde netwerkmap in welke Hallo ondersteuningspakket wordt geplaatst. |
| `-EncryptionPassphrase` |Vereist |Gebruik tooprovide een wachtwoordzin toohelp Hallo ondersteuningspakket versleutelen. |
| `-Credential` |Optioneel |Gebruik toosupply toegangsreferenties voor Hallo gedeelde netwerkmap. |
| `-Force` |Optioneel |Gebruik tooskip Hallo versleuteling wachtwoordzin bevestigen. |
| `-PackageTag` |Optioneel |Gebruik toospecify een map onder *pad* in welke ondersteuning Hallo pakket wordt geplaatst. Hallo standaard is [apparaatnaam]-[huidige datum en time:yyyy-MM-dd-HH-mm-ss]. |
| `-Scope` |Optioneel |Geef als **Cluster** (standaard) toocreate ondersteuningspakket voor beide domeincontrollers. Geef desgewenst kunt u een pakket toocreate alleen voor de huidige controller Hallo **Controller**. |

## <a name="edit-a-support-package"></a>Een ondersteuningspakket bewerken
Nadat u een ondersteuningspakket hebt gegenereerd, moet u mogelijk tooedit Hallo pakket tooremove gevoelige informatie. Dit kunnen bijvoorbeeld volumenamen, IP-adressen van apparaten en back-namen uit Hallo-logboekbestanden.

> [!IMPORTANT]
> U kunt alleen een ondersteuningspakket die is gegenereerd via Windows PowerShell voor StorSimple bewerken. U kunt een pakket gemaakt in de klassieke Azure-portal met de StorSimple Manager-service Hallo niet bewerken.
> 
> 

tooedit ondersteuningspakket voordat u dit uploadt op Hallo van Microsoft Support-site, eerst ontsleutelen ondersteuningspakket Hallo Hallo bestanden bewerken en vervolgens opnieuw versleutelen. Hallo stappen uitvoeren.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit ondersteuningspakket in Windows PowerShell voor StorSimple
1. Genereren van een ondersteuningspakket zoals is beschreven, worden eerder in [toocreate ondersteuningspakket in Windows PowerShell voor StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Hallo script downloaden](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokaal op de client.
3. Hallo Windows PowerShell-module importeren. Geef Hallo pad toohello lokale map waarin u Hallo script hebt gedownload. tooimport hello module invoeren:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Alle Hallo-bestanden zijn *.aes* bestanden die worden gecomprimeerd en versleuteld. Voer in toodecompress en ontsleutelen-bestanden:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Houd er rekening mee Hallo werkelijke bestandsextensies worden nu weergegeven voor alle Hallo-bestanden.
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-create-manage-support-package/IC750706.png)
5. Wanneer u wordt gevraagd om de wachtwoordzin voor versleuteling hello, voert u Hallo wachtwoordzin op die u hebt gebruikt toen Hallo ondersteuningspakket is gemaakt.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Blader toohello-map met logboekbestanden Hallo. Omdat het Hallo-logboekbestanden zijn nu gedecomprimeerd en ontsleuteld, wordt deze oorspronkelijke bestandsextensies hebben. Deze bestanden tooremove eventuele klantspecifieke informatie, zoals volumenamen en IP-adressen van apparaten, wijzigen en Hallo bestanden op te slaan.
7. Sluit Hallo bestanden toocompress ze met gzip en versleuteld met AES-256. Dit is van de snelheid en beveiliging bij het overbrengen van Hallo ondersteuningspakket via een netwerk. toocompress en bestanden te versleutelen, voert u de volgende Hallo:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Voor ondersteuningspakket bewerken](./media/storsimple-create-manage-support-package/IC750707.png)
8. Geef desgevraagd een wachtwoordzin voor versleuteling voor de gewijzigde ondersteuningspakket Hallo.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Noteer de nieuwe wachtwoordzin hello, zodat u het met Microsoft Support delen kunt wanneer dit wordt aangevraagd.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Voorbeeld: Bestanden in een ondersteuningspakket op een wachtwoord beveiligde share bewerken
Hallo volgende voorbeeld ziet u hoe toodecrypt, bewerken en opnieuw versleutelen een ondersteuningspakket.

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

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[gebruik ondersteuningspakketten en apparaat logboeken tootroubleshoot de implementatie van uw apparaten](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Meer informatie over hoe te[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).

