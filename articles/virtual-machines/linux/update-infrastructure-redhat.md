---
title: aaaRed Hat Update-infrastructuur (RHUI) | Microsoft Docs
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
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="6a305-103">Red Hat Update-infrastructuur (RHUI) voor on-demand Red Hat Enterprise Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="6a305-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="6a305-104">Virtuele machines die zijn gemaakt op basis van Hallo op aanvraag Red Hat Enterprise Linux (RHEL) installatiekopieën beschikbaar in Azure Marketplace zijn geregistreerde tooaccess Hallo Red Hat Update infrastructuur (RHUI) geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="6a305-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="6a305-105">Hallo op aanvraag RHEL exemplaren hebben toegang tot tooa regionale yum opslagplaats en kunnen tooreceive incrementele updates.</span><span class="sxs-lookup"><span data-stu-id="6a305-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="6a305-106">Hallo yum opslagplaats lijst, die wordt beheerd door RHUI, is geconfigureerd in uw exemplaar RHEL tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="6a305-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="6a305-107">U hoeft niet toodo extra configuratie - uitvoeren `yum update` nadat uw RHEL-exemplaar gereed tooget Hallo meest recente updates is.</span><span class="sxs-lookup"><span data-stu-id="6a305-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="6a305-108">In September 2016 we een bijgewerkte Azure RHUI hebt geïmplementeerd en in januari 2017 we gefaseerde afsluiten Hallo gestart oudere Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="6a305-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="6a305-109">Als u hebt gebruikt Hallo RHEL installatiekopieën (of hun momentopnamen) vanaf September 2016 of hoger - waarschijnlijk is geen actie vereist.</span><span class="sxs-lookup"><span data-stu-id="6a305-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="6a305-110">Als u echter oudere momentopnamen van virtuele machines hebben, moet hun configuratie toobe bijgewerkt in verband met ononderbroken toegang toohello Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="6a305-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="6a305-111">RHUI Azure-infrastructuur bijwerken</span><span class="sxs-lookup"><span data-stu-id="6a305-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="6a305-112">Vanaf September 2016 heeft Azure een nieuwe reeks servers met Red Hat Update-infrastructuur (RHUI).</span><span class="sxs-lookup"><span data-stu-id="6a305-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="6a305-113">Deze servers zijn geïmplementeerd met [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) zodat één eindpunt (rhui-1.microsoft.com) kan worden gebruikt door een virtuele machine ongeacht regio.</span><span class="sxs-lookup"><span data-stu-id="6a305-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="6a305-114">installatiekopieën van het nieuwe RHEL betalen naar gebruik (Omslagstelsel) in hello Azure Marketplace (versies van September 2016 of hoger) punt toohello nieuwe Azure RHUI servers Hallo en geen aanvullende maatregelen vereist.</span><span class="sxs-lookup"><span data-stu-id="6a305-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="6a305-115">Bepalen of de actie vereist is</span><span class="sxs-lookup"><span data-stu-id="6a305-115">Determine if action is required</span></span>
<span data-ttu-id="6a305-116">Als u hebt met het tooAzure RHUI verbinding te maken van uw virtuele machine in Azure RHEL Omslagstelsel problemen, als volgt te werk</span><span class="sxs-lookup"><span data-stu-id="6a305-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="6a305-117">Inspecteer de configuratie van de virtuele machine voor Azure RHUI eindpunt</span><span class="sxs-lookup"><span data-stu-id="6a305-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="6a305-118">Controleer of `/etc/yum.repos.d/rh-cloud.repo` bestand bevat een verwijzing naar te`rhui-[1-3].microsoft.com` in baseurl van `[rhui-microsoft-azure-rhel*]` sectie van het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="6a305-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="6a305-119">Als het is - u Hallo nieuwe Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="6a305-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="6a305-120">Als deze wijzen tooa locatie Hello patroon volgen `mirrorlist.*cds[1-4].cloudapp.net` -Hallo configuratie-update is vereist.</span><span class="sxs-lookup"><span data-stu-id="6a305-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="6a305-121">Als u van de nieuwe configuratie Hallo gebruikmaakt en nog steeds geen verbinding tooAzure RHUI - bestand een ondersteuningsaanvraag met Microsoft of Red Hat.</span><span class="sxs-lookup"><span data-stu-id="6a305-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6a305-122">Toegang tooAzure gehost RHUI is beperkt toohello virtuele machines binnen [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6a305-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="6a305-123">Als hello oude Azure RHUI nog steeds beschikbaar is wanneer u deze controle uitvoert en u tooautomatically update Hallo-configuratie wilt uitvoeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6a305-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="6a305-124">`sudo yum update RHEL6`of `sudo yum update RHEL7` , afhankelijk van familie Hallo RHEL-versie.</span><span class="sxs-lookup"><span data-stu-id="6a305-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="6a305-125">Als u niet meer verbinding maken met toohello oude Azure RHUI, volg Hallo handmatige stappen die worden beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="6a305-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="6a305-126">Zorg ervoor dat tooupdate Hallo-configuratie op Hallo bron/de momentopname van invloed op een virtuele machine is ingericht uit.</span><span class="sxs-lookup"><span data-stu-id="6a305-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="6a305-127">Gefaseerde afsluiten van de oude Azure RHUI Hallo</span><span class="sxs-lookup"><span data-stu-id="6a305-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="6a305-128">Tijdens het afsluiten van Hallo Hallo oude Azure RHUI we beperken tooit als volgt openen:</span><span class="sxs-lookup"><span data-stu-id="6a305-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="6a305-129">De toegang (ACL) tooset IP-adressen die al verbinding tooit maken verder te beperken.</span><span class="sxs-lookup"><span data-stu-id="6a305-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="6a305-130">Mogelijke neveneffecten: als u met behulp van doorgaat de oude Azure RHUI Hallo - uw nieuwe VM's zijn mogelijk niet kunnen tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="6a305-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="6a305-131">RHEL-virtuele machines met dynamische IP-adressen die door het afsluiten, toewijzing ongedaan maken/starten sequence nieuwe IP kan ontvangen en daarom ook kan mislukken tooconnect toohello oude Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="6a305-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="6a305-132">Afsluiten van de mirror contentlevering servers.</span><span class="sxs-lookup"><span data-stu-id="6a305-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="6a305-133">Mogelijke neveneffecten: als er meer CDSes afgesloten ziet u mogelijk meer `yum update` onderhoud tijd meer time-outs tot Hallo wijst wanneer u niet meer verbinding maken met toohello oude Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="6a305-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="6a305-134">Hallo IP-adressen voor Hallo-servers voor het leveren van inhoud van nieuwe RHUI zijn</span><span class="sxs-lookup"><span data-stu-id="6a305-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="6a305-135">Als u van network configuration toofurther gebruikmaakt toegang beperken van RHEL Omslagstelsel VM's en zorg ervoor dat de volgende IP-adressen Hallo zijn toegestaan voor `yum update` toowork, afhankelijk van het Hallo-omgeving in.</span><span class="sxs-lookup"><span data-stu-id="6a305-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="6a305-136">Handmatige update procedure toouse Hallo nieuwe Azure RHUI servers</span><span class="sxs-lookup"><span data-stu-id="6a305-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="6a305-137">Download (via curl) Hallo openbare sleutel handtekening</span><span class="sxs-lookup"><span data-stu-id="6a305-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="6a305-138">Controleer of de sleutel Hallo gedownload</span><span class="sxs-lookup"><span data-stu-id="6a305-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="6a305-139">Hallo uitvoer controleren, controleert u of `keyid` en `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="6a305-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

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

