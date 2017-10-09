---
title: access-aaaJust in tijd virtuele machine in Azure Security Center | Microsoft Docs
description: Dit document wordt u begeleid bij hoe NET tijdig VM-toegang in Azure Security Center helpt u toegang tot tooyour Azure virtuele machines.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="730a8-103">Virtuele machine toegang met behulp van in de tijd beheren</span><span class="sxs-lookup"><span data-stu-id="730a8-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="730a8-104">Alleen in tijd virtuele machine (VM) zijn toegang gebruikte toolock omlaag binnenkomend verkeer tooyour Azure Virtual machines blootstelling tooattacks verminderen terwijl er eenvoudig toegang tooconnect tooVMs wanneer deze nodig.</span><span class="sxs-lookup"><span data-stu-id="730a8-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="730a8-105">Hallo alleen in de functie is in preview en beschikbaar is op Hallo standaardcategorie van Security Center.</span><span class="sxs-lookup"><span data-stu-id="730a8-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="730a8-106">Zie [prijzen](security-center-pricing.md) toolearn meer informatie over Security Center de prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="730a8-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="730a8-107">Aanval</span><span class="sxs-lookup"><span data-stu-id="730a8-107">Attack scenario</span></span>

<span data-ttu-id="730a8-108">Brute force-aanvallen vaak doelpoorten management als een manier toogain toegang tooa VM.</span><span class="sxs-lookup"><span data-stu-id="730a8-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="730a8-109">Als dit lukt, kan een aanvaller besturen Hallo VM en een voet achter de deur tot stand brengen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="730a8-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="730a8-110">Eenzijdige tooreduce blootstelling tooa beveiligingsaanval is toolimit Hallo hoeveelheid tijd die een poort geopend is.</span><span class="sxs-lookup"><span data-stu-id="730a8-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="730a8-111">Poorten voor beheertaken doen niet nodig toobe open te allen tijde.</span><span class="sxs-lookup"><span data-stu-id="730a8-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="730a8-112">Hoeft alleen toobe openen terwijl u bent verbonden toohello VM, bijvoorbeeld tooperform management en-onderhoud.</span><span class="sxs-lookup"><span data-stu-id="730a8-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="730a8-113">Wanneer u in de tijd is ingeschakeld, wordt gebruikt door Security Center [Netwerkbeveiligingsgroep](../virtual-network/virtual-networks-nsg.md) (NSG), deze regels toomanagement toegangspoorten beperken zodat ze niet worden gericht door aanvallers.</span><span class="sxs-lookup"><span data-stu-id="730a8-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Alleen bij tijd scenario][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="730a8-115">Hoe werkt alleen bij het toegang in uitvoeringstijd combinatie?</span><span class="sxs-lookup"><span data-stu-id="730a8-115">How does just in time access work?</span></span>

<span data-ttu-id="730a8-116">Wanneer in de tijd is ingeschakeld, wordt in Security Center binnenkomend verkeer tooyour Azure Virtual machines vergrendelt door het maken van een NSG-regel.</span><span class="sxs-lookup"><span data-stu-id="730a8-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="730a8-117">U selecteert Hallo poorten op Hallo VM toowhich binnenkomend verkeer wordt worden vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="730a8-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="730a8-118">Deze poorten worden beheerd door Hallo NET in tijdoplossing.</span><span class="sxs-lookup"><span data-stu-id="730a8-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="730a8-119">Wanneer een gebruiker toegang tooa VM aanvraagt, Security Center controleert die gebruiker Hallo [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) machtigingen die schrijftoegang voor hello Azure-resource bieden.</span><span class="sxs-lookup"><span data-stu-id="730a8-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="730a8-120">Als ze schrijftoegang hebben, Hallo-aanvraag is goedgekeurd en Security Center configureert automatisch Hallo Netwerkbeveiligingsgroepen (nsg's) tooallow poorten voor verkeer toohello inkomende hello en de hoeveelheid tijd die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="730a8-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="730a8-121">Nadat het Hallo-tijd is verstreken, herstelt Security Center Hallo nsg's tootheir vorige staat.</span><span class="sxs-lookup"><span data-stu-id="730a8-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="730a8-122">Security Center alleen bij het VM-time-toegang ondersteunt momenteel alleen virtuele machines die zijn geïmplementeerd via Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="730a8-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="730a8-123">Zie informatie over het Hallo-classic en Resource Manager-implementatiemodel toolearn [Azure Resource Manager versus klassieke implementatie](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="730a8-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="730a8-124">Met behulp van alleen bij het time-toegang</span><span class="sxs-lookup"><span data-stu-id="730a8-124">Using just in time access</span></span>

<span data-ttu-id="730a8-125">Hallo **Just in time VM toegang** tegel op Hallo **Security Center** blade ziet u Hallo aantal VM's zijn geconfigureerd voor alleen bij tijd toegang en Hallo aantal goedgekeurde toegangsaanvragen in Hallo afgelopen week.</span><span class="sxs-lookup"><span data-stu-id="730a8-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="730a8-126">Selecteer Hallo **Just in time VM toegang** tegel en Hallo **Just in time VM toegang** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="730a8-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![Alleen in de tijd VM toegang tegel][2]

<span data-ttu-id="730a8-128">Hallo **Just in time VM toegang** blade bevat informatie over het Hallo-status van uw virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="730a8-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="730a8-129">**Geconfigureerd** -virtuele machines die geconfigureerd toosupport alleen bij het VM-time-toegang zijn.</span><span class="sxs-lookup"><span data-stu-id="730a8-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="730a8-130">Hallo-gegevens die worden gepresenteerd Hallo afgelopen week en voor elke VM Hallo aantal goedgekeurde aanvragen, de datum van laatste toegang en de tijd en de laatste gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="730a8-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="730a8-131">**Aanbevolen** -VM's die alleen bij het toegang in uitvoeringstijd VM kunnen ondersteunen, maar niet is geconfigureerd voor.</span><span class="sxs-lookup"><span data-stu-id="730a8-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="730a8-132">Het is raadzaam dat u alleen bij het VM-toegangsbeheer tijd voor deze virtuele machines inschakelt.</span><span class="sxs-lookup"><span data-stu-id="730a8-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="730a8-133">Zie [tijd VM toegang inschakelen](#enable-just-in-time-vm-access).</span><span class="sxs-lookup"><span data-stu-id="730a8-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="730a8-134">**Geen aanbeveling** -redenen die leiden een virtuele machine niet toobe aanbevolen tot kunnen zijn:</span><span class="sxs-lookup"><span data-stu-id="730a8-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="730a8-135">Ontbrekende NSG - Hallo NET in tijdoplossing vereist een NSG toobe aanwezig.</span><span class="sxs-lookup"><span data-stu-id="730a8-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="730a8-136">Klassieke VM - Security Center alleen bij het VM-time-toegang ondersteunt momenteel alleen virtuele machines die zijn geïmplementeerd via Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="730a8-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="730a8-137">Een klassieke implementatie wordt niet ondersteund door Hallo NET in tijdoplossing.</span><span class="sxs-lookup"><span data-stu-id="730a8-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="730a8-138">Andere - een virtuele machine is in deze categorie als Hallo NET tijdig oplossing is uitgeschakeld in het beveiligingsbeleid Hallo van Hallo abonnement of resourcegroep hello, of dat Hallo VM een openbaar IP-adres ontbreekt en niet beschikken over een NSG.</span><span class="sxs-lookup"><span data-stu-id="730a8-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="730a8-139">Configureren van een in het toegangsbeleid tijd</span><span class="sxs-lookup"><span data-stu-id="730a8-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="730a8-140">tooselect hello virtuele machines die u wilt dat tooenable:</span><span class="sxs-lookup"><span data-stu-id="730a8-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="730a8-141">Op Hallo **Just in time VM toegang** blade, selecteer Hallo **aanbevolen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="730a8-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Time-toegang inschakelen][3]

2. <span data-ttu-id="730a8-143">Onder **VMs**, Hallo virtuele machines die u tooenable wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="730a8-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="730a8-144">Hiermee wordt een vinkje volgende tooa VM geplaatst.</span><span class="sxs-lookup"><span data-stu-id="730a8-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="730a8-145">Selecteer **JIT op virtuele machines inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="730a8-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="730a8-146">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="730a8-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="730a8-147">Standaard-poorten</span><span class="sxs-lookup"><span data-stu-id="730a8-147">Default ports</span></span>

<span data-ttu-id="730a8-148">Hallo-standaardpoorten die Security Center aanbeveelt inschakelen in de tijd, kunt u zien.</span><span class="sxs-lookup"><span data-stu-id="730a8-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="730a8-149">Op Hallo **Just in time VM toegang** blade, selecteer Hallo **aanbevolen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="730a8-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![Standaardpoorten weergeven][6]

2. <span data-ttu-id="730a8-151">Onder **VMs**, selecteert u een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="730a8-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="730a8-152">Hiermee wordt een vinkje volgende toohello virtuele machine en wordt geopend Hallo geplaatst **JIT VM-configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="730a8-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="730a8-153">Deze blade geeft Hallo standaardpoorten.</span><span class="sxs-lookup"><span data-stu-id="730a8-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="730a8-154">Poorten toevoegen</span><span class="sxs-lookup"><span data-stu-id="730a8-154">Add ports</span></span>

<span data-ttu-id="730a8-155">Van Hallo **JIT VM-configuratie** blade kunt u ook toevoegen en configureren van een nieuwe poort waarop tooenable Hallo NET in tijdoplossing.</span><span class="sxs-lookup"><span data-stu-id="730a8-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="730a8-156">Op Hallo **JIT VM-configuratie** blade Selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="730a8-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="730a8-157">Hiermee opent u Hallo **toevoegen poortconfiguratie** blade.</span><span class="sxs-lookup"><span data-stu-id="730a8-157">This opens hello **Add port configuration** blade.</span></span>

  ![Poortconfiguratie][7]

2. <span data-ttu-id="730a8-159">Op **toevoegen poortconfiguratie** blade u identificeren Hallo-poort, protocoltype, bron-IP-adressen en de maximale duur van aanvraag toegestaan.</span><span class="sxs-lookup"><span data-stu-id="730a8-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="730a8-160">Bron-IP-adressen toegestaan zijn Hallo IP-adresbereiken toegestane tooget toegang op een verzoek goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="730a8-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="730a8-161">Maximale aanvraagtijd is Hallo maximale tijdsduur dat een specifieke poort kan worden geopend.</span><span class="sxs-lookup"><span data-stu-id="730a8-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="730a8-162">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="730a8-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="730a8-163">Aanvragen van toegang tooa VM</span><span class="sxs-lookup"><span data-stu-id="730a8-163">Requesting access tooa VM</span></span>

<span data-ttu-id="730a8-164">toorequest toegang tooa VM:</span><span class="sxs-lookup"><span data-stu-id="730a8-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="730a8-165">Op Hallo **Just in time VM toegang** blade, selecteer Hallo **geconfigureerde** tabblad.</span><span class="sxs-lookup"><span data-stu-id="730a8-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="730a8-166">Onder **VMs**, Hallo virtuele machines die u toegang tooenable wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="730a8-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="730a8-167">Hiermee wordt een vinkje volgende tooa VM geplaatst.</span><span class="sxs-lookup"><span data-stu-id="730a8-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="730a8-168">Selecteer **toegang aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="730a8-168">Select **Request access**.</span></span> <span data-ttu-id="730a8-169">Hiermee opent u Hallo **toegang aanvragen** blade.</span><span class="sxs-lookup"><span data-stu-id="730a8-169">This opens hello **Request access** blade.</span></span>

  ![Aanvraag toegang tooa VM][4]

4. <span data-ttu-id="730a8-171">Op Hallo **toegang aanvragen** blade u configureert voor elke VM Hallo poorten tooopen samen met de Hallo bron-IP dat Hallo poort geopend tooand Hallo-tijdvenster voor welke Hallo poort is geopend.</span><span class="sxs-lookup"><span data-stu-id="730a8-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="730a8-172">U kunt alleen toohello toegangspoorten die zijn geconfigureerd in Hallo NET in tijd beleid aanvragen.</span><span class="sxs-lookup"><span data-stu-id="730a8-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="730a8-173">Elke poort heeft een maximale toegestane tijd die is afgeleid van Hallo NET in tijd beleid.</span><span class="sxs-lookup"><span data-stu-id="730a8-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="730a8-174">Selecteer **poorten openen**.</span><span class="sxs-lookup"><span data-stu-id="730a8-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="730a8-175">Een bewerking in het toegangsbeleid tijd</span><span class="sxs-lookup"><span data-stu-id="730a8-175">Editing a just in time access policy</span></span>

<span data-ttu-id="730a8-176">U kunt wijzigen van een virtuele machine bestaande net in tijd beleid door toe te voegen en een nieuwe poort tooopen configureren voor die VM of door het wijzigen van de andere parameters gerelateerde tooan al poort beveiligd.</span><span class="sxs-lookup"><span data-stu-id="730a8-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="730a8-177">In volgorde tooedit een bestaande alleen bij het beleid van de tijd van een VM hello **geconfigureerde** tabblad wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="730a8-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="730a8-178">Onder **VMs**, selecteer een tooadd VM een poort tooby voor die VM op Hallo drie punten binnen Hallo rij te klikken.</span><span class="sxs-lookup"><span data-stu-id="730a8-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="730a8-179">Hiermee opent u een menu.</span><span class="sxs-lookup"><span data-stu-id="730a8-179">This opens a menu.</span></span>
2. <span data-ttu-id="730a8-180">Selecteer **bewerken** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="730a8-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="730a8-181">Hiermee opent u Hallo **JIT VM-configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="730a8-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![Beleid bewerken][8]

3. <span data-ttu-id="730a8-183">Op Hallo **JIT VM-configuratie** blade, u kunt de bestaande instellingen Hallo van een poort al beveiligde voor installatie zonder toezicht bewerken door te klikken op de poort of u kunt selecteren **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="730a8-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="730a8-184">Hiermee opent u Hallo **toevoegen poortconfiguratie** blade.</span><span class="sxs-lookup"><span data-stu-id="730a8-184">This opens hello **Add port configuration** blade.</span></span>

  ![Een poort toevoegen][7]

4. <span data-ttu-id="730a8-186">Op **toevoegen poortconfiguratie** blade Hallo-poort, protocoltype toegestane bron-IP-adressen en maximale aanvraagtijd identificeren.</span><span class="sxs-lookup"><span data-stu-id="730a8-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="730a8-187">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="730a8-187">Select **OK**.</span></span>
6. <span data-ttu-id="730a8-188">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="730a8-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="730a8-189">Controleren in activiteit voor het openen</span><span class="sxs-lookup"><span data-stu-id="730a8-189">Auditing just in time access activity</span></span>

<span data-ttu-id="730a8-190">U kunt Verkrijg inzicht in de VM-activiteiten logboek zoekactie.</span><span class="sxs-lookup"><span data-stu-id="730a8-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="730a8-191">tooview Logboeken:</span><span class="sxs-lookup"><span data-stu-id="730a8-191">tooview logs:</span></span>

1. <span data-ttu-id="730a8-192">Op Hallo **Just in time VM toegang** blade, selecteer Hallo **geconfigureerde** tabblad.</span><span class="sxs-lookup"><span data-stu-id="730a8-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="730a8-193">Onder **VMs**, selecteert u een VM tooview informatie over door te klikken op Hallo drie punten binnen Hallo rij voor die VM.</span><span class="sxs-lookup"><span data-stu-id="730a8-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="730a8-194">Hiermee opent u een menu.</span><span class="sxs-lookup"><span data-stu-id="730a8-194">This opens a menu.</span></span>
3. <span data-ttu-id="730a8-195">Selecteer **activiteitenlogboek** in Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="730a8-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="730a8-196">Hiermee opent u Hallo **activiteitenlogboek** blade.</span><span class="sxs-lookup"><span data-stu-id="730a8-196">This opens hello **Activity log** blade.</span></span>

![Activiteitenlogboek selecteren][9]

<span data-ttu-id="730a8-198">Hallo **activiteitenlogboek** blade biedt een gefilterde weergave van de vorige bewerkingen voor die VM samen met de tijd, datum en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="730a8-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![Logboek van de activiteit weergeven][5]

<span data-ttu-id="730a8-200">U kunt Hallo logboekgegevens downloaden door te selecteren **Klik hier toodownload alle Hallo items als CSV**.</span><span class="sxs-lookup"><span data-stu-id="730a8-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="730a8-201">Hallo filters wijzigen en selecteer **toepassen** toocreate Zoek- en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="730a8-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="730a8-202">Met behulp van alleen in de tijd VM toegang via PowerShell</span><span class="sxs-lookup"><span data-stu-id="730a8-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="730a8-203">In de volgorde toouse Hallo NET in tijdoplossing via PowerShell, Controleer of er Hallo [nieuwste](/powershell/azure/install-azurerm-ps) Azure PowerShell-versie.</span><span class="sxs-lookup"><span data-stu-id="730a8-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="730a8-204">Nadat u dit doet, moet u tooinstall hello [nieuwste](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center van Hallo PowerShell gallery.</span><span class="sxs-lookup"><span data-stu-id="730a8-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="730a8-205">Configureren van een in tijd beleid voor een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="730a8-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="730a8-206">een tooconfigure in tijd beleid op een specifieke virtuele machine, moet u toorun met deze opdracht in uw PowerShell-sessie: Set-ASCJITAccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="730a8-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="730a8-207">Ga als volgt Hallo cmdlet toolearn meer documentatie.</span><span class="sxs-lookup"><span data-stu-id="730a8-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="730a8-208">Aanvragen van toegang tooa VM</span><span class="sxs-lookup"><span data-stu-id="730a8-208">Requesting access tooa VM</span></span>

<span data-ttu-id="730a8-209">een specifieke virtuele machine die wordt beveiligd met tooaccess Hallo NET in tijdoplossing, moet u toorun met deze opdracht in uw PowerShell-sessie: aanroepen ASCJITAccess.</span><span class="sxs-lookup"><span data-stu-id="730a8-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="730a8-210">Ga als volgt Hallo cmdlet toolearn meer documentatie.</span><span class="sxs-lookup"><span data-stu-id="730a8-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="730a8-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="730a8-211">Next steps</span></span>
<span data-ttu-id="730a8-212">In dit artikel hebt u geleerd hoe alleen bij het VM-toegang in Security Center helpt tijd beheren van toegang tooyour Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="730a8-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="730a8-213">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="730a8-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="730a8-214">[Beveiligingsbeleid instellen](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="730a8-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="730a8-215">[Aanbevelingen voor beveiliging beheren](security-center-recommendations.md) : Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="730a8-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="730a8-216">[Beveiligingsstatus bewaken](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="730a8-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="730a8-217">[Beheren en erop reageren toosecurity waarschuwingen](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="730a8-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="730a8-218">[Partneroplossingen bewaken](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="730a8-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="730a8-219">[Security Center FAQ](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="730a8-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="730a8-220">[Azure-beveiligingsblog](https://blogs.msdn.microsoft.com/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.</span><span class="sxs-lookup"><span data-stu-id="730a8-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
