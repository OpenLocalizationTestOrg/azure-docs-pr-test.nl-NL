---
title: aaaCreate een virtuele Azure - Resource Manager - peering verschillende abonnementen netwerk | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk peering tussen virtuele netwerken gemaakt via de Resource-Manager die aanwezig zijn in verschillende Azure-abonnementen.
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Maak een virtueel netwerk peering - Resource Manager worden verschillende abonnementen 

In deze zelfstudie leert u toocreate een virtueel netwerk tussen virtuele netwerken die zijn gemaakt via Resource Manager-peering. Hallo virtuele netwerken bestaan uit verschillende abonnementen. Peering twee virtuele netwerken kunnen resources in verschillende virtuele netwerken toocommunicate met elkaar met dezelfde bandbreedte en latentie Hallo alsof Hallo resources in Hallo hetzelfde virtuele netwerk. Meer informatie over [virtuele netwerk peering](virtual-network-peering-overview.md). 

Hallo stappen toocreate een virtueel netwerk peering zijn verschillend, afhankelijk van of Hallo virtuele netwerken in Hallo dezelfde of verschillende, abonnementen en die zijn [Azure implementatiemodel](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Hallo virtuele netwerken worden gemaakt via. Meer informatie over hoe toocreate een virtueel netwerk door te klikken op Hallo scenario uit de volgende tabel Hallo-peering in andere scenario's:

|Azure-implementatiemodel  | Azure-abonnement  |
|--------- |---------|
|[Beide Resource Manager](virtual-network-create-peering.md) |Dezelfde|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models.md) |Dezelfde|
|[Een Resource Manager, een klassiek](create-peering-different-deployment-models-subscriptions.md) |Andere|

