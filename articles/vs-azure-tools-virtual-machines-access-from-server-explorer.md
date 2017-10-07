---
title: Azure virtuele Machines in Server Explorer aaaAccessing | Microsoft Docs
description: Biedt een overzicht van hoe tooview maken en beheren van Azure virtuele machines (VM's) in Server Explorer in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Toegang tot virtuele Machines van Azure in Server Explorer
Server Explorer in Visual Studio gebruikt, kunt u informatie weergeven over uw virtuele machines die door Azure worden gehost.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Toegang tot virtuele machines in Server Explorer
Als u virtuele machines die worden gehost door Azure hebt, kunt u deze kunt openen in Server Explorer. U moet eerst aanmelden tooyour Azure-abonnement tooview uw mobile services. toosign, Hallo snelmenu voor hello Azure knooppunt in Server Explorer te openen en kies **tooMicrosoft Azure verbinding**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget informatie over uw virtuele machines
1. In Server Explorer, kiest u een virtuele machine en kies vervolgens Hallo F4 sleutel tooshow het eigenschappenvenster.
   
    Hallo volgende tabel ziet u welke eigenschappen beschikbaar zijn, maar ze zijn allemaal alleen-lezen. toochange ze, gebruikt u Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Eigenschap | Beschrijving |
   | --- | --- |
   | DNS-naam |Hallo-URL met Hallo internetadres van Hallo virtuele machine. |
   | Omgeving |Hallo-waarde van deze eigenschap is voor een virtuele machine altijd productie. |
   | Naam |Hallo-naam van Hallo virtuele machine. |
   | Grootte |Hallo-grootte van Hallo virtuele machine, die weerspiegelt Hallo en de hoeveelheid geheugen en schijfruimte ruimte die beschikbaar is. Zie voor meer informatie How To: grootte van virtuele machines configureren. |
   | Status |Waarden zijn starten, gestart, gestopt, gestopt en Status ophalen. Als bij het ophalen van de Status wordt weergegeven, is de huidige status Hallo is onbekend. Hallo-waarden voor deze eigenschap verschillen van Hallo-waarden die worden gebruikt op Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | Abonnements-id |Hallo abonnements-ID voor uw Azure-account. U kunt deze informatie weergeven op Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885) door Hallo-eigenschappen voor een abonnement te bekijken. |
2. Kies een knooppunt van het eindpunt en bekijkt hello **eigenschappen** venster.
3. Hallo volgende tabel beschrijft Hallo beschikbare eigenschappen van eindpunten, maar ze zijn alleen-lezen. Hallo-eindpunten voor tooadd of bewerken voor een virtuele machine, gebruik Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Eigenschap | Beschrijving |
   | --- | --- |
   | Naam |Een id voor het Hallo-eindpunt. |
   | Particuliere poort |Hallo-poort voor het netwerk toegang tot interne tooyour toepassing. |
   | Protocol |Hallo-protocol dat Hallo transportlaag voor dit eindpunt wordt gebruikt, TCP of UDP. |
   | Openbare poort |Hallo-poort die wordt gebruikt voor openbare toegang tooyour toepassing. |

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het gebruik van Azure-functies in Visual Studio, Zie [met behulp van extern bureaublad met de Azure-rollen](vs-azure-tools-remote-desktop-roles.md).

