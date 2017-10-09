---
title: aaaManage Azure gereserveerde IP-adressen (klassiek) - PowerShell | Microsoft Docs
description: Gereserveerde IP-adressen (klassiek) te begrijpen en hoe toomanage ze met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a>Gereserveerde IP-adressen (klassiek)

> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-static-pip-arm-cli.md)
> * [Sjabloon](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (klassiek)](virtual-networks-reserved-public-ip.md)

IP-adressen in Azure worden onderverdeeld in twee categorieën: dynamische en gereserveerd. Openbare IP-adressen die worden beheerd door Azure worden standaard dynamisch. Dat betekent dat Hallo IP-adres voor een bepaalde cloud-service (VIP) of tooaccess een virtuele machine gebruikt of rechtstreeks rolinstantie (ILPIP) van tijd tootime, wijzigen kunt wanneer resources worden afgesloten of gestopt (toewijzing ongedaan gemaakt).

tooprevent IP-adressen kunnen wijzigen, kunt u een IP-adres reserveren. Gereserveerd IP-adressen kan alleen worden gebruikt als een VIP, waarbij u ervoor zorgt dat Hallo IP-adres voor de cloudservice Hallo blijft Hallo dezelfde zijn, zelfs als bronnen worden afgesloten of gestopt (toewijzing ongedaan gemaakt). Bovendien kunt u als een VIP tooa gereserveerd IP-adres gebruikt bestaande dynamische IP-adressen converteren.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe een statische openbare IP-adres met tooreserve Hallo [Resource Manager-implementatiemodel](virtual-network-ip-addresses-overview-arm.md).

toolearn meer over IP-adressen in Azure, Hallo lezen [IP-adressen](virtual-network-ip-addresses-overview-classic.md) artikel.

