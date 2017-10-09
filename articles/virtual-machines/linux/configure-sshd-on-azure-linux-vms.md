---
title: aaaConfigure SSHD op Azure Linux Virtual Machines | Microsoft Docs
description: Configureer SSHD voor aanbevolen beveiligingsprocedures en toolockdown SSH tooAzure virtuele Linux-Machines.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="88c68-103">SSHD op Azure Linux VM's configureren</span><span class="sxs-lookup"><span data-stu-id="88c68-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="88c68-104">Dit artikel laat zien hoe toolockdown SSH-Server op Linux-, tooprovide aanbevolen procedures voor beveiliging en ook toospeed up Hallo SSH-aanmelding Hallo met behulp van SSH-sleutels in plaats van wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="88c68-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="88c68-105">toofurther lockdown SSHD gaan we toodisable Hallo hoofdgebruiker kunnen toologin worden Hallo gebruikers beperken die toologin via een groepslijst met goedgekeurde zijn toegestaan voor het uitschakelen van SSH-protocolversie 1, een minimale sleutel bits instellen en configureren van automatische-Meld u af bij niet-actieve gebruikers.</span><span class="sxs-lookup"><span data-stu-id="88c68-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="88c68-106">Hallo-vereisten voor dit artikel zijn: een Azure-account ([ophalen van een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/)) en [SSH openbare en persoonlijke sleutelbestanden](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88c68-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="88c68-107">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="88c68-107">Quick Commands</span></span>

<span data-ttu-id="88c68-108">Configureer `/etc/ssh/sshd_config` Hello volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="88c68-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="88c68-109">Wachtwoord aanmeldingen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="88c68-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="88c68-110">Aanmelding door Hallo hoofdgebruiker uitschakelen</span><span class="sxs-lookup"><span data-stu-id="88c68-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="88c68-111">Groepslijst met toegestane</span><span class="sxs-lookup"><span data-stu-id="88c68-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="88c68-112">Lijst met toegestane gebruikers</span><span class="sxs-lookup"><span data-stu-id="88c68-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="88c68-113">SSH-protocol versie 1 uitschakelen</span><span class="sxs-lookup"><span data-stu-id="88c68-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="88c68-114">Minimale sleutel bits</span><span class="sxs-lookup"><span data-stu-id="88c68-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="88c68-115">Verbreek de verbinding met niet-actieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="88c68-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="88c68-116">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="88c68-116">Detailed Walkthrough</span></span>

