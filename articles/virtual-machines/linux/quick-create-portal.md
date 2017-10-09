---
title: aaaAzure Quick Start - VM-Portal maken | Microsoft Docs
description: Azure Quick Start - Een VM-portal maken
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a>Een virtuele Linux-machine maken met hello Azure-portal

Azure virtuele machines kunnen worden gemaakt via hello Azure-portal. Deze methode biedt een gebruikersinterface op basis van een browser voor het maken en configureren van virtuele machines en alle verwante resources. Met deze stappen Quick Start via een virtuele machine maken en de installatie van een webserver op Hallo VM.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="create-ssh-key-pair"></a>Een SSH-sleutelpaar maken

U moet een SSH-sleutelpaar toocomplete deze snel starten. Als u een bestaand SSH-sleutelpaar hebt, kunt u deze stap overslaan.

Deze opdracht uitvoert vanaf een Bash-shell en volg Hallo op het scherm aanwijzingen. opdrachtuitvoer Hallo bevat Hallo-bestandsnaam van het openbare sleutelbestand Hallo. Hallo-inhoud van Hallo openbaar-sleutelbestand toohello Klembord kopiëren.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a>Meld u bij tooAzure 

Toohello aanmelden met Azure-portal op http://portal.azure.com.

## <a name="create-virtual-machine"></a>Virtuele machine maken

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Selecteer **Compute** en selecteer vervolgens **Ubuntu Server 16.04 LTS**. 

3. Geef informatie op Hallo virtuele machine. Bij **Verificatietype** selecteert u **Openbare SSH-sleutel**. Bij het plakken in uw openbare SSH-sleutel, behandelen tooremove witruimte voorloop- of volgspaties. Na het voltooien klikt u op **OK**.

    ![Voer algemene informatie over uw virtuele machine Hallo-portalblade](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. Selecteer een grootte voor Hallo VM. toosee meer grootte en selecteer **weergeven van alle** of wijzig de Hallo **ondersteund schijftype** filter. 

    ![Schermopname van VM-grootten](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. Op de blade beleidinstellingen Hallo Hallo standaardinstellingen behouden en klik op **OK**.

6. Klik op de overzichtspagina Hallo **Ok** implementatie van de virtuele machine toostart Hallo.

7. Hallo VM is vastgemaakt toohello Azure-portaldashboard. Zodra het Hallo-implementatie is voltooid, wordt automatisch Hallo VM samenvatting blade geopend.


## <a name="connect-toovirtual-machine"></a>Verbinding maken met toovirtual machine

Een SSH-verbinding maken met Hallo virtuele machine.

1. Klik op Hallo **Connect** knop op Hallo virtuele machineblade. Hallo verbinding knop geeft een SSH-verbindingsreeks die kan worden gebruikt tooconnect toohello virtuele machine.

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. Voer Hallo volgende opdracht toocreate een SSH-sessie. Hallo-verbindingsreeks vervangen door Hallo die één u hebt gekopieerd uit hello Azure-portal.

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>NGINX installeren

Gebruik Hallo volgende scriptbronnen tooupdate pakket bash en installeer de meest recente NGINX-pakket Hallo. 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

Wanneer u klaar bent, sluit u Hallo SSH-sessie en retourneert Hallo VM-eigenschappen in hello Azure-portal.


## <a name="open-port-80-for-web-traffic"></a>Poort 80 openen voor webverkeer 

Een netwerkbeveiligingsgroep (NSG) beveiligt binnenkomend en uitgaand verkeer. Wanneer een virtuele machine vanuit hello Azure-portal wordt gemaakt, wordt een inkomende regel gemaakt op poort 22 voor SSH-verbindingen. Omdat deze virtuele machine fungeert als host voor een webserver, moet een regel voor het NSG toobe gemaakt voor poort 80.

1. Klik op de naam van de Hallo HALLO hallo voor virtuele machines **resourcegroep**.
2. Selecteer Hallo **netwerkbeveiligingsgroep**. Hallo NSG kan worden geïdentificeerd met Hallo **Type** kolom. 
3. Klik op het Hallo links menu onder instellingen **inkomende beveiligingsregels**.
4. Klik op **Toevoegen**.
5. Typ bij **Naam** **http**. Zorg ervoor dat **poortbereik** too80 is ingesteld en **actie** te is ingesteld,**toestaan**. 
6. Klik op **OK**.


## <a name="view-hello-nginx-welcome-page"></a>Hallo-NGINX welkomstpagina weergeven

Met NGINX geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet. Open een webbrowser en voer het openbare IP-adres Hallo Hallo VM. Hallo openbaar IP-adres, kunt u vinden op Hallo VM blade in hello Azure-portal.

![Standaardsite van NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, resourcegroep hello, virtuele machine en alle gerelateerde resources verwijderd. toodo dus resourcegroep Hallo Hallo virtuele machine blade selecteren en op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd. toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor virtuele Linux-machines.

> [!div class="nextstepaction"]
> [Zelfstudies over virtuele Linux-machines](./tutorial-manage-vm.md)
