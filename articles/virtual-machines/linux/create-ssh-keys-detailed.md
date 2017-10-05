---
title: Gedetailleerde stappen om in Azure een SSH-sleutelpaar te maken voor virtuele Linux-machines | Microsoft Docs
description: Informatie over extra stappen om in Azure een openbaar en persoonlijk SSH-sleutelpaar voor virtuele Linux-machines te maken, samen met specifieke certificaten voor verschillende gebruiksvoorbeelden.
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="8559f-103">Gedetailleerd stappenplan voor het maken van een SSH-sleutelpaar en extra certificaten voor een virtuele Linux-machine in Azure</span><span class="sxs-lookup"><span data-stu-id="8559f-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="8559f-104">Met een SSH-sleutelpaar kunt u virtuele machines in Azure maken die voor verificatie standaard gebruikmaken van SSH-sleutels, waardoor aanmelding met een wachtwoord niet meer nodig is.</span><span class="sxs-lookup"><span data-stu-id="8559f-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="8559f-105">Wachtwoorden kunnen worden geraden en stellen uw virtuele machines bloot aan voortdurende aanvalspogingen om uw wachtwoord te raden.</span><span class="sxs-lookup"><span data-stu-id="8559f-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="8559f-106">Virtuele machines die zijn gemaakt met de Azure CLI- of Resource Manager-sjablonen, kunnen uw openbare SSH-sleutel opnemen als onderdeel van de implementatie, waardoor configuratie na implementatie niet meer nodig is voor het uitschakelen van aanmelding met een wachtwoord voor SSH.</span><span class="sxs-lookup"><span data-stu-id="8559f-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="8559f-107">Dit artikel vindt gedetailleerde stappen en aanvullende voorbeelden gegeven van certificaten genereren, zoals voor gebruik met de virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="8559f-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="8559f-108">Als u snel een SSH-sleutelpaar wilt maken en gebruiken, raadpleegt u [Een openbaar en persoonlijk SSH-sleutelpaar maken voor Linux-VM's in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="8559f-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="8559f-109">Inzicht in SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="8559f-109">Understanding SSH keys</span></span>

<span data-ttu-id="8559f-110">Het gebruik van openbare en persoonlijke SSH-sleutels is de eenvoudigste manier om u aan te melden bij uw Linux-servers.</span><span class="sxs-lookup"><span data-stu-id="8559f-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="8559f-111">[Cryptografie met openbare sleutels](https://en.wikipedia.org/wiki/Public-key_cryptography) biedt een veel veiligere manier van aanmelding bij uw virtuele Linux- of BSD-machines in Azure dan wachtwoorden, die aanzienlijk eenvoudiger met een brute force-aanval kunnen worden aangevallen.</span><span class="sxs-lookup"><span data-stu-id="8559f-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="8559f-112">Uw openbare sleutel kan worden gedeeld met iedereen, maar alleen u (of uw lokale beveiligingsinfrastructuur) beschikt over uw persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="8559f-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="8559f-113">De privé-SSH-sleutel moet ter beveiliging een [zeer veilig wachtwoord](https://www.xkcd.com/936/) hebben (bron:[xkcd.com](https://xkcd.com)).</span><span class="sxs-lookup"><span data-stu-id="8559f-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="8559f-114">Dit wachtwoord dient alleen voor toegang tot het persoonlijke SSH-sleutelbestand en is **niet** het wachtwoord voor het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="8559f-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="8559f-115">Wanneer u een wachtwoord aan de SSH-sleutel toevoegt, wordt de privésleutel versleuteld met behulp van 128-bits AES, zodat deze niet kan worden gebruikt zonder het wachtwoord om de privésleutel te ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="8559f-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="8559f-116">Als een aanvaller uw persoonlijke sleutel zou stelen en deze geen wachtwoord zou hebben, zou de aanvaller in staat zijn om de persoonlijke sleutel te gebruiken voor aanmelding bij de servers waarop de bijbehorende openbare sleutel is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8559f-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="8559f-117">Als een persoonlijke sleutel is beveiligd met een wachtwoord, kan deze niet worden gebruikt door de aanvaller. Zo beschikt u over een extra beveiligingslaag voor uw infrastructuur in Azure.</span><span class="sxs-lookup"><span data-stu-id="8559f-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="8559f-118">In dit artikel wordt een openbaar en persoonlijk sleutelpaarbestand met SSH-protocolversie 2 RSA gemaakt (ook wel 'SSH-RSA-sleutels' genoemd), dat wordt aanbevolen voor implementaties met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8559f-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="8559f-119">*ssh-rsa*-sleutels zijn vereist in de [portal](https://portal.azure.com) voor zowel de klassieke implementatie als de implementatie voor resourcebeheer.</span><span class="sxs-lookup"><span data-stu-id="8559f-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="8559f-120">Gebruik en voordelen van SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="8559f-120">SSH keys use and benefits</span></span>

