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
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="7bb1e-103">Hoe tooprotect DNS-zones en registreert</span><span class="sxs-lookup"><span data-stu-id="7bb1e-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="7bb1e-104">DNS-zones en records zijn kritieke bronnen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="7bb1e-105">Verwijderen van een DNS-zone of zelfs slechts één DNS-record kan leiden tot een onderbreking van deze totale service.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="7bb1e-106">Het is daarom belangrijk dat kritieke DNS-zones en records zijn beschermd tegen onbevoegde of onbedoelde wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="7bb1e-107">Dit artikel wordt uitgelegd hoe Azure DNS kunt u tooprotect uw DNS-zones en records tegen dergelijke wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="7bb1e-108">Twee krachtige beveiligingsfuncties door Azure Resource Manager worden toegepast: [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md) en [resource vergrendelingen](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="7bb1e-109">Op rollen gebaseerd toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="7bb1e-109">Role-based access control</span></span>

<span data-ttu-id="7bb1e-110">Azure op rollen gebaseerde toegangsbeheer (RBAC) kunt Geavanceerd toegangsbeheer voor Azure-gebruikers, groepen en bronnen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="7bb1e-111">Met RBAC kunt verleent u precies Hallo mate van toegang dat gebruikers tooperform hun werk moeten.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="7bb1e-112">Zie voor meer informatie over hoe RBAC helpt u bij het beheren van toegang [wat toegangsbeheer op basis van rollen is](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="7bb1e-113">Hallo 'DNS-Zone Inzender'-rol</span><span class="sxs-lookup"><span data-stu-id="7bb1e-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="7bb1e-114">Hallo 'DNS-Zone Inzender'-rol is een ingebouwde rol die is geleverd door Azure voor het beheren van DNS-resources.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="7bb1e-115">DNS-Zone Inzender machtigingen tooa gebruiker of groep toe te wijzen, kunt deze groep toomanage DNS-resources, maar niet van de resources van een ander type.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="7bb1e-116">Stel bijvoorbeeld dat myzones' hello resource groep' bevat vijf zones voor Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="7bb1e-117">Verlenen Hallo DNS-beheerder 'DNS-Zone Inzender' machtigingen toothat resourcegroep, kunt volledige controle over de DNS-zones.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="7bb1e-118">Dit voorkomt ook onnodige machtigingen verlenen bijvoorbeeld Hallo DNS-beheerder niet maken of virtuele Machines stoppen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="7bb1e-119">Hallo eenvoudigste manier tooassign RBAC machtigingen is [via hello Azure-portal](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="7bb1e-120">Opent u de blade Hallo 'Access control (IAM)' voor de resourcegroep Hallo achtereenvolgens 'Add' en selecteer Hallo 'DNS-Zone Inzender' rol en selecteer Hallo vereist gebruikers of groepen toogrant machtigingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Niveau van de resourcegroep RBAC via hello Azure-portal](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="7bb1e-122">Machtigingen kunnen ook worden [verleend met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="7bb1e-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="7bb1e-123">Hallo gelijkwaardige opdracht is ook [beschikbaar via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="7bb1e-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="7bb1e-124">Zone-niveau RBAC</span><span class="sxs-lookup"><span data-stu-id="7bb1e-124">Zone level RBAC</span></span>

<span data-ttu-id="7bb1e-125">Azure RBAC-regels kunnen worden toegepast tooa abonnement, met een resource groep of tooan afzonderlijke resource.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="7bb1e-126">In geval van Azure DNS Hallo is die bron een afzonderlijke DNS-zone of een afzonderlijke Recordset.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="7bb1e-127">Stel bijvoorbeeld dat myzones' hello resource groep' hello zone 'contoso.com' en een subzone 'customers.contoso.com' waarin de CNAME-records die zijn gemaakt voor elk klantaccount bevat.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="7bb1e-128">Hallo-account gebruikt toomanage deze CNAME-records moeten worden toegewezen machtigingen toocreate records in Hallo 'customers.contoso.com' alleen zone, er mogen geen toegang tot toohello andere zones.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="7bb1e-129">Zoneniveau RBAC machtigingen kunnen worden verleend via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="7bb1e-130">Hallo Access control (IAM) blade voor de zone Hallo, Open achtereenvolgens 'Add- en Hallo 'DNS-Zone Inzender'-rol en selecteer Hallo vereist gebruikers of groepen toogrant machtigingen selecteren.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![DNS-Zone niveau RBAC via hello Azure-portal](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="7bb1e-132">Machtigingen kunnen ook worden [verleend met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="7bb1e-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="7bb1e-133">Hallo gelijkwaardige opdracht is ook [beschikbaar via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="7bb1e-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="7bb1e-134">Record RBAC-niveau instellen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-134">Record set level RBAC</span></span>

<span data-ttu-id="7bb1e-135">We kunt nog een stapje verder gaan.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-135">We can go one step further.</span></span> <span data-ttu-id="7bb1e-136">Houd rekening met Hallo mail-beheerder voor Contoso Corporation, die toegang toohello MX en TXT-records in het toppunt van de zone 'contoso.com' Hallo Hallo nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="7bb1e-137">Ze niet nodig hebt toegang tot tooany andere MX- of TXT-records of tooany records van een ander type.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="7bb1e-138">Azure DNS kunt u tooassign machtigingen op Hallo Recordset niveau, tooprecisely Hallo records die Hallo e-mail beheerder toegang tot nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="7bb1e-139">Hallo mailbeheerder krijgt precies Hallo bepalen die ze nodig, en is toomake kan geen andere wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="7bb1e-140">Record-set RBAC machtigingen kunnen worden geconfigureerd via Azure portal, met behulp van de knop Hallo 'gebruikers' hello Recordset blade Hallo:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![De recordset niveau RBAC via hello Azure-portal](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="7bb1e-142">Record-set machtigingen op gebruikersniveau RBAC kunnen ook worden [verleend met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="7bb1e-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="7bb1e-143">Hallo gelijkwaardige opdracht is ook [beschikbaar via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="7bb1e-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="7bb1e-144">Aangepaste rollen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-144">Custom roles</span></span>

<span data-ttu-id="7bb1e-145">Hallo ingebouwde 'DNS-Zone Inzender'-rol kunnen volledige controle over een DNS-bronrecords.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="7bb1e-146">Het is ook mogelijk toobuild uw eigen klant Azure rollen, tooprovide zelfs nauwkeurigere besturingselement.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="7bb1e-147">Bekijk opnieuw Hallo voorbeeld waarin een CNAME-record in customers.contoso.com' hello zone' is gemaakt voor elk account van de klant Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="7bb1e-148">Hallo-account gebruikt toomanage deze CNAMEs moeten worden verleend machtiging toomanage CNAME-records alleen hebben.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="7bb1e-149">Het is en kan niet toomodify records van andere bestandstypen (zoals het wijzigen van een MX-record) of zoneniveau bewerkingen zoals zone verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="7bb1e-150">Hallo volgende voorbeeld ziet u een aangepaste roldefinitie voor het beheren van CNAME-records:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="7bb1e-151">Hallo acties eigenschap definieert Hallo volgende DNS-specifieke machtigingen:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="7bb1e-152">`Microsoft.Network/dnsZones/CNAME/*`Hiermee wordt volledige controle over de CNAME-records</span><span class="sxs-lookup"><span data-stu-id="7bb1e-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="7bb1e-153">`Microsoft.Network/dnsZones/read`verleent toestemming tooread DNS-zones, maar niet toomodify ze u toosee inschakelen Hallo zone in welke Hallo CNAME wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="7bb1e-154">Hallo resterende acties worden gekopieerd van Hallo [ingebouwde rol van inzender van DNS-Zone](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="7bb1e-155">Een aangepaste RBAC-rol tooprevent record wordt verwijderd, wordt ingesteld terwijl u nog steeds zodat ze toobe bijgewerkt is niet een doeltreffende controle.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="7bb1e-156">Deze voorkomt dat recordsets worden verwijderd, maar dit voorkomt niet dat deze wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="7bb1e-157">Toegestane wijzigingen bevatten toe te voegen en tooleave een 'empty' Recordset verwijderen van records uit de recordset hello, met inbegrip van verwijderen van alle registreert.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="7bb1e-158">Dit heeft hetzelfde effect als het Hallo-record verwijderen uit een DNS-omzetting oogpunt ingesteld Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="7bb1e-159">Aangepaste roldefinities kunnen niet op dit moment worden gedefinieerd via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="7bb1e-160">Een aangepaste rol die is gebaseerd op de roldefinitie van deze kan worden gemaakt met Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="7bb1e-161">Het kan ook worden gemaakt via hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="7bb1e-162">Hallo rol kan vervolgens worden toegewezen in Hallo dezelfde manier als de ingebouwde rollen, zoals eerder in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="7bb1e-163">Zie voor meer informatie over hoe toocreate, beheren en aangepaste rollen toewijzen [aangepaste rollen in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="7bb1e-164">Resource-vergrendelingen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-164">Resource locks</span></span>

<span data-ttu-id="7bb1e-165">In toevoeging tooRBAC, Azure Resource Manager biedt ondersteuning voor een ander type beveiligingscontrole, namelijk Hallo mogelijkheid too'lock' resources.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="7bb1e-166">Waarbij RBAC regels u toocontrol Hallo acties van specifieke gebruikers en groepen kunt, resource vergrendelingen zijn toegepaste toohello resource en gelden voor alle gebruikers en rollen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="7bb1e-167">Zie voor meer informatie [Resources vergrendelen met Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="7bb1e-168">Er zijn twee soorten resource vergrendeling: **DoNotDelete** en **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="7bb1e-169">Deze kunnen worden toegepast tooa DNS-zone of tooan afzonderlijke Recordset.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="7bb1e-170">Hallo volgende secties beschrijven enkele algemene scenario's, en hoe toosupport ze gebruik van resource vergrendelingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="7bb1e-171">Bescherming tegen alle wijzigingen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-171">Protecting against all changes</span></span>

<span data-ttu-id="7bb1e-172">tooprevent wijzigingen worden aangebracht, een alleen-lezen vergrendeling toohello zone toepassen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="7bb1e-173">Dit voorkomt dat nieuwe recordsets wordt gemaakt en bestaande recordsets worden gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="7bb1e-174">Zone niveau resource vergrendelingen kunnen worden gemaakt via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="7bb1e-175">Klik op 'Vergrendelingen' hello DNS-zone blade vervolgens 'Add':</span><span class="sxs-lookup"><span data-stu-id="7bb1e-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Zone niveau resource vergrendelingen via hello Azure-portal](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="7bb1e-177">Zoneniveau resource vergrendelingen kunnen ook worden gemaakt via Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="7bb1e-178">Configureren van Azure-resource vergrendeld is momenteel niet ondersteund via hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="7bb1e-179">Afzonderlijke records beveiligen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-179">Protecting individual records</span></span>

<span data-ttu-id="7bb1e-180">een recordset van alleen-lezen vergrendeling toohello tooprevent een bestaande DNS-record is ingesteld op basis van de wijziging, van toepassing.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="7bb1e-181">Toepassen van een vergrendeling DoNotDelete tooa is recordset niet een doeltreffende controle.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="7bb1e-182">Deze voorkomt dat Hallo-recordset worden verwijderd, maar dit voorkomt niet dat deze wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="7bb1e-183">Toegestane wijzigingen bevatten toe te voegen en tooleave een 'empty' Recordset verwijderen van records uit de recordset hello, met inbegrip van verwijderen van alle registreert.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="7bb1e-184">Dit heeft hetzelfde effect als het Hallo-record verwijderen uit een DNS-omzetting oogpunt ingesteld Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="7bb1e-185">Recordset niveau resource vergrendelingen kunnen momenteel alleen worden geconfigureerd met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="7bb1e-186">Ze worden niet ondersteund in hello Azure-portal of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="7bb1e-187">Bescherming tegen zone verwijderen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-187">Protecting against zone deletion</span></span>

<span data-ttu-id="7bb1e-188">Wanneer een zone in Azure DNS wordt verwijderd, worden ook alle recordsets in de zone Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="7bb1e-189">Deze bewerking kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-189">This operation cannot be undone.</span></span>  <span data-ttu-id="7bb1e-190">Per ongeluk verwijderen van een kritieke zone heeft Hallo potentiële toohave een aanzienlijke zakelijke invloed.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="7bb1e-191">Het is daarom belangrijk tooprotect tegen het onbedoeld zone verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="7bb1e-192">Toepassen van een zone DoNotDelete vergrendeling tooa voorkomt u dat Hallo zone worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="7bb1e-193">Echter, omdat de vergrendelingen worden overgenomen door onderliggende resources, voorkomt u tevens dat alle recordsets in Hallo zone worden verwijderd, die mogelijk ongewenste.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="7bb1e-194">Bovendien zoals beschreven in bovenstaande Hallo opmerking, is het ook ongeschikt Aangezien records kunnen nog steeds worden verwijderd uit de bestaande recordsets Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="7bb1e-195">Als alternatief kunt u kunt toepassen van een record DoNotDelete vergrendeling tooa ingesteld voor de zone hello, zoals Hallo SOA-Recordset.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="7bb1e-196">Dit biedt bescherming tegen verwijderen van een zone, terwijl u nog steeds recordsets binnen Hallo zone toobe vrijelijk worden gewijzigd omdat Hallo zone kan niet worden verwijderd zonder ook Hallo recordsets te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="7bb1e-197">Als een poging wordt gedaan toodelete Hallo zone, detecteert de Azure Resource Manager dit ook Hallo SOA-recordset wilt verwijderen en blokken Hallo aanroep omdat Hallo SOA is vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="7bb1e-198">Er is geen recordsets worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-198">No record sets are deleted.</span></span>

<span data-ttu-id="7bb1e-199">Hallo volgende PowerShell-opdracht maakt een vergrendeling DoNotDelete tegen Hallo SOA-record Hallo zone gegeven:</span><span class="sxs-lookup"><span data-stu-id="7bb1e-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="7bb1e-200">Een andere manier tooprevent onbedoeld zone verwijderen is met behulp van een aangepaste rol tooensure Hallo operator en toomanage voor service-accounts die worden gebruikt uw zones niet doen hebben zone verwijderen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="7bb1e-201">Wanneer u een zone toodelete hoeft, kunt u afdwingen in twee stappen verwijderen, eerste verlenen zone machtigingen voor het verwijderen (op Hallo zone bereik tooprevent Hallo verkeerde zone verwijderen) en de tweede toodelete Hallo zone.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="7bb1e-202">Deze tweede methode is Hallo voordeel die geschikt is voor alle zones die toegankelijk is voor deze accounts zonder tooremember toocreate alle vergrendelingen.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="7bb1e-203">Hallo nadeel dat alle accounts met machtigingen op zone verwijderen, zoals eigenaar Hallo-abonnement, nog steeds per ongeluk een kritieke zone kunnen verwijderen heeft.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="7bb1e-204">Het is mogelijk toouse beide benaderingen op Hallo - resource vergrendelingen en aangepaste rollen - dezelfde tijd als een protection defense-in-depth benadering tooDNS zone.</span><span class="sxs-lookup"><span data-stu-id="7bb1e-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bb1e-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bb1e-205">Next steps</span></span>

* <span data-ttu-id="7bb1e-206">Zie voor meer informatie over het werken met RBAC [aan de slag met toegangsbeheer in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="7bb1e-207">Zie voor meer informatie over het werken met resource vergrendelingen [resources met Azure Resource Manager vergrendelen](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7bb1e-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

