---
title: "aaaConfigure altijd op beschikbaarheid Beschikbaarheidsgroeplisteners – Microsoft Azure | Microsoft Docs"
description: Beschikbaarheid van groep Listeners hello Azure Resource Manager-model, met behulp van een interne load balancer met een of meer IP-adressen configureren.
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Een of meer altijd op beschikbaarheid beschikbaarheidsgroeplisteners - Resource Manager configureren
Dit onderwerp wordt beschreven hoe:

* Maak een interne load balancer voor SQL Server-beschikbaarheidsgroepen met PowerShell-cmdlets.
* Extra IP-adressen tooa load balancer voor meer dan één beschikbaarheidsgroep toevoegen. 

Een beschikbaarheidsgroep-listener is de naam van een virtueel netwerk dat clients verbinding toofor toegang tot de database maken. Op virtuele machines in Azure bevat een load balancer Hallo IP-adres voor het Hallo-listener. Hallo load balancer routes verkeer toohello exemplaar van SQL Server die op Hallo testpoort luistert. Een beschikbaarheidsgroep maakt meestal gebruik van een interne load balancer. Een Azure interne load balancer kan één of meerdere IP-adressen te hosten. Elk IP-adres gebruikt een specifieke testpoort. Dit document beschrijft hoe toouse PowerShell toocreate een load balancer, of Voeg de IP-adressen tooan bestaande load balancer voor SQL Server-beschikbaarheidsgroepen. 

