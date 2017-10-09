---
title: aaaAzure Quick Start - Portal voor Windows VM maken | Microsoft Docs
description: Azure Quick Start - Een Windows VM-portal maken
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a>Maken van een virtuele machine van Windows Hello Azure-portal

Azure virtuele machines kunnen worden gemaakt via hello Azure-portal. Deze methode biedt een gebruikersinterface op basis van een browser voor het maken en configureren van virtuele machines en alle verwante resources. Met deze stappen Quick Start via een virtuele machine maken en de installatie van een webserver op Hallo VM.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Toohello aanmelden met Azure-portal op http://portal.azure.com.

## <a name="create-virtual-machine"></a>Virtuele machine maken

1. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Selecteer **Compute** en vervolgens **Windows Server 2016 Datacenter**. 

3. Geef informatie op Hallo virtuele machine. Hallo-gebruikersnaam en wachtwoord die u hier invoert is gebruikte toolog in toohello virtuele machine. Na het voltooien klikt u op **OK**.

    ![Voer algemene informatie over uw virtuele machine Hallo-portalblade](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. Selecteer een grootte voor Hallo VM. toosee meer grootte en selecteer **weergeven van alle** of wijzig de Hallo **ondersteund schijftype** filter. 

    ![Schermopname van VM-grootten](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. Op de blade beleidinstellingen Hallo Hallo standaardinstellingen behouden en klik op **OK**.

6. Klik op de overzichtspagina Hallo **Ok** implementatie van de virtuele machine toostart Hallo.

7. Hallo VM is vastgemaakt toohello Azure-portaldashboard. Zodra het Hallo-implementatie is voltooid, wordt automatisch Hallo VM samenvatting blade geopend.


## <a name="connect-toovirtual-machine"></a>Verbinding maken met toovirtual machine

Maak een verbinding met extern bureaublad toohello virtuele machine.

1. Klik op Hallo **Connect** knop op de eigenschappen van de virtuele machine Hallo. Er wordt een Remote Desktop Protocol-bestand (.rdp) gemaakt en gedownload.

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. tooconnect tooyour VM, open Hallo gedownload RDP-bestand. Als u hierom wordt gevraagd, klikt u op **Verbinden**. Op een Mac moet u een RDP-client, zoals deze [extern bureaublad-Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) van Hallo Mac App Store.

3. Voer Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven bij het maken van Hallo virtuele machine en klik vervolgens op **Ok**.

4. Foutbericht een certificaatwaarschuwing tijdens Hallo aanmelden. Klik op **Ja** of **doorgaan** tooproceed met Hallo-verbinding.


## <a name="install-iis-using-powershell"></a>IIS installeren met behulp van PowerShell

Op Hallo virtuele machine, een PowerShell-sessie starten en Voer Hallo opdracht tooinstall IIS te volgen.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Wanneer u klaar bent, sluit u Hallo RDP-sessie en retourneert Hallo VM-eigenschappen in hello Azure-portal.

## <a name="open-port-80-for-web-traffic"></a>Poort 80 openen voor webverkeer 

Een netwerkbeveiligingsgroep (NSG) beveiligt binnenkomend en uitgaand verkeer. Wanneer een virtuele machine vanuit hello Azure-portal wordt gemaakt, wordt een inkomende regel gemaakt op poort 3389 voor RDP-verbindingen. Omdat deze virtuele machine fungeert als host voor een webserver, moet een regel voor het NSG toobe gemaakt voor poort 80.

1. Klik op de naam van de Hallo HALLO hallo voor virtuele machines **resourcegroep**.
2. Selecteer Hallo **netwerkbeveiligingsgroep**. Hallo NSG kan worden geïdentificeerd met Hallo **Type** kolom. 
3. Klik op het Hallo links menu onder instellingen **inkomende beveiligingsregels**.
4. Klik op **Toevoegen**.
5. Typ bij **Naam** **http**. Zorg ervoor dat **poortbereik** too80 is ingesteld en **actie** te is ingesteld,**toestaan**. 
6. Klik op **OK**.


## <a name="view-hello-iis-welcome-page"></a>Weergave Hallo IIS-welkomstpagina

Met IIS geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet. Open een webbrowser en voer het openbare IP-adres Hallo Hallo VM. Hallo openbaar IP-adres, kunt u vinden op Hallo VM blade in hello Azure-portal.

![Standaardsite van IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, resourcegroep hello, virtuele machine en alle gerelateerde resources verwijderd. toodo dus resourcegroep Hallo Hallo virtuele machine blade selecteren en op **verwijderen**.

## <a name="next-steps"></a>Volgende stappen

In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd. toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor VM's van Windows.

> [!div class="nextstepaction"]
> [Zelfstudies over virtuele Windows-machines](./tutorial-manage-vm.md)
