---
title: aaaCreate een SSH-sleutelpaar voor virtuele Linux-machines in Azure | Microsoft Docs
description: "Maak op een veilige manier een sleutelpaar met een openbare en een privé-SSH-sleutel voor virtuele Azure Linux-machines."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="fe193-103">Een sleutelpaar met een openbare en een privé-SSH-sleutel maken voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="fe193-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="fe193-104">Dit artikel laat zien hoe een SSH-protocol versie 2 RSA openbare en persoonlijke sleutel toogenerate bestand paar toouse met virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="fe193-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="fe193-105">U kunt virtuele Machines in Azure die standaard toousing SSH-sleutels voor verificatie, hoeft u Hallo wachtwoorden toolog in maken met een SSH-sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="fe193-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="fe193-106">Wachtwoorden kunnen worden geraden en uw wachtwoord voor uw virtuele machines van toorelentless brute kracht aanvallen tooguess openen.</span><span class="sxs-lookup"><span data-stu-id="fe193-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="fe193-107">Virtuele machines die zijn gemaakt met Azure-sjablonen of Hallo `azure-cli` uw openbare SSH-sleutel kunt opnemen als onderdeel van Hallo-implementatie, het verwijderen van een post-implementatie stap in de configuratie van het wachtwoord aanmeldingen voor SSH uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="fe193-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="fe193-108">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="fe193-108">Quick Commands</span></span>

<span data-ttu-id="fe193-109">Hallo volgende opdrachten uit een Bash-shell, Hallo voorbeelden vervangen door uw eigen keuzes worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fe193-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="fe193-110">Uw openbare SSH-sleutelbestand wordt standaard gemaakt in `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="fe193-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="fe193-111">Als u wordt gevraagd met behulp van de volgende opdracht Hallo, moet u een 'wachtwoordzin' toosecure uw persoonlijke sleutel maken.</span><span class="sxs-lookup"><span data-stu-id="fe193-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="fe193-112">(Hallo wachtwoordzin is dat een wachtwoord gebruikt tooencrypt uw persoonlijke sleutel.)</span><span class="sxs-lookup"><span data-stu-id="fe193-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="fe193-113">Hallo nieuwe sleutel te toevoegen`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="fe193-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="fe193-114">Hallo hierboven opdrachten werk op Linux-besturingssystemen van bijna alle distributies, maar werken mogelijk niet in containers, zoals het Hallo-omgeving kan aanzienlijk worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="fe193-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="fe193-115">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="fe193-115">Detailed Walkthrough</span></span>

