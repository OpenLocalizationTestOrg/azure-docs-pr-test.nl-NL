---
title: aaaCreate de beschikbaarheid van een virtuele machine in Azure instellen | Microsoft Docs
description: Informatie over hoe ingesteld toocreate een beschikbare beheerde of onbeheerde beschikbaarheid instellen voor uw virtuele machines met Azure PowerShell of Hallo portal Hallo Resource Manager-implementatiemodel.
keywords: Beschikbaarheidsset
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Toename VM beschikbaarheid door het maken van een Azure beschikbaarheidsset 
Beschikbaarheidssets bieden redundantie tooyour toepassing. Het is raadzaam dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine zal beschikbaar zijn en voldoen aan Hallo 99,95% Azure SLA. Zie voor meer informatie, Hallo [SLA voor virtuele Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Virtuele machines moeten worden gemaakt in Hallo dezelfde resourcegroep als Hallo beschikbaarheidsset.
> 

Als u wilt dat uw VM toobe een deel van een beschikbaarheidsset, moet u toocreate Hallo beschikbaarheid instellen eerste of terwijl u uw eerste virtuele machine in maakt Hallo set. Als uw VM beheerd schijven gebruikt, moet de beschikbaarheidsset Hallo worden gemaakt als een beschikbaarheidsset beheerde.

Zie voor meer informatie over het maken en de hand van beschikbaarheidssets [Hallo beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Hallo portal toocreate beschikbaarheidsset voordat u uw virtuele machines gebruiken
1. Klik in het menu hub Hallo op **Bladeren** en selecteer **beschikbaarheidssets**.
2. Op Hallo **beschikbaarheidssets blade**, klikt u op **toevoegen**.
   
    ![Schermafbeelding van Hallo knop voor het maken van een nieuwe beschikbaarheidsset toevoegen.](./media/create-availability-set/add-availability-set.png)
3. Op Hallo **beschikbaarheidsset maken** blade, volledige Hallo-informatie voor uw set.
   
    ![Schermopname die toont informatie die u nodig tooenter toocreate Hallo beschikbaarheid Hallo ingesteld.](./media/create-availability-set/create-availability-set.png)
   
   * **Naam** -Hallo-naam moet 1-80 tekens bestaan uit getallen, letters, punten, onderstrepingstekens en streepjes bevatten. Hallo eerste teken moet een letter of cijfer zijn. Hallo laatste teken moet een letter, cijfer of onderstrepingsteken zijn.
   * **Fault-domeinen** -domeinen met fouten definiëren Hallo groep virtuele machines die een gemeenschappelijk power-bron- en switch delen. Standaard kunnen Hallo VMs gescheiden zijn in up toothree domeinen met fouten en gewijzigde toobetween 1 en 3.
   * **Bijwerken van domeinen** - vijf update domeinen worden standaard toegewezen en deze toobetween 1 en 20 kan worden ingesteld. Update domeinen groepen van virtuele machines en de onderliggende fysieke hardware die kan worden opgestart op Hallo duiden op hetzelfde moment. Bijvoorbeeld, als er vijf update domeinen, wanneer meer dan vijf virtuele machines worden geconfigureerd in een enkel Beschikbaarheidsset, Hallo zesde virtuele machine worden opgenomen in Hallo hetzelfde updatedomein als eerste virtuele machine Hallo Hallo zevende opgeeft Hallo dezelfde UD als Hallo tweede virtuele machine, enzovoort. mogelijk sequentiële volgorde Hallo Hallo opnieuw te worden opgestart niet, maar slechts één updatedomein tegelijk zal worden opgestart.
   * **Abonnement** -Selecteer Hallo abonnement toouse als er meer dan één.
   * **Resourcegroep** -Selecteer een bestaande resourcegroep door te klikken op de pijl Hallo en een resourcegroep te selecteren Hallo vervolgkeuzelijst. U kunt ook een nieuwe resourcegroep maken door een naam te typen. Hallo naam mag geen van de volgende tekens Hallo: letters, cijfers, punten, streepjes, onderstrepingstekens en openen of sluithaakje. Hallo-naam mag niet eindigen op een punt. Alle Hallo virtuele machines in de beschikbaarheidsgroep Hallo toobe in Hallo hebt gemaakt, moeten dezelfde resourcegroep als Hallo beschikbaarheidsset.
   * **Locatie** -Selecteer een locatie in de vervolgkeuzelijst Hallo.
   * **Beheerde** : Selecteer *Ja* toocreate een beschikbare beheerde ingesteld toouse met virtuele machines die gebruikmaken van beheerde schijven voor opslag. Selecteer **Nee** als Hallo virtuele machines die weergegeven in het Hallo-set worden niet-beheerde schijven in een opslagaccount gebruikt.
   
4. Wanneer u klaar bent met het invoeren van Hallo gegevens, klikt u op **maken**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Gebruik Hallo portal toocreate een virtuele machine en een beschikbaarheid op Hallo dezelfde instellen tijd
Als u een nieuwe virtuele machine met behulp van Hallo portal maakt, kunt u ook een nieuwe beschikbaarheidsset voor Hallo VM bij het maken van Hallo maken eerste VM in het Hallo-set. Als u toouse beheerd schijven voor uw virtuele machine kiest, kunt u een beheerde beschikbaarheidsset wordt gemaakt.

![Schermafbeelding van Hallo-proces voor het maken van een nieuwe beschikbaarheidsset bij het maken van Hallo VM.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Voeg een nieuwe VM tooan bestaande beschikbaarheidsset Hallo-portal
Hallo voor elke extra VM die u maakt moet deel uitmaken van Hallo set, zorg ervoor dat u maakt in dezelfde **resourcegroep** en vervolgens selecteert Hallo bestaande beschikbaarheidsset in stap 3. 

![Schermopname die laat zien hoe de bestaande beschikbaarheidsset tooselect toouse ingesteld voor uw virtuele machine.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>Gebruik PowerShell toocreate een beschikbaarheidsset instellen
In dit voorbeeld maakt u een beschikbaarheidsset benoemde **myAvailabilitySet** in Hallo **myResourceGroup** resourcegroep in Hallo **VS-West** locatie. Dit moet doen voordat u Hallo maakt toobe eerste virtuele machine die zich in Hallo set.

Voordat u begint, zorg ervoor dat u de meest recente versie Hallo Hallo AzureRM.Compute PowerShell-module hebt. Voer Hallo na de opdracht tooinstall deze.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Zie voor meer informatie [Azure PowerShell Versioning](/powershell/azure/overview).


Als u beheerde schijven voor uw virtuele machines gebruikt, typt u:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Als u uw eigen storage-accounts voor uw virtuele machines gebruikt, typt u:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Zie voor meer informatie [nieuw AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Problemen oplossen
* Bij het maken van een virtuele machine als Hallo beschikbaarheid sets die u wilt zich niet in Hallo vervolgkeuzelijst in de portal Hallo u mogelijk hebt gemaakt in een andere resourcegroep. Als u niet weet Hallo resourcegroep voor uw beschikbaarheid instellen, gaat u toohello hub-menu en klik op Bladeren > beschikbaarheidssets toosee Hiermee stelt u een lijst van de beschikbaarheid en welke resourcegroepen waartoe ze behoren.

## <a name="next-steps"></a>Volgende stappen
Toevoegen van extra opslagruimte tooyour VM door toe te voegen een extra [gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

