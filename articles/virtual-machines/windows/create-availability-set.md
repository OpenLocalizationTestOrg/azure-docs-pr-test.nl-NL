---
title: Maak een VM-beschikbaarheid instellen in Azure | Microsoft Docs
description: Informatie over het maken van een beschikbaarheidsset beheerde of onbeheerde beschikbaarheidsset voor uw virtuele machines met behulp van Azure PowerShell of de portal in het Resource Manager-implementatiemodel.
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Toename VM beschikbaarheid door het maken van een Azure beschikbaarheidsset 
Beschikbaarheidssets redundantie voor uw toepassing. Het is raadzaam dat u twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Deze configuratie zorgt ervoor dat tijdens de gepland of ongepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de 99,95% Azure SLA. Zie de [SLA voor virtuele machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/) voor meer informatie.

> [!IMPORTANT]
> Virtuele machines moeten worden gemaakt in dezelfde resourcegroep bevinden als de beschikbaarheidsset.
> 

Als u wilt dat uw virtuele machine deel uitmaken van een beschikbaarheidsset, moet u eerst de beschikbaarheidsset maken of bij het maken van uw eerste virtuele machine in de set. Als uw VM beheerd schijven gebruikt, kan de beschikbaarheidsset moet worden gemaakt als een beschikbaarheidsset beheerde.

Zie voor meer informatie over het maken en de hand van beschikbaarheidssets [de beschikbaarheid van virtuele machines beheren](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a>De portal gebruiken voor het maken van een beschikbaarheidsset voordat u uw virtuele machines
1. Klik in het hub-menu op **Bladeren** en selecteer **beschikbaarheidssets**.
2. Op de **beschikbaarheidssets blade**, klikt u op **toevoegen**.
   
    ![Schermafbeelding van de knop toevoegen voor het maken van een nieuwe beschikbaarheid instellen.](./media/create-availability-set/add-availability-set.png)
3. Op de **beschikbaarheidsset maken** blade Vul de gegevens voor de set.
   
    ![Schermafbeelding van de informatie die u wilt opgeven voor het maken van de beschikbaarheidsset.](./media/create-availability-set/create-availability-set.png)
   
   * **Naam** -de naam moet 1-80 tekens bestaan uit getallen, letters, punten, onderstrepingstekens en streepjes bevatten. Het eerste teken moet een letter of cijfer. Het laatste teken moet een letter, cijfer of onderstrepingsteken zijn.
   * **Fault-domeinen** -domeinen met fouten definiëren in de groep van virtuele machines die een gemeenschappelijk power-bron- en switch delen. Standaard worden de virtuele machines worden gescheiden over maximaal drie domeinen met fouten en kunnen worden gewijzigd in tussen 1 en 3.
   * **Bijwerken van domeinen** - vijf update domeinen worden standaard toegewezen en dit kan worden ingesteld op tussen 1 en 20. Update domeinen duiden op groepen van virtuele machines en de onderliggende fysieke hardware die op hetzelfde moment kan worden opgestart. Bijvoorbeeld, als er vijf-domeinen bijwerken wanneer meer dan vijf virtuele machines worden geconfigureerd in een enkel Beschikbaarheidsset opgeeft, de zesde virtuele machine worden opgenomen in hetzelfde updatedomein als de eerste virtuele machine, de zevende in de dezelfde UD als de tweede virtuele machine, enzovoort. De volgorde van de opnieuw wordt opgestart niet mogelijk sequentiële, maar slechts één updatedomein tegelijk zal worden opgestart.
   * **Abonnement** -de te gebruiken als u meer dan één abonnement selecteren.
   * **Resourcegroep** -Selecteer een bestaande resourcegroep door te klikken op de pijl en te selecteren van een resourcegroep in de vervolgkeuzelijst omlaag. U kunt ook een nieuwe resourcegroep maken door een naam te typen. De naam mag geen van de volgende tekens bevatten: letters, cijfers, punten, streepjes, onderstrepingstekens en openen of sluithaakje. De naam mag niet eindigen op een punt. Alle van de virtuele machines in de beschikbaarheidsgroep moet worden gemaakt in dezelfde resourcegroep bevinden als de beschikbaarheidsset.
   * **Locatie** -Selecteer een locatie in de vervolgkeuzelijst.
   * **Beheerde** : Selecteer *Ja* voor het maken van een beheerde beschikbaarheid instellen voor gebruik met virtuele machines die gebruikmaken van beheerde schijven voor opslag. Selecteer **Nee** als de virtuele machines die weergegeven in de set worden met niet-beheerde schijven in een opslagaccount.
   
4. Wanneer u klaar bent u de gegevens invoert, klikt u op **maken**. 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a>De portal gebruiken om een virtuele machine en op hetzelfde moment beschikbaarheidsset maken
Als u een nieuwe virtuele machine via de portal maakt, kunt u ook een nieuwe beschikbaarheidsset voor de virtuele machine bij het maken van de eerste virtuele machine in de set. Als u kiest moet worden beheerd schijven gebruikt voor uw virtuele machine, kunt u een beheerde beschikbaarheidsset wordt gemaakt.

![Schermafbeelding van het proces voor het maken van een nieuwe beschikbaarheidsset bij het maken van de virtuele machine.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a>Een nieuwe virtuele machine toevoegen aan een bestaande beschikbaarheidsset in de portal
Voor elke extra VM die u maakt die in de set moet behoren, zorg ervoor dat u dit hebt gemaakt in dezelfde **resourcegroep** en selecteer vervolgens de bestaande beschikbaarheidsset in stap 3. 

![Schermopname die laat zien hoe u een bestaande beschikbaarheidsset gebruiken voor uw virtuele machine selecteert.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a>Gebruik PowerShell voor het maken van een beschikbaarheidsset
In dit voorbeeld maakt u een beschikbaarheidsset benoemde **myAvailabilitySet** in de **myResourceGroup** resourcegroep in de **VS-West** locatie. Dit moet doen voordat u de eerste virtuele machine die zich in de set maakt.

Voordat u begint, zorg ervoor dat u de nieuwste versie van de AzureRM.Compute PowerShell-module hebt. Voer de volgende opdracht om deze te installeren.

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
* Bij het maken van een virtuele machine, als de gewenste beschikbaarheidsset niet in de vervolgkeuzelijst in de portal kunt u deze gemaakt in een andere resourcegroep. Als u niet weet de resourcegroep voor uw beschikbaarheid instellen, gaat u naar het hub-menu en klik op Bladeren > beschikbaarheidssets voor een overzicht van uw beschikbaarheidssets en welke resourcegroepen waartoe ze behoren.

## <a name="next-steps"></a>Volgende stappen
Extra opslagruimte toevoegen aan uw virtuele machine met het toevoegen van een extra [gegevensschijf](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

