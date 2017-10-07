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
# <a name="install-hello-azure-cli-10"></a>Hello Azure CLI 1.0 installeren
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Dit onderwerp wordt beschreven hoe tooinstall hello Azure CLI 1.0, die is gebaseerd op nodeJs en ondersteunt alle klassieke implementatie-API aanroept en een groot aantal implementatieactiviteiten van Resource Manager. Moet u Hallo [Azure CLI 2.0](/cli/azure/overview) voor nieuwe of toekomstgerichte CLI-implementaties en -beheer.

Snel installeren hello Azure-opdrachtregelinterface (Azure CLI 1.0) toouse een set van open-source shell-opdrachten voor het maken en beheren van resources in Microsoft Azure. U hebt verschillende opties tooinstall deze cross-platform-hulpprogramma's op uw computer:

* **npm pakket** - Run npm (Hallo package manager voor JavaScript) tooinstall Hallo nieuwste Azure CLI 1.0-pakket op uw Linux-distributie- of OS. Node.js en npm op uw computer vereist.
* **Installatieprogramma** -een installatieprogramma voor een eenvoudige installatie op de Mac- of Windows te downloaden.
* **Docker-container** - Start met behulp van Hallo nieuwste CLI in een kant-en-klaar Docker-container. Vereist Docker-host op uw computer.

Zie voor meer opties en achtergrond Hallo project opslagplaats op [GitHub](https://github.com/azure/azure-xplat-cli).

Nadat hello Azure CLI 1.0 is geïnstalleerd, [verbinding te maken met uw Azure-abonnement](xplat-cli-connect.md) en Voer Hallo **azure** opdrachten uit uw opdrachtregelinterface (Bash, Terminal, opdrachtprompt, enzovoort) toowork met uw Azure-resources.

## <a name="option-1-install-an-npm-package"></a>Optie 1: Een npm-pakket installeren
tooinstall hello CLI van een pakket npm, zorg ervoor dat u hebt gedownload en geïnstalleerd Hallo [nieuwste Node.js en npm](https://nodejs.org/en/download/package-manager/). Voer **npm installeren** tooinstall hello azure cli pakket:

```bash
npm install -g azure-cli
```

Op Linux-distributies, moet u mogelijk toouse **sudo** toosuccessfully uitvoeren Hallo **npm** opdracht als volgt:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Als u tooinstall moet of Node.js en npm op uw Linux-distributie- of OS bijwerken, wordt u aangeraden Hallo meest recente TNS Node.js-versie (4.x) te installeren. Als u een oudere versie gebruikt, krijgt u mogelijk installatiefouten.

Als u liever, downloaden Hallo nieuwste Linux [tar-bestand] [ linux-installer] pakket lokaal voor Hallo npm. Installeer vervolgens Hallo npm gedownloade pakket (op Linux-distributies moet u mogelijk toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Optie 2: Een installatieprogramma gebruiken
Als u een Mac- of Windows-computer gebruikt, zijn Hallo na CLI installatieprogramma's beschikbaar voor downloaden:

* [Mac OS X-installatieprogramma][mac-installer]
* [Windows MSI][windows-installer]

> [!TIP]
> In Windows, kunt u ook Hallo downloaden [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall Hallo CLI. Deze installer biedt u de optie tooinstall Hallo extra Azure-SDK en opdrachtregelprogramma's na de installatie van CLI Hallo.

## <a name="option-3-use-a-docker-container"></a>Optie 3: Een Docker-container gebruiken
Als u hebt ingesteld van uw computer als een [Docker](https://docs.docker.com/engine/understanding-docker/) host, kunt u uitvoeren Hallo nieuwste Azure CLI 1.0 in een Docker-container. Voer hello volgende opdracht (op Linux-distributies moet u mogelijk toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Azure CLI 1.0-opdrachten uitvoeren
Nadat hello Azure CLI 1.0 is geïnstalleerd, voert u Hallo **azure** opdracht uit vanaf de opdrachtregel gebruikersinterface (Bash, Terminal, opdrachtprompt, enzovoort). Typ bijvoorbeeld toorun Hallo help opdracht Hallo volgende:

```azurecli
azure help
```

> [!NOTE]
> Op sommige Linux-distributies, wordt een foutbericht weergegeven dat vergelijkbaar te`/usr/bin/env: ‘node’: No such file or directory`. Deze fout zijn afkomstig van recente installaties van Node.js op /usr/bin/nodejs wordt geïnstalleerd. toofix, een symbolische koppeling te/usr/bin/knooppunt maken met deze opdracht:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

toosee Hallo-versie van hello Azure CLI 1.0 u hebt geïnstalleerd, type hello te volgen:

```azurecli
azure --version
```

U bent nu klaar! alle tooaccess Hallo CLI-opdrachten toowork met uw eigen resources [tooyour Azure-abonnement verbinden van hello Azure CLI](xplat-cli-connect.md).

> [!NOTE]
> Als u Azure CLI voor het eerst gebruikt, ziet u een bericht waarin wordt gevraagd of u informatie over het gebruik van het Microsoft-toocollect tooallow. Deelname is niet verplicht. Als u tooparticipate kiest, kunt u stoppen op elk gewenst moment door het uitvoeren van `azure telemetry --disable`. tooenable deelname op elk gewenst moment uitvoeren `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Hallo CLI bijwerken
Bijgewerkte versies van hello Azure CLI regelmatig door Microsoft worden uitgegeven. Installeer Hallo CLI Hallo installatieprogramma gebruiken voor uw besturingssysteem of de meest recente Docker-container Hallo worden uitgevoerd. Of, als u hebt de meest recente Node.js en npm geïnstalleerd hello, bijwerken door Hallo volgende te typen (op Linux-distributies moet u mogelijk toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Tab-Aanvulling inschakelen
Tab-aanvulling van de CLI-opdrachten wordt ondersteund voor Mac en Linux.

tooenable in zsh, uitvoeren:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable in bash, uitvoeren:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Volgende stappen
* [Verbinding maken vanaf Hallo CLI tooyour Azure-abonnement](xplat-cli-connect.md) toocreate en Azure-resources te beheren.
* toolearn meer informatie over hello Azure CLI broncode downloaden, problemen, rapport of bijdragen toohello project, gaat u naar Hallo [GitHub-opslagplaats voor hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Als u vragen over het gebruik van hello Azure CLI of Azure hebt, gaat u naar Hallo [Azure-Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
