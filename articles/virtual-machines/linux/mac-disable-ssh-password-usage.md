---
title: SSH-wachtwoorden op uw Linux-VM uitschakelen door het configureren van SSHD | Microsoft Docs
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
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="0f9d1-103">SSH-wachtwoorden op uw Linux-VM uitschakelen door SSHD configureren</span><span class="sxs-lookup"><span data-stu-id="0f9d1-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="0f9d1-104">In dit artikel is gericht op het vergrendelen van de beveiliging van de aanmelding van de Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-104">This article focuses on how to lock down the login security of your Linux VM.</span></span>  <span data-ttu-id="0f9d1-105">Zodra de SSH-poort 22 wordt geopend op het world bots begin probeert door te raden wachtwoorden aanmelden.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span></span>  <span data-ttu-id="0f9d1-106">Wat gebeurt in dit artikel is wachtwoord aanmeldingen via SSH uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="0f9d1-107">Door het volledig verwijderen van de mogelijkheid om wachtwoorden te gebruiken beveiligen we de Linux-VM van dit type beveiligingsaanval.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="0f9d1-108">Bijkomend voordeel is dat we Linux SSHD zodat alleen aanmeldingen via SSH openbare en persoonlijke sleutels voor aanmelding bij Linux veel de veiligste manier configureert.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span></span>  <span data-ttu-id="0f9d1-109">De mogelijke combinaties van deze vereist te raden de persoonlijke sleutel is enorme en daarom raadt af bots van zelfs proberen alles uit te proberen te beveiligingsaanvallen SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="0f9d1-110">Doelstellingen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-110">Goals</span></span>
* <span data-ttu-id="0f9d1-111">Configureer SSHD om te blokkeren:</span><span class="sxs-lookup"><span data-stu-id="0f9d1-111">Configure SSHD to disallow:</span></span>
  * <span data-ttu-id="0f9d1-112">Wachtwoord aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-112">Password logins</span></span>
  * <span data-ttu-id="0f9d1-113">Hoofdmap gebruikersaanmelding</span><span class="sxs-lookup"><span data-stu-id="0f9d1-113">Root user login</span></span>
  * <span data-ttu-id="0f9d1-114">Vraag en antwoord-verificatie</span><span class="sxs-lookup"><span data-stu-id="0f9d1-114">Challenge-response authentication</span></span>
* <span data-ttu-id="0f9d1-115">Configureer SSHD om toe te staan:</span><span class="sxs-lookup"><span data-stu-id="0f9d1-115">Configure SSHD to allow:</span></span>
  * <span data-ttu-id="0f9d1-116">alleen sleutel SSH aanmeldingen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-116">only SSH key logins</span></span>
