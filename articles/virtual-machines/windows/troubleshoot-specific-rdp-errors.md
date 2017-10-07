---
title: aaaSpecific RDP-foutberichten voor Azure Virtual machines | Microsoft Docs
description: Inzicht in specifieke foutberichten die kunnen worden weergegeven bij het gebruik van extern bureaublad verbinding tooa Windows virtuele machine in Azure
keywords: Extern bureaublad-fout, verbinding met extern bureaublad-fout, kan geen verbinding maken tooVM, probleemoplossing extern bureaublad
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>Het oplossen van specifieke RDP fout berichten tooa Windows virtuele machine in Azure
Het foutbericht een specifiek foutbericht bij gebruik van extern bureaublad verbinding tooa Windows virtuele machine (VM) in Azure. De details van dit artikel enkele van de meestvoorkomende foutberichten die worden aangetroffen, samen met het oplossen van stappen tooresolve Hallo ze. Als er problemen met tooyour VM verbinden met RDP maar komen niet optreden van een specifiek foutbericht, raadpleegt u Hallo [problemen oplossen met extern bureaublad](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Zie voor informatie over specifieke foutberichten Hallo volgende:

* [Hallo externe sessie is beëindigd omdat er geen extern bureaublad-licentieservers beschikbaar tooprovide een licentie](#rdplicense).
* [Extern bureaublad Hallo kan niet zoeken computer 'name'](#rdpname).
* [Er is een verificatiefout opgetreden. Hallo Local Security Authority is niet bereikbaar](#rdpauth).
* [Fout bij de Windows-beveiliging: uw referenties werken niet](#wincred).
* [Deze computer kan geen verbinding van de externe computer toohello](#rdpconnect).

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>Hallo externe sessie is beëindigd omdat er geen extern bureaublad-licentieservers beschikbaar tooprovide een licentie.
Oorzaak: Hallo 120 dagen respijtperiode voor Hallo extern bureaublad-serverrol is verlopen en u tooinstall licenties nodig.

Een lokale kopie van Hallo RDP-bestand vanuit de portal Hallo opslaan en deze opdracht uitvoert op een PowerShell-opdrachtprompt tooconnect als tijdelijke oplossing. Deze stap wordt uitgeschakeld voor alleen die verbinding-licentieverlening:

        mstsc <File name>.RDP /admin

Als u niet meer dan twee gelijktijdige extern bureaublad-verbindingen toohello VM daadwerkelijk nodig, kunt u Serverbeheer tooremove Hallo extern bureaublad-serverfunctie.

Zie voor meer informatie Hallo blogbericht [Azure VM is mislukt met 'Geen extern bureaublad-licentieservers beschikbaar'](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>Extern bureaublad kan Hallo computer 'name' niet vinden.
Oorzaak: Hallo extern bureaublad-client op uw computer kan Hallo-naam van computer in de instellingen van RDP-bestand Hallo HALLO hallo niet omzetten.

Mogelijke oplossingen:

* Als u op het intranet van een organisatie, zorg ervoor dat uw computer toegang tot toohello proxyserver heeft en tooit voor HTTPS-verkeer kan verzenden.
* Als u een lokaal opgeslagen RDP-bestand gebruikt, probeert u Hallo één die wordt gegenereerd door Hallo-portal. Deze stap zorgt ervoor dat u het juiste DNS-naam Hallo voor Hallo virtuele machine, of Hallo-cloudservice en de eindpuntpoort Hallo Hallo VM. Hier volgt een voorbeeld RDP-bestand die worden gegenereerd door Hallo-portal:
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

Hallo gedeelte van dit RDP-bestand is:

* Hallo volledig gekwalificeerde domeinnaam van het Hallo-cloudservice met Hallo VM ('tailspin-azdatatier.cloudapp.net' in dit voorbeeld).
* Hallo externe TCP-poort van het Hallo-eindpunt voor extern bureaublad-verkeer (55919).

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>Er is een verificatiefout opgetreden. Hallo Local Security Authority is niet bereikbaar.
Oorzaak: Hallo doel VM kan Hallo certificeringsinstantie vinden in Hallo gebruiker-gedeelte van uw referenties.

Wanneer uw gebruikersnaam in de vorm Hallo is *SecurityAuthority*\\*gebruikersnaam* (voorbeeld: corp\gebruiker1), Hallo *SecurityAuthority* gedeelte is ofwel Hallo VM van de naam van de computer (voor lokale beveiligingsautoriteit Hallo) of de naam van een Active Directory-domein.

Mogelijke oplossingen:

* Als Hallo account lokale toohello VM, zorg er dan voor dat die Hallo VM-naam juist is gespeld.
* Als het Hallo-account is op een Active Directory-domein, spelling Hallo van Hallo domeinnaam.
* Als een Active Directory-domeinaccount en Hallo domeinnaam juist is gespeld, Controleer of een domeincontroller beschikbaar is in het domein. Er is een veelvoorkomend probleem in Azure virtuele netwerken die een domeincontroller is niet beschikbaar omdat deze nog niet is gestart domeincontrollers bevatten. U kunt een lokaal beheerdersaccount in plaats van een domeinaccount gebruiken als tijdelijke oplossing.

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Fout bij de Windows-beveiliging: uw referenties werken niet.
Oorzaak: Hallo doel VM kan niet worden gevalideerd uw accountnaam en wachtwoord.

Een Windows-computer kunt valideren Hallo referenties van een lokaal account of een domeinaccount.

* Gebruiken voor lokale accounts Hallo *ComputerName*\\*gebruikersnaam* syntaxis (voorbeeld: SQL1\Admin4798).
* Gebruik voor domeinaccounts Hallo *DomainName*\\*gebruikersnaam* syntaxis (voorbeeld: CONTOSO\peterodman).

Als uw VM tooa-domeincontroller in een nieuw Active Directory-forest is gepromoveerd, Hallo lokale administrator-account dat u aangemeld is geconverteerd tooan gelijkwaardige account Hello hetzelfde wachtwoord in Hallo nieuwe forest en domein. Hallo lokale account wordt vervolgens verwijderd.

Bijvoorbeeld, als u bent aangemeld met Hallo lokale account DC1\DCAdmin en vervolgens Hallo virtuele machine gepromoveerd tot een domeincontroller in een nieuw forest voor Hallo corp.contoso.com domein, Hallo DC1\DCAdmin lokale account wordt verwijderd en een nieuw domeinaccount (CORP\DCAdmin ) is gemaakt met de Hallo hetzelfde wachtwoord.

Zorg ervoor dat Hallo-accountnaam is een naam of Hallo virtuele machine als een geldig account kunt controleren, en dat Hallo-wachtwoord juist is.

Als u toochange Hallo wachtwoord van de lokale beheerdersaccount hello moet, Zie [hoe tooreset een wachtwoord of Hallo extern bureaublad voor virtuele machines van Windows service](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>Deze computer kan geen verbinding met het maken van de externe computer toohello.
Oorzaak: Hallo-account dat is gebruikt tooconnect heeft geen extern bureaublad aanmelden rechten.

Elke Windows-computer is een lokale gebruikersgroep van de extern bureaublad, die Hallo accounts en groepen die op afstand in de App kunnen ondertekenen bevat. Leden van de lokale beheerdersgroep Hallo hebben toegang, zelfs als deze accounts niet worden weergegeven in de lokale gebruikersgroep Hallo extern bureaublad. Hallo lokale groep administrators bevat ook Hallo Domeinbeheerders voor Hallo domein voor domein-machines.

Zorg ervoor dat Hallo account u tooconnect met extern bureaublad-aanmelden-rechten heeft. Gebruik als tijdelijke oplossing een domein of lokale administrator-account tooconnect via Extern bureaublad. tooadd Hallo lokale gebruikersgroep van gewenste account toohello extern bureaublad, Hallo Microsoft Management Console-module gebruiken (**Systeemwerkset > lokale gebruikers en groepen > groepen > Externe bureaubladgebruikers**).

## <a name="next-steps"></a>Volgende stappen
Als geen van deze fouten is opgetreden en er een onbekend probleem met het verbinding maken met behulp van RDP, raadpleegt u Hallo [problemen oplossen met extern bureaublad](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Zie voor probleemoplossing bij het openen van toepassingen die worden uitgevoerd op een virtuele machine, [problemen met toegang tooan toepassing die wordt uitgevoerd op een Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Als u problemen met het gebruik van Secure Shell (SSH) tooconnect tooa Linux VM in Azure hebt, raadpleegt u [oplossen SSH-verbindingen tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

