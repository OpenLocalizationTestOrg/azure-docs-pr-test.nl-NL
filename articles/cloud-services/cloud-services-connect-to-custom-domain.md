---
title: een Cloudservice tooa aaaConnect aangepaste domeincontroller | Microsoft Docs
description: Meer informatie over hoe tooconnect uw web/worker rollen tooa aangepaste AD-domein met behulp van PowerShell en uitbreiding van AD-domein
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Verbinding maken met Azure Cloud Services-functies tooa aangepaste AD-domeincontroller worden gehost in Azure
Er wordt eerst een virtueel netwerk (VNet) instellen in Azure. Er wordt een Active Directory-domeincontroller (gehost op een virtuele Machine van Azure) toohello VNet toegevoegd. Vervolgens wordt er bestaande cloud service rollen toohello vooraf gemaakte VNet toevoegen en verbind ze toohello domeincontroller.

Voordat we aan de slag, paar van tookeep rekening dingen:

1. Deze zelfstudie wordt gebruikgemaakt van PowerShell, dus zorg ervoor dat u hebt Azure PowerShell is geïnstalleerd en gereed toogo. Zie tooget hulp bij het instellen van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
2. Uw AD-domeincontroller en de functie Web/Worker-exemplaren moeten toobe in Hallo VNet.

Volg deze stapsgewijze handleiding en als u problemen ondervindt uitvoert, laat ons een opmerking achter Hallo Hallo artikel. Iemand krijg je terug tooyou (Ja, we opmerkingen lezen).

Hallo-netwerk waarnaar wordt verwezen door de cloudservice Hallo moet een **klassiek virtueel netwerk**.

## <a name="create-a-virtual-network"></a>Een virtueel netwerk maken
U kunt een virtueel netwerk maken in Azure met behulp van hello Azure-portal of PowerShell. Voor deze zelfstudie gebruiken we PowerShell. een virtueel netwerk met toocreate hello Azure portal, Zie [virtueel netwerk maken](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>Een virtuele machine maken
Als u klaar bent met het instellen van Hallo virtueel netwerk, moet u toocreate een AD-domeincontroller. Voor deze zelfstudie stellen we van een AD-domeincontroller op een virtuele Machine van Azure.

toodo hiervan kan een virtuele machine via PowerShell met behulp van de volgende opdrachten Hallo maken:

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>De virtuele Machine tooa domeincontroller promoveren
tooconfigure hello virtuele Machine als een AD-domeincontroller, wordt u toolog in toohello VM nodig hebt en configureert.

toolog in toohello VM ophalen Hallo RDP-bestand via PowerShell, gebruik Hallo volgende opdrachten:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Zodra u toohello VM bent aangemeld, instellen van uw virtuele Machine als AD-domeincontroller door de volgende Hallo stapsgewijze handleiding op [hoe tooset van uw klant AD-domeincontroller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Uw Cloudservice toohello virtueel netwerk toevoegen
Vervolgens moet u tooadd uw cloud service-implementatie toohello nieuwe VNet. toodo dit uw cloud service cscfg wijzigen door toe te voegen Hallo relevante secties tooyour cscfg met Visual Studio of Hallo editor naar keuze.

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

Vervolgens uw cloud services-project te bouwen en implementeren van deze tooAzure. Zie tooget hulp bij het implementeren van uw cloud services-pakket-tooAzure [hoe tooCreate en implementeren van een Service in de Cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Verbinding maken met uw web/worker rollen toohello domein
Zodra uw cloudserviceproject is geïmplementeerd in Azure, verbinding maken met uw rol exemplaren toohello aangepaste AD-domein met Hallo uitbreiding van AD-domein. tooadd hello AD-domein extensie tooyour bestaande cloud services-implementatie- en join Hallo aangepast domein, uitvoeren Hallo opdrachten in PowerShell te volgen:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

En dat is alles.

Uw cloudservices moet gekoppelde tooyour aangepaste domeincontroller. Als u wilt meer informatie over verschillende opties beschikbaar voor Hallo toolearn hoe tooconfigure uitbreiding van AD-domein, gebruik Hallo PowerShell helpen. Een aantal voorbeelden volgt:

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
