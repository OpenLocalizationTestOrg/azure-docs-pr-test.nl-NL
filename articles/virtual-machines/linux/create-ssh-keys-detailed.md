---
title: aaaDetailed stappen toocreate een SSH-sleutelpaar voor virtuele Linux-machines in Azure | Microsoft Docs
description: Informatie over extra stappen toocreate de openbare en persoonlijke sleutelpaar voor een SSH voor virtuele Linux-machines in Azure, samen met specifieke certificaten voor verschillende gebruiksscenario.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="4894e-103">Gedetailleerde doorloop toocreate een SSH-sleutelpaar en extra certificaten voor een Linux-VM in Azure</span><span class="sxs-lookup"><span data-stu-id="4894e-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="4894e-104">U kunt virtuele Machines in Azure die standaard toousing SSH-sleutels voor verificatie, hoeft u Hallo wachtwoorden toolog in maken met een SSH-sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="4894e-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="4894e-105">Wachtwoorden kunnen worden geraden en uw wachtwoord voor uw virtuele machines van toorelentless brute kracht aanvallen tooguess openen.</span><span class="sxs-lookup"><span data-stu-id="4894e-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="4894e-106">Virtuele machines die zijn gemaakt met hello Azure CLI of Resource Manager-sjablonen kunnen uw openbare SSH-sleutel als onderdeel van Hallo-implementatie, het verwijderen van een post-implementatie stap in de configuratie van het wachtwoord aanmeldingen uitschakelen voor SSH bevatten.</span><span class="sxs-lookup"><span data-stu-id="4894e-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="4894e-107">Dit artikel vindt gedetailleerde stappen en aanvullende voorbeelden gegeven van certificaten genereren, zoals voor gebruik met de virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="4894e-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="4894e-108">Als u tooquickly wilt maken en gebruiken van een SSH-sleutelpaar, Zie [hoe toocreate een SSH-sleutel voor openbare en persoonlijke koppelen voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="4894e-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="4894e-109">Inzicht in SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="4894e-109">Understanding SSH keys</span></span>

<span data-ttu-id="4894e-110">Met behulp van SSH openbare en persoonlijke sleutels is Hallo gemakkelijkste manier toolog in tooyour Linux-servers.</span><span class="sxs-lookup"><span data-stu-id="4894e-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="4894e-111">[Cryptografie met openbare sleutels](https://en.wikipedia.org/wiki/Public-key_cryptography) biedt een veel veiligere manier toolog in tooyour Linux- of BSD VM in Azure dan wachtwoorden, die brute-geforceerde aanzienlijk eenvoudiger worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="4894e-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="4894e-112">Uw openbare sleutel kan worden gedeeld met iedereen, maar alleen u (of uw lokale beveiligingsinfrastructuur) beschikt over uw persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="4894e-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="4894e-113">persoonlijke Hallo SSH-sleutel moet een [zeer beveiligd wachtwoord](https://www.xkcd.com/936/) (bron:[xkcd.com](https://xkcd.com)) toosafeguard deze.</span><span class="sxs-lookup"><span data-stu-id="4894e-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="4894e-114">Dit wachtwoord wordt alleen tooaccess Hallo persoonlijke SSH-sleutelbestand en **is niet** Hallo het wachtwoord voor gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="4894e-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="4894e-115">Wanneer u een wachtwoord tooyour SSH-sleutel toevoegt, gecodeerd Hallo persoonlijke sleutel met AES 128-bits, zodat hello persoonlijke sleutel zonder Hallo wachtwoord toodecrypt onbruikbaar is wordt.</span><span class="sxs-lookup"><span data-stu-id="4894e-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="4894e-116">Als een aanvaller stelen van uw persoonlijke sleutel en dat sleutel heeft geen een wachtwoord, is ze zou kunnen toouse dat persoonlijke sleutel toolog in tooany servers waarop de bijbehorende openbare sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4894e-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="4894e-117">Als een persoonlijke sleutel is beveiligd met een wachtwoord, kan deze niet worden gebruikt door de aanvaller. Zo beschikt u over een extra beveiligingslaag voor uw infrastructuur in Azure.</span><span class="sxs-lookup"><span data-stu-id="4894e-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="4894e-118">In dit artikel maakt een SSH-protocolversie 2 RSA openbare en persoonlijke sleutelbestand paar (ook waarnaar wordt verwezen tooas 'ssh-rsa' sleutels), wordt aanbevolen voor implementaties met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4894e-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="4894e-119">*SSH-rsa* sleutels zijn vereist op Hallo [portal](https://portal.azure.com) voor zowel klassieke implementaties van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4894e-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="4894e-120">Gebruik en voordelen van SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="4894e-120">SSH keys use and benefits</span></span>