<span data-ttu-id="8559f-121">Voor Azure zijn openbare en persoonlijke sleutels van minimaal 2048-bits, met SSH-protocol versie 2 en met RSA-indeling vereist. Het openbare-sleutelbestand heeft de `.pub`-containerindeling.</span><span class="sxs-lookup"><span data-stu-id="8559f-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="8559f-122">Voor het maken van de sleutels gebruiken we `ssh-keygen`, die een reeks vragen stelt en vervolgens een persoonlijke sleutel en een overeenkomende openbare sleutel schrijft.</span><span class="sxs-lookup"><span data-stu-id="8559f-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="8559f-123">Wanneer een virtuele Azure-machine wordt gemaakt, kopieert Azure de openbare sleutel naar de map `~/.ssh/authorized_keys` op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8559f-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="8559f-124">SSH-sleutels in `~/.ssh/authorized_keys` worden gebruikt om de client te vragen de bijbehorende persoonlijke sleutel te verstrekken bij verbinding via een SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8559f-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="8559f-125">Wanneer er in Azure een virtuele Linux-machine wordt gemaakt met SSH-sleutels voor verificatie, configureert Azure de SSHD-server zodanig dat aanmelding met een wachtwoord niet wordt toegestaan en alleen SSH-sleutels worden toegestaan.</span><span class="sxs-lookup"><span data-stu-id="8559f-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="8559f-126">Daarom kunt u helpen de VM-implementatie te beveiligen door virtuele Azure-machines in Linux met SSH-sleutels te maken. Ook kunt u uzelf de typische configuratiestap besparen die moet worden uitgevoerd na de implementatie: wachtwoorden uitschakelen in het bestand **sshd_config**.</span><span class="sxs-lookup"><span data-stu-id="8559f-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="8559f-127">ssh-keygen gebruiken</span><span class="sxs-lookup"><span data-stu-id="8559f-127">Using ssh-keygen</span></span>

<span data-ttu-id="8559f-128">Met deze opdracht wordt een met een wachtwoord beveiligd (versleuteld) SSH-sleutelpaar gemaakt met 2048-bits RSA waaraan opmerkingen worden toegevoegd om het gemakkelijk te kunnen identificeren.</span><span class="sxs-lookup"><span data-stu-id="8559f-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="8559f-129">SSH-sleutels worden standaard opgeslagen in de `~/.ssh`-directory.</span><span class="sxs-lookup"><span data-stu-id="8559f-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="8559f-130">Als u niet beschikt over de map `~/.ssh`, wordt deze door de opdracht `ssh-keygen` voor u gemaakt met de juiste machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8559f-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="8559f-131">*Uitleg van de opdracht*</span><span class="sxs-lookup"><span data-stu-id="8559f-131">*Command explained*</span></span>

