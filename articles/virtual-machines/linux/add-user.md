---
title: een gebruiker tooa Linux VM op Azure aaaAdd | Microsoft Docs
description: Een gebruiker tooa Linux VM op Azure toevoegen.
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
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="3e889-103">Toevoegen van een gebruiker tooan Azure VM</span><span class="sxs-lookup"><span data-stu-id="3e889-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="3e889-104">Een eerste taken op een nieuwe Linux-VM Hallo is toocreate een nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3e889-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="3e889-105">In dit artikel we helpt bij het maken van een sudo-gebruikersaccount en wachtwoord instellen hello, toe te voegen SSH openbare sleutels, en ten slotte gebruiken `visudo` tooallow sudo zonder wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3e889-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="3e889-106">Vereisten zijn: [een Azure-account](https://azure.microsoft.com/pricing/free-trial/), [SSH openbare en persoonlijke sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), een Azure-resourcegroep en hello Azure CLI geïnstalleerd en gewijzigd tooAzure Resource Manager modus gebruiken `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="3e889-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="3e889-107">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="3e889-107">Quick Commands</span></span>
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

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="3e889-108">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="3e889-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="3e889-109">Inleiding</span><span class="sxs-lookup"><span data-stu-id="3e889-109">Introduction</span></span>
<span data-ttu-id="3e889-110">Een van de eerste en de meest voorkomende taak Hallo met een nieuwe server is tooadd een gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="3e889-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="3e889-111">Hoofdmap aanmeldingen moeten zijn uitgeschakeld en Hallo root-account zelf mag niet worden gebruikt met uw Linux-server alleen sudo.</span><span class="sxs-lookup"><span data-stu-id="3e889-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="3e889-112">Geeft een gebruiker hoofdmap escalatie bevoegdheden met ' sudo ' het juiste manier tooadminister Hallo samen met Linux.</span><span class="sxs-lookup"><span data-stu-id="3e889-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="3e889-113">Met de opdracht Hallo `useradd` we gebruiker accounts toohello Linux VM toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3e889-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="3e889-114">Met `useradd` wijzigt `/etc/passwd`, `/etc/shadow`, `/etc/group`, en `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="3e889-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="3e889-115">We een opdrachtregelprogramma vlag toohello toevoegen `useradd` opdracht tooalso Hallo nieuwe toohello juiste sudo gebruikersgroep toevoegen op Linux.</span><span class="sxs-lookup"><span data-stu-id="3e889-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="3e889-116">Zelfs als u `useradd` maakt u een vermelding in de `/etc/passwd` deze geeft geen nieuwe gebruikersaccount Hallo een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3e889-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="3e889-117">Maakt een initiële wachtwoord voor de nieuwe gebruiker Hallo Hallo eenvoudig met `passwd` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3e889-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="3e889-118">de laatste stap Hallo is toomodify hello sudo regels tooallow die gebruiker tooexecute opdrachten met bevoegdheden voor sudo zonder tooenter een wachtwoord op voor elke opdracht.</span><span class="sxs-lookup"><span data-stu-id="3e889-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="3e889-119">Aanmelden met behulp van de persoonlijke sleutel hello wordt uitgegaan van een gebruikersaccount is beschermd tegen ongewenste actoren en gaat tooallow sudo toegang zonder een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3e889-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="3e889-120">Toevoegen van een sudo met één gebruiker tooan Azure VM</span><span class="sxs-lookup"><span data-stu-id="3e889-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="3e889-121">Meld u bij toohello Azure VM SSH-sleutels gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3e889-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="3e889-122">Als er geen installatie SSH openbare toegang tot de sleutel, eerst te voltooien in dit artikel [verificatie van openbare sleutel met Azure met behulp van](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="3e889-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="3e889-123">Hallo `useradd` opdracht is voltooid Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="3e889-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="3e889-124">een nieuw gebruikersaccount maken</span><span class="sxs-lookup"><span data-stu-id="3e889-124">create a new user account</span></span>
* <span data-ttu-id="3e889-125">Maak een nieuwe gebruikersgroep met de Hallo dezelfde naam</span><span class="sxs-lookup"><span data-stu-id="3e889-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="3e889-126">een lege waarde te toevoegen`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="3e889-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="3e889-127">een lege waarde te toevoegen`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="3e889-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="3e889-128">Hallo `-G` opdrachtregelprogramma vlag Hallo nieuwe gebruiker account toohello juiste Linux groep toegevoegd zodat nieuwe gebruikersaccount Hallo hoofdmap uitbreiding van bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="3e889-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="3e889-129">Hallo-gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e889-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="3e889-130">Een wachtwoord instellen</span><span class="sxs-lookup"><span data-stu-id="3e889-130">Set a password</span></span>
<span data-ttu-id="3e889-131">Hallo `useradd` opdracht Hallo gebruiker maakt en voegt u een vermelding tooboth `/etc/passwd` en `/etc/gpasswd` maar niet daadwerkelijk Hallo wachtwoord ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3e889-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="3e889-132">Hallo wachtwoord wordt toegevoegd toohello vermelding met Hallo `passwd` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3e889-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="3e889-133">We nu hebben een gebruiker met sudo-machtigingen op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="3e889-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="3e889-134">Uw openbare SSH-sleutel toohello nieuwe gebruikersaccount toevoegen</span><span class="sxs-lookup"><span data-stu-id="3e889-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="3e889-135">Gebruik van uw computer, Hallo `ssh-copy-id` opdracht met Hallo nieuwe wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3e889-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="3e889-136">Met behulp van visudo tooallow sudo gebruik zonder wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3e889-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="3e889-137">Met behulp van `visudo` tooedit hello `/etc/sudoers` bestand enkele lagen van bescherming tegen onjuist wijzigen van deze belangrijk bestand toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3e889-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="3e889-138">Bij het uitvoeren van `visudo`, Hallo `/etc/sudoers` bestand is vergrendeld tooensure andere gebruikers geen wijzigingen kunt aanbrengen, terwijl deze actief wordt bewerkt.</span><span class="sxs-lookup"><span data-stu-id="3e889-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="3e889-139">Hallo `/etc/sudoers` bestand ook gecontroleerd op fouten door `visudo` wanneer u probeert toosave of sluiten zodat u een verbroken sudoers-bestand niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="3e889-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="3e889-140">Er bestaat reeds gebruikers in de juiste standaardgroep Hallo voor sudo-toegang.</span><span class="sxs-lookup"><span data-stu-id="3e889-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="3e889-141">Nu gaan we tooenable die groepen toouse sudo zonder wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3e889-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="3e889-142">Controleer of gebruiker hello, ssh-sleutels en sudo</span><span class="sxs-lookup"><span data-stu-id="3e889-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
