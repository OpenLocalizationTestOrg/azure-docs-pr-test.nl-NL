---
title: Installeer de Azure CLI 1.0 | Microsoft Docs
description: Installeer de 1.0 Azure CLI voor Mac, Linux en Windows te starten met Azure-services
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="a10f9-103">Installeer de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a10f9-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a10f9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a10f9-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="a10f9-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a10f9-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="a10f9-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a10f9-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="a10f9-107">Dit onderwerp beschrijft het installeren van de Azure CLI 1.0, die is gebaseerd op nodeJs en ondersteunt alle klassieke implementatie API-aanroepen, evenals een groot aantal implementatieactiviteiten van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a10f9-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="a10f9-108">Moet u de [Azure CLI 2.0](/cli/azure/overview) voor nieuwe of toekomstgerichte CLI-implementaties en -beheer.</span><span class="sxs-lookup"><span data-stu-id="a10f9-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="a10f9-109">Snel het Azure-opdrachtregelinterface (Azure CLI 1.0) voor het gebruik van een set van open-source shell-opdrachten voor het maken en beheren van resources in Microsoft Azure installeren.</span><span class="sxs-lookup"><span data-stu-id="a10f9-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="a10f9-110">U hebt verschillende mogelijkheden voor het installeren van deze cross-platform-hulpprogramma's op uw computer:</span><span class="sxs-lookup"><span data-stu-id="a10f9-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="a10f9-111">**npm pakket** -npm (de package manager voor JavaScript) uitgevoerd voor het installeren van de nieuwste Azure CLI 1.0-pakket op uw Linux-distributie- of OS.</span><span class="sxs-lookup"><span data-stu-id="a10f9-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="a10f9-112">Node.js en npm op uw computer vereist.</span><span class="sxs-lookup"><span data-stu-id="a10f9-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="a10f9-113">**Installatieprogramma** -een installatieprogramma voor een eenvoudige installatie op de Mac- of Windows te downloaden.</span><span class="sxs-lookup"><span data-stu-id="a10f9-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="a10f9-114">**Docker-container** : begin met de meest recente CLI in een kant-en-klaar Docker-container.</span><span class="sxs-lookup"><span data-stu-id="a10f9-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="a10f9-115">Vereist Docker-host op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a10f9-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="a10f9-116">Zie voor meer opties en achtergrond, de project-opslagplaats op [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="a10f9-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="a10f9-117">Nadat de Azure CLI 1.0 is geïnstalleerd, [verbinding te maken met uw Azure-abonnement](xplat-cli-connect.md) en voer de **azure** opdrachten uit vanaf de opdrachtregelinterface (Bash, Terminal, opdrachtprompt, enzovoort) om te werken met uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a10f9-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="a10f9-118">Optie 1: Een npm-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="a10f9-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="a10f9-119">Als u wilt de CLI installeren vanaf een pakket npm, Controleer of u hebt gedownload en geïnstalleerd de [nieuwste Node.js en npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="a10f9-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="a10f9-120">Voer **npm installeren** om de azure cli-pakket te installeren:</span><span class="sxs-lookup"><span data-stu-id="a10f9-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="a10f9-121">Op Linux-distributies, moet u mogelijk gebruik **sudo** om uit te voeren de **npm** opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="a10f9-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="a10f9-122">Als u wilt installeren of bijwerken van Node.js en npm op uw Linux-distributie- of OS, raden wij aan dat u de meest recente versie van Node.js TNS (4.x) installeert.</span><span class="sxs-lookup"><span data-stu-id="a10f9-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="a10f9-123">Als u een oudere versie gebruikt, krijgt u mogelijk installatiefouten.</span><span class="sxs-lookup"><span data-stu-id="a10f9-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="a10f9-124">Als u liever, download de meest recente Linux [tar-bestand] [ linux-installer] voor de npm-pakket lokaal.</span><span class="sxs-lookup"><span data-stu-id="a10f9-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="a10f9-125">Installeer vervolgens het gedownloade npm-pakket (op Linux-distributies die u wilt gebruiken **sudo**):</span><span class="sxs-lookup"><span data-stu-id="a10f9-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="a10f9-126">Optie 2: Een installatieprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="a10f9-126">Option 2: Use an installer</span></span>
<span data-ttu-id="a10f9-127">Als u een Mac- of Windows-computer gebruikt, zijn de volgende CLI-installatieprogramma downloaden:</span><span class="sxs-lookup"><span data-stu-id="a10f9-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="a10f9-128">[Mac OS X-installatieprogramma][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="a10f9-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="a10f9-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="a10f9-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="a10f9-130">Op Windows, u kunt ook downloaden via de [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) voor het installeren van de CLI.</span><span class="sxs-lookup"><span data-stu-id="a10f9-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="a10f9-131">Dit installatieprogramma kunt u de optie voor het installeren van extra Azure-SDK en opdrachtregelprogramma's na de installatie van de CLI.</span><span class="sxs-lookup"><span data-stu-id="a10f9-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="a10f9-132">Optie 3: Een Docker-container gebruiken</span><span class="sxs-lookup"><span data-stu-id="a10f9-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="a10f9-133">Als u hebt ingesteld van uw computer als een [Docker](https://docs.docker.com/engine/understanding-docker/) host, kunt u de nieuwste Azure CLI 1.0 uitvoeren in een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="a10f9-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="a10f9-134">Voer de volgende opdracht (op Linux-distributies die u wilt gebruiken **sudo**):</span><span class="sxs-lookup"><span data-stu-id="a10f9-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="a10f9-135">Azure CLI 1.0-opdrachten uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a10f9-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="a10f9-136">Nadat de Azure CLI 1.0 is geïnstalleerd, voert u de **azure** opdracht uit vanaf de opdrachtregel gebruikersinterface (Bash, Terminal, opdrachtprompt, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="a10f9-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="a10f9-137">Bijvoorbeeld als u wilt de help-opdracht uitvoert, typt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="a10f9-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="a10f9-138">Op sommige Linux-distributies, wordt een foutbericht zoals `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="a10f9-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="a10f9-139">Deze fout zijn afkomstig van recente installaties van Node.js op /usr/bin/nodejs wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a10f9-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="a10f9-140">Om dit te corrigeren, een symbolische koppeling maken naar /usr/bin/node met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="a10f9-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="a10f9-141">Overzicht van de versie van de Azure CLI 1.0 die u hebt geïnstalleerd, typ het volgende:</span><span class="sxs-lookup"><span data-stu-id="a10f9-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="a10f9-142">U bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="a10f9-142">Now you are ready!</span></span> <span data-ttu-id="a10f9-143">Voor toegang tot de CLI-opdrachten voor het werken met uw eigen resources [verbinding maken met uw Azure-abonnement vanuit de Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a10f9-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a10f9-144">Als u Azure CLI voor het eerst gebruikt, ziet u een bericht waarin wordt gevraagd of u toestaan dat Microsoft wilt voor het verzamelen van informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="a10f9-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="a10f9-145">Deelname is niet verplicht.</span><span class="sxs-lookup"><span data-stu-id="a10f9-145">Participation is voluntary.</span></span> <span data-ttu-id="a10f9-146">Als u ervoor kiest om deel te nemen, kunt u stoppen op elk gewenst moment door het uitvoeren van `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="a10f9-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="a10f9-147">Inschakelen van deelname op elk gewenst moment `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="a10f9-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="a10f9-148">De CLI bijwerken</span><span class="sxs-lookup"><span data-stu-id="a10f9-148">Update the CLI</span></span>
<span data-ttu-id="a10f9-149">Bijgewerkte versies van de Azure CLI regelmatig door Microsoft worden uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="a10f9-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="a10f9-150">De CLI met behulp van het installatieprogramma voor het besturingssysteem opnieuw installeren of uitvoeren van de meest recente Docker-container.</span><span class="sxs-lookup"><span data-stu-id="a10f9-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="a10f9-151">Als u de meest recente Node.js en npm geïnstalleerd hebt, bijwerken door het volgende te typen (op Linux-distributies die u wilt gebruiken **sudo**).</span><span class="sxs-lookup"><span data-stu-id="a10f9-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="a10f9-152">Tab-Aanvulling inschakelen</span><span class="sxs-lookup"><span data-stu-id="a10f9-152">Enable tab completion</span></span>
<span data-ttu-id="a10f9-153">Tab-aanvulling van de CLI-opdrachten wordt ondersteund voor Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="a10f9-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="a10f9-154">Inschakelen in zsh uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a10f9-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="a10f9-155">Als u deze in bash, voert u het:</span><span class="sxs-lookup"><span data-stu-id="a10f9-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="a10f9-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a10f9-156">Next steps</span></span>
* <span data-ttu-id="a10f9-157">[Verbinding maken met CLI met uw Azure-abonnement](xplat-cli-connect.md) maken en beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="a10f9-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="a10f9-158">Als u meer informatie over de Azure CLI, broncode downloaden, problemen melden, of bijdragen aan het project, gaat u naar de [GitHub-opslagplaats voor de Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="a10f9-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="a10f9-159">Als u vragen over het gebruik van de Azure CLI of Azure hebt, gaat u naar de [Azure-Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="a10f9-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