<span data-ttu-id="4894e-121">Azure vereist ten minste 2048 bits SSH-protocol versie 2 RSA-indeling openbare en persoonlijke sleutels; Hallo-bestand met openbare sleutel heeft Hallo `.pub` containerindeling.</span><span class="sxs-lookup"><span data-stu-id="4894e-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="4894e-122">Hallo toocreate sleutels gebruik `ssh-keygen`, die een reeks vragen en schrijft u een persoonlijke sleutel en een overeenkomende openbare sleutel.</span><span class="sxs-lookup"><span data-stu-id="4894e-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="4894e-123">Wanneer een Azure VM is gemaakt, Azure kopieën openbare sleutel toohello Hallo `~/.ssh/authorized_keys` map op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="4894e-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="4894e-124">SSH-sleutels in `~/.ssh/authorized_keys` gebruikte toochallenge Hallo client toomatch Hallo bijbehorende persoonlijke sleutel van een SSH-aanmelding verbinding zijn.</span><span class="sxs-lookup"><span data-stu-id="4894e-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="4894e-125">Wanneer een virtuele machine van Azure Linux is gemaakt met behulp van SSH-sleutels voor verificatie, Azure Hallo SSHD configureert server toonot toestaan wachtwoord aanmeldingen, SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="4894e-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="4894e-126">Daarom maakt Azure Linux VM's met SSH-sleutels, kunt u helpen beveiligen Hallo VM-implementatie en besparen Hallo standaardconfiguratie na de implementatie stap van het uitschakelen van wachtwoorden in Hallo **sshd_config** bestand.</span><span class="sxs-lookup"><span data-stu-id="4894e-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="4894e-127">ssh-keygen gebruiken</span><span class="sxs-lookup"><span data-stu-id="4894e-127">Using ssh-keygen</span></span>

<span data-ttu-id="4894e-128">Deze opdracht maakt u een wachtwoord beveiligd (versleuteld) SSH-sleutelpaar met 2048-bits RSA en deze opmerkingen tooeasily worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="4894e-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="4894e-129">SSH sleutels zijn standaard bewaard in Hallo `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="4894e-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="4894e-130">Als u nog geen een `~/.ssh` directory, Hallo `ssh-keygen` opdracht maakt het voor u Hello juiste machtigingen.</span><span class="sxs-lookup"><span data-stu-id="4894e-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="4894e-131">*Uitleg van de opdracht*</span><span class="sxs-lookup"><span data-stu-id="4894e-131">*Command explained*</span></span>