<span data-ttu-id="8559f-132">`ssh-keygen` = het programma dat wordt gebruikt voor het maken van de sleutels</span><span class="sxs-lookup"><span data-stu-id="8559f-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="8559f-133">`-t rsa`= type sleutel maken die is de RSA-indeling [wikipedia][parens aan einde](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = aantal bits van de sleutel</span><span class="sxs-lookup"><span data-stu-id="8559f-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="8559f-134">`-C "azureuser@myserver"` = een opmerking die wordt toegevoegd aan het einde van het openbare sleutelbestand om het gemakkelijk te identificeren.</span><span class="sxs-lookup"><span data-stu-id="8559f-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="8559f-135">Normaal gesproken bestaat de opmerking uit een e-mailadres, maar u kunt ook iets anders gebruiken als dat beter aansluit bij uw infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="8559f-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="8559f-136">Klassieke implementatie met behulp van`asm`</span><span class="sxs-lookup"><span data-stu-id="8559f-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="8559f-137">Als u van het klassieke implementatiemodel gebruikmaakt (`asm` modus in de CLI), kunt u een openbare SSH-RSA-sleutel of een RFC4716 geformatteerd sleutel in een pem-container.</span><span class="sxs-lookup"><span data-stu-id="8559f-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="8559f-138">De openbare SSH-RSA-sleutel is de sleutel die eerder in dit artikel is gemaakt met behulp van `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="8559f-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="8559f-139">Een RFC4716-sleutel maken van een bestaande openbare SSH-sleutel:</span><span class="sxs-lookup"><span data-stu-id="8559f-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="8559f-140">Voorbeeld van ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="8559f-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
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

<span data-ttu-id="8559f-141">Opgeslagen sleutelbestanden:</span><span class="sxs-lookup"><span data-stu-id="8559f-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="8559f-142">De naam van het sleutelpaar voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8559f-142">The key pair name for this article.</span></span>  <span data-ttu-id="8559f-143">De naam **id_rsa** is de standaardwaarde voor een sleutelpaar. Sommige programma’s verwachten mogelijk **id_rsa** als naam voor het persoonlijke sleutelbestand, dus is het een goed idee als u er een hebt.</span><span class="sxs-lookup"><span data-stu-id="8559f-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="8559f-144">De map `~/.ssh/` is de standaardlocatie voor SSH-sleutelparen en het SSH-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8559f-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="8559f-145">Als `ssh-keygen` niet wordt opgegeven met een volledig pad, worden de sleutels in de huidige werkmap gemaakt in plaats van in de standaardmap `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="8559f-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="8559f-146">Een vermelding van de `~/.ssh`-map</span><span class="sxs-lookup"><span data-stu-id="8559f-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="8559f-147">Sleutelwachtwoord:</span><span class="sxs-lookup"><span data-stu-id="8559f-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="8559f-148">`ssh-keygen` verwijst naar een wachtwoord voor de privésleutel (een zogenaamde 'wachtwoordzin').</span><span class="sxs-lookup"><span data-stu-id="8559f-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="8559f-149">Het wordt *sterk* aanbevolen een wachtwoord toe te voegen aan uw privésleutel.</span><span class="sxs-lookup"><span data-stu-id="8559f-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="8559f-150">Zonder een wachtwoord dat het sleutelbestand beveiligt, kan iedereen met een exemplaar van het bestand zich aanmelden bij elke server die beschikt over de bijbehorende openbare sleutel.</span><span class="sxs-lookup"><span data-stu-id="8559f-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="8559f-151">Het toevoegen van een wachtwoord (wachtwoordzin) biedt veel meer bescherming in het geval iemand in staat is toegang te krijgen tot uw persoonlijke sleutelbestand. In de extra tijd die dit oplevert, kunt u de sleutels wijzigen waarmee u wordt geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="8559f-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="8559f-152">ssh-agent gebruiken voor het opslaan van het wachtwoord van uw persoonlijke sleutel</span><span class="sxs-lookup"><span data-stu-id="8559f-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="8559f-153">Om te voorkomen dat u het wachtwoord van uw persoonlijke sleutelbestand bij elke SSH-aanmelding moet opgeven, kunt u `ssh-agent` gebruiken om het wachtwoord van uw persoonlijke sleutelbestand in de cache te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="8559f-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="8559f-154">Als u een Mac gebruikt, worden de wachtwoorden van uw persoonlijke sleutels veilig opgeslagen door Sleutelhangertoegang van OSX wanneer u `ssh-agent` aanroept.</span><span class="sxs-lookup"><span data-stu-id="8559f-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="8559f-155">Controleer en gebruik ssh-agent en ssh-add om het SSH-systeem te informeren over de sleutelbestanden, zodat de wachtwoordzin niet interactief hoeft te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8559f-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="8559f-156">Voeg nu de persoonlijke sleutel toe aan `ssh-agent` met de opdracht `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="8559f-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="8559f-157">Het wachtwoord voor persoonlijke sleutel wordt nu opgeslagen in `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="8559f-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="8559f-158">`ssh-copy-id` gebruiken om de sleutel te kopiëren naar een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8559f-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="8559f-159">Als u al een virtuele machine hebt gemaakt, kunt u de nieuwe openbare SSH-sleutel installeren op uw virtuele Linux-machine met:</span><span class="sxs-lookup"><span data-stu-id="8559f-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="8559f-160">Een SSH-configuratiebestand maken en configureren</span><span class="sxs-lookup"><span data-stu-id="8559f-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="8559f-161">Het wordt aanbevolen om een `~/.ssh/config`-bestand te maken en te configureren om aanmeldingen te versnellen en het gedrag van uw SSH-clientgedrag te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="8559f-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="8559f-162">In het volgende voorbeeld wordt een standaardconfiguratie getoond.</span><span class="sxs-lookup"><span data-stu-id="8559f-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="8559f-163">Het bestand maken</span><span class="sxs-lookup"><span data-stu-id="8559f-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="8559f-164">Bewerk het bestand om de nieuwe SSH-configuratie toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="8559f-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="8559f-165">Voorbeeld van `~/.ssh/config`-bestand:</span><span class="sxs-lookup"><span data-stu-id="8559f-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="8559f-166">Deze SSH-configuratie bevat afzonderlijke secties voor elke server, zodat elke server kan beschikken over een eigen toegewezen sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="8559f-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="8559f-167">De standaardinstellingen (`Host *`) zijn voor alle hosts die niet overeenkomen met een van de specifieke hosts die hoger in het configuratiebestand staan.</span><span class="sxs-lookup"><span data-stu-id="8559f-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="8559f-168">Uitleg van configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="8559f-168">Config file explained</span></span>

