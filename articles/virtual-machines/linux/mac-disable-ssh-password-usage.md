---
title: aaaDisable SSH wachtwoorden op uw Linux-VM configureren SSHD | Microsoft Docs
description: Beveilig uw Linux-VM op Azure door wachtwoord aanmeldingen voor SSH uit te schakelen.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="aad59-103">SSH-wachtwoorden op uw Linux-VM uitschakelen door SSHD configureren</span><span class="sxs-lookup"><span data-stu-id="aad59-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="aad59-104">In dit artikel is gericht op het toolock omlaag Hallo aanmeldingsbeveiliging van uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="aad59-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="aad59-105">Zodra de Hallo SSH-poort 22 wordt geopend start toohello world bots toologin probeert door te raden wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="aad59-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="aad59-106">Wat gebeurt in dit artikel is wachtwoord aanmeldingen via SSH uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="aad59-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="aad59-107">Door het verwijderen van volledig Hallo mogelijkheid forceren toouse wachtwoorden we Hallo Linux VM beschermen tegen brute dit type aanval.</span><span class="sxs-lookup"><span data-stu-id="aad59-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="aad59-108">Hallo toegevoegd extra is we Linux SSHD tooonly toestaan configureert veel Hallo veiligste manier toologin tooLinux aanmeldingen via SSH openbare en persoonlijke sleutels.</span><span class="sxs-lookup"><span data-stu-id="aad59-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="aad59-109">Hallo mogelijke combinaties van deze vereist tooguess Hallo persoonlijke sleutel is enorme en daarom raadt af bots van zelfs proberen alles tootry toobrute force SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="aad59-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="aad59-110">Doelstellingen</span><span class="sxs-lookup"><span data-stu-id="aad59-110">Goals</span></span>
* <span data-ttu-id="aad59-111">SSHD toodisallow configureren:</span><span class="sxs-lookup"><span data-stu-id="aad59-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="aad59-112">Wachtwoord aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="aad59-112">Password logins</span></span>
  * <span data-ttu-id="aad59-113">Hoofdmap gebruikersaanmelding</span><span class="sxs-lookup"><span data-stu-id="aad59-113">Root user login</span></span>
  * <span data-ttu-id="aad59-114">Vraag en antwoord-verificatie</span><span class="sxs-lookup"><span data-stu-id="aad59-114">Challenge-response authentication</span></span>