<span data-ttu-id="4894e-132">`ssh-keygen`Hallo programma gebruikt toocreate Hallo sleutels =</span><span class="sxs-lookup"><span data-stu-id="4894e-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="4894e-133">`-t rsa`= type sleutel toocreate Hallo RSA-indeling [wikipedia][parens aan einde](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = aantal bits van Hallo-sleutel</span><span class="sxs-lookup"><span data-stu-id="4894e-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="4894e-134">`-C "azureuser@myserver"`= een opmerking toegevoegde toohello einde van Hallo openbaar-sleutelbestand tooeasily worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="4894e-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="4894e-135">Normaal gesproken een e-mailbericht wordt gebruikt als Hallo Opmerking maar kunt u wat het beste werkt voor uw infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="4894e-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="4894e-136">Klassieke implementatie met behulp van`asm`</span><span class="sxs-lookup"><span data-stu-id="4894e-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="4894e-137">Als u van het klassieke implementatiemodel hello gebruikmaakt (`asm` modus in Hallo CLI), kunt u een openbare SSH-RSA-sleutel of een RFC4716 geformatteerd sleutel in een pem-container.</span><span class="sxs-lookup"><span data-stu-id="4894e-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="4894e-138">openbare sleutel voor SSH-RSA Hallo is wat eerder in dit artikel met behulp van is gemaakt `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="4894e-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="4894e-139">een RFC4716 toocreate ingedeeld sleutel van een bestaande openbare SSH-sleutel:</span><span class="sxs-lookup"><span data-stu-id="4894e-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="4894e-140">Voorbeeld van ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="4894e-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="4894e-141">Opgeslagen sleutelbestanden:</span><span class="sxs-lookup"><span data-stu-id="4894e-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="4894e-142">Hallo sleutelpaar naam voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4894e-142">hello key pair name for this article.</span></span>  <span data-ttu-id="4894e-143">Een sleutelpaar met de naam **id_rsa** is Hallo standaard en een aantal hulpprogramma's verwachten mogelijk Hallo **id_rsa** persoonlijke sleutelbestand naam dus is het een goed idee.</span><span class="sxs-lookup"><span data-stu-id="4894e-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="4894e-144">Hallo directory `~/.ssh/` is de standaardlocatie Hallo voor SSH-sleutelparen en Hallo SSH-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="4894e-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="4894e-145">Als niet wordt opgegeven met een volledig pad `ssh-keygen` Hallo sleutels maakt in Hallo huidige werkmap, niet de standaard Hallo `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="4894e-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="4894e-146">Een lijst met Hallo `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="4894e-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="4894e-147">Sleutelwachtwoord:</span><span class="sxs-lookup"><span data-stu-id="4894e-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="4894e-148">`ssh-keygen`tooa wachtwoord verwezen voor persoonlijke sleutelbestand Hallo als 'een wachtwoordzin.'</span><span class="sxs-lookup"><span data-stu-id="4894e-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="4894e-149">Het is *sterk* tooadd aanbevolen een wachtwoord tooyour persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="4894e-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="4894e-150">Zonder een wachtwoord beschermen Hallo sleutelbestand, kunt iedereen met Hallo bestand gebruiken toolog in tooany-server die de bijbehorende openbare sleutel Hallo heeft.</span><span class="sxs-lookup"><span data-stu-id="4894e-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="4894e-151">Toevoegen van een wachtwoord (wachtwoordzin) biedt meer beveiliging voor het geval iemand kunnen toogain toegang tooyour persoonlijke sleutelbestand is, krijgt u tijd toochange Hallo sleutels gebruikt tooauthenticate u.</span><span class="sxs-lookup"><span data-stu-id="4894e-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="4894e-152">Het wachtwoord van uw persoonlijke sleutel met behulp van ssh-agent toostore</span><span class="sxs-lookup"><span data-stu-id="4894e-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="4894e-153">Typ uw wachtwoord persoonlijke sleutelbestand bij elke SSH-aanmelding tooavoid kunt u `ssh-agent` toocache uw persoonlijke sleutelbestand wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="4894e-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="4894e-154">Als u een Mac OSX-sleutelketen Hallo Hallo persoonlijke sleutels, wachtwoorden veilig opslaat wanneer u aanroept `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="4894e-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="4894e-155">Controleren en gebruiken van ssh-agent en ssh-toevoegen tooinform Hallo SSH systeem over Hallo sleutelbestanden zodat Hallo wachtwoordzin niet toobe interactief gebruikt hoeven.</span><span class="sxs-lookup"><span data-stu-id="4894e-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="4894e-156">Nu de persoonlijke sleutel hello te toevoegen`ssh-agent` met Hallo opdracht `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="4894e-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="4894e-157">Hallo-wachtwoord voor persoonlijke sleutel wordt nu opgeslagen in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="4894e-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="4894e-158">Met behulp van `ssh-copy-id` toocopy Hallo sleutel tooan bestaande VM</span><span class="sxs-lookup"><span data-stu-id="4894e-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="4894e-159">Als u al een virtuele machine hebt gemaakt kunt u Hallo nieuwe SSH openbare sleutel tooyour Linux VM installeren met:</span><span class="sxs-lookup"><span data-stu-id="4894e-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="4894e-160">Een SSH-configuratiebestand maken en configureren</span><span class="sxs-lookup"><span data-stu-id="4894e-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="4894e-161">Het is een aanbevolen best practice toocreate en configureer een `~/.ssh/config` bestand toospeed up aanmeldingen en voor het optimaliseren van het gedrag van uw SSH-client.</span><span class="sxs-lookup"><span data-stu-id="4894e-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="4894e-162">Hallo volgende voorbeeld wordt een standaardconfiguratie getoond.</span><span class="sxs-lookup"><span data-stu-id="4894e-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="4894e-163">Hallo-bestand maken</span><span class="sxs-lookup"><span data-stu-id="4894e-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="4894e-164">Hallo bestand tooadd Hallo nieuwe SSH-configuratie bewerken:</span><span class="sxs-lookup"><span data-stu-id="4894e-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="4894e-165">Voorbeeld van `~/.ssh/config`-bestand:</span><span class="sxs-lookup"><span data-stu-id="4894e-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="4894e-166">Deze SSH-configuratie kunt u secties voor elke server tooenable elke toohave zijn eigen toegewezen sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="4894e-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="4894e-167">Hallo standaardinstellingen (`Host *`) zijn voor alle hosts die niet overeenkomen met de Hallo specifieke hosts hoger staan in het Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="4894e-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="4894e-168">Uitleg van configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="4894e-168">Config file explained</span></span>