* <span data-ttu-id="0f9d1-117">Opnieuw opstarten SSHD terwijl u nog steeds bent aangemeld</span><span class="sxs-lookup"><span data-stu-id="0f9d1-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="0f9d1-118">De configuratie van de nieuwe SSHD testen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-118">Test the new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="0f9d1-119">Inleiding</span><span class="sxs-lookup"><span data-stu-id="0f9d1-119">Introduction</span></span>
[<span data-ttu-id="0f9d1-120">SSH gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="0f9d1-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="0f9d1-121">SSHD is de SSH-Server die wordt uitgevoerd op de Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-121">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="0f9d1-122">SSH is een client die op een shell op uw werkstation MacBook- of Linux wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="0f9d1-123">SSH is ook het protocol dat wordt gebruikt voor het beveiligen en de communicatie tussen uw werkstation en de Linux-VM te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span></span>

<span data-ttu-id="0f9d1-124">Voor dit artikel is zeer belangrijk dat openen één aanmelding bij uw Linux-VM voor de hele doorlopen.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span></span>  <span data-ttu-id="0f9d1-125">Om deze reden wordt we twee aansluitingen en SSH voor Linux VM openen vanuit een van beide.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="0f9d1-126">De eerste terminal zullen worden gebruikt voor de wijzigingen aanbrengen in het configuratiebestand SSHDs en start de service SSHD.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="0f9d1-127">De tweede terminal zullen worden gebruikt voor het testen van deze wijzigingen zodra de service is gestart.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-127">We will use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="0f9d1-128">Omdat we bij het uitschakelen van SSH wachtwoorden afhankelijk strikt SSH-sleutels, als uw SSH-sleutels niet juist zijn en sluiten van de verbinding met de virtuele machine, de virtuele machine wordt permanent vergrendeld en kan niemand zich kunnen aanmelden bij deze verplicht stelt worden verwijderd en opnieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f9d1-129">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0f9d1-129">Prerequisites</span></span>
* [<span data-ttu-id="0f9d1-130">SSH-sleutels maken in Linux en Mac voor virtuele Linux-machines in Azure</span><span class="sxs-lookup"><span data-stu-id="0f9d1-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="0f9d1-131">Azure-account</span><span class="sxs-lookup"><span data-stu-id="0f9d1-131">Azure account</span></span>
  * [<span data-ttu-id="0f9d1-132">gratis proefversie te registreren</span><span class="sxs-lookup"><span data-stu-id="0f9d1-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="0f9d1-133">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0f9d1-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="0f9d1-134">Linux-VM uitgevoerd op azure</span><span class="sxs-lookup"><span data-stu-id="0f9d1-134">Linux VM running on azure</span></span>
* <span data-ttu-id="0f9d1-135">SSH openbare sleutelpaar in`~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="0f9d1-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="0f9d1-136">Openbare SSH-sleutel in `~/.ssh/authorized_keys` op de Linux-VM</span><span class="sxs-lookup"><span data-stu-id="0f9d1-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span></span>
* <span data-ttu-id="0f9d1-137">Sudo-rechten op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="0f9d1-137">Sudo rights on the VM</span></span>
* <span data-ttu-id="0f9d1-138">Poort 22 openen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0f9d1-139">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="0f9d1-139">Quick Commands</span></span>
<span data-ttu-id="0f9d1-140">*Doorgewinterde Linux Admins die de versie TLDR begint u hier.  Voor alle andere wil de gedetailleerde uitleg en doorloop deze sectie met overslaan.*</span><span class="sxs-lookup"><span data-stu-id="0f9d1-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="0f9d1-141">Bewerk het configuratiebestand wordt als volgt:</span><span class="sxs-lookup"><span data-stu-id="0f9d1-141">Edit the config file as follows:</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

<span data-ttu-id="0f9d1-142">Start de service SSHD.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-142">Restart the SSHD service.</span></span> <span data-ttu-id="0f9d1-143">Op op basis van Debian distributies:</span><span class="sxs-lookup"><span data-stu-id="0f9d1-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="0f9d1-144">Op op basis van Red Hat distributies:</span><span class="sxs-lookup"><span data-stu-id="0f9d1-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="0f9d1-145">Gedetailleerde Doorloop</span><span class="sxs-lookup"><span data-stu-id="0f9d1-145">Detailed Walk Through</span></span>
<span data-ttu-id="0f9d1-146">Meld u aan de Linux-VM op terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="0f9d1-146">Login to the Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="0f9d1-147">Meld u aan de Linux-VM op terminal 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="0f9d1-147">Login to the Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="0f9d1-148">Op tijdstip T2 gaan we het configuratiebestand SSHD bewerken.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-148">On T2 we are going to edit the SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="0f9d1-149">Hier bewerken we alleen de instellingen voor het uitschakelen van wachtwoorden en SSH-sleutel aanmeldingen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="0f9d1-150">Er zijn veel instellingen in dit bestand waarin u moet onderzoeken en wijzigt u Linux & SSH als beveiligen als u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="0f9d1-151">Wachtwoord aanmeldingen uitschakelen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="0f9d1-152">Verificatie van openbare sleutels inschakelen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="0f9d1-153">Hoofdmap aanmelding uitschakelen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="0f9d1-154">Vraag en antwoord-verificatie uit te schakelen</span><span class="sxs-lookup"><span data-stu-id="0f9d1-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="0f9d1-155">Opnieuw opstarten SSHD</span><span class="sxs-lookup"><span data-stu-id="0f9d1-155">Restart SSHD</span></span>
<span data-ttu-id="0f9d1-156">Op de shell T1 controleren dat u nog steeds bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-156">From the T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="0f9d1-157">Dit is essentieel zodat u bent niet toegang buiten uw virtuele machine als uw SSH-sleutels niet correct zijn omdat wachtwoorden zijn nu uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="0f9d1-158">Als u alle instellingen zijn onjuist op uw Linux-VM kunt u T1 om op te lossen sshd_config als u nog steeds wordt vastgelegd in en SSH de verbinding actief tijdens de service SSHD houden wordt start opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span></span>

<span data-ttu-id="0f9d1-159">Van T2 uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0f9d1-159">From T2 run:</span></span>

##### <a name="on-the-debian-family"></a><span data-ttu-id="0f9d1-160">Op de Debian-familie</span><span class="sxs-lookup"><span data-stu-id="0f9d1-160">On the Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a><span data-ttu-id="0f9d1-161">Op de familie RedHat</span><span class="sxs-lookup"><span data-stu-id="0f9d1-161">On the RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="0f9d1-162">Wachtwoorden zijn nu uitgeschakeld op de virtuele machine die beschermt tegen beveiligingsaanvallen wachtwoord aanmeldingspogingen.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="0f9d1-163">Toegestaan dat kunt u zich aanmelden sneller en veel veiligere met alleen de SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="0f9d1-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span></span>

