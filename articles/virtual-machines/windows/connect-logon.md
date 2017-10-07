---
title: aaaConnect tooa VM van Windows Server | Microsoft Docs
description: Meer informatie over hoe tooconnect en aanmelding tooa virtuele machine van Windows hello Azure portal en Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows
U Hallo **Connect** knop in hello Azure portal toostart een Remote Desktop (RDP)-sessie op een Windows-bureaublad. Eerst maakt u verbinding toohello virtuele machine en u zich aanmeldt.

Als u tooconnect tooa Windows VM van een Mac probeert, moet u een RDP-client voor Mac, zoals tooinstall [Microsoft Extern bureaublad](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Verbinding maken met toohello virtuele machine
1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Klik op het menu Hub Hallo **virtuele Machines**.
3. Selecteer Hallo virtuele machine uit de lijst Hallo.
4. Klik op de blade voor de virtuele machine van Hallo Hallo **Connect**.
   
    ![Schermopname van hello Azure portal weergeeft hoe tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Als hello **Connect** knop in Hallo portal grijs is en u niet bent verbonden tooAzure via een [Express Route](../../expressroute/expressroute-introduction.md) of [Site-naar-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) verbinding, moet u toocreate en toewijzen van de VM een openbaar IP-adres voordat u extern bureaublad kunt gebruiken. Er is meer informatie over [openbare IP-adressen in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) beschikbaar.
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Meld u aan toohello virtuele machine
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Volgende stappen
Als u ondervindt wanneer u tooconnect probeert, Zie [problemen met extern bureaublad-verbindingen](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Dit artikel leidt u door het opsporen en oplossen van veelvoorkomende problemen.