<span data-ttu-id="88c68-117">SSHD is hello SSH-Server die wordt uitgevoerd op Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="88c68-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="88c68-118">SSH is een client die wordt uitgevoerd vanuit een shell op uw MacBook, Linux-werkstation of vanuit een Bash op Windows.</span><span class="sxs-lookup"><span data-stu-id="88c68-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="88c68-119">SSH is ook Hallo-protocol gebruikt toosecure en coderen Hallo uitgewisseld tussen uw werkstation en het Hallo Linux VM maken SSH ook een VPN (virtueel particulier netwerk).</span><span class="sxs-lookup"><span data-stu-id="88c68-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="88c68-120">Voor dit artikel is zeer belangrijk tookeep één aanmelding tooyour Linux-VM voor de volledige procedure Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="88c68-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="88c68-121">Wanneer een SSH-verbinding is gemaakt, blijft deze als een geopende sessie, zolang het Hallo-venster niet is gesloten.</span><span class="sxs-lookup"><span data-stu-id="88c68-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="88c68-122">Met één terminal aangemeld, kunt u wijzigingen aangebracht toobe toohello SSHD service zonder dat ze worden geblokkeerd als een belangrijke wijziging wordt doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="88c68-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="88c68-123">Als u ophalen vergrendeld buiten uw Linux-VM met een verbroken SSHD configuratie, Azure biedt Hallo mogelijkheid tooreset een verbroken SSHD-configuratie met Hallo [Azure VM-extensie voor toegang tot](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88c68-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="88c68-124">Om deze reden openen we twee aansluitingen en SSH toohello Linux VM vanuit van beide.</span><span class="sxs-lookup"><span data-stu-id="88c68-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="88c68-125">We Hallo eerste terminal toomake Hallo wijzigingen tooSSHDs configuratiebestand gebruiken en Hallo SSHD-service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="88c68-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="88c68-126">We gebruiken Hallo tweede terminal tootest die wordt gewijzigd nadat het Hallo-service opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="88c68-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="88c68-127">Omdat we bij het uitschakelen van SSH wachtwoorden afhankelijk strikt SSH-sleutels, als uw SSH-sleutels niet juist zijn en sluiten van Hallo verbinding toohello VM, hello VM wordt permanent vergrendeld en kan niemand zich kunnen toologin tooit verplicht stelt toobe verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88c68-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="88c68-128">Wachtwoord aanmeldingen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="88c68-128">Disable password logins</span></span>

<span data-ttu-id="88c68-129">Hallo snelste manier toosecure u Linux VM toodisable wachtwoord aanmeldingen is.</span><span class="sxs-lookup"><span data-stu-id="88c68-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="88c68-130">Wanneer wachtwoord aanmeldingen zijn ingeschakeld, afdwingen bots verkennen Hallo web wordt direct gestart probeert toobrute raden Hallo wachtwoord voor uw Linux-VM met behulp van SSH.</span><span class="sxs-lookup"><span data-stu-id="88c68-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="88c68-131">Wachtwoord aanmeldingen volledig is uitgeschakeld, kunnen Hallo SSH server tooignore alle wachtwoord aanmeldingspogingen.</span><span class="sxs-lookup"><span data-stu-id="88c68-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="88c68-132">Aanmelding door Hallo hoofdgebruiker uitschakelen</span><span class="sxs-lookup"><span data-stu-id="88c68-132">Disable login by hello root user</span></span>

<span data-ttu-id="88c68-133">Volgende aanbevolen procedures voor Linux hello `root` gebruiker moet nooit worden aangemeld via SSH of met behulp van `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="88c68-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="88c68-134">Alle opdrachten die behoefte hebben aan machtigingen voor het niveau van hoofdmap moeten altijd worden uitgevoerd via Hallo `sudo` opdracht alle acties voor toekomstige controle registreert.</span><span class="sxs-lookup"><span data-stu-id="88c68-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="88c68-135">Uitschakelen Hallo `root` gebruiker aanmelden via SSH is een best practices beveiligingsstap die ervoor zorgt dat alleen geautoriseerde gebruikers tooSSH zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="88c68-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="88c68-136">Groepslijst met toegestane</span><span class="sxs-lookup"><span data-stu-id="88c68-136">Allowed groups list</span></span>

<span data-ttu-id="88c68-137">SSH biedt een methode voor het beperken van gebruikers en groepen die worden toegestaan of niet is toegestaan via SSH aanmelden.</span><span class="sxs-lookup"><span data-stu-id="88c68-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="88c68-138">Deze functie maakt gebruik van een lijst met tooapprove of specifieke gebruikers en groepen aanmelden weigeren.</span><span class="sxs-lookup"><span data-stu-id="88c68-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="88c68-139">Hallo wheel groep toohello instelling `AllowGroups` lijst met goedgekeurde aanmeldingen via SSH toojust gebruikersaccounts die in Hallo wheel groep beperkt.</span><span class="sxs-lookup"><span data-stu-id="88c68-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="88c68-140">Lijst met toegestane gebruikers</span><span class="sxs-lookup"><span data-stu-id="88c68-140">Allowed users list</span></span>

<span data-ttu-id="88c68-141">Beperken van de SSH-aanmeldingen toojust gebruikers is een meer specifiek manier tooaccomplish Hallo dezelfde taak die `AllowGroups` is.</span><span class="sxs-lookup"><span data-stu-id="88c68-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="88c68-142">SSH-protocol versie 1 uitschakelen</span><span class="sxs-lookup"><span data-stu-id="88c68-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="88c68-143">SSH-protocolversie 1 is niet veilig en moet zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="88c68-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="88c68-144">SSH-protocolversie 2 is Hallo huidige versie een veilige manier tooSSH tooyour-server biedt.</span><span class="sxs-lookup"><span data-stu-id="88c68-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="88c68-145">Uitschakelen van versie 1 van SSH, weigert SSH-clients die tooestablish probeert een verbinding met de Hallo SSH-server met versie 1 van SSH.</span><span class="sxs-lookup"><span data-stu-id="88c68-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="88c68-146">Alleen versie 2-SSH-verbindingen zijn toegestaan toonegotiate een verbinding met de Hallo SSH-server.</span><span class="sxs-lookup"><span data-stu-id="88c68-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="88c68-147">Minimale sleutel bits</span><span class="sxs-lookup"><span data-stu-id="88c68-147">Minimum key bits</span></span>

<span data-ttu-id="88c68-148">Aanbevolen beveiligingsprocedures wachtwoord SSH-aanmeldingen zijn uitgeschakeld en SSH-sleutels toobe tooauthenticate gebruikt met Hallo SSH-server zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="88c68-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="88c68-149">Deze SSH-sleutels kunnen worden gemaakt met behulp van verschillende lengtes sleutels, gemeten in bits.</span><span class="sxs-lookup"><span data-stu-id="88c68-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="88c68-150">Aanbevolen procedures statussen dat sleutels van 2048 bits lang Hallo minimale acceptabele sleutelsterkte zijn.</span><span class="sxs-lookup"><span data-stu-id="88c68-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="88c68-151">Sleutels van minder dan 2048 bits kunnen theoretisch worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="88c68-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="88c68-152">Instelling Hallo `ServerKeyBits` te`2048` staat verbindingen met behulp van de sleutels van 2048 bits of hoger en verbindingen van minder dan 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="88c68-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="88c68-153">Verbreek de verbinding met niet-actieve gebruikers</span><span class="sxs-lookup"><span data-stu-id="88c68-153">Disconnect idle users</span></span>

<span data-ttu-id="88c68-154">SSH heeft Hallo mogelijkheid toodisconnect gebruikers die open verbinding die meer dan een ingestelde periode van seconden inactief zijn gebleven.</span><span class="sxs-lookup"><span data-stu-id="88c68-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="88c68-155">Open sessies tooonly houden die gebruikers die active limieten Hallo blootstelling van Hallo Linux VM zijn.</span><span class="sxs-lookup"><span data-stu-id="88c68-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="88c68-156">Opnieuw opstarten SSHD</span><span class="sxs-lookup"><span data-stu-id="88c68-156">Restart SSHD</span></span>

<span data-ttu-id="88c68-157">instellingen voor tooenable Hallo in `/etc/ssh/sshd_config` hello SSHD proces opnieuw Hallo SSH-server opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="88c68-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="88c68-158">Hallo terminalvenster u toorestart Hallo SSH-server gebruiken zonder verlies van Hallo open SSH-sessie geopend blijven.</span><span class="sxs-lookup"><span data-stu-id="88c68-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="88c68-159">tootest hello nieuwe SSH-serverinstellingen gebruiken een tweede terminalvenster of tabblad.  Kunt u met behulp van een afzonderlijke terminal tootest Hallo SSH-verbinding toogo terug en controleer aanvullende wijzigingen toohello `/etc/ssh/sshd_config` in de eerste terminal Hallo zonder dat ze worden geblokkeerd door een recente SSHD wijziging.</span><span class="sxs-lookup"><span data-stu-id="88c68-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="88c68-160">Op Redhat, Centos en Fedora</span><span class="sxs-lookup"><span data-stu-id="88c68-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="88c68-161">Op Debian en Ubuntu</span><span class="sxs-lookup"><span data-stu-id="88c68-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="88c68-162">Opnieuw instellen van SSHD met behulp van Azure reset-toegang</span><span class="sxs-lookup"><span data-stu-id="88c68-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="88c68-163">Als u van een recente wijziging toohello SSHD configuratie zijn vergrendeld kunt u hello Azure VM-uitbreiding voor toegang tot tooreset hello SSHD configuratie back toohello oorspronkelijke configuratie.</span><span class="sxs-lookup"><span data-stu-id="88c68-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="88c68-164">Alle voorbeeldnamen vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="88c68-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="88c68-165">Fail2ban installeren</span><span class="sxs-lookup"><span data-stu-id="88c68-165">Install Fail2ban</span></span>

<span data-ttu-id="88c68-166">Het is raadzaam tooinstall en setup Hallo open-source app Fail2ban, welke blokken herhaalde pogingen toologin tooyour Linux VM via SSH met brute kracht.</span><span class="sxs-lookup"><span data-stu-id="88c68-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="88c68-167">Fail2ban logboeken herhaalde pogingen toologin mislukt via SSH en maakt vervolgens firewallregels tooblock Hallo IP-adres dat Hallo pogingen afkomstig zijn uit.</span><span class="sxs-lookup"><span data-stu-id="88c68-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="88c68-168">Fail2ban startpagina</span><span class="sxs-lookup"><span data-stu-id="88c68-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="88c68-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88c68-169">Next Steps</span></span>

<span data-ttu-id="88c68-170">Nu dat u hebt geconfigureerd en Hallo SSH-server op uw Linux-VM vergrendeld zijn er aanbevolen procedures voor extra beveiliging die kunt u volgen.</span><span class="sxs-lookup"><span data-stu-id="88c68-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="88c68-171">Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="88c68-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="88c68-172">Versleutelen van schijven op een Linux-VM met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="88c68-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="88c68-173">Toegang en beveiliging in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="88c68-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
