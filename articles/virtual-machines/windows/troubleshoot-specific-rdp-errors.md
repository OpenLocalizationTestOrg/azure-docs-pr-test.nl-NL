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
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a><span data-ttu-id="974d1-104">Het oplossen van specifieke RDP fout berichten tooa Windows virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="974d1-104">Troubleshooting specific RDP error messages tooa Windows VM in Azure</span></span>
<span data-ttu-id="974d1-105">Het foutbericht een specifiek foutbericht bij gebruik van extern bureaublad verbinding tooa Windows virtuele machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="974d1-105">You may receive a specific error message when using Remote Desktop connection tooa Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="974d1-106">De details van dit artikel enkele van de meestvoorkomende foutberichten die worden aangetroffen, samen met het oplossen van stappen tooresolve Hallo ze.</span><span class="sxs-lookup"><span data-stu-id="974d1-106">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span> <span data-ttu-id="974d1-107">Als er problemen met tooyour VM verbinden met RDP maar komen niet optreden van een specifiek foutbericht, raadpleegt u Hallo [problemen oplossen met extern bureaublad](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974d1-107">If you are having issues connecting tooyour VM using RDP but do not encounter a specific error message, see hello [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="974d1-108">Zie voor informatie over specifieke foutberichten Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="974d1-108">For information on specific error messages, see hello following:</span></span>

* <span data-ttu-id="974d1-109">[Hallo externe sessie is beëindigd omdat er geen extern bureaublad-licentieservers beschikbaar tooprovide een licentie](#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="974d1-109">[hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license](#rdplicense).</span></span>
* <span data-ttu-id="974d1-110">[Extern bureaublad Hallo kan niet zoeken computer 'name'](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="974d1-110">[Remote Desktop can't find hello computer "name"](#rdpname).</span></span>
* <span data-ttu-id="974d1-111">[Er is een verificatiefout opgetreden. Hallo Local Security Authority is niet bereikbaar](#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="974d1-111">[An authentication error has occurred. hello Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="974d1-112">[Fout bij de Windows-beveiliging: uw referenties werken niet](#wincred).</span><span class="sxs-lookup"><span data-stu-id="974d1-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="974d1-113">[Deze computer kan geen verbinding van de externe computer toohello](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="974d1-113">[This computer can't connect toohello remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a><span data-ttu-id="974d1-114">Hallo externe sessie is beëindigd omdat er geen extern bureaublad-licentieservers beschikbaar tooprovide een licentie.</span><span class="sxs-lookup"><span data-stu-id="974d1-114">hello remote session was disconnected because there are no Remote Desktop License Servers available tooprovide a license.</span></span>
<span data-ttu-id="974d1-115">Oorzaak: Hallo 120 dagen respijtperiode voor Hallo extern bureaublad-serverrol is verlopen en u tooinstall licenties nodig.</span><span class="sxs-lookup"><span data-stu-id="974d1-115">Cause: hello 120-day licensing grace period for hello Remote Desktop Server role has expired and you need tooinstall licenses.</span></span>

<span data-ttu-id="974d1-116">Een lokale kopie van Hallo RDP-bestand vanuit de portal Hallo opslaan en deze opdracht uitvoert op een PowerShell-opdrachtprompt tooconnect als tijdelijke oplossing.</span><span class="sxs-lookup"><span data-stu-id="974d1-116">As a workaround, save a local copy of hello RDP file from hello portal and run this command at a PowerShell command prompt tooconnect.</span></span> <span data-ttu-id="974d1-117">Deze stap wordt uitgeschakeld voor alleen die verbinding-licentieverlening:</span><span class="sxs-lookup"><span data-stu-id="974d1-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="974d1-118">Als u niet meer dan twee gelijktijdige extern bureaublad-verbindingen toohello VM daadwerkelijk nodig, kunt u Serverbeheer tooremove Hallo extern bureaublad-serverfunctie.</span><span class="sxs-lookup"><span data-stu-id="974d1-118">If you don't actually need more than two simultaneous Remote Desktop connections toohello VM, you can use Server Manager tooremove hello Remote Desktop Server role.</span></span>

<span data-ttu-id="974d1-119">Zie voor meer informatie Hallo blogbericht [Azure VM is mislukt met 'Geen extern bureaublad-licentieservers beschikbaar'](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span><span class="sxs-lookup"><span data-stu-id="974d1-119">For more information, see hello blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a><span data-ttu-id="974d1-120">Extern bureaublad kan Hallo computer 'name' niet vinden.</span><span class="sxs-lookup"><span data-stu-id="974d1-120">Remote Desktop can't find hello computer "name".</span></span>
<span data-ttu-id="974d1-121">Oorzaak: Hallo extern bureaublad-client op uw computer kan Hallo-naam van computer in de instellingen van RDP-bestand Hallo HALLO hallo niet omzetten.</span><span class="sxs-lookup"><span data-stu-id="974d1-121">Cause: hello Remote Desktop client on your computer can't resolve hello name of hello computer in hello settings of hello RDP file.</span></span>

<span data-ttu-id="974d1-122">Mogelijke oplossingen:</span><span class="sxs-lookup"><span data-stu-id="974d1-122">Possible solutions:</span></span>

* <span data-ttu-id="974d1-123">Als u op het intranet van een organisatie, zorg ervoor dat uw computer toegang tot toohello proxyserver heeft en tooit voor HTTPS-verkeer kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="974d1-123">If you're on an organization's intranet, make sure that your computer has access toohello proxy server and can send HTTPS traffic tooit.</span></span>
* <span data-ttu-id="974d1-124">Als u een lokaal opgeslagen RDP-bestand gebruikt, probeert u Hallo één die wordt gegenereerd door Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="974d1-124">If you're using a locally stored RDP file, try using hello one that's generated by hello portal.</span></span> <span data-ttu-id="974d1-125">Deze stap zorgt ervoor dat u het juiste DNS-naam Hallo voor Hallo virtuele machine, of Hallo-cloudservice en de eindpuntpoort Hallo Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="974d1-125">This step ensures that you have hello correct DNS name for hello virtual machine, or hello cloud service and hello endpoint port of hello VM.</span></span> <span data-ttu-id="974d1-126">Hier volgt een voorbeeld RDP-bestand die worden gegenereerd door Hallo-portal:</span><span class="sxs-lookup"><span data-stu-id="974d1-126">Here is a sample RDP file generated by hello portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="974d1-127">Hallo gedeelte van dit RDP-bestand is:</span><span class="sxs-lookup"><span data-stu-id="974d1-127">hello address portion of this RDP file has:</span></span>

* <span data-ttu-id="974d1-128">Hallo volledig gekwalificeerde domeinnaam van het Hallo-cloudservice met Hallo VM ('tailspin-azdatatier.cloudapp.net' in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="974d1-128">hello fully qualified domain name of hello cloud service that contains hello VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="974d1-129">Hallo externe TCP-poort van het Hallo-eindpunt voor extern bureaublad-verkeer (55919).</span><span class="sxs-lookup"><span data-stu-id="974d1-129">hello external TCP port of hello endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="974d1-130">Er is een verificatiefout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="974d1-130">An authentication error has occurred.</span></span> <span data-ttu-id="974d1-131">Hallo Local Security Authority is niet bereikbaar.</span><span class="sxs-lookup"><span data-stu-id="974d1-131">hello Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="974d1-132">Oorzaak: Hallo doel VM kan Hallo certificeringsinstantie vinden in Hallo gebruiker-gedeelte van uw referenties.</span><span class="sxs-lookup"><span data-stu-id="974d1-132">Cause: hello target VM can't locate hello security authority in hello user name portion of your credentials.</span></span>

<span data-ttu-id="974d1-133">Wanneer uw gebruikersnaam in de vorm Hallo is *SecurityAuthority*\\*gebruikersnaam* (voorbeeld: corp\gebruiker1), Hallo *SecurityAuthority* gedeelte is ofwel Hallo VM van de naam van de computer (voor lokale beveiligingsautoriteit Hallo) of de naam van een Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="974d1-133">When your user name is in hello form *SecurityAuthority*\\*UserName* (example: CORP\User1), hello *SecurityAuthority* portion is either hello VM's computer name (for hello local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="974d1-134">Mogelijke oplossingen:</span><span class="sxs-lookup"><span data-stu-id="974d1-134">Possible solutions:</span></span>

* <span data-ttu-id="974d1-135">Als Hallo account lokale toohello VM, zorg er dan voor dat die Hallo VM-naam juist is gespeld.</span><span class="sxs-lookup"><span data-stu-id="974d1-135">If hello account is local toohello VM, make sure that hello VM name is spelled correctly.</span></span>
* <span data-ttu-id="974d1-136">Als het Hallo-account is op een Active Directory-domein, spelling Hallo van Hallo domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="974d1-136">If hello account is on an Active Directory domain, check hello spelling of hello domain name.</span></span>
* <span data-ttu-id="974d1-137">Als een Active Directory-domeinaccount en Hallo domeinnaam juist is gespeld, Controleer of een domeincontroller beschikbaar is in het domein.</span><span class="sxs-lookup"><span data-stu-id="974d1-137">If it is an Active Directory domain account and hello domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="974d1-138">Er is een veelvoorkomend probleem in Azure virtuele netwerken die een domeincontroller is niet beschikbaar omdat deze nog niet is gestart domeincontrollers bevatten.</span><span class="sxs-lookup"><span data-stu-id="974d1-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="974d1-139">U kunt een lokaal beheerdersaccount in plaats van een domeinaccount gebruiken als tijdelijke oplossing.</span><span class="sxs-lookup"><span data-stu-id="974d1-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="974d1-140">Fout bij de Windows-beveiliging: uw referenties werken niet.</span><span class="sxs-lookup"><span data-stu-id="974d1-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="974d1-141">Oorzaak: Hallo doel VM kan niet worden gevalideerd uw accountnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="974d1-141">Cause: hello target VM can't validate your account name and password.</span></span>

<span data-ttu-id="974d1-142">Een Windows-computer kunt valideren Hallo referenties van een lokaal account of een domeinaccount.</span><span class="sxs-lookup"><span data-stu-id="974d1-142">A Windows-based computer can validate hello credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="974d1-143">Gebruiken voor lokale accounts Hallo *ComputerName*\\*gebruikersnaam* syntaxis (voorbeeld: SQL1\Admin4798).</span><span class="sxs-lookup"><span data-stu-id="974d1-143">For local accounts, use hello *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="974d1-144">Gebruik voor domeinaccounts Hallo *DomainName*\\*gebruikersnaam* syntaxis (voorbeeld: CONTOSO\peterodman).</span><span class="sxs-lookup"><span data-stu-id="974d1-144">For domain accounts, use hello *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="974d1-145">Als uw VM tooa-domeincontroller in een nieuw Active Directory-forest is gepromoveerd, Hallo lokale administrator-account dat u aangemeld is geconverteerd tooan gelijkwaardige account Hello hetzelfde wachtwoord in Hallo nieuwe forest en domein.</span><span class="sxs-lookup"><span data-stu-id="974d1-145">If you have promoted your VM tooa domain controller in a new Active Directory forest, hello local administrator account that you signed in with is converted tooan equivalent account with hello same password in hello new forest and domain.</span></span> <span data-ttu-id="974d1-146">Hallo lokale account wordt vervolgens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="974d1-146">hello local account is then deleted.</span></span>

<span data-ttu-id="974d1-147">Bijvoorbeeld, als u bent aangemeld met Hallo lokale account DC1\DCAdmin en vervolgens Hallo virtuele machine gepromoveerd tot een domeincontroller in een nieuw forest voor Hallo corp.contoso.com domein, Hallo DC1\DCAdmin lokale account wordt verwijderd en een nieuw domeinaccount (CORP\DCAdmin ) is gemaakt met de Hallo hetzelfde wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="974d1-147">For example, if you signed in with hello local account DC1\DCAdmin, and then promoted hello virtual machine as a domain controller in a new forest for hello corp.contoso.com domain, hello DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with hello same password.</span></span>

<span data-ttu-id="974d1-148">Zorg ervoor dat Hallo-accountnaam is een naam of Hallo virtuele machine als een geldig account kunt controleren, en dat Hallo-wachtwoord juist is.</span><span class="sxs-lookup"><span data-stu-id="974d1-148">Make sure that hello account name is a name that hello virtual machine can verify as a valid account, and that hello password is correct.</span></span>

<span data-ttu-id="974d1-149">Als u toochange Hallo wachtwoord van de lokale beheerdersaccount hello moet, Zie [hoe tooreset een wachtwoord of Hallo extern bureaublad voor virtuele machines van Windows service](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974d1-149">If you need toochange hello password of hello local administrator account, see [How tooreset a password or hello Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a><span data-ttu-id="974d1-150">Deze computer kan geen verbinding met het maken van de externe computer toohello.</span><span class="sxs-lookup"><span data-stu-id="974d1-150">This computer can't connect toohello remote computer.</span></span>
<span data-ttu-id="974d1-151">Oorzaak: Hallo-account dat is gebruikt tooconnect heeft geen extern bureaublad aanmelden rechten.</span><span class="sxs-lookup"><span data-stu-id="974d1-151">Cause: hello account that's used tooconnect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="974d1-152">Elke Windows-computer is een lokale gebruikersgroep van de extern bureaublad, die Hallo accounts en groepen die op afstand in de App kunnen ondertekenen bevat.</span><span class="sxs-lookup"><span data-stu-id="974d1-152">Every Windows computer has a Remote Desktop users local group, which contains hello accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="974d1-153">Leden van de lokale beheerdersgroep Hallo hebben toegang, zelfs als deze accounts niet worden weergegeven in de lokale gebruikersgroep Hallo extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="974d1-153">Members of hello local administrators group also have access, even though those accounts are not listed in hello Remote Desktop users local group.</span></span> <span data-ttu-id="974d1-154">Hallo lokale groep administrators bevat ook Hallo Domeinbeheerders voor Hallo domein voor domein-machines.</span><span class="sxs-lookup"><span data-stu-id="974d1-154">For domain-joined machines, hello local administrators group also contains hello domain administrators for hello domain.</span></span>

<span data-ttu-id="974d1-155">Zorg ervoor dat Hallo account u tooconnect met extern bureaublad-aanmelden-rechten heeft.</span><span class="sxs-lookup"><span data-stu-id="974d1-155">Make sure that hello account you're using tooconnect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="974d1-156">Gebruik als tijdelijke oplossing een domein of lokale administrator-account tooconnect via Extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="974d1-156">As a workaround, use a domain or local administrator account tooconnect over Remote Desktop.</span></span> <span data-ttu-id="974d1-157">tooadd Hallo lokale gebruikersgroep van gewenste account toohello extern bureaublad, Hallo Microsoft Management Console-module gebruiken (**Systeemwerkset > lokale gebruikers en groepen > groepen > Externe bureaubladgebruikers**).</span><span class="sxs-lookup"><span data-stu-id="974d1-157">tooadd hello desired account toohello Remote Desktop users local group, use hello Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="974d1-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="974d1-158">Next steps</span></span>
<span data-ttu-id="974d1-159">Als geen van deze fouten is opgetreden en er een onbekend probleem met het verbinding maken met behulp van RDP, raadpleegt u Hallo [problemen oplossen met extern bureaublad](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974d1-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see hello [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="974d1-160">Zie voor probleemoplossing bij het openen van toepassingen die worden uitgevoerd op een virtuele machine, [problemen met toegang tooan toepassing die wordt uitgevoerd op een Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974d1-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access tooan application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="974d1-161">Als u problemen met het gebruik van Secure Shell (SSH) tooconnect tooa Linux VM in Azure hebt, raadpleegt u [oplossen SSH-verbindingen tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="974d1-161">If you are having issues using Secure Shell (SSH) tooconnect tooa Linux VM in Azure, see [Troubleshoot SSH connections tooa Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

