---
title: aaaProtecting DNS-Zones en Records | Microsoft Docs
description: Hoe tooprotect DNS-zones en -record wordt in Microsoft Azure DNS worden ingesteld.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a>Hoe tooprotect DNS-zones en registreert

DNS-zones en records zijn kritieke bronnen. Verwijderen van een DNS-zone of zelfs slechts één DNS-record kan leiden tot een onderbreking van deze totale service.  Het is daarom belangrijk dat kritieke DNS-zones en records zijn beschermd tegen onbevoegde of onbedoelde wijzigingen.

Dit artikel wordt uitgelegd hoe Azure DNS kunt u tooprotect uw DNS-zones en records tegen dergelijke wijzigingen.  Twee krachtige beveiligingsfuncties door Azure Resource Manager worden toegepast: [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) en [resource vergrendelingen](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer

Azure op rollen gebaseerde toegangsbeheer (RBAC) kunt Geavanceerd toegangsbeheer voor Azure-gebruikers, groepen en bronnen. Met RBAC kunt verleent u precies Hallo mate van toegang dat gebruikers tooperform hun werk moeten. Zie voor meer informatie over hoe RBAC helpt u bij het beheren van toegang [wat toegangsbeheer op basis van rollen is](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>Hallo 'DNS-Zone Inzender'-rol

Hallo 'DNS-Zone Inzender'-rol is een ingebouwde rol die is geleverd door Azure voor het beheren van DNS-resources.  DNS-Zone Inzender machtigingen tooa gebruiker of groep toe te wijzen, kunt deze groep toomanage DNS-resources, maar niet van de resources van een ander type.

Stel bijvoorbeeld dat myzones' hello resource groep' bevat vijf zones voor Contoso Corporation. Verlenen Hallo DNS-beheerder 'DNS-Zone Inzender' machtigingen toothat resourcegroep, kunt volledige controle over de DNS-zones. Dit voorkomt ook onnodige machtigingen verlenen bijvoorbeeld Hallo DNS-beheerder niet maken of virtuele Machines stoppen.

Hallo eenvoudigste manier tooassign RBAC machtigingen is [via hello Azure-portal](../active-directory/role-based-access-control-configure.md).  Opent u de blade Hallo 'Access control (IAM)' voor de resourcegroep Hallo achtereenvolgens 'Add' en selecteer Hallo 'DNS-Zone Inzender' rol en selecteer Hallo vereist gebruikers of groepen toogrant machtigingen.

![Niveau van de resourcegroep RBAC via hello Azure-portal](./media/dns-protect-zones-recordsets/rbac1.png)

Machtigingen kunnen ook worden [verleend met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

Hallo gelijkwaardige opdracht is ook [beschikbaar via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>Zone-niveau RBAC

Azure RBAC-regels kunnen worden toegepast tooa abonnement, met een resource groep of tooan afzonderlijke resource. In geval van Azure DNS Hallo is die bron een afzonderlijke DNS-zone of een afzonderlijke Recordset.

Stel bijvoorbeeld dat myzones' hello resource groep' hello zone 'contoso.com' en een subzone 'customers.contoso.com' waarin de CNAME-records die zijn gemaakt voor elk klantaccount bevat.  Hallo-account gebruikt toomanage deze CNAME-records moeten worden toegewezen machtigingen toocreate records in Hallo 'customers.contoso.com' alleen zone, er mogen geen toegang tot toohello andere zones.

Zoneniveau RBAC machtigingen kunnen worden verleend via hello Azure-portal.  Hallo Access control (IAM) blade voor de zone Hallo, Open achtereenvolgens 'Add- en Hallo 'DNS-Zone Inzender'-rol en selecteer Hallo vereist gebruikers of groepen toogrant machtigingen selecteren.

![DNS-Zone niveau RBAC via hello Azure-portal](./media/dns-protect-zones-recordsets/rbac2.png)

Machtigingen kunnen ook worden [verleend met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

Hallo gelijkwaardige opdracht is ook [beschikbaar via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>Record RBAC-niveau instellen

We kunt nog een stapje verder gaan. Houd rekening met Hallo mail-beheerder voor Contoso Corporation, die toegang toohello MX en TXT-records in het toppunt van de zone 'contoso.com' Hallo Hallo nodig heeft.  Ze niet nodig hebt toegang tot tooany andere MX- of TXT-records of tooany records van een ander type.  Azure DNS kunt u tooassign machtigingen op Hallo Recordset niveau, tooprecisely Hallo records die Hallo e-mail beheerder toegang tot nodig heeft.  Hallo mailbeheerder krijgt precies Hallo bepalen die ze nodig, en is toomake kan geen andere wijzigingen.

Record-set RBAC machtigingen kunnen worden geconfigureerd via Azure portal, met behulp van de knop Hallo 'gebruikers' hello Recordset blade Hallo:

![De recordset niveau RBAC via hello Azure-portal](./media/dns-protect-zones-recordsets/rbac3.png)

Record-set machtigingen op gebruikersniveau RBAC kunnen ook worden [verleend met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

Hallo gelijkwaardige opdracht is ook [beschikbaar via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Aangepaste rollen

Hallo ingebouwde 'DNS-Zone Inzender'-rol kunnen volledige controle over een DNS-bronrecords. Het is ook mogelijk toobuild uw eigen klant Azure rollen, tooprovide zelfs nauwkeurigere besturingselement.

Bekijk opnieuw Hallo voorbeeld waarin een CNAME-record in customers.contoso.com' hello zone' is gemaakt voor elk account van de klant Contoso Corporation.  Hallo-account gebruikt toomanage deze CNAMEs moeten worden verleend machtiging toomanage CNAME-records alleen hebben.  Het is en kan niet toomodify records van andere bestandstypen (zoals het wijzigen van een MX-record) of zoneniveau bewerkingen zoals zone verwijderen.

Hallo volgende voorbeeld ziet u een aangepaste roldefinitie voor het beheren van CNAME-records:

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

Hallo acties eigenschap definieert Hallo volgende DNS-specifieke machtigingen:

* `Microsoft.Network/dnsZones/CNAME/*`Hiermee wordt volledige controle over de CNAME-records
* `Microsoft.Network/dnsZones/read`verleent toestemming tooread DNS-zones, maar niet toomodify ze u toosee inschakelen Hallo zone in welke Hallo CNAME wordt gemaakt.

Hallo resterende acties worden gekopieerd van Hallo [ingebouwde rol van inzender van DNS-Zone](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Een aangepaste RBAC-rol tooprevent record wordt verwijderd, wordt ingesteld terwijl u nog steeds zodat ze toobe bijgewerkt is niet een doeltreffende controle. Deze voorkomt dat recordsets worden verwijderd, maar dit voorkomt niet dat deze wordt gewijzigd.  Toegestane wijzigingen bevatten toe te voegen en tooleave een 'empty' Recordset verwijderen van records uit de recordset hello, met inbegrip van verwijderen van alle registreert. Dit heeft hetzelfde effect als het Hallo-record verwijderen uit een DNS-omzetting oogpunt ingesteld Hallo.

Aangepaste roldefinities kunnen niet op dit moment worden gedefinieerd via hello Azure-portal. Een aangepaste rol die is gebaseerd op de roldefinitie van deze kan worden gemaakt met Azure PowerShell:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Het kan ook worden gemaakt via hello Azure CLI:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hallo rol kan vervolgens worden toegewezen in Hallo dezelfde manier als de ingebouwde rollen, zoals eerder in dit artikel wordt beschreven.

Zie voor meer informatie over hoe toocreate, beheren en aangepaste rollen toewijzen [aangepaste rollen in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Resource-vergrendelingen

In toevoeging tooRBAC, Azure Resource Manager biedt ondersteuning voor een ander type beveiligingscontrole, namelijk Hallo mogelijkheid too'lock' resources. Waarbij RBAC regels u toocontrol Hallo acties van specifieke gebruikers en groepen kunt, resource vergrendelingen zijn toegepaste toohello resource en gelden voor alle gebruikers en rollen. Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

Er zijn twee soorten resource vergrendeling: **DoNotDelete** en **ReadOnly**. Deze kunnen worden toegepast tooa DNS-zone of tooan afzonderlijke Recordset.  Hallo volgende secties beschrijven enkele algemene scenario's, en hoe toosupport ze gebruik van resource vergrendelingen.

### <a name="protecting-against-all-changes"></a>Bescherming tegen alle wijzigingen

tooprevent wijzigingen worden aangebracht, een alleen-lezen vergrendeling toohello zone toepassen.  Dit voorkomt dat nieuwe recordsets wordt gemaakt en bestaande recordsets worden gewijzigd of verwijderd.

Zone niveau resource vergrendelingen kunnen worden gemaakt via hello Azure-portal.  Klik op 'Vergrendelingen' hello DNS-zone blade vervolgens 'Add':

![Zone niveau resource vergrendelingen via hello Azure-portal](./media/dns-protect-zones-recordsets/locks1.png)

Zoneniveau resource vergrendelingen kunnen ook worden gemaakt via Azure PowerShell:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Configureren van Azure-resource vergrendeld is momenteel niet ondersteund via hello Azure CLI.

### <a name="protecting-individual-records"></a>Afzonderlijke records beveiligen

een recordset van alleen-lezen vergrendeling toohello tooprevent een bestaande DNS-record is ingesteld op basis van de wijziging, van toepassing.

> [!NOTE]
> Toepassen van een vergrendeling DoNotDelete tooa is recordset niet een doeltreffende controle. Deze voorkomt dat Hallo-recordset worden verwijderd, maar dit voorkomt niet dat deze wordt gewijzigd.  Toegestane wijzigingen bevatten toe te voegen en tooleave een 'empty' Recordset verwijderen van records uit de recordset hello, met inbegrip van verwijderen van alle registreert. Dit heeft hetzelfde effect als het Hallo-record verwijderen uit een DNS-omzetting oogpunt ingesteld Hallo.

Recordset niveau resource vergrendelingen kunnen momenteel alleen worden geconfigureerd met behulp van Azure PowerShell.  Ze worden niet ondersteund in hello Azure-portal of Azure CLI.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Bescherming tegen zone verwijderen

Wanneer een zone in Azure DNS wordt verwijderd, worden ook alle recordsets in de zone Hallo verwijderd.  Deze bewerking kan niet ongedaan worden gemaakt.  Per ongeluk verwijderen van een kritieke zone heeft Hallo potentiële toohave een aanzienlijke zakelijke invloed.  Het is daarom belangrijk tooprotect tegen het onbedoeld zone verwijderen.

Toepassen van een zone DoNotDelete vergrendeling tooa voorkomt u dat Hallo zone worden verwijderd.  Echter, omdat de vergrendelingen worden overgenomen door onderliggende resources, voorkomt u tevens dat alle recordsets in Hallo zone worden verwijderd, die mogelijk ongewenste.  Bovendien zoals beschreven in bovenstaande Hallo opmerking, is het ook ongeschikt Aangezien records kunnen nog steeds worden verwijderd uit de bestaande recordsets Hallo.

Als alternatief kunt u kunt toepassen van een record DoNotDelete vergrendeling tooa ingesteld voor de zone hello, zoals Hallo SOA-Recordset.  Dit biedt bescherming tegen verwijderen van een zone, terwijl u nog steeds recordsets binnen Hallo zone toobe vrijelijk worden gewijzigd omdat Hallo zone kan niet worden verwijderd zonder ook Hallo recordsets te verwijderen. Als een poging wordt gedaan toodelete Hallo zone, detecteert de Azure Resource Manager dit ook Hallo SOA-recordset wilt verwijderen en blokken Hallo aanroep omdat Hallo SOA is vergrendeld.  Er is geen recordsets worden verwijderd.

Hallo volgende PowerShell-opdracht maakt een vergrendeling DoNotDelete tegen Hallo SOA-record Hallo zone gegeven:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Een andere manier tooprevent onbedoeld zone verwijderen is met behulp van een aangepaste rol tooensure Hallo operator en toomanage voor service-accounts die worden gebruikt uw zones niet doen hebben zone verwijderen machtigingen. Wanneer u een zone toodelete hoeft, kunt u afdwingen in twee stappen verwijderen, eerste verlenen zone machtigingen voor het verwijderen (op Hallo zone bereik tooprevent Hallo verkeerde zone verwijderen) en de tweede toodelete Hallo zone.

Deze tweede methode is Hallo voordeel die geschikt is voor alle zones die toegankelijk is voor deze accounts zonder tooremember toocreate alle vergrendelingen. Hallo nadeel dat alle accounts met machtigingen op zone verwijderen, zoals eigenaar Hallo-abonnement, nog steeds per ongeluk een kritieke zone kunnen verwijderen heeft.

Het is mogelijk toouse beide benaderingen op Hallo - resource vergrendelingen en aangepaste rollen - dezelfde tijd als een protection defense-in-depth benadering tooDNS zone.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over het werken met RBAC [aan de slag met toegangsbeheer in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).
* Zie voor meer informatie over het werken met resource vergrendelingen [resources met Azure Resource Manager vergrendelen](../azure-resource-manager/resource-group-lock-resources.md).