## <a name="when-do-i-need-a-reserved-ip"></a>Wanneer moet ik een gereserveerde IP-adres?
* **U wilt dat tooensure die Hallo IP is gereserveerd in uw abonnement**. Als u wilt dat een IP-adres dat wordt niet vrijgegeven tooreserve uit uw abonnement onder enkel beding, moet u een gereserveerde openbare IP-adres gebruiken.  
* **U wilt dat uw IP-toostay met uw cloudservice zelfs meerdere gestopt of toewijzing opgeheven status (VM's)**. Als u wilt dat uw service toobe toegankelijk via een IP-adres dat niet verandert, zelfs wanneer virtuele machines in Hallo cloud-service worden afgesloten of gestopt (toewijzing ongedaan gemaakt).
* **U wilt dat uitgaand verkeer vanuit Azure gebruikmaakt van een voorspelbare IP-adres tooensure**. Mogelijk hebt u uw lokale geconfigureerde firewall tooallow alleen het verkeer van specifieke IP-adressen. Door een IP-adres reserveren, weet u Hallo bron-IP adres en hoeft niet tooupdate uw firewallregels vanwege tooan IP-wijzigen.

## <a name="faq"></a>Veelgestelde vragen
1. Kan ik een gereserveerde IP-adres gebruiken voor alle Azure-services? <br>
    Nee. Gereserveerd IP-adressen kan alleen worden gebruikt voor virtuele machines en cloud service-exemplaar rollen weergegeven via een VIP-adres.
2. Het aantal gereserveerde IP's kan ik hebben? <br>
    Zie voor meer informatie, Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.
3. Is er kosten met zich mee voor gereserveerde IP's? <br>
    Soms. Zie voor prijsinformatie, Hallo [gereserveerde IP-adres prijsinformatie](http://go.microsoft.com/fwlink/?LinkID=398482) pagina.
4. Hoe ik een IP-adres reserveren? <br>
    U kunt PowerShell gebruiken, hello [Management REST API van Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), of Hallo [Azure-portal](https://portal.azure.com) tooreserve een IP-adres in een Azure-regio. Een gereserveerd IP-adres is gekoppeld tooyour abonnement.
5. Kan ik een gereserveerde IP-adres gebruiken met VNets op basis van een affiniteitsgroep <br>
    Nee. Gereserveerd IP-adressen worden alleen ondersteund in regionaal vnet's. Gereserveerd IP-adressen worden niet ondersteund voor VNets die zijn gekoppeld aan affiniteitsgroepen. Zie voor meer informatie over het koppelen van een VNet met een regio of affiniteitsgroep hello [over regionaal vnet's en Affiniteitsgroepen](virtual-networks-migrate-to-regional-vnet.md) artikel.

## <a name="manage-reserved-vips"></a>Gereserveerde VIP's beheren

Zorg ervoor dat u hebt geïnstalleerd en geconfigureerd PowerShell via Hallo stappen in Hallo [installeren en configureren van PowerShell](/powershell/azure/overview) artikel. 

Voordat u gereserveerde IP's gebruiken kunt, moet u deze tooyour abonnement toevoegen. toocreate een gereserveerde IP-adres van de groep Hallo met openbare IP-adressen beschikbaar zijn in Hallo *VS-midden* locatie, Hallo volgende opdracht uitvoeren:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

U ziet, echter, u niet opgeven wat IP wordt gereserveerd. tooview welke IP-adressen zijn gereserveerd in uw abonnement, Hallo volgende PowerShell-opdracht uitvoeren en Let op Hallo waarden voor *ReservedIPName* en *adres*:

```powershell
Get-AzureReservedIP
```

Verwachte uitvoer:

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
>Wanneer u een gereserveerd IP-adres met PowerShell maakt, kunt u een resource groep toocreate Hallo gereserveerd IP-adres in niet opgeven. Azure plaatsen in een resourcegroep met de naam *standaard netwerken* automatisch. Als u Hallo gereserveerd IP met Hallo maakt [Azure-portal](http://portal.azure.com), kunt u een resourcegroep die u kiest. Als u Hallo gereserveerd IP anders dan in een resourcegroep maken *standaard netwerken* echter, wanneer u verwijst naar Hallo gereserveerde IP-adres met opdrachten zoals `Get-AzureReservedIP` en `Remove-AzureReservedIP`, moet u verwijzen naar Hallo naam *Resourcegroepnaam gereserveerd-ip-naam van de groep*.  Bijvoorbeeld, als u een gereserveerde IP-adres met de naam *myReservedIP* in een resourcegroep met de naam *myResourceGroup*, u moet verwijzen naar de naam van Hallo gereserveerd IP-adres als Hallo *groep myResourceGroup myReservedIP*.   

Nadat een IP-adres is gereserveerd, blijft deze gekoppelde tooyour abonnement totdat u het verwijdert. toodelete een gereserveerde IP-adres, Voer Hallo volgende PowerShell-opdracht:

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a>Reserveer Hallo IP-adres van een bestaande cloudservice
U kunt Hallo IP-adres van een bestaande cloudservice reserveren door toe te voegen Hallo `-ServiceName` parameter. tooreserve hello IP-adres van een cloudservice *TestService* in Hallo *VS-midden* locatie, Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a>Koppelen van een gereserveerd IP-tooa nieuwe cloudservice
Hallo volgende script maakt een nieuw gereserveerd IP-adres en vervolgens koppelt u deze tooa nieuwe cloudservice met de naam *TestService*.

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> Wanneer u een gereserveerd IP-toouse met een cloudservice maakt, u nog steeds toohello VM verwijzen met behulp van *VIP:&lt;poortnummer >* voor binnenkomende communicatie. Een IP-adres reserveren betekent niet dat toohello virtuele machine rechtstreeks kan worden aangesloten. Hallo gereserveerde IP-adres is toegewezen toohello cloud service die Hallo VM is geïmplementeerd op. Als u rechtstreeks tooconnect tooa VM door IP wilt, hebt u tooconfigure een openbaar IP op exemplaarniveau. Een openbaar IP op exemplaarniveau is een openbaar IP-adres (een ILPIP genoemd) die rechtstreeks tooyour VM is toegewezen. Deze kan niet worden gereserveerd. Lees voor meer informatie, Hallo [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) artikel.
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a>Een gereserveerd IP-adres van een actieve implementatie verwijderen
tooremove een gereserveerde IP-adres toegevoegd tooa nieuwe cloudservice Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> Een gereserveerd IP-adres worden van een actieve implementatie niet verwijderd Hallo reservering uit uw abonnement. Het wordt gewoon vrijgemaakt Hallo IP-toobe gebruikt door een andere resource in uw abonnement.
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a>Koppelen van een gereserveerd IP-tooa waarop implementatie wordt uitgevoerd
Hallo volgende opdrachten een cloudservice maken met de naam *TestService2* met een nieuwe virtuele machine met de naam *TestVM2*. Hallo bestaande gereserveerde IP-adres met de naam *MyReservedIP* zich bevindt, wordt het bijbehorende toohello cloudservice.

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a>Een gereserveerd IP-tooa cloudservice koppelen via een configuratiebestand voor de service
U kunt ook een gereserveerd IP-tooa cloudservice koppelen met behulp van een service-configuratiebestand (CSCFG). Hallo volgende XML-code voorbeeld ziet u hoe tooconfigure een cloud service toouse een gereserveerd VIP-adres met de naam *MyReservedIP*:

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a>Volgende stappen
* Begrijpen hoe [IP-adressering](virtual-network-ip-addresses-overview-classic.md) werkt in het klassieke implementatiemodel Hallo.
* Meer informatie over [privé IP-adressen gereserveerd](virtual-networks-reserved-private-ip.md).
* Meer informatie over [Instance Level Public IP (ILPIP) adressen](virtual-networks-instance-level-public-ip.md).

