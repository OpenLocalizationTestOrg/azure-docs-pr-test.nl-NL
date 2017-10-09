---
title: aaaHow tootag een virtuele machine van Windows-resource in Azure | Microsoft Docs
description: Meer informatie over virtuele Windows-machine gemaakt in Azure met Resource Manager-implementatiemodel Hallo-tagging
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Hoe tootag virtuele Windows-machine in Azure
In dit artikel beschrijft de verschillende manieren tootag virtuele Windows-machine in Azure via Hallo Resource Manager-implementatiemodel. Labels zijn de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks op een resource of een resourcegroep kunnen worden geplaatst. Azure biedt momenteel ondersteuning voor maximaal too15 labels per resource en resourcegroep. Labels van een resource kunnen worden geplaatst op Hallo moment gemaakt of bestaande resource tooan toegevoegd. Houd er rekening mee dat de labels voor resources die zijn gemaakt via Hallo Resource Manager-implementatiemodel alleen worden ondersteund. Als u een virtuele Linux-machine tootag wilt, Zie [hoe een virtuele Linux-machine in Azure tootag](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Labels met PowerShell
toocreate, toevoegen en verwijderen van de labels via PowerShell, moet u eerst tooset van uw [PowerShell-omgeving met Azure Resource Manager][PowerShell environment with Azure Resource Manager]. Nadat u Hallo-installatie hebt voltooid, kunt u labels kunt plaatsen op Compute, netwerk en opslag bronnen bij het maken of nadat het Hallo-resource is gemaakt via PowerShell. In dit artikel zal zich concentreren op weergeven/bewerken labels geplaatst op virtuele Machines.

Ga eerst tooa virtuele Machine via Hallo `Get-AzureRmVM` cmdlet.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Als uw virtuele Machine al labels bevat, klikt u vervolgens ziet u alle Hallo-tags van uw resources:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Als u de labels tooadd via PowerShell dat wilt, kunt u Hallo `Set-AzureRmResource` opdracht. Houd er rekening mee bij het bijwerken van labels via PowerShell, tags worden bijgewerkt als geheel. Dus als u een bron van de tag tooa waarvoor al labels toevoegt, moet u tooinclude alle Hallo-labels die u wilt dat toobe op Hallo resource geplaatst. Hieronder volgt een voorbeeld van hoe extra tooadd tags tooa resource via PowerShell-Cmdlets.

Deze eerste cmdlet worden alle Hallo labels op geplaatst *MyTestVM* toohello *$tags* variabele, met behulp van Hallo `Get-AzureRmResource` en `Tags` eigenschap.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Hallo tweede opdracht geeft Hallo labels voor Hallo variabele opgegeven.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

Hallo derde opdracht voegt een extra tag toohello *$tags* variabele. Houd er rekening mee Hallo gebruik van Hallo  **+=**  tooappend Hallo nieuwe sleutel/waarde-paar toohello *$tags* lijst.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

Hallo vierde opdracht worden alle Hallo codes, gedefinieerd in Hallo *$tags* variabele toohello resource opgegeven. In dit geval is het MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

Hallo vijfde opdracht geeft alle Hallo labels op Hallo resource. Zoals u ziet, *locatie* is nu gedefinieerd als een label met *MyLocation* Hallo-waarde.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

informatie over toolearn Hallo tagging via PowerShell, Bekijk [Azure Resource Cmdlets][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over uw Azure-resources te labelen [overzicht van Azure Resource Manager] [ Azure Resource Manager Overview] en [tooorganize labels met behulp van uw Azure-Resources] [ Using Tags tooorganize your Azure Resources].
* toosee hoe labels kunt u uw gebruik van Azure-resources beheren raadpleegt [inzicht in uw Azure-factuur] [ Understanding your Azure Bill] en [inzicht in uw Microsoft Azure-brongebruik] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
