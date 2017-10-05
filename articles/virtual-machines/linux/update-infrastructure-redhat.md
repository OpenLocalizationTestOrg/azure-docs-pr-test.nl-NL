---
title: Red Hat Update-infrastructuur (RHUI) | Microsoft Docs
description: Meer informatie over Red Hat Update infrastructuur (RHUI) voor op aanvraag Red Hat Enterprise Linux-exemplaren in Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: 07815d691ffe57f0349f7a90ced4a2fcc1ab834f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="10c37-103">Red Hat Update-infrastructuur (RHUI) voor on-demand Red Hat Enterprise Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="10c37-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="10c37-104">Virtuele machines die zijn gemaakt op basis van de op aanvraag Red Hat Enterprise Linux (RHEL) afbeeldingen beschikbaar in Azure Marketplace zijn geregistreerd voor toegang tot de Red Hat Update infrastructuur (RHUI) geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="10c37-104">Virtual machines created from the on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered to access the Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="10c37-105">De RHEL op aanvraag exemplaren hebben toegang naar een regionaal yum-opslagplaats en kan incrementele updates ontvangen.</span><span class="sxs-lookup"><span data-stu-id="10c37-105">The on-demand RHEL instances have access to a regional yum repository and able to receive incremental updates.</span></span>

<span data-ttu-id="10c37-106">De lijst van de opslagplaats yum, die wordt beheerd door RHUI, is geconfigureerd in uw exemplaar RHEL tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="10c37-106">The yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="10c37-107">U hoeft niet te doen van extra configuratie - uitvoeren `yum update` nadat uw RHEL-exemplaar gereed is voor de nieuwste updates downloaden.</span><span class="sxs-lookup"><span data-stu-id="10c37-107">You don't need to do any additional configuration - run `yum update` after your RHEL instance is ready to get the latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="10c37-108">In September 2016 we een bijgewerkte Azure RHUI hebt geïmplementeerd en in januari 2017 we gefaseerde afsluiten van de oudere Azure RHUI gestart.</span><span class="sxs-lookup"><span data-stu-id="10c37-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of the older Azure RHUI.</span></span> <span data-ttu-id="10c37-109">Als u hebt gebruikt de RHEL afbeeldingen (of hun momentopnamen) vanaf September 2016 of hoger - waarschijnlijk is geen actie vereist.</span><span class="sxs-lookup"><span data-stu-id="10c37-109">If you have been using the RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="10c37-110">Als u echter oudere momentopnamen van virtuele machines hebben, moet de configuratie voor ononderbroken toegang tot de Azure-RHUI worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="10c37-110">If, however, you have older snapshots/VMs, their configuration needs to be updated for uninterrupted access to the Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="10c37-111">RHUI Azure-infrastructuur bijwerken</span><span class="sxs-lookup"><span data-stu-id="10c37-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="10c37-112">Vanaf September 2016 heeft Azure een nieuwe reeks servers met Red Hat Update-infrastructuur (RHUI).</span><span class="sxs-lookup"><span data-stu-id="10c37-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="10c37-113">Deze servers zijn geïmplementeerd met [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) zodat één eindpunt (rhui-1.microsoft.com) kan worden gebruikt door een virtuele machine ongeacht regio.</span><span class="sxs-lookup"><span data-stu-id="10c37-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="10c37-114">De installatiekopieën van het nieuwe RHEL betalen naar gebruik (Omslagstelsel) in Azure Marketplace (versies van September 2016 of hoger) verwijzen naar de nieuwe Azure RHUI-servers en geen aanvullende maatregelen vereist.</span><span class="sxs-lookup"><span data-stu-id="10c37-114">The new RHEL Pay-As-You-Go (PAYG) images in the Azure Marketplace (versions dated September 2016 or later) point to the new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="10c37-115">Bepalen of de actie vereist is</span><span class="sxs-lookup"><span data-stu-id="10c37-115">Determine if action is required</span></span>
<span data-ttu-id="10c37-116">Als u hebt met het verbinding maken met Azure RHUI van uw virtuele machine in Azure RHEL Omslagstelsel problemen, als volgt te werk</span><span class="sxs-lookup"><span data-stu-id="10c37-116">If you are experiencing problems connecting to Azure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="10c37-117">Inspecteer de configuratie van de virtuele machine voor Azure RHUI eindpunt</span><span class="sxs-lookup"><span data-stu-id="10c37-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="10c37-118">Controleer of `/etc/yum.repos.d/rh-cloud.repo` bestand bevat een verwijzing naar `rhui-[1-3].microsoft.com` in baseurl van `[rhui-microsoft-azure-rhel*]` gedeelte van het bestand.</span><span class="sxs-lookup"><span data-stu-id="10c37-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference to `rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of the file.</span></span> <span data-ttu-id="10c37-119">-Als het gebruikt u de nieuwe Azure-RHUI.</span><span class="sxs-lookup"><span data-stu-id="10c37-119">If it is - you are using the new Azure RHUI.</span></span>

    <span data-ttu-id="10c37-120">Als deze verwijzen naar een locatie met het volgende patroon `mirrorlist.*cds[1-4].cloudapp.net` -de update van de configuratie is vereist.</span><span class="sxs-lookup"><span data-stu-id="10c37-120">If it pointing to a location with the following pattern `mirrorlist.*cds[1-4].cloudapp.net` - the configuration update is required.</span></span>

    <span data-ttu-id="10c37-121">Als u van de nieuwe configuratie gebruikmaakt en nog steeds geen verbinding met Azure RHUI maken - bestand een ondersteuningsaanvraag met Microsoft of Red Hat.</span><span class="sxs-lookup"><span data-stu-id="10c37-121">If you are using the new configuration and still cannot connect to Azure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10c37-122">Toegang tot Azure gehoste RHUI is beperkt tot de virtuele machines binnen [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="10c37-122">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="10c37-123">Als de oude Azure RHUI nog steeds beschikbaar is wanneer u deze controle uitvoert en u wilt automatisch bijwerken van de configuratie, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="10c37-123">If the old Azure RHUI is still available when you do this check and you would like to automatically update the configuration, execute the following command:</span></span>

    <span data-ttu-id="10c37-124">`sudo yum update RHEL6`of `sudo yum update RHEL7` afhankelijk van de familie RHEL-versie.</span><span class="sxs-lookup"><span data-stu-id="10c37-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on the RHEL family version.</span></span>

3. <span data-ttu-id="10c37-125">Als u niet meer verbinding met de oude Azure RHUI maken kunt, volgt u de handmatige stappen in de volgende sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="10c37-125">If you can no longer connect to the old Azure RHUI, follow the manual steps described in the next section.</span></span>

4. <span data-ttu-id="10c37-126">Zorg ervoor dat de configuratie bijwerken op de bron/de momentopname van invloed op een virtuele machine is ingericht uit.</span><span class="sxs-lookup"><span data-stu-id="10c37-126">Make sure to update the configuration on the source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-the-old-azure-rhui"></a><span data-ttu-id="10c37-127">Gefaseerde afsluiten van de oude Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="10c37-127">Phased shutdown of the old Azure RHUI</span></span>
<span data-ttu-id="10c37-128">Tijdens het afsluiten van de oude Azure RHUI beperken we toegang tot het als volgt:</span><span class="sxs-lookup"><span data-stu-id="10c37-128">During the shutdown of the old Azure RHUI we restrict access to it as follows:</span></span>

1. <span data-ttu-id="10c37-129">De (ACL) in te stellen van IP-adressen die al verbinding met deze maken toegang verder te beperken.</span><span class="sxs-lookup"><span data-stu-id="10c37-129">Further restrict access (ACL) to set of IP addresses that are already connecting to it.</span></span> <span data-ttu-id="10c37-130">Mogelijke neveneffecten: als u doorgaat met behulp van de oude Azure RHUI - de nieuwe virtuele machines mogelijk niet tot stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="10c37-130">Possible side-effects: if you continue using the old Azure RHUI - your new VMs may not be able to connect to it.</span></span> <span data-ttu-id="10c37-131">RHEL-virtuele machines met dynamische IP-adressen die door het afsluiten, toewijzing ongedaan maken/starten sequence nieuwe IP kan ontvangen en daarom ook kan mislukken verbinding maken met de oude Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="10c37-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing to connect to the old Azure RHUI</span></span>

2. <span data-ttu-id="10c37-132">Afsluiten van de mirror contentlevering servers.</span><span class="sxs-lookup"><span data-stu-id="10c37-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="10c37-133">Mogelijke neveneffecten: als er meer CDSes afgesloten ziet u mogelijk meer `yum update` tijd meer time-outs tot het moment waarop u niet meer verbinding met de oude Azure RHUI maken kunt onderhoud.</span><span class="sxs-lookup"><span data-stu-id="10c37-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until the point when you can no longer connect to the old Azure RHUI.</span></span>

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="10c37-134">De IP-adressen voor de nieuwe RHUI contentlevering servers zijn</span><span class="sxs-lookup"><span data-stu-id="10c37-134">The IPs for the new RHUI content delivery servers are</span></span>
<span data-ttu-id="10c37-135">Als u de netwerkconfiguratie voor de toegang verder te beperken van RHEL Omslagstelsel VM's gebruikt, zorg ervoor dat de volgende IP's zijn toegestaan voor `yum update` werken, afhankelijk van de omgeving die u in.</span><span class="sxs-lookup"><span data-stu-id="10c37-135">If you are using network configuration to further restrict access from RHEL PAYG VMs, make sure the following IPs are allowed for `yum update` to work depending on the environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a><span data-ttu-id="10c37-136">Handmatige updateprocedure voor het gebruik van de nieuwe Azure RHUI-servers</span><span class="sxs-lookup"><span data-stu-id="10c37-136">Manual update procedure to use the new Azure RHUI servers</span></span>
<span data-ttu-id="10c37-137">Downloaden van de handtekening van de openbare sleutel (via curl)</span><span class="sxs-lookup"><span data-stu-id="10c37-137">Download (via curl) the public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="10c37-138">Controleer of de gedownloade sleutel</span><span class="sxs-lookup"><span data-stu-id="10c37-138">Verify the downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="10c37-139">Controleer de uitvoer, controleert u of `keyid` en `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="10c37-139">Check the output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="10c37-140">Installeren van de openbare sleutel</span><span class="sxs-lookup"><span data-stu-id="10c37-140">Install the public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="10c37-141">Downloaden, te controleren en RPM-Client installeren</span><span class="sxs-lookup"><span data-stu-id="10c37-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="10c37-142">Download: Voor RHEL 6</span><span class="sxs-lookup"><span data-stu-id="10c37-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="10c37-143">Voor RHEL 7</span><span class="sxs-lookup"><span data-stu-id="10c37-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="10c37-144">Controleren:</span><span class="sxs-lookup"><span data-stu-id="10c37-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="10c37-145">Controleer in de uitvoer die handtekening van het pakket is in orde</span><span class="sxs-lookup"><span data-stu-id="10c37-145">Check in output that signature of the package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="10c37-146">De RPM installeren</span><span class="sxs-lookup"><span data-stu-id="10c37-146">Install the RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="10c37-147">Na voltooiing, Controleer of u toegang hebt tot Azure RHUI formulier de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="10c37-147">Upon completion, verify that you can access Azure RHUI form the VM</span></span>

