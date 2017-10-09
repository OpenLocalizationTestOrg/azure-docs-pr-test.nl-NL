---
title: aaaPowerShell voor het beheer van StorSimple-apparaten | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell voor StorSimple toomanage uw StorSimple-apparaat.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Windows PowerShell voor StorSimple tooadminister uw apparaat gebruiken
## <a name="overview"></a>Overzicht
Windows PowerShell voor StorSimple biedt een opdrachtregelinterface waarmee u toomanage uw Microsoft Azure StorSimple-apparaat kunt. Zoals de naam van de Hallo wordt voorgesteld, is een Windows PowerShell gebaseerde opdrachtregelinterface die is ingebouwd in een beperkte runspace. Vanuit het perspectief van de Hallo van gebruiker op de opdrachtregel Hallo Hallo wordt weergegeven een beperkte runspace als een beperkte versie van Windows PowerShell. Deze interface heeft terwijl sommige Hallo essentiële mogelijkheden van Windows PowerShell andere speciale cmdlets die zijn gericht op het beheren van uw Microsoft Azure StorSimple-apparaat. 

In dit artikel beschrijft Hallo Windows PowerShell voor StorSimple-onderdelen, met inbegrip van hoe u verbinding kunt maken van toothis-interface en bevat koppelingen toostep-voor-stap procedures of werkstromen die u kunt uitvoeren met behulp van deze interface. Hallo-werkstromen omvatten hoe tooregister uw apparaat Hallo netwerkinterface configureren op uw apparaat updates installeren die Hallo apparaat toobe in de onderhoudsmodus vereisen, wijzigen van de apparaatstatus hello, en los eventuele problemen die kunnen optreden.

Na het lezen van dit artikel kunt u zich kunt:

* Verbind tooyour StorSimple-apparaat met Windows PowerShell voor StorSimple.
* Beheren van uw StorSimple-apparaat met Windows PowerShell voor StorSimple.
* Help opvragen in Windows PowerShell voor StorSimple.

