---
title: een virtuele Azure-netwerk peering - aaaCreate verschillende implementatie modellen - verschillende abonnementen | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk peering tussen virtuele netwerken gemaakt via andere Azure-implementatiemodellen die aanwezig zijn in verschillende Azure-abonnementen.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Maak een virtueel netwerk peering - verschillend implementatiemodellen en -abonnementen

In deze zelfstudie leert u toocreate een virtueel netwerk peering tussen virtuele netwerken die zijn gemaakt via verschillende implementatiemodellen. Hallo virtuele netwerken bestaan uit verschillende abonnementen. Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken toocommunicate met elkaar met dezelfde bandbreedte en latentie Hallo alsof Hallo resources in Hallo hetzelfde virtuele netwerk. Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md). 

Hallo stappen toocreate een virtueel netwerk peering zijn verschillend, afhankelijk van of Hallo virtuele netwerken in Hallo dezelfde of verschillende, abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Hallo virtuele netwerken worden gemaakt via. Meer informatie over hoe toocreate een virtueel netwerk door te klikken op Hallo scenario uit de volgende tabel Hallo-peering in andere scenario's:

|Azure-implementatiemodel  | Azure-abonnement  |
|--------- |---------|
|[Beide Resource Manager](virtual-network-create-peering.md) |Dezelfde|
|[Beide Resource Manager](create-peering-different-subscriptions.md) |Andere|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models.md) |Dezelfde|

Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via Hallo klassieke implementatiemodel. Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die bestaan in Hallo dezelfde Azure-regio. Bij het maken van een virtueel netwerk peering tussen virtuele netwerken die bestaan uit verschillende abonnementen, Hallo abonnementen beide moeten gekoppelde toohello dezelfde Azure Active Directory-tenant. Als u een Azure Active Directory-tenant nog geen hebt, kunt u snel [maken van een](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Als u moet tooconnect virtuele netwerken die zijn beide gemaakt met behulp van het klassieke implementatiemodel hello, of die zijn opgenomen in abonnementen die zijn opgenomen in verschillende Azure-regio's die zijn gekoppeld toodifferent Azure Active Directory-tenants, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hallo virtuele netwerken. 

> [!WARNING]
> Maken van een virtueel netwerk peering tussen virtuele netwerken in via andere Azure-implementatiemodellen die bestaan uit verschillende abonnementen gemaakt is momenteel in preview. Virtueel netwerk peerings gemaakt in dit scenario mogelijk geen Hallo van hetzelfde niveau van beschikbaarheid en betrouwbaarheid als voor het maken van een virtueel netwerk in het algemeen beschikbaarheid release peering in scenario's. Virtueel netwerk peerings gemaakt in dit scenario worden niet ondersteund, kunnen hebben beperkte mogelijkheden en mogelijk niet beschikbaar in alle Azure-regio's. Meest recente meldingen Hallo niet op de beschikbaarheid en de status van deze functie, Controleer Hallo [Azure Virtual Network updates](https://azure.microsoft.com/updates/?product=virtual-network) pagina.

Kunt u Hallo [Azure-portal](#portal), hello Azure [opdrachtregelinterface](#cli) (CLI) of Azure [PowerShell](#powershell) toocreate peering van een virtueel netwerk. Klik op Hallo vorige hulpprogramma koppelingen toogo direct toohello stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze.

## <a name="register"></a>Registreren voor Hallo preview

tooregister voor Hallo preview voltooid Hallo stappen volgen voor beide abonnementen die Hallo virtuele netwerken bevatten die u wilt toopeer. Hallo is alleen hulpprogramma kunt u tooregister voor Hallo preview PowerShell.

1. Installeer de meest recente versie Hallo Hallo PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Start een PowerShell-sessie en meld u met behulp van Hallo tooAzure `login-azurermaccount` opdracht.
3. Registreer uw abonnement voor Hallo preview hiertoe Hallo volgende opdrachten:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Hallo stappen in de Portal, Azure CLI of PowerShell secties Hallo van dit artikel niet voltooit tot Hallo **RegistrationState** uitvoer wordt weergegeven nadat Hallo volgende opdracht in te voeren is **geregistreerde** voor beide abonnementen:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Maken van de peering - Azure-portal

Deze zelfstudie maakt gebruik van verschillende accounts voor elk abonnement. Als u een account met machtigingen tooboth abonnementen heeft, kunt u Hallo dezelfde account voor alle stappen, Hallo stappen voor de logboekregistratie van buiten het Hallo-portal overslaan en doorgaan Hallo stappen voor het toewijzen van een andere gebruiker machtigingen toohello virtuele netwerken. Voordat u een van de volgende stappen uit Hallo, moet u registreren voor Hallo preview. tooregister, stappen voor voltooid Hallo Hallo [registreren voor preview Hallo](#register) sectie van dit artikel. Ga niet verder met de resterende stappen totdat beide abonnementen zijn geregistreerd voor de preview Hallo Hallo.
 
1. Meld u bij toohello [Azure-portal](https://portal.azure.com) als GebruikerA. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
2. Klik op **+ nieuw**, klikt u op **Networking**, klikt u vervolgens op **virtueel netwerk**.
3. In Hallo **virtueel netwerk maken** blade invoert, of Selecteer waarden voor Hallo na instellingen en klik vervolgens op **maken**:
    - **Naam**: *myVnetA*
    - **Adresruimte**: *10.0.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.0.0.0/24*
    - **Abonnement**: Selecteer abonnement A.
    - **Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroupA*
    - **Locatie**: *VS-Oost*
4. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myVnetA*. Klik op **myVnetA** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myVnetA** virtueel netwerk.
5. In Hallo **myVnetA** blade die wordt weergegeven, klikt u op **toegangsbeheer (IAM)** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo.
6. In Hallo **myVnetA - toegangsbeheer (IAM)** blade die wordt weergegeven, klikt u op **+ toevoegen**.
7. In Hallo **machtigingen toevoegen** blade die wordt weergegeven, selecteer **Network contributor** in Hallo **rol** vak.
8. In Hallo **Selecteer** selecteert gebruiker b, of typ gebruiker b van e-mailadres toosearch voor. Hallo lijst van gebruikers weergegeven is van Hallo dezelfde Azure Active Directory-tenant als het virtuele netwerk Hallo u instelt Hallo-peering voor. Wanneer deze wordt weergegeven in de lijst hello, klikt u op gebruiker b.
9. Klik op **Opslaan**.
10. Meld u af bij Hallo-portal aan als gebruiker a en meld u aan als gebruiker b.
11. Klik op **+ nieuw**, type *virtueel netwerk* in Hallo **zoeken Hallo Marketplace** vak en klik vervolgens op **virtueel netwerk** in zoekresultaten Hallo .
12. In Hallo **virtueel netwerk** blade die wordt weergegeven, selecteer **klassieke** in Hallo **een implementatiemodel selecteren** vak en klik vervolgens op **maken**.
13.   Hallo maken virtueel netwerk (klassiek) die wordt weergegeven, typ in Hallo volgende waarden:

    - **Naam**: *myVnetB*
    - **Adresruimte**: *10.1.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.1.0.0/24*
    - **Abonnement**: Selecteer abonnement B.
    - **Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroupB*
    - **Locatie**: *VS-Oost*

14. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myVnetB*. Klik op **myVnetB** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myVnetB** virtueel netwerk.
15. In Hallo **myVnetB** blade die wordt weergegeven, klikt u op **eigenschappen** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo. Kopiëren Hallo **RESOURCE-ID**, die wordt gebruikt in een latere stap. Hallo resource-ID is vergelijkbaar toohello voorbeeld te volgen: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Herhaal stap 5-9 voor myVnetB, voeren **GebruikerA** in stap 8.
17. Meld u af bij Hallo-portal aan als gebruiker b en meld u aan als gebruiker a.
18. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myVnetA*. Klik op **myVnetA** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myVnet** virtueel netwerk.
19. Klik op **myVnetA**.
20. In Hallo **myVnetA** blade die wordt weergegeven, klikt u op **Peerings** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo.
21. In Hallo **myVnetA - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**
22. In Hallo **toevoegen peering** blade die wordt weergegeven, invoeren, of selecteer Hallo volgend opties en klik vervolgens op **OK**:
     - **Naam**: *myVnetAToMyVnetB*
     - **Virtueel netwerk implementatiemodel**: Selecteer **klassieke**.
     - **Ik weet mijn resource-ID**: Schakel dit selectievakje in.
     - **De resource-ID**: Geef Hallo bron-ID van myVnetB uit stap 15.
     - **Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.
    Er zijn geen andere instellingen worden gebruikt in deze zelfstudie. toolearn over alle peering instellingen lezen [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).
23. Wanneer u op **OK** in de vorige stap Hallo Hallo **toevoegen peering** blade wordt gesloten en u ziet Hallo **myVnetA - Peerings** blade opnieuw. Na enkele seconden verschijnt Hallo peering u hebt gemaakt in Hallo-blade. **Verbonden** wordt vermeld in Hallo **PEERING STATUS** kolom voor Hallo **myVnetAToMyVnetB** peering u gemaakt. Hallo peer wordt nu ingesteld. Er is geen noodzaak toopeer Hallo virtueel netwerk (klassiek) toohello virtuele netwerk (Resource Manager).

    Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
25. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete-portal) sectie van dit artikel.

## <a name="cli"></a>Peering - maken Azure CLI

Deze zelfstudie maakt gebruik van verschillende accounts voor elk abonnement. Als u een account met machtigingen tooboth abonnementen heeft, kunt u Hallo dezelfde account voor alle stappen Hallo stappen voor logboekregistratie buiten Azure overslaan en Hallo regels script die gebruiker roltoewijzingen maakt verwijderen. Vervang UserA@azure.com en UserB@azure.com in alle Hallo scripts met Hallo gebruikersnamen die u voor GebruikerA en gebruiker b te volgen. 

Voordat u een van de volgende stappen uit Hallo, moet u registreren voor Hallo preview. tooregister, stappen voor voltooid Hallo Hallo [registreren voor preview Hallo](#register) sectie van dit artikel. Ga niet verder met de resterende stappen totdat beide abonnementen zijn geregistreerd voor de preview Hallo Hallo.

1. [Installeer](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate Hallo virtueel netwerk (klassiek).
2. Open een CLI-sessie en tooAzure aanmelden als gebruiker b met Hallo `azure login` opdracht.
3. Hallo CLI in Service Management-modus uitgevoerd door te voeren Hallo `azure config mode asm` opdracht.
4. Voer Hallo opdracht toocreate Hallo virtueel netwerk (klassiek) te volgen:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Hallo resterende stappen moet worden uitgevoerd met behulp van een bash-shell Hello Azure CLI 2.0.4 of hoger [geïnstalleerd](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), of met behulp van hello Azure Cloud-Shell. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. Klik op Hallo **Try it** knop in Hallo scripts die vervolgens een Cloud-Shell waarmee u zich in tooyour Azure-account aanmeldt te openen. Zie voor opties op die wordt uitgevoerd bash-scripts CLI op een Windows-client, [hello Azure CLI uitvoeren in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Kopieer Hallo script tooa teksteditor op uw PC te volgen. Vervang `<SubscriptionB-Id>` met uw abonnement-ID. Als u uw abonnements-Id niet weet, voert u Hallo `az account show` opdracht. waarde voor Hallo **id** in Hallo uitvoer is de abonnement-id. Hallo aangepast script kopiëren, plak deze in tooyour CLI 2.0-sessie en druk vervolgens op `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Wanneer u Hallo virtueel netwerk (klassiek) in stap 4 hebt gemaakt, Azure Hallo virtueel netwerk gemaakt in Hallo *standaard netwerken* resourcegroep.
7. Aanmelden gebruiker b buiten Azure en zich aanmelden als gebruiker a Hallo CLI 2.0.
8. Maak een resourcegroep en een virtueel netwerk (Resource Manager). Kopiëren Hallo volgende script, plak deze in tooyour CLI-sessie en druk vervolgens op `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Maak een virtueel netwerk peering tussen Hallo twee virtuele netwerken via Hallo verschillende implementatiemodellen is gemaakt. Kopieer Hallo script tooa teksteditor op uw PC te volgen. Vervang `<SubscriptionB-id>` met uw abonnements-id. Als u uw abonnements-Id niet weet, voert u Hallo `az account show` opdracht. waarde voor Hallo **id** in Hallo uitvoer is de abonnement-id. Azure gemaakt Hallo virtueel netwerk (klassiek u hebt gemaakt in stap 4 in een resourcegroep met de naam) *standaard netwerken*. Hallo gewijzigd script plakken in uw CLI-sessie en druk vervolgens op `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Nadat het Hallo-script wordt uitgevoerd, moet u controleren Hallo-peering voor Hallo virtueel netwerk (Resource Manager). Hallo script volgen Kopieer en plak deze in de CLI-sessie:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    Hallo uitvoer toont **verbonden** in Hallo **PeeringState** kolom.

    Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
12. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-cli) in dit artikel.

## <a name="powershell"></a>Maken van de peering - PowerShell

Deze zelfstudie maakt gebruik van verschillende accounts voor elk abonnement. Als u een account met machtigingen tooboth abonnementen heeft, kunt u Hallo dezelfde account voor alle stappen Hallo stappen voor logboekregistratie buiten Azure overslaan en Hallo regels script die gebruiker roltoewijzingen maakt verwijderen. Vervang UserA@azure.com en UserB@azure.com in alle Hallo scripts met Hallo gebruikersnamen die u voor GebruikerA en gebruiker b te volgen. 

Voordat u een van de volgende stappen uit Hallo, moet u registreren voor Hallo preview. tooregister, stappen voor voltooid Hallo Hallo [registreren voor preview Hallo](#register) sectie van dit artikel. Ga niet verder met de resterende stappen totdat beide abonnementen zijn geregistreerd voor de preview Hallo Hallo.

1. Installeer de meest recente versie Hallo Hallo PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) en [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Een PowerShell-sessie starten.
3. In PowerShell aanmelden tooUserB van abonnement als gebruiker b door te voeren Hallo `Add-AzureAccount` opdracht.
4. toocreate een virtueel netwerk (klassiek) met PowerShell, moet u maken een nieuwe, of wijzig een bestaande netwerk configuratiebestand. Meer informatie over hoe te[exporteren, bijwerken en importeren van configuratie van netwerkbestanden](virtual-networks-using-network-configuration-file.md). Hallo bestand moet bevatten de volgende Hallo **VirtualNetworkSite** element voor Hallo virtueel netwerk in deze zelfstudie gebruikt:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen tooexisting virtuele netwerken (klassiek) in uw abonnement. Zorg ervoor dat u alleen Hallo vorige virtueel netwerk toevoegen en u niet wijzigen of verwijderen van een bestaande virtuele netwerken uit uw abonnement. 

5. Meld u bij tooUserB van abonnement als gebruiker b toouse Resource Manager-opdrachten door te voeren Hallo `login-azurermaccount` opdracht.
6. Toewijzen GebruikerA machtigingen toovirtual netwerk B. kopie Hallo volgende script tooa teksteditor op uw PC en vervang `<SubscriptionB-id>` met Hallo-ID van het abonnement B. Als u Hallo abonnements-Id niet weet, voert u Hallo `Get-AzureRmSubscription` opdracht tooview deze. waarde voor Hallo **Id** in Hallo geretourneerd uitvoer is uw abonnements-ID. Azure gemaakt Hallo virtueel netwerk (klassiek u hebt gemaakt in stap 4 in een resourcegroep met de naam) *standaard netwerken*. tooexecute hello script kopiëren Hallo gewijzigd script, plak deze in tooPowerShell en druk vervolgens op `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Meld u af bij Azure als gebruiker b en meld u in de tooUserA abonnement als GebruikerA hiertoe Hallo `login-azurermaccount` opdracht. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
8. Hallo virtueel netwerk (Resource Manager) maken van het script, plakken in tooPowerShell en drukt u vervolgens op volgende Hallo kopiëren `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Verleent machtigingen toomyVnetA toewijzen. Kopiëren Hallo volgende script tooa teksteditor op uw PC en vervang `<SubscriptionA-Id>` met Hallo-ID van het abonnement A. Als u Hallo abonnements-Id niet weet, voert u Hallo `Get-AzureRmSubscription` opdracht tooview deze. waarde voor Hallo **Id** in Hallo geretourneerd uitvoer is uw abonnements-ID. Hallo gewijzigde versie van script Hallo plakken in PowerShell en druk vervolgens op `Enter` tooexecute deze.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Kopiëren Hallo volgende script tooa teksteditor op uw PC en vervang `<SubscriptionB-id>` met de ID van het abonnement B. toopeer myVnetA toomyVNetB Hallo Hallo gewijzigd script kopiëren, plak deze in tooPowerShell en druk vervolgens op `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Weergavestatus Hallo peering van myVnetA kopiëren Hallo script plakken in PowerShell en zwaarwegende na `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hallo-status is **verbonden**. Deze wijzigingen te**verbonden** zodra u de peering toomyVnetA Hallo van myVnetB instellen.

    Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
13. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-powershell) in dit artikel.

## <a name="permissions"></a>Machtigingen

Hallo-accounts gebruiken van een virtueel netwerk peering toocreate beschikken Hallo benodigde rol of machtigingen. Bijvoorbeeld, als u twee virtuele netwerken met de naam myVnetA en myVnetB zijn peering, moet uw account worden toegewezen Hallo minimale rol of machtiging voor elke virtuele netwerk te volgen:
    
|Virtueel netwerk|Implementatiemodel|Rol|Machtigingen|
|---|---|---|---|
|myVnetA|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N.v.t.|
|myVnetB|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen te[aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="delete"></a>Resources verwijderen
Wanneer u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt in de zelfstudie hello, zodat u geen gebruik kosten. Verwijderen van een resourcegroep, worden ook alle resources die in de resourcegroep Hallo verwijderd.

### <a name="delete-portal"></a>Azure-portal

1. Voer in de portal zoekvak Hallo **myResourceGroupA**. Klik in de zoekresultaten Hallo **myResourceGroupA**.
2. Op Hallo **myResourceGroupA** blade, klikt u op Hallo **verwijderen** pictogram.
3. tooconfirm hello wordt verwijderd, Hallo **TYPE Hallo RESOURCEGROEPNAAM** Voer **myResourceGroupA**, en klik vervolgens op **verwijderen**.
4. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myVnetB*. Klik op **myVnetB** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myVnetB** virtueel netwerk.
5. In Hallo **myVnetB** blade, klikt u op **verwijderen**.
6. tooconfirm hello verwijdering, klikt u op **Ja** in Hallo **virtuele netwerk verwijderen** vak.

### <a name="delete-cli"></a>Azure CLI

1. Meld u bij tooAzure Hallo met CLI 2.0 toodelete Hallo virtueel netwerk (Resource Manager) Hello volgende opdracht:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Meld u bij tooAzure Hallo met Azure CLI 1.0 toodelete Hallo virtueel netwerk (klassiek) Hello volgende opdrachten:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Voer op Hallo PowerShell-opdrachtprompt Hallo opdracht toodelete Hallo virtueel netwerk (Resource Manager) te volgen:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello virtueel netwerk (klassiek) met PowerShell, moet u een bestaand bestand van de netwerk-configuratie wijzigen. Meer informatie over hoe te[exporteren, bijwerken en importeren van configuratie van netwerkbestanden](virtual-networks-using-network-configuration-file.md). Verwijder Hallo VirtualNetworkSite element voor Hallo virtuele netwerk dat wordt gebruikt in deze zelfstudie te volgen:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Een configuratiebestand gewijzigde netwerk importeren kan leiden tot wijzigingen tooexisting virtuele netwerken (klassiek) in uw abonnement. Zorg ervoor dat u alleen Hallo vorige virtuele netwerk verwijderen en u niet wijzigen of andere bestaande virtuele netwerken uit uw abonnement verwijderen. 

## <a name="next-steps"></a>Volgende stappen

- Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.
- Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).
- Meer informatie over hoe te[maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.
