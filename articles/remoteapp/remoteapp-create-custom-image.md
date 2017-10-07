---
title: aaaHow toocreate de installatiekopie van een aangepaste sjabloon voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toocreate een aangepaste sjabloon voor Azure RemoteApp image. Deze sjabloon kunt u met een hybride of de cloud-verzameling.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Hoe toocreate een aangepaste sjabloon voor Azure RemoteApp image
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp gebruikt een Windows Server 2012 R2 sjabloon installatiekopie toohost alle Hallo-programma's die u wilt de tooshare met uw gebruikers. toocreate een aangepaste installatiekopie van de RemoteApp-sjabloon, kunt u beginnen met een bestaande installatiekopie of een nieuwe maken. 

> [!TIP]
> Wist u dat u kunt een installatiekopie van het maken van een Azure VM? True verhaal en deze geknipt omlaag op Hallo hoeveelheid tijd vergt tooimport Hallo installatiekopie. Bekijk Hallo stappen [hier](remoteapp-image-on-azurevm.md).
> 
> 

Hallo-vereisten voor het Hallo-installatiekopie die kan worden geüpload voor gebruik met Azure RemoteApp zijn:

* Afbeeldingsgrootte Hallo moet een veelvoud van MB. Als u een installatiekopie die is geen exacte veelvoud tooupload probeert, mislukt de Hallo uploaden.
* Hallo afbeeldingsformaat moet 127 GB of kleiner.
* Dit moet een VHD-bestand (VHDX-bestanden [Hyper-V virtuele harde schijven] worden momenteel niet ondersteund).
* Hallo VHD mag geen virtuele machines van generatie 2.
* Hallo VHD kan een vaste grootte of dynamisch uitbreidbare zijn. Een dynamisch uitbreidbare VHD wordt aanbevolen omdat duurt het minder tijd tooupload tooAzure dan een vaste grootte VHD-bestand.
* Hallo-schijf moet worden geïnitialiseerd met Hallo Master Boot Record (MBR) partitionering stijl. Hallo partitiestijl van GUID partition table (GPT) wordt niet ondersteund.
* Hallo VHD moet één installatie van Windows Server 2012 R2 bevatten. Meerdere volumes, maar slechts één met een installatie van Windows kan bevatten.
* Hallo Remote Desktop Session Host (RDSH)-functie en de functie Bureaubladervaring Hallo moeten worden geïnstalleerd.
* Hallo Remote Desktop Connection Broker-rol moet *niet* worden geïnstalleerd.
* Hallo Encrypting File System (EFS) moet worden uitgeschakeld.
* Hallo-installatiekopie moet SYSPREPed met Hallo parameters **/oobe / generalize/shutdown** (gebruikt Hallo **/mode:vm** parameter).
* Uploaden van uw VHD van een keten van de momentopname wordt niet ondersteund.

**Voordat u begint**

U moet toodo Hallo volgende voordat het Hallo-service maken:

* [Aanmelden](https://azure.microsoft.com/services/remoteapp/) voor RemoteApp.
* Een gebruikersaccount in Active Directory-toouse als Hallo RemoteApp-service-account maken. Hallo-machtigingen voor dit account beperken zodat deze alleen worden toegevoegd aan machines toohello domein. Zie [Azure Active Directory configureren voor RemoteApp](remoteapp-ad.md) voor meer informatie.
* Informatie verzamelen over uw on-premises netwerk: IP-adres informatie en details van VPN-apparaat.
* Hallo installeren [Azure PowerShell](/powershell/azure/overview) module.
* Informatie over het Hallo-gebruikers die u toegang tot toogrant wilt verzamelen. Dit kan zijn Microsoft-accountgegevens of Active Directory work accountgegevens voor gebruikers.

## <a name="create-a-template-image"></a>De sjablooninstallatiekopie van een maken
Dit zijn de Hallo hoog niveau stappen toocreate een nieuwe sjablooninstallatiekopie maken:

1. Ga naar een DVD voor Windows Server 2012 R2-Update- of ISO-installatiekopie.
2. Maak een VHD-bestand.
3. Installeer Windows Server 2012 R2.
4. Hallo Remote Desktop Session Host (RDSH)-functie en de functie Bureaubladervaring Hallo installeren.
5. Installeer aanvullende functies die nodig zijn voor uw toepassingen.
6. Installeer en configureer uw toepassingen. toomake delen apps eenvoudiger, voeg apps of programma's die u wilt dat tooshare toohello **Start** menu van de afbeelding hello, in het bijzonder in **%systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programma 's.
7. Geen aanvullende Windows-configuraties die nodig zijn voor uw toepassingen uitvoeren.
8. Hallo Encrypting File System (EFS) uitschakelen.
9. **VEREIST:** tooWindows Update gaat en installeert u alle belangrijke updates.
10. SYSPREP Hallo-afbeelding.

Hallo gedetailleerde stappen voor het maken van een nieuwe installatiekopie is zijn:

1. Ga naar een DVD voor Windows Server 2012 R2-Update- of ISO-installatiekopie.
2. Een VHD-bestand maken met behulp van Schijfbeheer.
   
   1. Start Schijfbeheer (diskmgmt.msc).
   2. Maak een VHD dynamisch uitbreidbare 40 GB of meer in grootte. (Schatting Hallo hoeveelheid ruimte die nodig zijn voor Windows, uw toepassingen en aanpassingen. WindowsServer met Hallo RDSH-rol en de functie Bureaubladervaring geïnstalleerd wordt ongeveer 10 GB aan ruimte vereist).
      
      1. Klik op **actie > VHD maken**.
      2. Geef de locatie van de hello, grootte en VHD-indeling. Selecteer **dynamisch uitbreidbare**, en klik vervolgens op **OK**.
      
      Enkele seconden wordt uitgevoerd. Wanneer Hallo VHD maken voltooid is, ziet u een nieuwe schijf zonder een stationsletter en in staat 'Niet geïnitialiseerd' hello Schijfbeheer-console.
      
      * Met de rechtermuisknop op Hallo schijf (niet Hallo niet-toegewezen ruimte) en klik vervolgens op **schijf initialiseren**. Selecteer **MBR** (Master Boot Record) als de partitiestijl Hallo en klik op **OK**.
      * Maak een nieuw volume: met de rechtermuisknop op Hallo niet-toegewezen ruimte en klik vervolgens op **Nieuw eenvoudig Volume**. U kunt Hallo standaardinstellingen in de wizard Hallo accepteren, maar zorg ervoor dat u een stationsletter tooavoid potentiële problemen toewijzen tijdens het uploaden van Hallo-sjablooninstallatiekopie.
      * Met de rechtermuisknop op Hallo schijf en klik vervolgens op **VHD ontkoppelen**.
3. Installeer Windows Server 2012 R2:
   
   1. Maak een nieuwe virtuele machine. Gebruik de Wizard Nieuwe virtuele Machine in Hyper-V-beheer of Hyper-V voor Client Hallo.
      1. Kies op Hallo generatie opgeven pagina **generatie 1**.
      2. Selecteer op de pagina virtuele hardeschijf aansluiten Hallo **gebruik een bestaande virtuele harde schijf**, en blader toohello VHD die u hebt gemaakt in de vorige stap Hallo.
      3. Selecteer op de pagina installatieopties Hallo **een besturingssysteem installeren vanaf een opstart-CD/DVD_ROM**, en selecteer vervolgens Hallo-locatie van de installatiemedia van Windows Server 2012 R2.
      4. Kies andere opties in Hallo wizard nodig tooinstall Windows en uw toepassingen. Hallo-wizard hebt voltooid.
   2. Nadat de wizard Hallo is voltooid, Hallo-instellingen van Hallo virtuele machine te bewerken en breng eventuele andere wijzigingen nodig tooinstall Windows en uw programma's, zoals het aantal virtuele processors Hallo en klik vervolgens op **OK**.
   3. Verbind toohello virtuele machine en installeer Windows Server 2012 R2.
4. Hallo Remote Desktop Session Host (RDSH)-functie en de functie Bureaubladervaring Hallo installeren:
   1. Start Serverbeheer.
   2. Klik op **functies en onderdelen toevoegen** op Hallo-aanmeldingsscherm of in Hallo **beheren** menu.
   3. Klik op **volgende** op de pagina Hallo voordat u begint.
   4. Selecteer **op basis van functie of onderdeel gebaseerde installatie**, en klik vervolgens op **volgende**.
   5. Selecteert u de lokale computer Hallo in Hallo lijst en klik vervolgens op **volgende**.
   6. Selecteer **extern bureaublad-Services**, en klik vervolgens op **volgende**.
   7. Vouw **gebruikersinterfaces en infrastructuur** en selecteer **Bureaubladervaring**.
   8. Klik op **onderdelen toevoegen**, en klik vervolgens op **volgende**.
   9. Op de pagina Hallo extern bureaublad-Services op **volgende**.
   10. Klik op **extern bureaublad-sessiehost**.
   11. Klik op **onderdelen toevoegen**, en klik vervolgens op **volgende**.
   12. Selecteer op Hallo pagina installatieselecties bevestigen, **Hallo doelserver opnieuw opstarten automatisch indien nodig**, en klik vervolgens op **Ja** op Hallo start opnieuw op de waarschuwing.
   13. Klik op **Install**. Hallo-computer wordt opnieuw opgestart.
5. Extra functies die vereist zijn voor uw toepassingen, zoals Hallo .NET Framework 3.5 installeren. tooinstall hello functies, Wizard Hallo toevoegen functies en onderdelen worden uitgevoerd.
6. Installeer en configureer Hallo programma's en toepassingen die u wilt dat toopublish via RemoteApp.

> [!IMPORTANT]
> Hallo RDSH-functie installeren voordat u toepassingen tooensure installeert tooRemoteApp dat problemen met de compatibiliteit van toepassingen worden gedetecteerd voordat de installatiekopie van het Hallo is geüpload.
> 
> Zorg ervoor dat de toepassing van een snelkoppeling tooyour (**lnk** bestand) wordt weergegeven in Hallo **Start** menu voor alle gebruikers (%systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programma 's). Zorg er ook voor dat u in Hallo ziet Hallo-pictogram **Start** menu is wat u wilt dat gebruikers toosee. Als dat niet het geval is, is deze te wijzigen. (U geen *hebben* tooadd hello toohello Start toepassingsmenu, maar maakt het veel eenvoudiger toopublish Hallo-toepassing in RemoteApp. Anders hebt tooprovide Hallo installatiepad voor de toepassing hello wanneer u Hallo app publiceert.)
> 
> 

1. Geen aanvullende Windows-configuraties die nodig zijn voor uw toepassingen uitvoeren.
2. Hallo Encrypting File System (EFS) uitschakelen. Voer Hallo volgende opdracht in een venster van de opdracht met verhoogde bevoegdheid:
   
     Werking van fsutil instellen disableencryption 1
   
   U kunt ook instellen of toevoegen van de volgende DWORD-waarde in het register Hallo Hallo:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Als u uw afbeelding binnen een virtuele machine in Azure maakt, wijzig de naam van Hallo  **\%windir%\Panther\Unattend.xml** bestand, zoals dit Hallo uploaden script later gebruikt werken wordt geblokkeerd. Hallo-naam van dit bestand tooUnattend.old wijzigen zodat u nog altijd Hallo bestand hebt geval u toorevert die uw implementatie nodig.
4. Ga tooWindows Update en installeer alle belangrijke updates. Mogelijk moet u Windows Update meerdere keren tooget toorun alle updates. (Soms u een update installeert, en die update zelf moet worden bijgewerkt.)
5. SYSPREP Hallo-afbeelding. Voer bij een opdrachtprompt met verhoogde bevoegdheid Hallo volgende opdracht:
   
   **C:\Windows\System32\sysprep\sysprep.exe / generalize/shutdown/oobe**
   
   **Opmerking:** gebruik geen Hallo **/mode:vm** switch Hallo SYSPREP opdracht zelfs als dit een virtuele machine.

## <a name="next-steps"></a>Volgende stappen
Nu u de installatiekopie van uw aangepaste sjabloon hebt, moet u tooupload die installatiekopie tooyour RemoteApp-collectie. Gebruik Hallo-informatie in de volgende artikelen toocreate Hallo uw verzameling:

* [Hoe toocreate een hybride verzameling van RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Hoe toocreate een cloudverzameling van RemoteApp](remoteapp-create-cloud-deployment.md)