* <span data-ttu-id="aad59-115">SSHD tooallow configureren:</span><span class="sxs-lookup"><span data-stu-id="aad59-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="aad59-116">alleen sleutel SSH aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="aad59-116">only SSH key logins</span></span>
* <span data-ttu-id="aad59-117">Opnieuw opstarten SSHD terwijl u nog steeds bent aangemeld</span><span class="sxs-lookup"><span data-stu-id="aad59-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="aad59-118">Test Hallo nieuwe SSHD configuratie</span><span class="sxs-lookup"><span data-stu-id="aad59-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="aad59-119">Inleiding</span><span class="sxs-lookup"><span data-stu-id="aad59-119">Introduction</span></span>
[<span data-ttu-id="aad59-120">SSH gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="aad59-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="aad59-121">SSHD is hello SSH-Server die wordt uitgevoerd op Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="aad59-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="aad59-122">SSH is een client die op een shell op uw werkstation MacBook- of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aad59-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="aad59-123">SSH is ook Hallo-protocol gebruikt toosecure en Hallo uitgewisseld tussen uw werkstation en het Hallo Linux VM versleutelen.</span><span class="sxs-lookup"><span data-stu-id="aad59-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="aad59-124">Voor dit artikel is zeer belangrijk tookeep één aanmelding tooyour Linux VM geopend voor de hele Hallo doorlopen.</span><span class="sxs-lookup"><span data-stu-id="aad59-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="aad59-125">Om deze reden wordt we twee aansluitingen en SSH toohello Linux VM openen vanuit van beide.</span><span class="sxs-lookup"><span data-stu-id="aad59-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="aad59-126">We Hallo eerste terminal toomake Hallo wijzigingen tooSSHDs configuratiebestand gebruiken en Hallo SSHD-service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="aad59-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="aad59-127">We gebruiken Hallo tweede terminal tootest die wordt gewijzigd nadat het Hallo-service opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="aad59-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="aad59-128">Omdat we bij het uitschakelen van SSH wachtwoorden afhankelijk strikt SSH-sleutels, als uw SSH-sleutels niet juist zijn en sluiten van Hallo verbinding toohello VM, hello VM wordt permanent vergrendeld en kan niemand zich kunnen toologin tooit verplicht stelt toobe verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aad59-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aad59-129">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aad59-129">Prerequisites</span></span>
* [<span data-ttu-id="aad59-130">SSH-sleutels maken in Linux en Mac voor virtuele Linux-machines in Azure</span><span class="sxs-lookup"><span data-stu-id="aad59-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="aad59-131">Azure-account</span><span class="sxs-lookup"><span data-stu-id="aad59-131">Azure account</span></span>
  * [<span data-ttu-id="aad59-132">gratis proefversie te registreren</span><span class="sxs-lookup"><span data-stu-id="aad59-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="aad59-133">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aad59-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="aad59-134">Linux-VM uitgevoerd op azure</span><span class="sxs-lookup"><span data-stu-id="aad59-134">Linux VM running on azure</span></span>
* <span data-ttu-id="aad59-135">SSH openbare sleutelpaar in`~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="aad59-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="aad59-136">Openbare SSH-sleutel in `~/.ssh/authorized_keys` op Hallo Linux VM</span><span class="sxs-lookup"><span data-stu-id="aad59-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="aad59-137">Sudo-rechten op Hallo VM</span><span class="sxs-lookup"><span data-stu-id="aad59-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="aad59-138">Poort 22 openen</span><span class="sxs-lookup"><span data-stu-id="aad59-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="aad59-139">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="aad59-139">Quick Commands</span></span>
<span data-ttu-id="aad59-140">*Doorgewinterde Linux-beheerders die Hallo TLDR versie begint u hier.  Voor alle andere Hallo wil overslaan gedetailleerde uitleg en doorloop in deze sectie.*</span><span class="sxs-lookup"><span data-stu-id="aad59-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="aad59-141">Hallo-configuratiebestand als volgt bewerken:</span><span class="sxs-lookup"><span data-stu-id="aad59-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="aad59-142">Hallo SSHD service opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="aad59-142">Restart hello SSHD service.</span></span> <span data-ttu-id="aad59-143">Op op basis van Debian distributies:</span><span class="sxs-lookup"><span data-stu-id="aad59-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="aad59-144">Op op basis van Red Hat distributies:</span><span class="sxs-lookup"><span data-stu-id="aad59-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="aad59-145">Gedetailleerde Doorloop</span><span class="sxs-lookup"><span data-stu-id="aad59-145">Detailed Walk Through</span></span>
<span data-ttu-id="aad59-146">Aanmelding toohello Linux VM op terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="aad59-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="aad59-147">Aanmelding toohello Linux VM op terminal 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="aad59-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="aad59-148">Op tijdstip T2 gaan we tooedit hello SSHD-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="aad59-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="aad59-149">Hier wordt alleen Hallo instellingen toodisable wachtwoorden bewerken en SSH-sleutel aanmeldingen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="aad59-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="aad59-150">Er zijn veel instellingen in dit bestand dat u moet onderzoeken en toomake Linux & SSH zo veilig naar wens wijzigen.</span><span class="sxs-lookup"><span data-stu-id="aad59-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="aad59-151">Wachtwoord aanmeldingen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="aad59-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="aad59-152">Verificatie van openbare sleutels inschakelen</span><span class="sxs-lookup"><span data-stu-id="aad59-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="aad59-153">Hoofdmap aanmelding uitschakelen</span><span class="sxs-lookup"><span data-stu-id="aad59-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="aad59-154">Vraag en antwoord-verificatie uit te schakelen</span><span class="sxs-lookup"><span data-stu-id="aad59-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="aad59-155">Opnieuw opstarten SSHD</span><span class="sxs-lookup"><span data-stu-id="aad59-155">Restart SSHD</span></span>
<span data-ttu-id="aad59-156">Controleer of dat u nog steeds bent aangemeld vanuit Hallo T1-shell.</span><span class="sxs-lookup"><span data-stu-id="aad59-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="aad59-157">Dit is essentieel zodat u bent niet toegang buiten uw virtuele machine als uw SSH-sleutels niet correct zijn omdat wachtwoorden zijn nu uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="aad59-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="aad59-158">Als u alle instellingen zijn onjuist op uw Linux-VM kunt u T1 toofix sshd_config als u nog steeds wordt vastgelegd in en SSH Hallo verbinding actief tijdens Hallo SSHD-service houden wordt opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="aad59-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="aad59-159">Van T2 uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="aad59-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="aad59-160">Op Hallo Debian-familie</span><span class="sxs-lookup"><span data-stu-id="aad59-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="aad59-161">Op Hallo RedHat familie</span><span class="sxs-lookup"><span data-stu-id="aad59-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="aad59-162">Wachtwoorden zijn nu uitgeschakeld op de virtuele machine die beschermt tegen beveiligingsaanvallen wachtwoord aanmeldingspogingen.</span><span class="sxs-lookup"><span data-stu-id="aad59-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="aad59-163">U kunt toologin sneller en veel veiligere worden met alleen de SSH-sleutels toegestaan.</span><span class="sxs-lookup"><span data-stu-id="aad59-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

