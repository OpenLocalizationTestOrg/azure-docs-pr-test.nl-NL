---
title: Een gebruiker toevoegen aan een Linux-VM op Azure | Microsoft Docs
description: Een gebruiker toevoegen aan een Linux-VM op Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: a95157f57c0cbd1f2a9ed68a0fe83140d7c9ec40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-user-to-an-azure-vm"></a><span data-ttu-id="61328-103">Een gebruiker toevoegen aan een Azure VM</span><span class="sxs-lookup"><span data-stu-id="61328-103">Add a user to an Azure VM</span></span>
<span data-ttu-id="61328-104">Een van de eerste taken op een nieuwe Linux-VM is het maken van een nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="61328-104">One of the first tasks on any new Linux VM is to create a new user.</span></span>  <span data-ttu-id="61328-105">In dit artikel we doorlopen een sudo-gebruikersaccount maken voor het instellen van het wachtwoord toe te voegen SSH openbare sleutels, en ten slotte gebruiken `visudo` om toe te staan sudo zonder wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="61328-105">In this article, we walk through creating a sudo user account, setting the password, adding SSH Public Keys, and finally use `visudo` to allow sudo without a password.</span></span>

<span data-ttu-id="61328-106">Vereisten zijn: [een Azure-account](https://azure.microsoft.com/pricing/free-trial/), [SSH openbare en persoonlijke sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), een Azure-resourcegroep en Azure CLI geïnstalleerd en wordt overgeschakeld naar het gebruik van Azure Resource Manager-modus `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="61328-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and the Azure CLI installed and switched to Azure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="61328-107">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="61328-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy the SSH Public Key to the new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers to allow no password
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify the SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="61328-108">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="61328-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="61328-109">Inleiding</span><span class="sxs-lookup"><span data-stu-id="61328-109">Introduction</span></span>
<span data-ttu-id="61328-110">Een van de eerste en de meest voorkomende taak met een nieuwe server is het toevoegen van een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="61328-110">One of the first and most common task with a new server is to add a user account.</span></span>  <span data-ttu-id="61328-111">Hoofdmap aanmeldingen moeten zijn uitgeschakeld en het hoofdaccount zelf mag niet worden gebruikt met uw Linux-server alleen sudo.</span><span class="sxs-lookup"><span data-stu-id="61328-111">Root logins should be disabled and the root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="61328-112">Uitbreiding van bevoegdheden met ' sudo ' voor de hoofdmap van een gebruiker zodat deze de juiste manier te beheren en gebruiken van Linux.</span><span class="sxs-lookup"><span data-stu-id="61328-112">Giving a user root escalation privileges using sudo it the proper way to administer and use Linux.</span></span>

<span data-ttu-id="61328-113">Met de opdracht `useradd` we gebruikersaccounts toevoegen aan de Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="61328-113">Using the command `useradd` we are adding user accounts to the Linux VM.</span></span>  <span data-ttu-id="61328-114">Met `useradd` wijzigt `/etc/passwd`, `/etc/shadow`, `/etc/group`, en `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="61328-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="61328-115">We een opdrachtregelprogramma vlag wilt toevoegen de `useradd` opdracht ook de nieuwe gebruiker toevoegen aan de juiste sudo-groep op Linux.</span><span class="sxs-lookup"><span data-stu-id="61328-115">We are adding a command-line flag to the `useradd` command to also add the new user to the proper sudo group on Linux.</span></span>  <span data-ttu-id="61328-116">Zelfs als u `useradd` maakt u een vermelding in de `/etc/passwd` deze geeft geen nieuwe gebruikersaccount een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="61328-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give the new user account a password.</span></span>  <span data-ttu-id="61328-117">Maakt u een eerste wachtwoord voor de nieuwe gebruiker met behulp van de eenvoudige `passwd` opdracht.</span><span class="sxs-lookup"><span data-stu-id="61328-117">We are creating an initial password for the new user using the simple `passwd` command.</span></span>  <span data-ttu-id="61328-118">De laatste stap is het wijzigen van de sudo-regels voor het toestaan van die gebruiker met bevoegdheden voor sudo-opdrachten uitvoeren zonder een wachtwoord opgeven voor elke opdracht.</span><span class="sxs-lookup"><span data-stu-id="61328-118">The last step is to modify the sudo rules to allow that user to execute commands with sudo privileges without having to enter a password for every command.</span></span>  <span data-ttu-id="61328-119">Aanmelden met behulp van de persoonlijke sleutel wordt uitgegaan van een gebruikersaccount is beschermd tegen ongewenste actoren en gaan sudo toegang zonder wachtwoord toestaan.</span><span class="sxs-lookup"><span data-stu-id="61328-119">Logging in using the Private key we are assuming that user account is safe from bad actors and are going to allow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-to-an-azure-vm"></a><span data-ttu-id="61328-120">Een gebruiker één sudo toe te voegen aan een Azure VM</span><span class="sxs-lookup"><span data-stu-id="61328-120">Adding a single sudo user to an Azure VM</span></span>
<span data-ttu-id="61328-121">Aanmelden bij de virtuele machine in Azure met behulp van SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="61328-121">Log in to the Azure VM using SSH keys.</span></span>  <span data-ttu-id="61328-122">Als er geen installatie SSH openbare toegang tot de sleutel, eerst te voltooien in dit artikel [verificatie van openbare sleutel met Azure met behulp van](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="61328-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="61328-123">De `useradd` opdracht is voltooid de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="61328-123">The `useradd` command completes the following tasks:</span></span>

* <span data-ttu-id="61328-124">een nieuw gebruikersaccount maken</span><span class="sxs-lookup"><span data-stu-id="61328-124">create a new user account</span></span>
* <span data-ttu-id="61328-125">Maak een nieuwe groep met dezelfde naam</span><span class="sxs-lookup"><span data-stu-id="61328-125">create a new user group with the same name</span></span>
* <span data-ttu-id="61328-126">een lege vermelding toevoegen`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="61328-126">add a blank entry to `/etc/passwd`</span></span>
* <span data-ttu-id="61328-127">een lege vermelding toevoegen`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="61328-127">add a blank entry to `/etc/gpasswd`</span></span>

<span data-ttu-id="61328-128">De `-G` opdrachtregelprogramma vlag wordt het nieuwe gebruikersaccount toegevoegd aan de juiste Linux-groep geeft het nieuwe gebruikersaccount hoofdmap uitbreiding van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="61328-128">The `-G` command-line flag adds the new user account to the proper Linux group giving the new user account root escalation privileges.</span></span>

#### <a name="add-the-user"></a><span data-ttu-id="61328-129">De gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="61328-129">Add the user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="61328-130">Een wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="61328-130">Set a password</span></span>
<span data-ttu-id="61328-131">De `useradd` opdracht maakt u de gebruiker en wordt een vermelding toegevoegd aan beide `/etc/passwd` en `/etc/gpasswd` , maar het wachtwoord niet daadwerkelijk ingesteld.</span><span class="sxs-lookup"><span data-stu-id="61328-131">The `useradd` command creates the user and adds an entry to both `/etc/passwd` and `/etc/gpasswd` but does not actually set the password.</span></span>  <span data-ttu-id="61328-132">Het wachtwoord wordt toegevoegd aan de vermelding met behulp van de `passwd` opdracht.</span><span class="sxs-lookup"><span data-stu-id="61328-132">The password is added to the entry using the `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="61328-133">We hebben nu een gebruiker met sudo-machtigingen op de server.</span><span class="sxs-lookup"><span data-stu-id="61328-133">We now have a user with sudo privileges on the server.</span></span>

### <a name="add-your-ssh-public-key-to-the-new-user-account"></a><span data-ttu-id="61328-134">Uw openbare SSH-sleutel aan het nieuwe gebruikersaccount toevoegen</span><span class="sxs-lookup"><span data-stu-id="61328-134">Add your SSH Public Key to the new user account</span></span>
<span data-ttu-id="61328-135">Gebruik van uw computer, de `ssh-copy-id` opdracht met het nieuwe wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="61328-135">From your machine, use the `ssh-copy-id` command with the new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-to-allow-sudo-usage-without-a-password"></a><span data-ttu-id="61328-136">Met behulp van visudo voor het gebruik van sudo zonder wachtwoord toestaan</span><span class="sxs-lookup"><span data-stu-id="61328-136">Using visudo to allow sudo usage without a password</span></span>
<span data-ttu-id="61328-137">Met behulp van `visudo` bewerken de `/etc/sudoers` bestand enkele lagen van bescherming tegen onjuist wijzigen van deze belangrijk bestand toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="61328-137">Using `visudo` to edit the `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="61328-138">Bij het uitvoeren van `visudo`, wordt de `/etc/sudoers` bestand is vergrendeld zodat andere gebruikers geen wijzigingen kunt aanbrengen, terwijl deze actief wordt bewerkt.</span><span class="sxs-lookup"><span data-stu-id="61328-138">Upon executing `visudo`, the `/etc/sudoers` file is locked to ensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="61328-139">De `/etc/sudoers` bestand ook gecontroleerd op fouten door `visudo` wanneer u probeert op te slaan of te sluiten, zodat u een verbroken sudoers-bestand niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="61328-139">The `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt to save or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="61328-140">Er bestaat reeds gebruikers in de juiste standaardgroep voor sudo-toegang.</span><span class="sxs-lookup"><span data-stu-id="61328-140">We already have users in the correct default group for sudo access.</span></span>  <span data-ttu-id="61328-141">Nu gaan we om in te schakelen die groepen sudo gebruiken zonder wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="61328-141">Now we are going to enable those groups to use sudo with no password.</span></span>

```bash
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-the-user-ssh-keys-and-sudo"></a><span data-ttu-id="61328-142">Controleer of de gebruiker de ssh-sleutels en sudo</span><span class="sxs-lookup"><span data-stu-id="61328-142">Verify the user, ssh keys, and sudo</span></span>
```bash
# Verify the SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