Een virtueel netwerk peering kan niet worden gemaakt tussen twee virtuele netwerken die zijn geïmplementeerd via Hallo klassieke implementatiemodel. Een virtueel netwerk peering kan alleen worden gemaakt tussen twee virtuele netwerken die bestaan in Hallo dezelfde Azure-regio. Bij het maken van een virtueel netwerk peering tussen virtuele netwerken die bestaan uit verschillende abonnementen, Hallo abonnementen beide moeten gekoppelde toohello dezelfde Azure Active Directory-tenant. Als u een Azure Active Directory-tenant nog geen hebt, kunt u snel [maken van een](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Als u moet tooconnect virtuele netwerken die zijn beide gemaakt met behulp van het klassieke implementatiemodel hello, of die zijn opgenomen in abonnementen die zijn opgenomen in verschillende Azure-regio's die zijn gekoppeld toodifferent Azure Active Directory-tenants, kunt u een Azure [VPN-Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hallo virtuele netwerken. 

Kunt u Hallo [Azure-portal](#portal), hello Azure [opdrachtregelinterface](#cli) (CLI) of Azure [PowerShell](#powershell) toocreate peering van een virtueel netwerk. Klik op Hallo vorige hulpprogramma koppelingen toogo direct toohello stappen voor het maken van een virtueel netwerk peering met behulp van het hulpprogramma naar keuze.

## <a name="portal"></a>Maken van de peering - Azure-portal

Deze zelfstudie maakt gebruik van verschillende accounts voor elk abonnement. Als u een account met machtigingen tooboth abonnementen heeft, kunt u Hallo dezelfde account voor alle stappen, Hallo stappen voor de logboekregistratie van buiten het Hallo-portal overslaan en doorgaan Hallo stappen voor het toewijzen van een andere gebruiker machtigingen toohello virtuele netwerken.

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
8. In Hallo **Selecteer** vak, selecteert u een gebruiker b of gebruiker b van e-mailadres toosearch voor het type. Hallo lijst van gebruikers weergegeven is van Hallo dezelfde Azure Active Directory-tenant als het virtuele netwerk Hallo u instelt Hallo-peering voor.
9. Klik op **Opslaan**.
10. In Hallo **myVnetA - toegangsbeheer (IAM)** blade, klikt u op **eigenschappen** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo. Kopiëren Hallo **RESOURCE-ID**, die wordt gebruikt in een latere stap. Hallo resource-ID is vergelijkbaar toohello voorbeeld te volgen: /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Meld u af bij Hallo-portal aan als gebruiker a en meld u aan als gebruiker b.
12. Volg de stappen 2-3, invoeren of selecteren Hallo volgende waarden in stap 3:

    - **Naam**: *myVnetB*
    - **Adresruimte**: *10.1.0.0/16*
    - **Subnetnaam**: *standaard*
    - **Subnet-adresbereik**: *10.1.0.0/24*
    - **Abonnement**: Selecteer abonnement B.
    - **Resourcegroep**: Selecteer **nieuw** en voer *myResourceGroupB*
    - **Locatie**: *VS-Oost*

13. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myVnetB*. Klik op **myVnetB** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myVnetB** virtueel netwerk.
14. In Hallo **myVnetB** blade die wordt weergegeven, klikt u op **eigenschappen** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo. Kopiëren Hallo **RESOURCE-ID**, die wordt gebruikt in een latere stap. Hallo resource-ID is vergelijkbaar toohello voorbeeld te volgen: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Klik op **toegangsbeheer (IAM)** in Hallo **myVnetB** blade en vervolgens voltooit stappen 5 tot 10 voor myVnetB, voeren **GebruikerA** in stap 8.
16. Meld u af bij Hallo-portal aan als gebruiker b en meld u aan als gebruiker a.
17. In Hallo **zoeken bronnen** vak Hallo boven aan het Hallo-portal, type *myVnetA*. Klik op **myVnetA** wanneer deze wordt weergegeven in zoekresultaten Hallo. Een blade wordt weergegeven voor Hallo **myVnet** virtueel netwerk.
18. Klik op **myVnetA**.
19. In Hallo **myVnetA** blade die wordt weergegeven, klikt u op **Peerings** uit Hallo verticale lijst met opties op de linkerkant van de blade Hallo Hallo.
20. In Hallo **myVnetA - Peerings** blade die werden weergegeven, klikt u op **+ toevoegen**
21. In Hallo **toevoegen peering** blade die wordt weergegeven, invoeren, of selecteer Hallo volgend opties en klik vervolgens op **OK**:
     - **Naam**: *myVnetAToMyVnetB*
     - **Virtueel netwerk implementatiemodel**: Selecteer **Resource Manager**.
     - **Ik weet mijn resource-ID**: Schakel dit selectievakje in.
     - **De resource-ID**: Geef Hallo resource-ID uit stap 14.
     - **Toestaan van toegang tot het virtuele netwerk:** ervoor te zorgen dat **ingeschakeld** is geselecteerd.
    Er zijn geen andere instellingen worden gebruikt in deze zelfstudie. toolearn over alle peering instellingen lezen [beheren van virtueel netwerk peerings](virtual-network-manage-peering.md#create-a-peering).
22. Wanneer u op **OK** in de vorige stap Hallo Hallo **toevoegen peering** blade wordt gesloten en u ziet Hallo **myVnetA - Peerings** blade opnieuw. Na enkele seconden verschijnt Hallo peering u hebt gemaakt in Hallo-blade. **Geïnitieerd** wordt vermeld in Hallo **PEERING STATUS** kolom voor Hallo **myVnetAToMyVnetB** peering u gemaakt. U hebt ingesteld als peer myVnetA toomyVnetB, maar u moet nu myVnetB toomyVnetA peer. Hallo peering moet worden gemaakt in beide richtingen tooenable bronnen in Hallo virtuele netwerken toocommunicate met elkaar.
23. Meld u af bij Hallo-portal aan als gebruiker a en aanmelden als gebruiker b.
24. Herhaal stap 17-21 opnieuw voor myVnetB. In stap 21 naam Hallo peering *myVnetBToMyVnetA*, selecteer *myVnetA* voor **virtueel netwerk**, en Voer Hallo ID vanaf stap 10 van Hallo **-bron-ID** vak.
25. Een paar seconden na het klikken op **OK** toocreate Hallo-peering voor myVnetB, hello **myVnetBToMyVnetA** peering u zojuist hebt gemaakt wordt vermeld met **verbonden** in Hallo  **STATUS van de PEERING** kolom.
26. Meld u af bij Hallo-portal aan als gebruiker b en meld u aan als gebruiker a.
27. Voltooi stap 17-19 opnieuw. Hallo **PEERING STATUS** voor Hallo **myVnetAToVNetB** peering is nu er ook **verbonden**. Hallo-peering is tot stand gebracht nadat er **verbonden** in Hallo **PEERING STATUS** kolom voor beide virtuele netwerken in het Hallo-peering. Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
29. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, stappen voor voltooid Hallo Hallo [resources verwijderen](#delete-portal) sectie van dit artikel.

## <a name="cli"></a>Peering - maken Azure CLI

Deze zelfstudie maakt gebruik van verschillende accounts voor elk abonnement. Als u een account met machtigingen tooboth abonnementen heeft, kunt u Hallo dezelfde account voor alle stappen Hallo stappen voor logboekregistratie buiten Azure overslaan en Hallo regels script die gebruiker roltoewijzingen maakt verwijderen. Vervang UserA@azure.com en UserB@azure.com in alle Hallo scripts met Hallo gebruikersnamen die u voor GebruikerA en gebruiker b te volgen.

Hallo script volgen:

- Hello Azure CLI versie 2.0.4 vereist of hoger. toofind hello versie, voer `az --version`. Als u tooupgrade moet, Zie [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Werkt in een Bash-shell. Zie voor opties op Azure CLI-scripts die worden uitgevoerd op Windows-client [hello Azure CLI uitvoeren in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

U kunt in plaats van installatie Hallo CLI en de bijbehorende afhankelijkheden, hello Azure Cloud Shell gebruiken. Hello Azure Cloud Shell is een gratis Bash-shell die u rechtstreeks vanuit hello Azure-portal kunt uitvoeren. Hello Azure CLI vooraf is geïnstalleerd en geconfigureerd toouse met uw account heeft. Klik op Hallo **Try it** knop in Hallo script dat volgt, die een Cloud-Shell die u tooyour Azure-account met aanmelden kunt aanroept. 

1. Open een CLI-sessie en tooAzure aanmelden als gebruiker a middels Hallo `azure login` opdracht. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
2. Kopieer Hallo script tooa teksteditor op uw PC te volgen, Vervang `<SubscriptionA-Id>` met Hallo-ID van SubscriptionA, gewijzigd kopie Hallo vervolgens script, plak deze in de CLI-sessie en druk op `Enter`. Als u uw abonnements-Id niet weet, voert u Hallo 'az account weergeven'-opdracht. waarde voor Hallo **id** in Hallo uitvoer is de abonnement-id.

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     Hallo machtigingen worden toegewezen voor gebruiker b is geen vereiste. Peering kan worden vastgesteld zelfs als gebruikers afzonderlijk peering aanvragen voor hun respectieve virtuele netwerken verhogen, zolang Hallo overeenkomst aanvraagt. Een bevoegde gebruiker van myVNetB als medewerker netwerk in Hallo lokale virtuele netwerk toe te voegen, maakt het eenvoudiger toodo Hallo instellen.
3. Meld u af bij Azure als gebruiker a middels Hallo `az logout` en klik tooAzure als gebruiker b aanmelden. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
4. MyVnetB maken. Kopieer de inhoud van het script Hallo in stap 2 tooa teksteditor op uw PC. Vervang `<SubscriptionA-Id>` Hello-ID van SubscriptionB. 10.0.0.0/16 too10.1.0.0/16, Wijzig alle als tooB en alle Bs tooA wijzigen. Hallo gewijzigd script kopiëren, plak het in tooyour CLI sessie en druk op `Enter`. 
5. Meld u af bij Azure als gebruiker b en tooAzure als GebruikerA aanmelden.
6. Maak een virtueel netwerk van myVnetA toomyVnetB-peering. Kopieer Hallo script inhoud tooa teksteditor op uw PC te volgen. Vervang `<SubscriptionB-Id>` Hello-ID van SubscriptionB. tooexecute Hallo script, Hallo gewijzigd script kopiëren, plak deze in de CLI-sessie en druk op Enter.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Hallo peering status van myVnetA weergeven.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    Hallo-status is **gestarte**. Deze wijzigingen te**verbonden** zodra u de peering toomyVnetA Hallo van myVnetB maakt.

8. Gebruiker a uit Azure afmelden en aanmelden tooAzure als gebruiker b.
9. Hallo-peering van myVnetB toomyVnetA maken. Kopieer de inhoud van het script Hallo in stap 6 tooa teksteditor op uw PC. Vervang `<SubscriptionB-Id>` met Hallo-ID voor SubscriptionA en wijzig alle als tooB en alle Bs tooA. Zodra u Hallo wijzigingen hebt aangebracht, kopie Hallo script gewijzigd, plak het in uw CLI-sessie en druk op `Enter`.
10. Hallo peering status van myVnetB weergeven. Kopieer de inhoud van het script Hallo in stap 7 tooa teksteditor op uw PC. Wijzigen van een tooB voor Hallo resourcegroep en de namen van het virtuele netwerk, Hallo script kopiëren, Hallo gewijzigd script plakken in tooyour CLI-sessie en druk vervolgens op `Enter`. Hallo peering status is **verbonden**. Hallo peering status van myVnetA wijzigingen te**verbonden** nadat u het Hallo-peering van myVnetB toomyVnetA hebt gemaakt. U kunt aanmelden gebruiker a terug tooAzure en volledige stap 7 opnieuw tooverify hello peering status van myVnetA. 

    > [!NOTE]
    > Hallo peering is niet tot stand gebracht totdat Hallo peering status **verbonden** voor beide virtuele netwerken.

11. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
12. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-cli) in dit artikel.

Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Maken van de peering - PowerShell

Deze zelfstudie maakt gebruik van verschillende accounts voor elk abonnement. Als u een account met machtigingen tooboth abonnementen heeft, kunt u Hallo dezelfde account voor alle stappen Hallo stappen voor logboekregistratie buiten Azure overslaan en Hallo regels script die gebruiker roltoewijzingen maakt verwijderen. Vervang UserA@azure.com en UserB@azure.com in alle Hallo scripts met Hallo gebruikersnamen die u voor GebruikerA en gebruiker b te volgen.

1. Installeer de meest recente versie Hallo Hallo PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, Zie [overzicht van Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Een PowerShell-sessie starten.
3. In PowerShell aanmelden tooAzure als GebruikerA hiertoe Hallo `login-azurermaccount` opdracht. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
4. Maak een resourcegroep en virtueel netwerk A. kopie Hallo na tooa scripttekst editor op uw PC. Vervang `<SubscriptionA-Id>` Hello-ID van SubscriptionA. Als u uw abonnements-Id niet weet, voert u Hallo `Get-AzureRmSubscription` opdracht tooview deze. waarde voor Hallo **Id** in Hallo geretourneerd uitvoer is uw abonnements-ID. tooexecute hello script kopiëren Hallo gewijzigd script, plak deze in tooPowerShell en druk vervolgens op `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    Hallo machtigingen worden toegewezen voor gebruiker b is geen vereiste. Peering kan worden vastgesteld zelfs als gebruikers afzonderlijk peering aanvragen voor hun respectieve virtuele netwerken verhogen, zolang Hallo overeenkomst aanvraagt. Toevoeging van een bevoegde gebruiker Hallo maakt andere virtuele netwerk als een gebruiker in de lokale virtuele netwerk Hallo het eenvoudiger toodo Hallo instellen.
5. Gebruiker a uit Azure afmelden en aanmelden gebruiker b. Hallo-account in waarbij u zich moet Hallo noodzakelijke machtigingen toocreate hebben een virtueel netwerk peering. Zie Hallo [machtigingen](#permissions) sectie van dit artikel voor meer informatie.
6. Kopieer de inhoud van het script Hallo in stap 4 tooa teksteditor op uw PC. Vervang `<SubscriptionA-Id>` met Hallo-ID voor het abonnement B. wijziging 10.0.0.0/16 too10.1.0.0/16. Alle als tooB en alle Bs tooA is gewijzigd. tooexecute hello script kopiëren Hallo gewijzigd script, plak in PowerShell en druk vervolgens op `Enter`.
7. Gebruiker b van Azure afmelden en aanmelden gebruiker a.
8. Hallo-peering van myVnetA toomyVnetB maken. Kopieer Hallo script tooa teksteditor op uw PC te volgen. Vervang `<SubscriptionB-Id>` met de ID van het abonnement B. tooexecute Hallo script Hallo Hallo gewijzigd script kopiëren, plak in tooPowerShell en druk vervolgens op `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Hallo peering status van myVnetA weergeven.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Hallo-status is **gestarte**. Deze wijzigingen te**verbonden** zodra u de peering toomyVnetA Hallo van myVnetB instellen.

10. Gebruiker a uit Azure afmelden en aanmelden gebruiker b.
11. Hallo-peering van myVnetB toomyVnetA maken. Kopieer de inhoud van het script Hallo in stap 8 tooa teksteditor op uw PC. Vervang `<SubscriptionB-Id>` met Hallo-ID van een abonnement en wijzig de tooB en alle B tooA. tooexecute hello script kopiëren Hallo gewijzigd script, plak deze in tooPowerShell en druk vervolgens op `Enter`.
12. Hallo peering status van myVnetB weergeven. Kopieer de inhoud van het script Hallo in stap 9 tooa teksteditor op uw PC. Een tooB voor resourcegroep Hallo en virtueel netwerknamen wijzigen. tooexecute hello script, plak Hallo gewijzigd script in PowerShell en druk vervolgens op `Enter`. Hallo-status is **verbonden**. Hallo peering status van **myVnetA** wijzigingen te**verbonden** nadat u hebt gemaakt met het Hallo-peering van **myVnetB** te**myVnetA**. U kunt aanmelden gebruiker a terug tooAzure en volledige stap 9 opnieuw tooverify hello peering status van myVnetA. 

    > [!NOTE]
    > Hallo peering is niet tot stand gebracht totdat Hallo peering status **verbonden** voor beide virtuele netwerken.

    Alle Azure-resources die in een virtueel netwerk hebt u bent nu kunnen toocommunicate met elkaar via hun IP-adressen. Als u standaard Azure-naamomzetting voor virtuele netwerken hello, Hallo resources in virtuele netwerken Hallo zijn niet kunnen tooresolve namen in Hallo virtuele netwerken. Als u tooresolve namen over virtuele netwerken in een peering wilt, moet u uw eigen DNS-server maken. Meer informatie over hoe tooset up [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Optionele**: hoewel maken van virtuele machines wordt niet behandeld in deze zelfstudie, kunt u een virtuele machine maken in elk virtueel netwerk en verbinding maken vanaf een virtuele machine toohello andere, toovalidate connectiviteit.
14. **Optionele**: toodelete Hallo-resources die u in deze zelfstudie maakt, volledige Hallo stappen in [resources verwijderen](#delete-powershell) in dit artikel.

## <a name="permissions"></a>Machtigingen

Hallo-accounts gebruiken van een virtueel netwerk peering toocreate beschikken Hallo benodigde rol of machtigingen. Bijvoorbeeld, als u twee virtuele netwerken met de naam zijn peering **myVnetA** en **myVnetB**, uw account Hallo volgen minimale rol of machtiging voor elke virtuele netwerk moet worden toegewezen:
    
|Virtueel netwerk|Rol|Machtigingen|
|---|---|---|
|myVnetA|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen te[aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="delete"></a>Resources verwijderen
Wanneer u deze zelfstudie hebt voltooid, kunt u toodelete Hallo resources die u hebt gemaakt in de zelfstudie hello, zodat u geen gebruik kosten. Verwijderen van een resourcegroep, worden ook alle resources die in de resourcegroep Hallo verwijderd.

### <a name="delete-portal"></a>Azure-portal

1. Meld u bij toohello Azure-portal als GebruikerA.
2. Voer in de portal zoekvak Hallo **myResourceGroupA**. Klik in de zoekresultaten Hallo **myResourceGroupA**.
3. Op Hallo **myResourceGroupA** blade, klikt u op Hallo **verwijderen** pictogram.
4. tooconfirm hello wordt verwijderd, Hallo **TYPE Hallo RESOURCEGROEPNAAM** Voer **myResourceGroupA**, en klik vervolgens op **verwijderen**.
5. Meld u af bij Hallo-portal aan als gebruiker a en aanmelden als gebruiker b.
6. Herhaal stap 2-4 voor myResourceGroupB.

### <a name="delete-cli"></a>Azure CLI

1. Meld u bij tooAzure als GebruikerA en Hallo volgende opdracht uitvoeren:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Meld u af bij Azure als GebruikerA en aanmelden als gebruiker b.
3. Hallo volgende opdracht uitvoeren:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. Meld u bij tooAzure als GebruikerA en Hallo volgende opdracht uitvoeren:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Meld u af bij Azure als GebruikerA en aanmelden als gebruiker b.
3. Hallo volgende opdracht uitvoeren:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Volgende stappen

- Grondig raken met belangrijke [peering beperkingen virtueel netwerk en het gedrag](virtual-network-manage-peering.md#requirements-and-constraints) voordat het maken van een virtueel netwerk voor productie-peering gebruikt.
- Meer informatie over alle [peering virtuele netwerkinstellingen](virtual-network-manage-peering.md#create-a-peering).
- Meer informatie over hoe te[maken van een hub en spaak netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) met het virtuele netwerk peering.