<span data-ttu-id="4894e-169">`Host`= Hallo-naam van Hallo-host wordt aangeroepen op Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="4894e-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="4894e-170">`ssh fedora22`vertelt `SSH` toouse Hallo waarden in Hallo instellingenblok met het label `Host fedora22` Opmerking: Host mag een label dat logisch is voor uw gebruik en vertegenwoordigt geen Hallo werkelijke hostnaam van een server.</span><span class="sxs-lookup"><span data-stu-id="4894e-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="4894e-171">`Hostname 102.160.203.241`= Hallo IP-adres of de DNS-naam voor het Hallo-server die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4894e-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="4894e-172">`User ahmet`Hallo externe gebruiker account toouse = bij het aanmelden toohello-server.</span><span class="sxs-lookup"><span data-stu-id="4894e-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="4894e-173">`PubKeyAuthentication yes`= vertelt SSH in de gewenste toouse een SSH-sleutel toolog.</span><span class="sxs-lookup"><span data-stu-id="4894e-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="4894e-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= persoonlijke Hallo SSH-sleutel en de bijbehorende openbare sleutel toouse voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="4894e-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="4894e-175">SSH in Linux zonder een wachtwoord</span><span class="sxs-lookup"><span data-stu-id="4894e-175">SSH into Linux without a password</span></span>

<span data-ttu-id="4894e-176">Nu u een SSH-sleutelpaar en een geconfigureerd SSH-configuratiebestand hebt, bent u kunnen toolog in tooyour Linux VM snel en veilig.</span><span class="sxs-lookup"><span data-stu-id="4894e-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="4894e-177">Hallo eerste keer dat u zich aanmelden met behulp van de opdrachtprompts van een SSH-sleutel Hallo tooa-server u voor Hallo wachtwoordzin voor dat sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="4894e-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="4894e-178">Uitleg van de opdracht</span><span class="sxs-lookup"><span data-stu-id="4894e-178">Command explained</span></span>

<span data-ttu-id="4894e-179">Wanneer `ssh fedora22` wordt uitgevoerd SSH eerst zoekt en laadt u de instellingen van Hallo `Host fedora22` blok en laadt het vervolgens alle resterende instellingen van het laatste blok, Hallo Hallo `Host *`.</span><span class="sxs-lookup"><span data-stu-id="4894e-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4894e-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4894e-180">Next Steps</span></span>

<span data-ttu-id="4894e-181">Naast up toocreate Azure Linux VM's gebruikt Hallo nieuwe openbare SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="4894e-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="4894e-182">Azure virtuele machines die zijn gemaakt met een openbare SSH-sleutel als Hallo aanmelding zijn beter beveiligd dan virtuele machines die zijn gemaakt met de Hallo aanmelding standaardmethode wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="4894e-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="4894e-183">Virtuele Azure-machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden uitgeschakeld, waarmee brute force-aanvallen om wachtwoorden te raden worden voorkomen.</span><span class="sxs-lookup"><span data-stu-id="4894e-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="4894e-184">Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="4894e-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4894e-185">Maak een beveiligde Linux-VM met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4894e-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="4894e-186">Maak een beveiligde Linux VM hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="4894e-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