### <a name="all-in-one-script-for-automating-the-preceding-task"></a><span data-ttu-id="10c37-148">Alles in één script voor het automatiseren van de vorige bewerking</span><span class="sxs-lookup"><span data-stu-id="10c37-148">All-in-one script for automating the preceding task</span></span>
<span data-ttu-id="10c37-149">Gebruik het volgende script waar nodig voor het automatiseren van de taak voor het bijwerken van invloed op een virtuele machines naar de nieuwe Azure RHUI-servers.</span><span class="sxs-lookup"><span data-stu-id="10c37-149">Use the following script as needed to automate the task of updating affected VMs to the new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="10c37-150">Overzicht van RHUI</span><span class="sxs-lookup"><span data-stu-id="10c37-150">RHUI overview</span></span>
<span data-ttu-id="10c37-151">[Red Hat Update-infrastructuur](https://access.redhat.com/products/red-hat-update-infrastructure) biedt een zeer schaalbare oplossing voor het beheren van inhoud van de opslagplaats yum voor Red Hat Enterprise Linux cloud-exemplaren die worden gehost door providers van Red Hat gecertificeerd Clouds.</span><span class="sxs-lookup"><span data-stu-id="10c37-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution to manage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="10c37-152">Op basis van de upstream Pulp-project, kunt RHUI cloudproviders lokaal spiegelen Red Hat gehost opslagplaats inhoud, aangepaste opslagplaatsen met hun eigen inhoud maken en deze opslagplaatsen beschikbaar te maken voor een grote groep met eindgebruikers via een taakverdeling systeem voor verzending van inhoud.</span><span class="sxs-lookup"><span data-stu-id="10c37-152">Based on the upstream Pulp project, RHUI allows cloud providers to locally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available to a large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="10c37-153">Regio's waar RHUI beschikbaar is</span><span class="sxs-lookup"><span data-stu-id="10c37-153">Regions where RHUI is available</span></span>
<span data-ttu-id="10c37-154">RHUI is beschikbaar in alle regio's waar RHEL op aanvraag installatiekopieën beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="10c37-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="10c37-155">Bevat momenteel alle openbare regio's die worden weergegeven op de [Azure status dashboard](https://azure.microsoft.com/status/) pagina Azure US Government en Duitse Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="10c37-155">It currently includes all public regions listed on the [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="10c37-156">RHUI toegang voor virtuele machines die zijn ingericht van RHEL op aanvraag afbeeldingen is opgenomen in de prijs.</span><span class="sxs-lookup"><span data-stu-id="10c37-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="10c37-157">Beschikbaarheid van extra regionale/national cloud worden bijgewerkt omdat we uitbreiding RHEL op aanvraag beschikbaar in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="10c37-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="10c37-158">Toegang tot Azure gehoste RHUI is beperkt tot de virtuele machines binnen [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="10c37-158">Access to Azure-hosted RHUI is limited to the VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="10c37-159">Updates downloaden van een andere update opslagplaats</span><span class="sxs-lookup"><span data-stu-id="10c37-159">Get updates from another update repository</span></span>
<span data-ttu-id="10c37-160">Als u nodig hebt om updates te downloaden vanaf een andere update opslagplaats (in plaats van Azure gehoste RHUI), moet u eerst uw exemplaren van RHUI registratie.</span><span class="sxs-lookup"><span data-stu-id="10c37-160">If you need to get updates from a different update repository (instead of Azure-hosted RHUI), first you need to unregister your instances from RHUI.</span></span> <span data-ttu-id="10c37-161">Vervolgens moet u opnieuw wilt registreren met de gewenste update-infrastructuur (zoals Red Hat satelliet of Red Hat Customer Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="10c37-161">Then you need to re-register them with the desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="10c37-162">U moet toepassing Red Hat abonnementen voor deze services en registratie voor [toegang tot de Cloud Red Hat in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="10c37-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="10c37-163">Volg deze stappen om het register te RHUI en Registreer opnieuw met uw update-infrastructuur:</span><span class="sxs-lookup"><span data-stu-id="10c37-163">To unregister RHUI and reregister to your update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="10c37-164">/Etc/yum.repos.d/rh-cloud.repo bewerken en wijzig alle `enabled=1` naar `enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="10c37-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` to `enabled=0`.</span></span> <span data-ttu-id="10c37-165">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="10c37-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="10c37-166">/Etc/yum/pluginconf.d/rhnplugin.conf bewerkt en wijzigt u `enabled=0` naar `enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="10c37-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` to `enabled=1`.</span></span>
3. <span data-ttu-id="10c37-167">Klik met de gewenste infrastructuur, zoals Red Hat Customer Portal registreren.</span><span class="sxs-lookup"><span data-stu-id="10c37-167">Then register with the desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="10c37-168">Ga als volgt Red Hat solution guide op [registreren en een systeem voor Red Hat Customer Portal abonneren](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="10c37-168">Follow Red Hat solution guide on [how to register and subscribe a system to the Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="10c37-169">Toegang tot de Azure gehoste RHUI is opgenomen in de prijs van de installatiekopie RHEL betalen naar gebruik (Omslagstelsel).</span><span class="sxs-lookup"><span data-stu-id="10c37-169">Access to the Azure-hosted RHUI is included in the RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="10c37-170">De registratie van een Omslagstelsel RHEL VM van de Azure gehoste RHUI, komt de virtuele machine niet converteren naar type Bring-Your-eigenaar-License (BYOL) VM.</span><span class="sxs-lookup"><span data-stu-id="10c37-170">Unregistering a PAYG RHEL VM from the Azure-hosted RHUI does not convert the virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="10c37-171">Als u dezelfde virtuele machine met een andere bron van updates registreert u dubbele kosten kan aangaan: de eerste keer dat voor Azure RHEL software kosten en de tweede keer voor Red Hat abonnementen.</span><span class="sxs-lookup"><span data-stu-id="10c37-171">If you register the same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and the second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="10c37-172">Als u consistent moet een update-infrastructuur dan gebruiken Azure gehoste RHUI kunt maken en implementeren van uw eigen installatiekopieën (BYOL-type), zoals beschreven in [maken en uploaden Red Hat virtuele-machinenaam voor Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikel.</span><span class="sxs-lookup"><span data-stu-id="10c37-172">If you consistently need to use an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="10c37-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10c37-173">Next steps</span></span>
<span data-ttu-id="10c37-174">Een Red Hat Enterprise Linux VM maken vanuit Azure Marketplace betalen naar gebruik installatiekopie en gebruik Azure gehoste RHUI gaat u naar [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="10c37-174">To create a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="10c37-175">U mag gebruiken `yum update` in uw exemplaar RHEL zonder aanvullende instellingen.</span><span class="sxs-lookup"><span data-stu-id="10c37-175">You will be able to use `yum update` in your RHEL instance without any additional setup.</span></span>

