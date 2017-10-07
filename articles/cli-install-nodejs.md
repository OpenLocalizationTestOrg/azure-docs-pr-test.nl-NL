---
title: aaaInstall hello Azure CLI 1.0 | Microsoft Docs
description: Hallo 1.0 van Azure CLI voor Mac, Linux en Windows toostart met behulp van Azure services installeren
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
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="8b74b-103">Hello Azure CLI 1.0 installeren</span><span class="sxs-lookup"><span data-stu-id="8b74b-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b74b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b74b-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="8b74b-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8b74b-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="8b74b-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8b74b-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="8b74b-107">Dit onderwerp wordt beschreven hoe tooinstall hello Azure CLI 1.0, die is gebaseerd op nodeJs en ondersteunt alle klassieke implementatie-API aanroept en een groot aantal implementatieactiviteiten van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b74b-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="8b74b-108">Moet u Hallo [Azure CLI 2.0](/cli/azure/overview) voor nieuwe of toekomstgerichte CLI-implementaties en -beheer.</span><span class="sxs-lookup"><span data-stu-id="8b74b-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="8b74b-109">Snel installeren hello Azure-opdrachtregelinterface (Azure CLI 1.0) toouse een set van open-source shell-opdrachten voor het maken en beheren van resources in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8b74b-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="8b74b-110">U hebt verschillende opties tooinstall deze cross-platform-hulpprogramma's op uw computer:</span><span class="sxs-lookup"><span data-stu-id="8b74b-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="8b74b-111">**npm pakket** - Run npm (Hallo package manager voor JavaScript) tooinstall Hallo nieuwste Azure CLI 1.0-pakket op uw Linux-distributie- of OS.</span><span class="sxs-lookup"><span data-stu-id="8b74b-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="8b74b-112">Node.js en npm op uw computer vereist.</span><span class="sxs-lookup"><span data-stu-id="8b74b-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="8b74b-113">**Installatieprogramma** -een installatieprogramma voor een eenvoudige installatie op de Mac- of Windows te downloaden.</span><span class="sxs-lookup"><span data-stu-id="8b74b-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="8b74b-114">**Docker-container** - Start met behulp van Hallo nieuwste CLI in een kant-en-klaar Docker-container.</span><span class="sxs-lookup"><span data-stu-id="8b74b-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="8b74b-115">Vereist Docker-host op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8b74b-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="8b74b-116">Zie voor meer opties en achtergrond Hallo project opslagplaats op [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="8b74b-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="8b74b-117">Nadat hello Azure CLI 1.0 is geïnstalleerd, [verbinding te maken met uw Azure-abonnement](xplat-cli-connect.md) en Voer Hallo **azure** opdrachten uit uw opdrachtregelinterface (Bash, Terminal, opdrachtprompt, enzovoort) toowork met uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="8b74b-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="8b74b-118">Optie 1: Een npm-pakket installeren</span><span class="sxs-lookup"><span data-stu-id="8b74b-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="8b74b-119">tooinstall hello CLI van een pakket npm, zorg ervoor dat u hebt gedownload en geïnstalleerd Hallo [nieuwste Node.js en npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="8b74b-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="8b74b-120">Voer **npm installeren** tooinstall hello azure cli pakket:</span><span class="sxs-lookup"><span data-stu-id="8b74b-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="8b74b-121">Op Linux-distributies, moet u mogelijk toouse **sudo** toosuccessfully uitvoeren Hallo **npm** opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="8b74b-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="8b74b-122">Als u tooinstall moet of Node.js en npm op uw Linux-distributie- of OS bijwerken, wordt u aangeraden Hallo meest recente TNS Node.js-versie (4.x) te installeren.</span><span class="sxs-lookup"><span data-stu-id="8b74b-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="8b74b-123">Als u een oudere versie gebruikt, krijgt u mogelijk installatiefouten.</span><span class="sxs-lookup"><span data-stu-id="8b74b-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="8b74b-124">Als u liever, downloaden Hallo nieuwste Linux [tar-bestand] [ linux-installer] pakket lokaal voor Hallo npm.</span><span class="sxs-lookup"><span data-stu-id="8b74b-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="8b74b-125">Installeer vervolgens Hallo npm gedownloade pakket (op Linux-distributies moet u mogelijk toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="8b74b-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="8b74b-126">Optie 2: Een installatieprogramma gebruiken</span><span class="sxs-lookup"><span data-stu-id="8b74b-126">Option 2: Use an installer</span></span>
<span data-ttu-id="8b74b-127">Als u een Mac- of Windows-computer gebruikt, zijn Hallo na CLI installatieprogramma's beschikbaar voor downloaden:</span><span class="sxs-lookup"><span data-stu-id="8b74b-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="8b74b-128">[Mac OS X-installatieprogramma][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="8b74b-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="8b74b-129">[Windows MSI][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="8b74b-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="8b74b-130">In Windows, kunt u ook Hallo downloaden [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall Hallo CLI.</span><span class="sxs-lookup"><span data-stu-id="8b74b-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="8b74b-131">Deze installer biedt u de optie tooinstall Hallo extra Azure-SDK en opdrachtregelprogramma's na de installatie van CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b74b-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="8b74b-132">Optie 3: Een Docker-container gebruiken</span><span class="sxs-lookup"><span data-stu-id="8b74b-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="8b74b-133">Als u hebt ingesteld van uw computer als een [Docker](https://docs.docker.com/engine/understanding-docker/) host, kunt u uitvoeren Hallo nieuwste Azure CLI 1.0 in een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="8b74b-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="8b74b-134">Voer hello volgende opdracht (op Linux-distributies moet u mogelijk toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="8b74b-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="8b74b-135">Azure CLI 1.0-opdrachten uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8b74b-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="8b74b-136">Nadat hello Azure CLI 1.0 is geïnstalleerd, voert u Hallo **azure** opdracht uit vanaf de opdrachtregel gebruikersinterface (Bash, Terminal, opdrachtprompt, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="8b74b-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="8b74b-137">Typ bijvoorbeeld toorun Hallo help opdracht Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8b74b-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="8b74b-138">Op sommige Linux-distributies, wordt een foutbericht weergegeven dat vergelijkbaar te`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="8b74b-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="8b74b-139">Deze fout zijn afkomstig van recente installaties van Node.js op /usr/bin/nodejs wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8b74b-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="8b74b-140">toofix, een symbolische koppeling te/usr/bin/knooppunt maken met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="8b74b-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="8b74b-141">toosee Hallo-versie van hello Azure CLI 1.0 u hebt geïnstalleerd, type hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b74b-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="8b74b-142">U bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="8b74b-142">Now you are ready!</span></span> <span data-ttu-id="8b74b-143">alle tooaccess Hallo CLI-opdrachten toowork met uw eigen resources [tooyour Azure-abonnement verbinden van hello Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8b74b-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8b74b-144">Als u Azure CLI voor het eerst gebruikt, ziet u een bericht waarin wordt gevraagd of u informatie over het gebruik van het Microsoft-toocollect tooallow.</span><span class="sxs-lookup"><span data-stu-id="8b74b-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="8b74b-145">Deelname is niet verplicht.</span><span class="sxs-lookup"><span data-stu-id="8b74b-145">Participation is voluntary.</span></span> <span data-ttu-id="8b74b-146">Als u tooparticipate kiest, kunt u stoppen op elk gewenst moment door het uitvoeren van `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="8b74b-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="8b74b-147">tooenable deelname op elk gewenst moment uitvoeren `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="8b74b-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="8b74b-148">Hallo CLI bijwerken</span><span class="sxs-lookup"><span data-stu-id="8b74b-148">Update hello CLI</span></span>
<span data-ttu-id="8b74b-149">Bijgewerkte versies van hello Azure CLI regelmatig door Microsoft worden uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="8b74b-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="8b74b-150">Installeer Hallo CLI Hallo installatieprogramma gebruiken voor uw besturingssysteem of de meest recente Docker-container Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8b74b-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="8b74b-151">Of, als u hebt de meest recente Node.js en npm geïnstalleerd hello, bijwerken door Hallo volgende te typen (op Linux-distributies moet u mogelijk toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="8b74b-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="8b74b-152">Tab-Aanvulling inschakelen</span><span class="sxs-lookup"><span data-stu-id="8b74b-152">Enable tab completion</span></span>
<span data-ttu-id="8b74b-153">Tab-aanvulling van de CLI-opdrachten wordt ondersteund voor Mac en Linux.</span><span class="sxs-lookup"><span data-stu-id="8b74b-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="8b74b-154">tooenable in zsh, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8b74b-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="8b74b-155">tooenable in bash, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8b74b-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="8b74b-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b74b-156">Next steps</span></span>
* <span data-ttu-id="8b74b-157">[Verbinding maken vanaf Hallo CLI tooyour Azure-abonnement](xplat-cli-connect.md) toocreate en Azure-resources te beheren.</span><span class="sxs-lookup"><span data-stu-id="8b74b-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="8b74b-158">toolearn meer informatie over hello Azure CLI broncode downloaden, problemen, rapport of bijdragen toohello project, gaat u naar Hallo [GitHub-opslagplaats voor hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="8b74b-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="8b74b-159">Als u vragen over het gebruik van hello Azure CLI of Azure hebt, gaat u naar Hallo [Azure-Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="8b74b-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