<span data-ttu-id="6a305-140">De openbare sleutel Hallo installeren</span><span class="sxs-lookup"><span data-stu-id="6a305-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="6a305-141">Downloaden, te controleren en RPM-Client installeren</span><span class="sxs-lookup"><span data-stu-id="6a305-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="6a305-142">Download: Voor RHEL 6</span><span class="sxs-lookup"><span data-stu-id="6a305-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="6a305-143">Voor RHEL 7</span><span class="sxs-lookup"><span data-stu-id="6a305-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="6a305-144">Controleren:</span><span class="sxs-lookup"><span data-stu-id="6a305-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="6a305-145">Controleer in de uitvoer die handtekening Hallo pakket is OK</span><span class="sxs-lookup"><span data-stu-id="6a305-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="6a305-146">Hallo RPM installeren</span><span class="sxs-lookup"><span data-stu-id="6a305-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="6a305-147">Na voltooiing, Controleer of u toegang hebt tot Azure RHUI formulier Hallo VM</span><span class="sxs-lookup"><span data-stu-id="6a305-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="6a305-148">Alles in één script voor het automatiseren van Hallo voorafgaand aan de taak</span><span class="sxs-lookup"><span data-stu-id="6a305-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="6a305-149">Hallo script volgen als benodigde tooautomate Hallo taak voor het bijwerken van de betrokken virtuele machines toohello nieuwe Azure RHUI servers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6a305-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

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

