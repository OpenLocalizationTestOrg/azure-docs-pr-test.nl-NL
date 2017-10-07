---
title: aaaTrack wijzigingen met Azure Log Analytics | Microsoft Docs
description: Hallo oplossing voor wijzigingen bijhouden in Log Analytics kunt u identificeren van software- en Windows-Service-wijzigingen die in uw omgeving plaatsvinden.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Bijhouden van wijzigingen in de software in uw omgeving met Hallo oplossing bijhouden

![Bijhouden symbool wijzigen](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Dit artikel helpt u gebruik Hallo oplossing voor wijzigingen bijhouden in logboekanalyse tooeasily identificeren wijzigingen in uw omgeving. Hallo oplossing houdt wijzigingen tooWindows en Linux-software, Windows-bestanden en registersleutels services voor Windows en Linux-daemons. Wijzigingen in de configuratie te identificeren, kunt u operationele problemen te lokaliseren.

U installeert Hallo tooupdate Hallo oplossingstype van de agent die u hebt geïnstalleerd. Wijzigingen tooinstalled software, services voor Windows en Linux-daemons op Hallo bewaakte servers worden gelezen. Hallo gegevens verzonden vervolgens toohello Log Analytics-service in de cloud Hallo voor verwerking. Logica is toegepaste toohello ontvangen gegevens en Hallo cloudservice registreert Hallo-gegevens. Met Hallo informatie op Hallo bijhouden dashboard kunt kunt u gemakkelijk zien Hallo-wijzigingen die zijn aangebracht in uw serverinfrastructuur.

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.

* U moet hebben een [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), of [Linux](log-analytics-linux-agents.md) -agent op elke computer waarop u wilt dat toomonitor wijzigingen.
* Hallo bijhouden oplossing tooyour OMS-werkruimte van Hallo toevoegen [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Of u kunt Hallo-oplossing met behulp van informatie in Hallo toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Er is geen verdere configuratie vereist.

### <a name="configure-linux-files-tootrack"></a>Linux-bestanden tootrack configureren
Hallo stappen tooconfigure bestanden tootrack volgen op Linux-computers gebruiken.

1. Klik in de OMS-portal Hallo **instellingen** (symbol Hallo tandwielpictogram).
2. Op Hallo **instellingen** pagina, klikt u op **gegevens**, en klik vervolgens op **Linux File Tracking**.
3. Typ onder Linux bestand Change Tracking Hallo gehele pad, inclusief de bestandsnaam Hallo van Hallo-bestand dat u wilt dat tootrack en klik vervolgens op Hallo **toevoegen** symbool. Bijvoorbeeld: '/etc/*.conf'
4. Klik op **Opslaan**.  

> [!NOTE]
> Linux-bestand bijhouden heeft aanvullende mogelijkheden, waaronder directory bijhouden, recrusion via mappen en de jokertekens bijhouden.

### <a name="configure-windows-files-tootrack"></a>Windows-bestanden tootrack configureren
Volgende stappen tooconfigure bestanden tootrack op computers met Windows hello gebruiken.

1. Klik in de OMS-portal Hallo **instellingen** (symbol Hallo tandwielpictogram).
2. Op Hallo **instellingen** pagina, klikt u op **gegevens**, en klik vervolgens op **Windows File Tracking**.
3. Typ onder Windows bestand Change Tracking Hallo gehele pad, inclusief de bestandsnaam Hallo van Hallo-bestand dat u wilt dat tootrack en klik vervolgens op Hallo **toevoegen** symbool. Bijvoorbeeld: C:\Program Files (x86) \Internet Explorer\iexplore.exe of C:\Windows\System32\drivers\etc\hosts.
4. Klik op **Opslaan**.  
   ![Windows-bestand met bijhouden](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Windows-register sleutels tootrack configureren
Volgende stappen tooconfigure Register sleutels tootrack op computers met Windows hello gebruiken.

1. Klik in de OMS-portal Hallo **instellingen** (symbol Hallo tandwielpictogram).
2. Op Hallo **instellingen** pagina, klikt u op **gegevens**, en klik vervolgens op **Windows-register bijhouden**.
3. Typ onder Windows-register bijhouden, de gehele sleutel Hallo dat u wilt dat tootrack en klik vervolgens op Hallo **toevoegen** symbool.
4. Klik op **Opslaan**.  
   ![Windows-register bijhouden](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Uitleg van de verzameling van Linux bestandseigenschappen
1. **Type**
   * **Bestand** (rapport bestandsmetagegevens - grootte, wijzigingsdatum, hash, enz.)
   * **Directory** (rapport directory metagegevens - grootte, wijzigingsdatum, enz.)
2. **Koppelingen** (afhandeling van Linux symlink verwijst naar tooother bestanden of mappen)
   * **Negeren** (symlinks negeren tijdens recurions toonot omvatten Hallo bestanden/mappen waarnaar wordt verwezen)
   * **Ga als volgt** (Volg Hallo symlinks tijdens recursie tooalso omvatten Hallo bestanden/mappen waarnaar wordt verwezen)
   * **Beheren** (Ga als volgt Hallo symlinks en alter Hallo behandeling van geretourneerde inhoud)

   > [!NOTE]   
   > Hallo 'Beheren' koppelingen optie wordt niet aanbevolen. Inhoud ophalen van bestand wordt niet ondersteund.

3. **Recurse** (Recurse via niveaus van de map en alle bestanden die voldoen aan de padinstructie Hallo bijhouden)
4. **Sudo** (voor het inschakelen van toegang tot bestanden of mappen die sudo bevoegdheid vereist)

### <a name="limitations"></a>Beperkingen
Hallo bijhouden oplossing ondersteunt momenteel geen Hallo volgende items:

* Mappen voor het bijhouden van de Windows-bestand
* Recursie voor Windows-bestand bijhouden
* Jokertekens voor het bijhouden van de Windows-bestand
* Padvariabelen
* Netwerk-bestandssystemen
* Bestandsinhoud

Andere beperkingen:

* Hallo **maximale bestandsgrootte** kolom en -waarden niet worden gebruikt in de huidige implementatie Hallo zijn.
* Als u meer dan 2500 bestanden in Hallo 30 minuten Verzamelfase bestanden verzamelt, mogelijk tot slechtere met prestaties van de oplossing.
* Wanneer het netwerkverkeer hoog, kunnen wijzigingsrecords duren tooa maximaal zes uur toodisplay.
* Als u Hallo-configuratie wijzigen terwijl een computer wordt afgesloten, posten Hallo computer bestandswijzigingen die deel uitmaakten van de vorige configuratie toohello.

## <a name="change-tracking-data-collection-details"></a>Details van verzameling gegevens bijhouden wijzigen
Bijhouden van wijzigingen worden verzameld voor software-inventaris en metagegevens van de Windows-Service gebruikt Hallo-agents die u hebt ingeschakeld.

Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor het bijhouden.

| Platform | Directe Agent | Operations Manager-agent | Linux-agent | Azure Storage | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Frequentie van de verzameling |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows- en Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minuten too50 minuten, afhankelijk van het type van de wijziging Hallo. Zie Hallo volgende tabel voor meer informatie. |


Hallo toont volgende tabel Hallo gegevens verzameling frequentie voor Hallo typen wijzigingen.

| **type wijzigen** | **frequentie** | **Biedt****agent****verschillen wanneer gevonden verzenden?**  |
| --- | --- | --- |
| Windows-register | 50 minuten | Nee |
| Windows-bestand | 30 minuten | Ja. Als er geen wijziging in 24 uur, wordt een momentopname wordt verzonden. |
| Linux-bestand | 15 minuten | Ja. Als er geen wijziging in 24 uur, wordt een momentopname wordt verzonden. |
| Windows-services | 30 minuten | Ja, elke 30 minuten wanneer wijzigingen zijn gevonden. Elke 24 uur een momentopname wordt verzonden, ongeacht de wijziging. Dus Hallo momentopname zelfs wordt verzonden wanneer er geen wijzigingen zijn. |
| Daemons Linux | 5 minuten | Ja. Als er geen wijziging in 24 uur, wordt een momentopname wordt verzonden. |
| Windows-software | 30 minuten | Ja, elke 30 minuten wanneer wijzigingen zijn gevonden. Elke 24 uur een momentopname wordt verzonden, ongeacht de wijziging. Dus Hallo momentopname zelfs wordt verzonden wanneer er geen wijzigingen zijn. |
| Linux-software | 5 minuten | Ja. Als er geen wijziging in 24 uur, wordt een momentopname wordt verzonden. |

### <a name="registry-key-change-tracking"></a>Wijziging van de registersleutel bijhouden

Log Analytics voert Windows-register bewaken en bijhouden met Hallo oplossing bijhouden. Hallo-doel van de bewaking wijzigingen tooregistry sleutels is toopinpoint Uitbreidingspunten waar de code van derden en schadelijke software kunnen activeren. Hallo volgende lijst bevat Hallo standaard registersleutels die worden bijgehouden door Hallo oplossing en waarom elk wordt bijgehouden.

- HKEY\_lokale\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Monitors scripts die worden uitgevoerd bij het opstarten.
- HKEY\_lokale\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Monitors scripts die worden uitgevoerd bij het afsluiten.
- HKEY\_lokale\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Sleutels die worden geladen voordat Hallo gebruiker zich aanmeldt tootheir Windows-account worden gecontroleerd. Hallo-sleutel wordt gebruikt voor 32-bits programma's uitgevoerd op 64-bits computers.
- HKEY\_lokale\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed onderdelen
    - Monitors tooapplication instellingen gewijzigd.
- HKEY\_lokale\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Monitors algemene autostart vermeldingen die rechtstreeks in Windows Verkenner en meestal uitvoeren in-process met Explorer.exe koppelen.
- HKEY\_lokale\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Monitors algemene autostart vermeldingen die rechtstreeks in Windows Verkenner en meestal uitvoeren in-process met Explorer.exe koppelen.
- HKEY\_lokale\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Monitors algemene autostart vermeldingen die rechtstreeks in Windows Verkenner en meestal uitvoeren in-process met Explorer.exe koppelen.
- HKEY\_lokale\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitors voor pictogram overlay handler registratie.
- HKEY\_lokale\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Monitors voor pictogram overlay handler-registratie voor 32-bits programma's uitgevoerd op 64-bits computers.
- HKEY\_lokale\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper-objecten
    - De monitoren voor nieuwe browser helper object invoegtoepassingen voor Internet Explorer. Gebruikte tooaccess Hallo Document Object Model (DOM) van de huidige pagina en toocontrol navigatie Hallo.
- HKEY\_lokale\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper-objecten
    - De monitoren voor nieuwe browser helper object invoegtoepassingen voor Internet Explorer. Gebruikte tooaccess Hallo Document Object Model (DOM) van Hallo huidige pagina en toocontrol navigatie voor 32-bits programma's uitgevoerd op 64-bits computers.
- HKEY\_lokale\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - De monitoren voor nieuwe Internet Explorer-uitbreidingen, zoals aangepaste hulpprogramma's en aangepaste werkbalkknoppen.
- HKEY\_lokale\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - De monitoren voor nieuwe Internet Explorer-uitbreidingen, zoals aangepaste hulpprogramma's en aangepaste werkbalkknoppen voor 32-bits programma's uitgevoerd op 64-bits computers.
- HKEY\_lokale\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Hallo 32-bits stuurprogramma's die zijn gekoppeld aan wavemapper, wave1 en wave2 msacm.imaadpcm, .msadpcm, .msgsm610 en vidc bewaakt. Vergelijkbare toohello [drivers]-sectie in Hallo systeem. INI-bestand.
- HKEY\_lokale\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Monitors Hallo 32-bits stuurprogramma's die zijn gekoppeld aan wavemapper, wave1 en wave2 msacm.imaadpcm, .msadpcm, .msgsm610 en vidc voor 32-bits programma's uitgevoerd op 64-bits computers. Vergelijkbare toohello [drivers]-sectie in Hallo systeem. INI-bestand.
- HKEY\_lokale\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Monitors Hallo lijst met bekende of veelgebruikte systeem-dll's; Dit systeem wordt voorkomen dat mensen misbruik van zwakke toepassing mapmachtigingen door slepen en neerzetten in Trojaanse paard versies van systeem-dll's.
- HKEY\_lokale\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Monitors Hallo lijst met pakketten kunnen tooreceive gebeurtenismeldingen van Winlogon, Hallo interactieve aanmelding ondersteuningsmodel voor Hallo Windows-besturingssysteem.


## <a name="use-change-tracking"></a>Gebruik bijhouden
Nadat het Hallo-oplossing is geïnstalleerd, kunt u Hallo overzicht van wijzigingen voor uw bewaakte servers weergeven met behulp van Hallo **bijhouden** tegel op Hallo **overzicht** pagina in OMS.

![afbeelding van de tegel bijhouden](./media/log-analytics-change-tracking/change-tracking-tile.png)

U kunt wijzigingen tooyour infrastructuur en vervolgens inzoomen in details voor de volgende categorieën Hallo bekijken:

* Wijzigingen per configuratietype voor software- en Windows-services
* Softwarewijzigingen tooapplications en updates voor afzonderlijke servers
* Totaal aantal wijzigingen in de software voor elke toepassing
* Linux-pakketten
* Windows-servicewijzigingen voor afzonderlijke servers
* Linux-daemonwijzigingen

![afbeelding van dashboard bijhouden](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![afbeelding van dashboard bijhouden](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview wijzigingen voor elk wijzigen type
1. Op Hallo **overzicht** pagina, klikt u op Hallo **bijhouden** tegel.
2. Op Hallo **wijzigen bijhouden** dashboard Hallo samenvattingsinformatie in een Hallo wijziging type blades controleren en klik op een tooview gedetailleerde informatie over het in Hallo **logboek zoeken** pagina.
3. U kunt op een van de Hallo logboek zoekpagina's, resultaten weergeven door de tijd, gedetailleerde resultaten en uw Logboekgeschiedenis zoeken. U kunt ook facetten toonarrow Hallo resultaten filteren.

## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor het bijhouden.