<span data-ttu-id="8559f-169">`Host` = de naam van de host die wordt aangeroepen op de terminal.</span><span class="sxs-lookup"><span data-stu-id="8559f-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="8559f-170">`ssh fedora22` vertelt `SSH` dat de waarden moeten worden gebruikt in het instellingenblok met het label `Host fedora22` OPMERKING: de host kan elk label zijn dat logisch is voor uw gebruik. Het label vertegenwoordigt niet de werkelijke hostnaam van een server.</span><span class="sxs-lookup"><span data-stu-id="8559f-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="8559f-171">`Hostname 102.160.203.241` = het IP-adres of de DNS-naam van de server die wordt benaderd.</span><span class="sxs-lookup"><span data-stu-id="8559f-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="8559f-172">`User ahmet` = het account van de externe gebruiker dat moet worden gebruikt bij het aanmelden bij de server.</span><span class="sxs-lookup"><span data-stu-id="8559f-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="8559f-173">`PubKeyAuthentication yes` = vertelt SSH dat u gebruik wilt maken van een SSH-sleutel voor aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8559f-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="8559f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = de persoonlijke SSH-sleutel en de bijbehorende openbare sleutel te gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="8559f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="8559f-175">SSH in Linux zonder een wachtwoord</span><span class="sxs-lookup"><span data-stu-id="8559f-175">SSH into Linux without a password</span></span>

<span data-ttu-id="8559f-176">Nu u een SSH-sleutelpaar en een geconfigureerd SSH-configuratiebestand hebt, kunt u zich snel en veilig aanmelden bij uw virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="8559f-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="8559f-177">De eerste keer dat u zich met een SSH-sleutel bij een server aanmeldt, wordt u gevraagd naar de wachtwoordzin voor dat sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="8559f-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="8559f-178">Uitleg van de opdracht</span><span class="sxs-lookup"><span data-stu-id="8559f-178">Command explained</span></span>

<span data-ttu-id="8559f-179">Wanneer `ssh fedora22` wordt uitgevoerd, zoekt en laadt SSH eerst instellingen uit het `Host fedora22`-blok en laadt het vervolgens alle overige instellingen uit het laatste blok, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="8559f-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8559f-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8559f-180">Next Steps</span></span>

<span data-ttu-id="8559f-181">De volgende stap bestaat uit het maken van virtuele Linux-machines in Azure met de nieuwe openbare SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="8559f-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="8559f-182">Virtuele Azure-machines die zijn gemaakt met een openbare SSH-sleutel voor aanmelding, zijn beter beveiligd dan virtuele machines die zijn gemaakt met een wachtwoord als standaardaanmeldingsmethode.</span><span class="sxs-lookup"><span data-stu-id="8559f-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="8559f-183">Virtuele Azure-machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden uitgeschakeld, waarmee brute force-aanvallen om wachtwoorden te raden worden voorkomen.</span><span class="sxs-lookup"><span data-stu-id="8559f-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="8559f-184">Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="8559f-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8559f-185">Een beveiligde virtuele Linux-machine maken met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8559f-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8559f-186">Een beveiligde virtuele Linux-machine maken met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8559f-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