> [!NOTE]
> * Windows PowerShell voor StorSimple-cmdlets kunt u toomanage uw StorSimple-apparaat van een seriële console of extern via Windows PowerShell op afstand. Voor meer informatie over elk met afzonderlijke Hallo-cmdlets die kunnen worden gebruikt in deze interface gaat te[cmdlet-naslaginformatie voor Windows PowerShell voor StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * Hallo StorSimple van Azure PowerShell-cmdlets zijn een andere verzameling van cmdlets waarmee u tooautomate StorSimple serviceniveau- en migratietaken vanaf de opdrachtregel Hallo. Ga voor meer informatie over hello Azure PowerShell-cmdlets voor StorSimple toohello [Azure StorSimple-cmdlet-verwijzing](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

U kunt toegang krijgen tot de Hallo Windows PowerShell voor StorSimple met een van de volgende methoden Hallo:

* [Verbinding maken met de seriële console van tooStorSimple apparaat](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Extern verbinding maken met Windows PowerShell tooStorSimple](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>TooWindows PowerShell voor StorSimple-verbinding via de seriële console van Hallo apparaat
U kunt [download PuTTY](http://www.putty.org/) of soortgelijke terminal emulatie software tooconnect tooWindows PowerShell voor StorSimple. U moet tooconfigure PuTTY specifiek tooaccess Hallo Microsoft Azure StorSimple-apparaat. Hallo volgende onderwerpen bevatten gedetailleerde stappen voor het tooconfigure PuTTy en toohello apparaat aansluit. Verschillende opties in de seriële console hello, worden ook beschreven.

### <a name="putty-settings"></a>Instellingen voor PuTTY
Zorg ervoor dat u Hallo PuTTY instellingen tooconnect toohello Windows PowerShell-interface van de seriële console hello te volgen.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY
1. In Hallo PuTTY **herconfiguratie** dialoogvenster in Hallo **categorie** deelvenster **toetsenbord**.
2. Zorg ervoor dat Hallo volgende opties zijn geselecteerd (dit zijn de standaardinstellingen Hallo wanneer u een nieuwe sessie start). 
   
   | Toetsenbord-item | Selecteer |
   | --- | --- |
   | BACKSPACE sleutel |Controle-? (127) |
   | Start en End sleutels |Standard |
   | Functietoetsen en toetsenblok |ESC [n ~ |
   | Oorspronkelijke status van de cursor sleutels |Normaal |
   | Oorspronkelijke status van het numerieke toetsenblok |Normaal |
   | Extra toetsenbord-functies inschakelen |CTRL + ALT + verschilt van AltGr |
   
    ![Ondersteunde instellingen voor Putty](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Klik op **Toepassen**.
4. In Hallo **categorie** deelvenster **vertaling**.
5. In Hallo **externe tekenset** keuzelijst met invoervak, selecteer **UTF-8**.
6. Onder **afhandeling van regel tekening tekens**, selecteer **gebruik Unicode-regel tekenen-codepunten**. Hallo volgende afbeelding ziet u de juiste PuTTY selecties Hallo.
   
    ![Instellingen voor Putty UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Klik op **Toepassen**.

U kunt PuTTY tooconnect toohello de seriële console apparaat nu gebruiken als volgt Hallo stappen te volgen.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Over Hallo seriële console
Wanneer u Windows PowerShell-interface Hallo van uw StorSimple-apparaat via de seriële console Hallo opent, wordt een bannerbericht gepresenteerd, gevolgd door de menuopties. 

banner het Hallo-bericht bevat StorSimple-apparaat basisinformatie zoals Hallo model, de naam, de versie van de geïnstalleerde software en de status van Hallo controller die krijgt u toegang tot. Hallo volgende afbeelding toont een voorbeeld van een bannerbericht.

![Seriële bannerbericht aangegeven](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> U kunt Hallo banner bericht tooidentify of Hallo controller zijn toois actief of passief is verbonden.
> 
> 

Hallo volgende afbeelding toont Hallo verschillende runspace opties die beschikbaar in het menu van de seriële console Hallo zijn.

![Registreer uw apparaat 2](./media/storsimple-windows-powershell-administration/IC740906.png)

U kunt kiezen uit Hallo volgende instellingen:

1. **Meld u aan met volledige toegang** deze optie kunt u tooconnect (met correcte referenties Hallo) toohello **SSAdminConsole** runspace op Hallo lokale domeincontroller. (de lokale domeincontroller Hallo is Hallo-domeincontroller die u momenteel via de seriële console Hallo van uw StorSimple-apparaat opent.) Deze optie kan ook worden gebruikt tooallow Microsoft Support tooaccess onbeperkte runspace (een ondersteuningssessie) tootroubleshoot problemen mogelijke apparaten. Nadat u optie 1 toolog op gebruikt, kunt u Microsoft Support engineer van Hallo tooaccess onbeperkte runspace toestaan door het uitvoeren van een bepaalde cmdlet. Voor meer informatie, Raadpleeg te[ondersteuningssessie starten](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Meld u bij de domeincontroller toopeer met volledige toegang** deze optie is dezelfde Hallo als optie 1, behalve dat u verbinding (met correcte referenties Hallo maken kunt) toohello **SSAdminConsole** runspace op Hallo peer-domeincontroller. Omdat Hallo StorSimple-apparaat een hoge beschikbaarheid-apparaat met twee domeincontrollers in een actief / passief-configuratie, peer verwijst naar toohello andere domeincontroller in het Hallo-apparaat die u via de seriële console Hallo openen wilt).
   Vergelijkbare toooption 1, wordt deze optie kan ook worden gebruikt tooallow Microsoft Support tooaccess onbeperkte runspace op een peer-domeincontroller.
3. **Verbinding maken met beperkte toegang** deze optie gebruikt tooaccess Windows PowerShell-interface is in de beperkte modus. U wordt niet gevraagd om referenties voor toegang. Deze optie verbindt tooa beperkte runspace vergeleken toooptions 1 en 2.  Hallo-taken die beschikbaar via de optie 1 zijn die **kan niet* worden uitgevoerd in deze runspace zijn:
   
   * Toohello factory instellingen opnieuw instellen
   * Hallo-wachtwoord wijzigen
   * In- of uitschakelen van ondersteuning toegang
   * Updates toepassen
   * Installeren van hotfixes 

    > [!NOTE]
    > Dit is Hallo voorkeurs-optie als u wachtwoord apparaatbeheerder hello vergeten bent en kan geen verbinding met behulp van de optie 1 of 2 maken.

4. **Taal wijzigen** deze optie kunt u de weergavetaal van toochange Hallo op Hallo Windows PowerShell-interface. Hallo talen die worden ondersteund zijn Engels, Japans, Russisch, Frans, Zuid Koreaans, Spaans, Italiaans, Duits, Chinees en Portugees (Brazilië).

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Extern verbinding maken met Windows PowerShell voor StorSimple tooStorSimple
U kunt Windows PowerShell voor externe toegang tooconnect tooyour StorSimple-apparaat gebruiken. Als u op deze manier verbinding, ziet u een menu. (U ziet een menu alleen als u de seriële console Hallo op Hallo apparaat tooconnect gebruiken. Extern verbinding maakt, gaat u rechtstreeks toohello equivalent van de 'optie 1: volledige toegang' op de seriële console Hallo.) Met Windows PowerShell op afstand, moet u specifieke runspace tooa verbinden. U kunt ook de weergavetaal Hallo opgeven. 

Hallo weergavetaal is onafhankelijk van Hallo taal die u instelt met behulp van Hallo **taal wijzigen** optie in het menu van de seriële console Hallo. Externe PowerShell wordt automatisch kunnen worden opgepikt landinstellingen van de Hallo van Hallo apparaat die u verbinding maakt vanaf als niets wordt opgegeven.

> [!NOTE]
> Als u met virtuele Microsoft Azure-hosts en virtuele StorSimple-apparaten werkt, kunt u Windows PowerShell voor externe toegang en Hallo virtuele host tooconnect toohello virtueel apparaat gebruiken. Als u een locatie op de host op waarin toosave de informatie uit de Windows PowerShell-sessie Hallo Hallo hebt ingesteld, moet u zich bewust dat Hallo die iedereen principal bevat alleen geverifieerde gebruikers. Als u Hallo share tooallow toegang door iedereen hebt ingesteld en u verbinding maken zonder het opgeven van referenties, Hallo niet geverifieerde anonieme principal wordt gebruikt en worden er een fout opgetreden. Dit probleem er op Hallo host, moet u Hallo gastaccount inschakelen en vervolgens geeft Hallo Gast-account volledige toegang toohello share of als u delen toofix moet geldige referenties samen met Windows PowerShell-cmdlet Hallo opgeven.
> 
> 

Hier kunt u HTTP of HTTPS tooconnect via Windows PowerShell op afstand. Hallo-instructies in volgende zelfstudies hello gebruiken:

* [Verbinding maken op afstand via HTTP](storsimple-remote-connect.md#connect-through-http)
* [Verbinding maken op afstand via HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Beveiligingsoverwegingen voor verbinding
Wanneer u beslist hoe tooconnect tooWindows PowerShell voor StorSimple, houd rekening met Hallo volgende:

* Toohello rechtstreeks verbinding maken de seriële console apparaat beveiligd is, maar verbindende toohello seriële console via netwerkswitches is niet. Wees voorzichtig met van Hallo beveiligingsrisico, omdat het toodevice serieel via netwerkswitches verbinding te maken.
* Verbinding maken via een HTTP-sessie biedt meer beveiliging dan verbinding maken via de seriële console Hallo via netwerk mogelijk. Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken.
* Verbinding maken via een HTTPS-sessie is Hallo veiligste en aanbevolen optie Hallo.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Beheren van uw StorSimple-apparaat met Windows PowerShell voor StorSimple
Hallo bevat volgende tabel een overzicht van alle Hallo veelvoorkomende beheertaken en complexe werkstromen die kunnen worden uitgevoerd in Windows PowerShell-interface Hallo van uw StorSimple-apparaat. Klik op Hallo desbetreffende vermelding in Hallo tabel voor meer informatie over elke werkstroom.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Windows PowerShell voor StorSimple-werkstromen
| Als u dat toodo wilt... | Gebruik deze procedure. |
| --- | --- |
| Registreer uw apparaat |[Hallo-apparaat met Windows PowerShell voor StorSimple configureren en registreren](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Webproxy configureren</br>Web proxy-instellingen weergeven |[Webproxy voor uw StorSimple-apparaat configureren](storsimple-configure-web-proxy.md) |
| DATA 0 netwerkinterface-instellingen op uw apparaat wijzigen |[DATA 0-netwerkinterface voor uw StorSimple-apparaat wijzigen](storsimple-modify-data-0.md) |
| Stoppen van een domeincontroller </br> Opnieuw opstarten of afsluiten van een domeincontroller </br> Een apparaat afsluiten</br>Hallo apparaat toofactory standaardinstellingen herstellen |[Apparaatcontrollers beheren](storsimple-manage-device-controller.md) |
| Onderhoud modus updates en hotfixes installeren |[Uw apparaat bijwerken](storsimple-update-device.md) |
| Voer de onderhoudsmodus </br>Onderhoudsmodus afsluiten |[Modi voor StorSimple-apparaat](storsimple-device-modes.md) |
| Een ondersteuningspakket maken</br>Ontsleutelen en een ondersteuningspakket bewerken |[Maken en beheren van een ondersteuningspakket](storsimple-create-manage-support-package.md) |
| Een ondersteuningssessie starten</br> |[Een support-sessie te starten in Windows PowerShell voor StorSimple](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Help opvragen in Windows PowerShell voor StorSimple
In Windows PowerShell voor StorSimple is de cmdlet Help beschikbaar. Een actuele versie van dit Help-onderwerp is ook beschikbaar, waarmee u kunt tooupdate Hallo Help op uw systeem.

Help opvragen in deze interface is vergelijkbaar toothat in Windows PowerShell en de meeste Hallo Help-gerelateerde cmdlets zal werken. U vindt Help voor Windows PowerShell online in Hallo TechNet-bibliotheek: [met Windows PowerShell-scripts](http://go.microsoft.com/fwlink/?LinkID=108518).

Hallo Hieronder volgt een korte beschrijving van Hallo soorten Help-informatie voor deze Windows PowerShell-interface, met inbegrip van hoe tooupdate Hallo Help.

#### <a name="tooget-help-for-a-cmdlet"></a>tooget Help voor een cmdlet
* tooget Help voor cmdlet of functie, gebruik Hallo volgende opdracht:`Get-Help <cmdlet-name>`
* tooget online-Help voor een cmdlet, gebruikt u de vorige cmdlet Hallo met Hallo `-Online` parameter:`Get-Help <cmdlet-name> -Online`
* Volledige hulp nodig hebt, kunt u Hallo `–Full` parameter, en voor voorbeelden gebruiken Hallo `–Examples` parameter.

#### <a name="tooupdate-help"></a>tooupdate Help
U kunt eenvoudig hello Help in Windows PowerShell-interface Hallo bijwerken. Volgende stappen tooupdate Hallo Help op uw systeem Hallo uitvoeren.

#### <a name="tooupdate-cmdlet-help"></a>tooupdate cmdlet Help
1. Windows PowerShell starten met Hallo **als administrator uitvoeren** optie.
2. Typ het volgende achter de opdrachtprompt Hallo:`Update-Help`
3. Hallo bijgewerkte Help-bestanden geïnstalleerd.
4. Nadat het Hallo-helpbestanden zijn geïnstalleerd, typt: `Get-Help Get-Command`. Hiermee wordt een lijst met cmdlets waarvoor Help beschikbaar is weergegeven.

> [!NOTE]
> een lijst met alle beschikbare Hallo-cmdlets in een runspace tooget aan overeenkomstige menuoptie toohello en Voer Hallo `Get-Command` cmdlet.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Als u problemen met uw StorSimple-apparaat ondervindt bij het uitvoeren van een van de Hallo hierboven werkstromen, raadpleeg dan te[hulpprogramma's voor probleemoplossing StorSimple implementaties](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