<span data-ttu-id="fe193-116">Met behulp van SSH openbare en persoonlijke sleutels is Hallo gemakkelijkste manier toolog in tooyour Linux-servers.</span><span class="sxs-lookup"><span data-stu-id="fe193-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="fe193-117">[Cryptografie met openbare sleutels](https://en.wikipedia.org/wiki/Public-key_cryptography) biedt een veel veiligere manier toolog in tooyour Linux- of BSD VM in Azure dan wachtwoorden, die brute-geforceerde aanzienlijk eenvoudiger worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="fe193-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe193-118">Uw openbare sleutel kan worden gedeeld met iedereen, maar alleen u (of uw lokale beveiligingsinfrastructuur) beschikt over uw persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="fe193-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="fe193-119">persoonlijke Hallo SSH-sleutel moet een [zeer beveiligd wachtwoord](https://www.xkcd.com/936/) (bron:[xkcd.com](https://xkcd.com)) toosafeguard deze.</span><span class="sxs-lookup"><span data-stu-id="fe193-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="fe193-120">Dit wachtwoord wordt alleen tooaccess Hallo persoonlijke SSH-sleutel en **is niet** Hallo het wachtwoord voor gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="fe193-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="fe193-121">Wanneer u een wachtwoord tooyour SSH-sleutel toevoegt, gecodeerd Hallo persoonlijke sleutel met AES 128-bits, zodat hello persoonlijke sleutel zonder Hallo wachtwoord toodecrypt onbruikbaar is wordt.</span><span class="sxs-lookup"><span data-stu-id="fe193-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="fe193-122">Als een aanvaller stelen van uw persoonlijke sleutel en dat sleutel heeft geen een wachtwoord, is ze zou kunnen toouse dat persoonlijke sleutel toolog in tooany servers waarop de bijbehorende openbare sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe193-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="fe193-123">Als een persoonlijke sleutel is beveiligd met een wachtwoord, kan deze niet worden gebruikt door de aanvaller. Zo beschikt u over een extra beveiligingslaag voor uw infrastructuur in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe193-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="fe193-124">In dit artikel maakt SSH-protocolversie 2 RSA openbare en persoonlijke sleutelbestanden, wordt aanbevolen voor implementaties op Hallo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe193-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="fe193-125">*SSH-rsa* sleutels zijn vereist op Hallo [portal](https://portal.azure.com) voor zowel klassieke implementaties van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe193-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="fe193-126">SSH-wachtwoorden uitschakelen met SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="fe193-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="fe193-127">Azure vereist openbare en persoonlijke sleutels van ten minste 2048 bits in ssh-rsa-indeling.</span><span class="sxs-lookup"><span data-stu-id="fe193-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="fe193-128">Hallo toocreate sleutels gebruik `ssh-keygen`, die een reeks vragen en schrijft u een persoonlijke sleutel en een overeenkomende openbare sleutel.</span><span class="sxs-lookup"><span data-stu-id="fe193-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="fe193-129">Als er een Azure VM is gemaakt, Hallo openbare sleutel te gekopieerd`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="fe193-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="fe193-130">SSH-sleutels in `~/.ssh/authorized_keys` gebruikte toochallenge Hallo client toomatch Hallo bijbehorende persoonlijke sleutel van een SSH-aanmelding verbinding zijn.</span><span class="sxs-lookup"><span data-stu-id="fe193-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="fe193-131">Wanneer een virtuele machine van Azure Linux is gemaakt met behulp van SSH-sleutels voor verificatie, Azure Hallo SSHD configureert server toonot toestaan wachtwoord aanmeldingen, SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="fe193-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="fe193-132">Daarom maakt Azure Linux VM's met SSH-sleutels, kunt u beveiligde Hallo VM-implementatie te en opslaan zelf Hallo standaardconfiguratie na de implementatie stap van het uitschakelen van wachtwoorden in Hallo sshd_config config-bestand.</span><span class="sxs-lookup"><span data-stu-id="fe193-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="fe193-133">ssh-keygen gebruiken</span><span class="sxs-lookup"><span data-stu-id="fe193-133">Using ssh-keygen</span></span>

<span data-ttu-id="fe193-134">Deze opdracht maakt u een wachtwoord beveiligd (versleuteld) SSH-sleutelpaar met 2048-bits RSA en deze opmerkingen tooeasily worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="fe193-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="fe193-135">SSH sleutels zijn standaard bewaard in Hallo `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="fe193-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="fe193-136">Als u nog geen een `~/.ssh` directory, Hallo `ssh-keygen` opdracht maakt het voor u Hello juiste machtigingen.</span><span class="sxs-lookup"><span data-stu-id="fe193-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="fe193-137">*Uitleg van de opdracht*</span><span class="sxs-lookup"><span data-stu-id="fe193-137">*Command explained*</span></span>

<span data-ttu-id="fe193-138">`ssh-keygen`Hallo programma gebruikt toocreate Hallo sleutels =</span><span class="sxs-lookup"><span data-stu-id="fe193-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="fe193-139">`-t rsa`= type sleutel toocreate Hallo RSA-indeling [](https://en.wikipedia.org/wiki/RSA_(cryptosystem) Wikipedia (Engelstalig)</span><span class="sxs-lookup"><span data-stu-id="fe193-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="fe193-140">`-b 2048`= aantal bits van Hallo-sleutel</span><span class="sxs-lookup"><span data-stu-id="fe193-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="fe193-141">Klassieke portal en X.509-certificaten</span><span class="sxs-lookup"><span data-stu-id="fe193-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="fe193-142">Als u Azure Hallo [klassieke portal](https://manage.windowsazure.com/), het x.509-certificaten voor Hallo SSH-sleutels vereist.</span><span class="sxs-lookup"><span data-stu-id="fe193-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="fe193-143">Er zijn geen andere typen openbare SSH-sleutels toegestaan. Het *moeten* X.509-certificaten zijn.</span><span class="sxs-lookup"><span data-stu-id="fe193-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="fe193-144">toocreate een X.509-certificaat van uw bestaande persoonlijke SSH-RSA-sleutel:</span><span class="sxs-lookup"><span data-stu-id="fe193-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="fe193-145">Klassieke implementatie met behulp van`asm`</span><span class="sxs-lookup"><span data-stu-id="fe193-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="fe193-146">Als u van Hallo-classic gebruikmaakt model implementeren (Azure CLI-servicebeheer `asm`), kunt u een openbare SSH-RSA-sleutel of een RFC4716 geformatteerd sleutel in een **.pem** container.</span><span class="sxs-lookup"><span data-stu-id="fe193-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="fe193-147">openbare sleutel voor SSH-RSA Hallo is wat eerder in dit artikel met behulp van is gemaakt `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="fe193-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="fe193-148">een RFC4716 toocreate ingedeeld sleutel van een bestaande openbare SSH-sleutel:</span><span class="sxs-lookup"><span data-stu-id="fe193-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="fe193-149">Voorbeeld van ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="fe193-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="fe193-150">Opgeslagen sleutelbestanden:</span><span class="sxs-lookup"><span data-stu-id="fe193-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="fe193-151">Hallo sleutelpaar naam voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="fe193-151">hello key pair name for this article.</span></span>  <span data-ttu-id="fe193-152">Een sleutelpaar met de naam **id_rsa** is Hallo standaard en een aantal hulpprogramma's verwachten mogelijk Hallo **id_rsa** persoonlijke sleutelbestand naam dus is het een goed idee.</span><span class="sxs-lookup"><span data-stu-id="fe193-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="fe193-153">Hallo directory `~/.ssh/` is de standaardlocatie Hallo voor SSH-sleutelparen en Hallo SSH-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="fe193-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="fe193-154">Als niet wordt opgegeven met een volledig pad `ssh-keygen` zal Hallo-sleutels maken in de huidige werkmap hello, niet standaard Hallo `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="fe193-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="fe193-155">Een lijst met Hallo `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="fe193-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="fe193-156">Sleutelwachtwoord:</span><span class="sxs-lookup"><span data-stu-id="fe193-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="fe193-157">`ssh-keygen`tooa wachtwoord gebruikt tooencrypt Hallo persoonlijke sleutel verwezen als 'een wachtwoordzin.'</span><span class="sxs-lookup"><span data-stu-id="fe193-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="fe193-158">Het is *sterk* tooadd een wachtwoordzin tooyour-sleutelparen aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="fe193-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="fe193-159">Zonder een wachtwoordzin beschermen Hallo persoonlijke sleutel, iedereen met Hallo sleutelbestand kan worden gebruikt toolog in tooany-server die de bijbehorende openbare sleutel Hallo heeft.</span><span class="sxs-lookup"><span data-stu-id="fe193-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="fe193-160">Toevoegen van een wachtwoordzin biedt meer beveiliging voor het geval iemand kunnen toogain toegang tooyour persoonlijke sleutelbestand is, zodat u tijd toochange Hallo sleutels gebruikt tooauthenticate u.</span><span class="sxs-lookup"><span data-stu-id="fe193-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="fe193-161">Het wachtwoord van uw persoonlijke sleutel met behulp van ssh-agent toostore</span><span class="sxs-lookup"><span data-stu-id="fe193-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="fe193-162">uw persoonlijke sleutel te typen tooavoid bestand wachtwoordzin met elke SSH-aanmelding, kunt u `ssh-agent` toocache uw persoonlijke sleutelbestand wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="fe193-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="fe193-163">Als u een Mac OSX-sleutelketen Hallo Hallo persoonlijke sleutels, wachtwoorden veilig opslaat wanneer u aanroept `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="fe193-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="fe193-164">Controleer en gebruik `ssh-agent` en `ssh-add` tooinform SSH systeem over sleutelbestanden Hallo Hallo zodat Hallo wachtwoordzin, hoeven niet toobe interactief gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fe193-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="fe193-165">Nu de persoonlijke sleutel hello te toevoegen`ssh-agent` met Hallo opdracht `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="fe193-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="fe193-166">Hallo-wachtwoord voor persoonlijke sleutel wordt nu opgeslagen in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="fe193-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="fe193-167">Met behulp van `ssh-copy-id` tooinstall Hallo nieuwe sleutel</span><span class="sxs-lookup"><span data-stu-id="fe193-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="fe193-168">Als u al een virtuele machine hebt gemaakt, kunt u Hallo nieuwe SSH openbare sleutel tooyour Linux VM installeren Hello de volgende opdracht, Hallo VM gebruikersnaam en het Hallo-serveradres vervangen door uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="fe193-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="fe193-169">Een SSH-configuratiebestand maken en configureren</span><span class="sxs-lookup"><span data-stu-id="fe193-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="fe193-170">Het is een best practice toocreate en configureer een `~/.ssh/config` bestand toospeed up aanmeldingen en voor het optimaliseren van het gedrag van uw SSH-client.</span><span class="sxs-lookup"><span data-stu-id="fe193-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="fe193-171">Hallo volgende voorbeeld wordt een standaardconfiguratie getoond.</span><span class="sxs-lookup"><span data-stu-id="fe193-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="fe193-172">Hallo-bestand maken</span><span class="sxs-lookup"><span data-stu-id="fe193-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="fe193-173">Hallo bestand tooadd Hallo nieuwe SSH-configuratie bewerken:</span><span class="sxs-lookup"><span data-stu-id="fe193-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="fe193-174">Voorbeeld van `~/.ssh/config`-bestand:</span><span class="sxs-lookup"><span data-stu-id="fe193-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="fe193-175">Deze SSH-configuratie kunt u secties voor elke server tooenable elke toohave zijn eigen toegewezen sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="fe193-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="fe193-176">Hallo standaardinstellingen (`Host *`) zijn voor alle hosts die niet overeenkomen met de Hallo specifieke hosts hoger staan in het Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="fe193-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="fe193-177">Uitleg van configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="fe193-177">Config file explained</span></span>

<span data-ttu-id="fe193-178">`Host`= Hallo-naam van Hallo-host wordt aangeroepen op Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="fe193-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="fe193-179">`ssh fedora22`vertelt `SSH` toouse Hallo waarden in Hallo instellingenblok met het label `Host fedora22` Opmerking: Host mag een label dat logisch is voor uw gebruik en vertegenwoordigt geen Hallo werkelijke hostnaam van een server.</span><span class="sxs-lookup"><span data-stu-id="fe193-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="fe193-180">`Hostname 102.160.203.241`= Hallo IP-adres of de DNS-naam voor het Hallo-server die wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="fe193-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="fe193-181">`User ahmet`Hallo externe gebruiker account toouse = bij het aanmelden toohello-server.</span><span class="sxs-lookup"><span data-stu-id="fe193-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="fe193-182">`PubKeyAuthentication yes`= vertelt SSH in de gewenste toouse een SSH-sleutel toolog.</span><span class="sxs-lookup"><span data-stu-id="fe193-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="fe193-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= persoonlijke Hallo SSH-sleutel en de bijbehorende openbare sleutel toouse voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="fe193-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="fe193-184">SSH in Linux zonder een wachtwoord</span><span class="sxs-lookup"><span data-stu-id="fe193-184">SSH into Linux without a password</span></span>

<span data-ttu-id="fe193-185">Nu u een SSH-sleutelpaar en een geconfigureerd SSH-configuratiebestand hebt, bent u kunnen toolog in tooyour Linux VM snel en veilig.</span><span class="sxs-lookup"><span data-stu-id="fe193-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="fe193-186">Hallo eerste keer dat u zich aanmelden met behulp van de opdrachtprompts van een SSH-sleutel Hallo tooa-server u voor Hallo wachtwoordzin voor dat sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="fe193-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="fe193-187">Uitleg van de opdracht</span><span class="sxs-lookup"><span data-stu-id="fe193-187">Command explained</span></span>

<span data-ttu-id="fe193-188">Wanneer `ssh fedora22` wordt uitgevoerd SSH eerst zoekt en laadt u de instellingen van Hallo `Host fedora22` blok en laadt het vervolgens alle resterende instellingen van het laatste blok, Hallo Hallo `Host *`.</span><span class="sxs-lookup"><span data-stu-id="fe193-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe193-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe193-189">Next Steps</span></span>

<span data-ttu-id="fe193-190">Naast up toocreate Azure Linux VM's gebruikt Hallo nieuwe openbare SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="fe193-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="fe193-191">Azure virtuele machines die zijn gemaakt met een openbare SSH-sleutel als Hallo aanmelding zijn beter beveiligd dan virtuele machines die zijn gemaakt met de Hallo aanmelding standaardmethode wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="fe193-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="fe193-192">Virtuele Azure-machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden uitgeschakeld, waarmee brute force-aanvallen om wachtwoorden te raden worden voorkomen.</span><span class="sxs-lookup"><span data-stu-id="fe193-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="fe193-193">Als u meer hulp bij het maken van uw SSH-sleutelpaar nodig of extra certificaten nodig, bijvoorbeeld voor gebruik met de klassieke portal hello, Zie [gedetailleerde stappen toocreate SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="fe193-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="fe193-194">Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="fe193-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fe193-195">Maak een beveiligde Linux-VM met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="fe193-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fe193-196">Maak een beveiligde Linux VM hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="fe193-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
