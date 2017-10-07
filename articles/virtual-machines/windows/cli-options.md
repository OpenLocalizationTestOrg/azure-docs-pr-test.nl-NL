---
title: aaaUsing hello Azure CLI in Windows | Microsoft Docs
description: Met behulp van hello Azure CLI in Windows
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Met behulp van hello Azure CLI in Windows

Hello Azure-opdrachtregelinterface (CLI) biedt een opdrachtregel en scriptomgeving op servers voor het maken en beheren van Azure-resources. Hello Azure CLI is beschikbaar voor Mac OS-, Linux- en Windows-besturingssystemen. In deze besturingssystemen zijn Hallo CLI-opdrachten identiek, maar de specifieke scriptsyntaxis besturingssysteem kan verschillen.

Dit document details Hallo manieren waarop u Azure CLI Hallo kan worden geïnstalleerd en uitgevoerd op Windows en details syntactische overwegingen voor elke. Zie in de gedetailleerde Azure CLI-documentatie voor [documentatie van Azure CLI]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Windows-subsysteem voor Linux

Hallo Windows-subsysteem voor Linux (WSL) biedt een omgeving Ubuntu Linux op Windows 10 Verjaardag en latere versies. Wanneer ingeschakeld, WSL levert een systeemeigen Bash-ervaring die kan worden gebruikt voor het maken en uitvoeren van scripts voor Azure CLI. Omdat WSL een systeemeigen Bash-ervaring biedt, kunnen Azure CLI-scripts worden gedeeld tussen Mac OS-, Linux- en Windows zonder aanpassing.

toouse hello Azure CLI in WSL, Hallo volgende voltooien.

|Taak | Instructies |
|---|---|
| WSL inschakelen | [WSL documentatie installeren](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Hello Azure CLI installeren |[Hallo CLI installeren op WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Hello Azure CLI kunt systeemeigen in Windows worden uitgevoerd. In deze configuratie hello Azure CLI-pakket is geïnstalleerd op Windows-besturingssysteem Hallo en opdrachten kunnen worden uitgevoerd vanuit PowerShell. In deze configuratie, kunnen Azure CLI-opdrachten en scripts worden uitgevoerd op een ondersteunde versie van Windows, maar de specifieke scriptsyntaxis platform vereist is. Als gevolg hiervan kunnen geen scripts altijd worden gedeeld tussen Mac OS-, Linux- en Windows zonder aanpassingen.

toouse hello Azure CLI op Windows hello pakket installeren via deze instructies [installeren Hallo CLI in Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Docker-afbeelding

Wanneer u Docker voor Windows, kan een Docker-installatiekopie worden gestart met hello Azure CLI. Deze installatiekopie is gebaseerd op Linux en bevat een systeemeigen Bash-ervaring.  Als u Docker voor Windows en hello Azure CLI-installatiekopie, scripts toobe gedeeld tussen Mac OS-, Linux- en Windows. 

toouse hello Azure CLI op Docker voor Windows, zorg ervoor dat Docker voor Windows wordt uitgevoerd en Hallo volgende opdracht uitvoeren.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Zodra de voltooid, wordt een sessie wordt gestart, dat wil Bash vooraf geladen met hello Azure CLI-hulpprogramma's.

## <a name="next-steps"></a>Volgende stappen

[Voorbeeld voor virtuele machines van Azure CLI](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Voorbeelden voor Web-Apps van Azure CLI](../../app-service-web/app-service-cli-samples.md)

[Voorbeelden voor SQL Azure CLI](../../sql-database/sql-database-cli-samples.md)
