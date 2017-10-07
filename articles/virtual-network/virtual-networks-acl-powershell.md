---
title: toegang tot Azure-eindpunt aaaManage lijsten beheren | PowerShell | Klassieke | Microsoft Docs
description: Meer informatie over hoe toomanage ACL's met PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Eindpunt toegangsbeheerlijsten met PowerShell in het klassieke implementatiemodel Hallo beheren
U kunt maken en beheren van netwerk-toegangsbeheerlijsten (ACL's) voor eindpunten met behulp van Azure PowerShell of in het Hallo-beheerportal. In dit onderwerp vindt u procedures voor ACL algemene taken die u kunt uitvoeren met behulp van PowerShell. Zie voor Hallo overzicht van Azure PowerShell cmdlets [Azure Management-Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721). Zie voor meer informatie over ACL's, [wat is er een netwerk lijst ACL (Access Control)?](virtual-networks-acl.md). Als u uw ACL's toomanage wilt met behulp van Hallo-beheerportal, Zie [hoe tooSet Up eindpunten tooa virtuele Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Netwerk-ACL's beheren met behulp van Azure PowerShell
U kunt Azure PowerShell-cmdlets toocreate, verwijderen en te configureren (set) netwerk toegangsbeheerlijsten (ACL's). Vindt u enkele voorbeelden van een aantal Hallo manieren waarop die u een ACL die met behulp van PowerShell kunt configureren.

tooretrieve een volledige lijst met Hallo ACL PowerShell-cmdlets, kunt u een van de volgende Hallo:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Maken van een netwerk-ACL met regels die toegang vanaf een extern subnet verlenen
Hallo in het volgende voorbeeld ziet u een manier toocreate een nieuwe ACL dat regels bevat. Deze ACL wordt vervolgens toegepast eindpunt van de virtuele machine tooa. Hallo ACL-regels in Hallo in het volgende voorbeeld wordt toegang toestaan via een extern subnet. een nieuwe netwerk-ACL met regels voor toestaan voor een extern subnet toocreate open een Azure PowerShell ISE. Kopiëren en plakken onderstaande Hallo script configureren met uw eigen waarden Hallo-script en vervolgens Hallo-script uitvoeren.

1. Hallo nieuw netwerk ACL-object maken.
   
        $acl1 = New-AzureAclConfig
2. Een regel waarmee de toegang van een extern subnet instellen. In onderstaande Hallo voorbeeld, stelt u de regel *100* (dit heeft voorrang op de regel 200 en hoger) tooallow Hallo extern subnet *10.0.0.0/8* toegang tot toohello virtuele machine-eindpunt. Hallo waarden vervangt door uw eigen configuratievereisten. Hallo-naam "SharePoint ACL-config" moet worden vervangen door Hallo beschrijvende naam die u toocall met deze regel wilt.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Herhaal Hallo-cmdlet, waarbij Hallo waarden vervangt door uw eigen configuratievereisten voor extra regels. Worden ervoor toochange Hallo regel nummer volgorde tooreflect Hallo volgorde waarin u Hallo regels toobe toegepast. Hallo minder regel heeft voorrang op Hallo hoger nummer.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Vervolgens kunt u een nieuw eindpunt (toevoegen) maken of Hallo ACL voor een bestaand eindpunt (Set) ingesteld. In dit voorbeeld wordt we voegen dat een nieuw eindpunt van de virtuele machine genaamd 'web' en update Hallo virtuele machine-eindpunt met de Hallo ACL-instellingen.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Vervolgens Hallo cmdlets met elkaar combineren en Hallo-script uitvoeren. In dit voorbeeld hello gecombineerde cmdlets eruit als volgt:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Verwijderen van een netwerk-ACL-regel waarmee de toegang van een extern subnet
Hallo in het volgende voorbeeld ziet u een manier tooremove een netwerk-ACL-regel.  een regel netwerk ACL met toestaan tooremove regels voor een extern subnet, open een Azure PowerShell ISE. Kopiëren en plakken onderstaande Hallo script configureren met uw eigen waarden Hallo-script en vervolgens Hallo-script uitvoeren.

1. Eerste stap is tooget Hallo netwerk ACL-object voor het eindpunt van de virtuele machine Hallo. Vervolgens verwijdert u Hallo ACL-regel. In dit geval wordt het wilt verwijderen op regel-ID. Hiermee wordt alleen Hallo regel-ID 0 uit Hallo ACL verwijderd. Hallo ACL-object wordt niet verwijderd uit het eindpunt van de virtuele machine Hallo.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. U moet vervolgens toepassen Hallo netwerk ACL-object toohello virtuele machine eindpunt en Hallo virtuele machine bijwerken.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Een netwerk-ACL verwijderen uit het eindpunt van een virtuele machine
In bepaalde gevallen, kunt u tooremove een netwerk-ACL-object van het eindpunt van een virtuele machine. toodo dat openen van een Azure PowerShell ISE. Kopiëren en plakken onderstaande Hallo script configureren met uw eigen waarden Hallo-script en vervolgens Hallo-script uitvoeren.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Volgende stappen
[Wat is een netwerk lijst ACL (Access Control)?](virtual-networks-acl.md)