## <a name="rhui-overview"></a><span data-ttu-id="6a305-150">Overzicht van RHUI</span><span class="sxs-lookup"><span data-stu-id="6a305-150">RHUI overview</span></span>
<span data-ttu-id="6a305-151">[Red Hat Update-infrastructuur](https://access.redhat.com/products/red-hat-update-infrastructure) biedt een zeer schaalbare oplossing toomanage yum opslagplaats inhoud voor Red Hat Enterprise Linux cloud-exemplaren die worden gehost door providers van Red Hat gecertificeerd Clouds.</span><span class="sxs-lookup"><span data-stu-id="6a305-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="6a305-152">Op basis van Hallo upstream Pulp project, RHUI kunt cloudproviders toolocally mirror Red Hat gehost opslagplaats inhoud, aangepaste opslagplaatsen met hun eigen inhoud maken en deze opslagplaatsen beschikbaar tooa grote groep eindgebruikers via een taakverdeling maken systeem voor verzending van inhoud.</span><span class="sxs-lookup"><span data-stu-id="6a305-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="6a305-153">Regio's waar RHUI beschikbaar is</span><span class="sxs-lookup"><span data-stu-id="6a305-153">Regions where RHUI is available</span></span>
<span data-ttu-id="6a305-154">RHUI is beschikbaar in alle regio's waar RHEL op aanvraag installatiekopieën beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="6a305-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="6a305-155">Bevat momenteel alle openbare regio's die worden weergegeven op Hallo [Azure status dashboard](https://azure.microsoft.com/status/) pagina Azure US Government en Duitse Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="6a305-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="6a305-156">RHUI toegang voor virtuele machines die zijn ingericht van RHEL op aanvraag afbeeldingen is opgenomen in de prijs.</span><span class="sxs-lookup"><span data-stu-id="6a305-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="6a305-157">Beschikbaarheid van extra regionale/national cloud worden bijgewerkt omdat we RHEL op aanvraag beschikbaar in toekomstige Hallo uitvouwen.</span><span class="sxs-lookup"><span data-stu-id="6a305-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="6a305-158">Toegang tooAzure gehost RHUI is beperkt toohello virtuele machines binnen [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6a305-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="6a305-159">Updates downloaden van een andere update opslagplaats</span><span class="sxs-lookup"><span data-stu-id="6a305-159">Get updates from another update repository</span></span>
<span data-ttu-id="6a305-160">Als u moet tooget updates vanaf een andere update opslagplaats (in plaats van Azure gehoste RHUI), moet u eerst toounregister uw exemplaren van RHUI.</span><span class="sxs-lookup"><span data-stu-id="6a305-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="6a305-161">Moet u toore registreren ze met Hallo gewenste update-infrastructuur (zoals Red Hat satelliet of Red Hat Customer Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="6a305-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="6a305-162">U moet toepassing Red Hat abonnementen voor deze services en registratie voor [toegang tot de Cloud Red Hat in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="6a305-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="6a305-163">Ga als volgt toounregister RHUI en Registreer opnieuw tooyour update-infrastructuur:</span><span class="sxs-lookup"><span data-stu-id="6a305-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="6a305-164">/Etc/yum.repos.d/rh-cloud.repo bewerken en wijzig alle `enabled=1` te`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="6a305-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="6a305-165">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6a305-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="6a305-166">/Etc/yum/pluginconf.d/rhnplugin.conf bewerkt en wijzigt u `enabled=0` te`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="6a305-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="6a305-167">Vervolgens registreren met de gewenste Hallo-infrastructuur, zoals Red Hat Customer Portal.</span><span class="sxs-lookup"><span data-stu-id="6a305-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="6a305-168">Ga als volgt Red Hat solution guide op [hoe tooregister en zich abonneren een systeem toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="6a305-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="6a305-169">Toegang toohello Azure gehoste RHUI is opgenomen in Hallo RHEL betalen naar gebruik (Omslagstelsel) installatiekopie prijs.</span><span class="sxs-lookup"><span data-stu-id="6a305-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="6a305-170">De registratie van een VM Omslagstelsel RHEL van hello Azure gehoste RHUI, biedt Hallo virtuele machine niet converteren naar type Bring-Your-eigenaar-License (BYOL) VM.</span><span class="sxs-lookup"><span data-stu-id="6a305-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="6a305-171">Als u zich registreert Hallo dezelfde virtuele machine met een andere bron van updates u het dubbele kosten kan aangaan: de eerste keer voor Azure RHEL software kosten en Hallo tweede keer voor Red Hat abonnementen.</span><span class="sxs-lookup"><span data-stu-id="6a305-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="6a305-172">Als u toouse consistent moet een update-infrastructuur dan Azure gehoste RHUI kunt maken en implementeren van uw eigen installatiekopieën (BYOL-type), zoals beschreven in [maken en uploaden Red Hat virtuele-machinenaam voor Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikel.</span><span class="sxs-lookup"><span data-stu-id="6a305-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="6a305-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6a305-173">Next steps</span></span>
<span data-ttu-id="6a305-174">een Red Hat Enterprise Linux VM van betalen naar gebruik van Azure Marketplace-installatiekopie en gebruik Azure gehoste RHUI toocreate te gaan[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="6a305-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="6a305-175">U zult kunnen toouse `yum update` in uw exemplaar RHEL zonder aanvullende instellingen.</span><span class="sxs-lookup"><span data-stu-id="6a305-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

