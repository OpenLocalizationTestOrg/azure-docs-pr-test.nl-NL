---
title: aaaMove bestanden tooand van Azure Linux VM's met SCP | Microsoft Docs
description: Veilig verplaatsen bestanden tooand van een Linux-VM in Azure met behulp van SCP en een SSH-sleutelpaar.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Bestanden tooand verplaatsen van een Linux-VM met SCP

Dit artikel laat zien hoe toomove bestanden van uw werkstation up tooan Azure Linux VM of van een Azure Linux VM omlaag tooyour werkstation met behulp van Secure kopiëren (SCP). Verplaatsen van bestanden tussen uw werkstation en Linux-VM snel en veilig is essentieel voor het beheren van uw Azure-infrastructuur. 

Dit artikel, moet u een Linux-VM is geïmplementeerd in Azure worden verkregen met [SSH openbare en persoonlijke sleutelbestanden](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). U moet ook een SCP-client voor de lokale computer. Het is gebouwd op SSH en opgenomen in Hallo standaard Bash-shell van de meeste Linux en Mac-computers en sommige houders van Windows.

## <a name="quick-commands"></a>Snelle opdrachten

Kopieer een bestand up toohello Linux VM

```bash
scp file azureuser@azurehost:directory/targetfile
```

Een bestand kopiëren naar beneden van Hallo Linux VM

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Gedetailleerd overzicht

Als voorbeelden, we een Azure-configuratiebestand up tooa Linux VM verplaatsen en ophalen van een logboekmap beide SCP en de SSH-sleutels gebruiken.   

## <a name="ssh-key-pair-authentication"></a>SSH-sleutelpaar verificatie

SCP gebruikt SSH voor Hallo transportlaag. SSH ingangen Hallo verificatie op de doelhost Hallo en het Hallo-bestand in een versleutelde standaard meegeleverd met SSH-tunnel wordt verplaatst. Voor SSH-verificatie, de gebruikersnamen en wachtwoorden kunnen worden gebruikt. SSH openbare en persoonlijke sleutel verificatie worden echter aanbevolen als aanbevolen beveiligingsprocedure. Als SSH heeft geverifieerd Hallo verbinding, SCP begint vervolgens met de Hallo-bestand wordt gekopieerd. Met behulp van een correct geconfigureerde `~/.ssh/config` en SSH-openbare en persoonlijke sleutels, Hallo SCP verbinding kunnen worden gemaakt met behulp van slechts een servernaam (of IP-adres). Als u slechts één SSH-sleutel hebt, SCP in Hallo voor gezocht `~/.ssh/` directory, en wordt gebruikt door standaard toolog in toohello VM.

Voor meer informatie over het configureren van uw `~/.ssh/config` en SSH-openbare en persoonlijke sleutels, Zie [maken SSH-sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP een bestand tooa Linux VM

Voor het eerste voorbeeld hello kopieert u een Azure-configuratiebestand up tooa Linux VM die is gebruikt toodeploy automatisering. Beveiliging is belangrijk, omdat dit bestand bevat de Azure-API-referenties, waaronder geheimen. Hallo gecodeerde tunnel geleverd door SSH beveiligt Hallo inhoud van Hallo-bestand.

Hallo na de opdracht kopieën Hallo lokale *.azure/config* tooan virtuele machine van Azure met FQDN-naam bestand *myserver.eastus.cloudapp.azure.com*. Hallo-beheerdersgebruikersnaam op Hallo Azure VM is *azureuser* . Hallo-bestand is gerichte toohello */home/azureuser/* directory. Vervangt door uw eigen waarden in deze opdracht.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>SCP een map van een Linux-VM

In dit voorbeeld wordt een map met logbestanden van Hallo Linux VM tooyour Workstation kopiëren. Een logboekbestand kan of kan geen gevoelige of geheime gegevens. Echter, SCP zorgt u ervoor Hallo inhoud van de logboekbestanden Hallo zijn versleuteld. SCP tootransfer Hallo bestanden is de eenvoudigste manier tooget Hallo Hallo logboekmap en bestanden tooyour Workstation, terwijl tegelijkertijd ook beveiligd.

Hallo volgende opdracht kopieert bestanden in Hallo *thuis-/azureuser/logboeken/* directory op Hallo Azure VM toohello lokale map directory:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Hallo `-r` cli vlag Hiermee geeft u SCP toorecursively kopie Hallo bestanden en mappen van Hallo punt van Hallo-map weergegeven in het Hallo-opdracht.  U ziet dat de opdrachtregelsyntaxis Hallo is ook vergelijkbare tooa `cp` -opdracht kopiëren.

## <a name="next-steps"></a>Volgende stappen

* [Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
