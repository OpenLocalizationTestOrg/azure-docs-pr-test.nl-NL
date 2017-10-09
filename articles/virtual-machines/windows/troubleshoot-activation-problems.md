---
title: aaaTroubleshoot Windows virtuele machine activeringsproblemen in Azure | Microsoft Docs
description: Hallo bevat stappen voor het oplossen van problemen met Windows virtuele machine activation in Azure oplossen
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Windows Azure virtuele machine activation problemen oplossen

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Als u problemen hebt bij het activeren van Windows Azure virtuele machine (VM) die van een aangepaste installatiekopie wordt gemaakt, kunt u Hallo informatie in dit document tootroubleshoot Hallo probleem. 

## <a name="symptom"></a>Symptoom

Wanneer u een Windows Azure VM tooactivate, u een foutbericht ontvangt bericht lijkt op Hallo voorbeeld te volgen:

**Fout: 0xC004F074 Hallo Software LicensingService gerapporteerd dat die Hallo-computer kan niet worden geactiveerd. Er is geen ManagementService KMS (Key) kan worden bereikt. Zie Hallo toepassingslogboek voor meer informatie.**

## <a name="cause"></a>Oorzaak
In het algemeen optreden activeringsproblemen van de virtuele machine van Azure als virtuele machine van Windows hello niet is geconfigureerd met juiste Installatiecode voor KMS-client met behulp van Hallo of Hallo Windows VM heeft een connectiviteit probleem toohello Azure KMS-service (kms.core.windows.net, poort 1668). 

## <a name="solution"></a>Oplossing

>[!NOTE]
>Als u een site-naar-site-VPN en geforceerde tunneling, Zie [gebruik Azure aangepaste routes tooenable KMS-activering met geforceerde tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>Als u ExpressRoute gebruikt en u hebt een standaardroute gepubliceerd, Zie [Azure VM mislukken tooactivate via ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>Stap 1 configureren Hallo juiste KMS-clientinstallatiecode (voor Windows Server 2016 en Windows Server 2012 R2)

Hallo virtuele machine die wordt gemaakt van een aangepaste installatiekopie van Windows Server 2016 of Windows Server 2012 R2, moet u Hallo juiste KMS-clientinstallatiecode voor Hallo VM configureren.

Deze stap is niet van toepassing tooWindows 2012 of Windows 2008 R2. Hallo activering automatisering van virtuele Machine (AVMA) functie, wordt alleen ondersteund door Windows Server 2016 en Windows Server 2012 R2 wordt gebruikt.

1. Voer **slmgr.vbs/dlv** bij een opdrachtprompt met verhoogde bevoegdheden. Hallo beschrijvingswaarde in Hallo uitvoer controleren en Ga na of deze is gemaakt vanuit retail (RETAIL kanaal) of (VOLUME_KMSCLIENT) volume license-media:
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Als **slmgr.vbs/dlv** detailhandel, uitvoeren van opdrachten tooset Hallo na Hallo toont [Installatiecode voor KMS-client](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) voor Hallo-versie van Windows Server wordt gebruikt en gedwongen tooretry activering: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Bijvoorbeeld: voor Windows Server 2016 Datacenter, moet u Hallo volgende opdracht uitvoeren:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>Stap 2 Controleer Hallo de verbinding tussen Hallo VM en Azure KMS-service

1. Downloaden en uitpakken van Hallo [psping om](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) hulpprogramma tooa lokale map in Hallo virtuele machine die niet worden geactiveerd. 

2. Ga tooStart, zoeken op Windows PowerShell, met de rechtermuisknop op Windows PowerShell en selecteer als administrator uitvoeren.

3. Zorg ervoor dat de VM bevindt zich Hallo toouse Hallo juiste Azure KMS-server geconfigureerd. toodo dit de volgende opdracht uitvoeren:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    Hallo-opdracht moet worden geretourneerd: Key Management Service-computernaam tookms.core.windows.net:1688 is ingesteld.

4. Controleer of met behulp van psping om dat er verbinding toohello KMS-server. Toohello map waar u Hallo Pstools.zip downloaden uitgepakt switch en voer vervolgens de volgende Hallo:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Zorg ervoor dat u ziet in Hallo seconde laatste regel van het Hallo-uitvoer wordt: verzonden = 4, ontvangen = 4, verloren = 0 (0% verlies).

  Als verloren is groter dan 0 (nul), is Hallo VM heeft geen connectiviteit toohello KMS-server. In deze situatie is als hello VM bevindt zich in een virtueel netwerk en heeft een aangepaste DNS-server opgegeven, moet u ervoor zorgen dat DNS-server kunnen tooresolve kms.core.windows.net. Of wijzigen van Hallo DNS-server tooone die kms.core.windows.net is opgelost.

  U ziet dat als u alle DNS-servers uit een virtueel netwerk verwijderen, virtuele machines van Azure interne DNS-service gebruiken. Deze service kunt kms.core.windows.net oplossen.
  
Controleer ook dat of Hallo Gast de firewall is niet geconfigureerd op een wijze waarbij activation pogingen blokkeren.

5. Nadat u tookms.core.windows.net van geslaagde verbinding verifieert, Hallo volgen die opdrachtprompt van Windows PowerShell-opdracht worden uitgevoerd. Met deze opdracht wordt activering geprobeerd meerdere keren.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Een geslaagde activering wordt informatie Hallo volgende strekking weergegeven:

**Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) activeren... Product is geactiveerd.**

## <a name="faq"></a>Veelgestelde vragen 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Ik heb gemaakt Hallo Windows Server 2016 uit Azure Marketplace. Moet ik tooconfigure KMS-code voor het activeren van Windows Server 2016 Hallo? 
 
Nee. Hallo-installatiekopie in Azure Marketplace heeft Hallo juiste KMS-clientinstallatiecode al is geconfigureerd. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Windows activation werk Hallo dezelfde manier ongeacht als Hallo VM van Azure hybride gebruik voordeel (HUB) of niet gebruikmaakt? 
 
Ja. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Wat gebeurt er als Windows-activering is verlopen? 
 
Wanneer Hallo respijtperiode verlopen en Windows is nog niet geactiveerd, wordt Windows Server 2008 R2 en latere versies van Windows extra meldingen over het activeren van weergeven. Hallo bureaubladachtergrond blijft zwart en Windows Update wordt geïnstalleerd, beveiliging en alleen essentiële updates, maar niet optionele updates. Zie Hallo meldingen sectie onderin Hallo Hallo [licentieverlening voorwaarden](http://technet.microsoft.com/en-us/library/ff793403.aspx) pagina.   

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