Hallo mogelijkheid tooassign meerdere IP-adressen tooan interne load balancer is nieuwe tooAzure en is alleen beschikbaar in het Resource Manager-model. toocomplete deze taak moet u een SQL Server-beschikbaarheidsgroep is geïmplementeerd op Azure virtuele machines in de Resource Manager-model toohave. Beide virtuele machines van SQL Server moet behoren toohello dezelfde beschikbaarheidsset. U kunt Hallo [Microsoft sjabloon](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Hallo-beschikbaarheidsgroep maken in Azure Resource Manager. Deze sjabloon wordt automatisch de beschikbaarheidsgroep hello, inclusief Hallo interne load balancer voor u gemaakt. Als u liever, kunt u [handmatig configureren van een AlwaysOn-beschikbaarheidsgroep](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

In dit onderwerp is vereist dat uw beschikbaarheidsgroepen al zijn geconfigureerd.  

Verwante onderwerpen zijn:

* [AlwaysOn-beschikbaarheidsgroepen configureren in Azure virtuele machine (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Een VNet-naar-VNet-verbinding configureren met behulp van Azure Resource Manager en PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Hallo Windows Firewall configureren
Hallo Windows Firewall tooallow SQL Server-toegang configureren. Hallo-firewallregels toestaan TCP-verbindingen toohello poorten gebruiken door Hallo SQL Server-exemplaar en Hallo-listener-test. Zie voor gedetailleerde instructies [Windows Firewall configureren voor toegang tot de Database-Engine](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Een inkomende regel voor Hallo SQL Server-poort en de testpoort Hallo maken.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Voorbeeldscript: Een interne load balancer maken met PowerShell
> [!NOTE]
> Als u de beschikbaarheidsgroep hebt gemaakt met de Hallo [Microsoft sjabloon](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), Hallo interne load balancer al is gemaakt. 
> 
> 

Hallo volgende PowerShell-script maakt een interne load balancer, configureert u regels voor taakverdeling hello, en stelt een IP-adres voor Hallo load balancer. toorun hello script, opent u Windows PowerShell ISE en Hallo script in het scriptvenster hello te plakken. Gebruik `Login-AzureRMAccount` toolog in tooPowerShell. Als u meerdere Azure-abonnementen hebt, gebruikt u `Select-AzureRmSubscription ` tooset Hallo abonnement. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a>Voorbeeldscript: een IP-adres tooan bestaande load balancer toevoegen met PowerShell
Voeg een extra IP-adres toohello load balancer toouse meer dan één beschikbaarheidsgroep. Elk IP-adres vereist een eigen taakverdeling regel, testpoort en front-poort.

Hallo front-endpoort is Hallo-poort dat toepassingen tooconnect toohello SQL Server-exemplaar gebruiken. IP-adressen voor verschillende beschikbaarheid groepen kunnen gebruiken dezelfde front-endpoort Hallo.

> [!NOTE]
> Elk IP-adres vereist voor beschikbaarheidsgroepen van SQL Server, een specifieke testpoort. Als u één IP-adres voor een load balancer testpoort 59999 gebruikt, kunnen geen andere IP-adressen op die load balancer testpoort 59999 gebruiken.

* Zie voor meer informatie over de load balancer limieten **persoonlijke front-end-IP per load balancer** onder [Networking limieten - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Zie voor meer informatie over de beschikbaarheid van groep limieten [beperkingen (beschikbaarheidsgroepen)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Hallo voegt volgende script een nieuwe IP-adres tooan bestaande load balancer. Hallo ILB gebruikt Hallo-listener-poort voor Hallo-front-endpoort voor taakverdeling. Deze poort kan worden Hallo-poort die SQL Server luistert. Hallo-poort is voor standaardexemplaren van SQL Server is 1433. taakverdelingsregel voor een beschikbaarheidsgroep Hallo vereist een zwevend IP (direct server return) zodat Hallo back-endpoort Hallo dezelfde als de front-endpoort Hallo. Hallo variabelen voor uw omgeving bijwerken. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a>Hallo-listener configureren

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>Hallo-listener-poort ingesteld in SQL Server Management Studio

1. Start SQL Server Management Studio en maak verbinding toohello primaire replica.

1. Navigeer te**AlwaysOn hoge beschikbaarheid** | **beschikbaarheidsgroepen** | **beschikbaarheid Beschikbaarheidsgroeplisteners**. 

1. U ziet nu Hallo-listener-naam die u hebt gemaakt in Failoverclusterbeheer. Met de rechtermuisknop op de naam van de beschikbaarheidsgroeplistener hello en klik op **eigenschappen**.

1. In Hallo **poort** Geef Hallo-poortnummer voor Hallo beschikbaarheidsgroep-listener met behulp van Hallo $EndpointPort u eerder hebt gebruikt (1433 was Hallo standaard), klikt u vervolgens op **OK**.

## <a name="test-hello-connection-toohello-listener"></a>Test Hallo verbinding toohello listener

tootest hello verbinding:

1. RDP-tooa SQL-Server die zich in Hallo hetzelfde virtuele netwerk, maar niet eigen Hallo replica. Dit kan Hallo andere SQL-Server in het Hallo-cluster.

1. Gebruik **sqlcmd** hulpprogramma tootest Hallo verbinding. Bijvoorbeeld Hallo script volgen stelt een **sqlcmd** verbinding toohello primaire replica via het Hallo-listener met de Windows-verificatie:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Als het Hallo-listener poort wordt gebruikt door een andere waarde dan Hallo standaard poort (1433), Hallo-poort in de verbindingsreeks Hallo opgeven. Bijvoorbeeld: hello volgende sqlcmd-opdracht verbindt tooa listener op poort 1435: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hallo SQLCMD-verbinding verbinding automatisch toowhichever exemplaar van SQL Server-hosts Hallo primaire replica. 

> [!NOTE]
> Zorg ervoor dat Hallo poort die u opgeeft geopend op Hallo firewall beide SQL-servers is. Beide servers vereisen een inkomende regel voor Hallo TCP-poort die u gebruikt. Zie [toevoegen of bewerken firewallregel](http://technet.microsoft.com/library/cc753558.aspx) voor meer informatie. 
> 
> 

## <a name="guidelines-and-limitations"></a>Richtlijnen en beperkingen
Houd er rekening mee Hallo richtlijnen op beschikbaarheidsgroep-listener in Azure met behulp van de interne load balancer:

* Met een interne load balancer u alleen toegang tot Hallo-listener van Hallo hetzelfde virtuele netwerk.


## <a name="for-more-information"></a>Voor meer informatie
Zie voor meer informatie [configureren altijd op de beschikbaarheidsgroep in Azure VM handmatig](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>PowerShell-cmdlets
Hallo volgende PowerShell-cmdlets toocreate een interne load balancer voor virtuele machines in Azure gebruiken.

* [Nieuwe AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) maakt u een load balancer. 
* [Nieuwe AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) maakt een front-end-IP-configuratie voor een load balancer. 
* [Nieuwe AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) maakt u de regelconfiguratie van een voor een load balancer. 
* [Nieuwe AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) maakt een back-end-pool-adresconfiguratie voor een load balancer. 
* [Nieuwe AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) maakt u een test-configuratie voor een load balancer.
* [Verwijder AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) Hiermee verwijdert u een load balancer van een Azure-resourcegroep.
