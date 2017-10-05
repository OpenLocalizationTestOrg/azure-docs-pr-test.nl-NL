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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat Update-infrastructuur (RHUI) voor on-demand Red Hat Enterprise Linux virtuele machines in Azure
Virtuele machines die zijn gemaakt op basis van de op aanvraag Red Hat Enterprise Linux (RHEL) afbeeldingen beschikbaar in Azure Marketplace zijn geregistreerd voor toegang tot de Red Hat Update infrastructuur (RHUI) geïmplementeerd in Azure.  De RHEL op aanvraag exemplaren hebben toegang naar een regionaal yum-opslagplaats en kan incrementele updates ontvangen.

De lijst van de opslagplaats yum, die wordt beheerd door RHUI, is geconfigureerd in uw exemplaar RHEL tijdens het inrichten. U hoeft niet te doen van extra configuratie - uitvoeren `yum update` nadat uw RHEL-exemplaar gereed is voor de nieuwste updates downloaden.

> [!NOTE]
> In September 2016 we een bijgewerkte Azure RHUI hebt geïmplementeerd en in januari 2017 we gefaseerde afsluiten van de oudere Azure RHUI gestart. Als u hebt gebruikt de RHEL afbeeldingen (of hun momentopnamen) vanaf September 2016 of hoger - waarschijnlijk is geen actie vereist. Als u echter oudere momentopnamen van virtuele machines hebben, moet de configuratie voor ononderbroken toegang tot de Azure-RHUI worden bijgewerkt.
> 

## <a name="rhui-azure-infrastructure-update"></a>RHUI Azure-infrastructuur bijwerken
Vanaf September 2016 heeft Azure een nieuwe reeks servers met Red Hat Update-infrastructuur (RHUI). Deze servers zijn geïmplementeerd met [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) zodat één eindpunt (rhui-1.microsoft.com) kan worden gebruikt door een virtuele machine ongeacht regio. De installatiekopieën van het nieuwe RHEL betalen naar gebruik (Omslagstelsel) in Azure Marketplace (versies van September 2016 of hoger) verwijzen naar de nieuwe Azure RHUI-servers en geen aanvullende maatregelen vereist.

### <a name="determine-if-action-is-required"></a>Bepalen of de actie vereist is
Als u hebt met het verbinding maken met Azure RHUI van uw virtuele machine in Azure RHEL Omslagstelsel problemen, als volgt te werk
1. Inspecteer de configuratie van de virtuele machine voor Azure RHUI eindpunt

    Controleer of `/etc/yum.repos.d/rh-cloud.repo` bestand bevat een verwijzing naar `rhui-[1-3].microsoft.com` in baseurl van `[rhui-microsoft-azure-rhel*]` gedeelte van het bestand. -Als het gebruikt u de nieuwe Azure-RHUI.

    Als deze verwijzen naar een locatie met het volgende patroon `mirrorlist.*cds[1-4].cloudapp.net` -de update van de configuratie is vereist.

    Als u van de nieuwe configuratie gebruikmaakt en nog steeds geen verbinding met Azure RHUI maken - bestand een ondersteuningsaanvraag met Microsoft of Red Hat.

    > [!NOTE]
    > Toegang tot Azure gehoste RHUI is beperkt tot de virtuele machines binnen [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Als de oude Azure RHUI nog steeds beschikbaar is wanneer u deze controle uitvoert en u wilt automatisch bijwerken van de configuratie, voer de volgende opdracht:

    `sudo yum update RHEL6`of `sudo yum update RHEL7` afhankelijk van de familie RHEL-versie.

3. Als u niet meer verbinding met de oude Azure RHUI maken kunt, volgt u de handmatige stappen in de volgende sectie beschreven.

4. Zorg ervoor dat de configuratie bijwerken op de bron/de momentopname van invloed op een virtuele machine is ingericht uit.

### <a name="phased-shutdown-of-the-old-azure-rhui"></a>Gefaseerde afsluiten van de oude Azure RHUI
Tijdens het afsluiten van de oude Azure RHUI beperken we toegang tot het als volgt:

1. De (ACL) in te stellen van IP-adressen die al verbinding met deze maken toegang verder te beperken. Mogelijke neveneffecten: als u doorgaat met behulp van de oude Azure RHUI - de nieuwe virtuele machines mogelijk niet tot stand te brengen. RHEL-virtuele machines met dynamische IP-adressen die door het afsluiten, toewijzing ongedaan maken/starten sequence nieuwe IP kan ontvangen en daarom ook kan mislukken verbinding maken met de oude Azure RHUI

2. Afsluiten van de mirror contentlevering servers. Mogelijke neveneffecten: als er meer CDSes afgesloten ziet u mogelijk meer `yum update` tijd meer time-outs tot het moment waarop u niet meer verbinding met de oude Azure RHUI maken kunt onderhoud.

### <a name="the-ips-for-the-new-rhui-content-delivery-servers-are"></a>De IP-adressen voor de nieuwe RHUI contentlevering servers zijn
Als u de netwerkconfiguratie voor de toegang verder te beperken van RHEL Omslagstelsel VM's gebruikt, zorg ervoor dat de volgende IP's zijn toegestaan voor `yum update` werken, afhankelijk van de omgeving die u in. 

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

### <a name="manual-update-procedure-to-use-the-new-azure-rhui-servers"></a>Handmatige updateprocedure voor het gebruik van de nieuwe Azure RHUI-servers
Downloaden van de handtekening van de openbare sleutel (via curl)

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Controleer of de gedownloade sleutel

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Controleer de uitvoer, controleert u of `keyid` en `user ID packet`:

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

Installeren van de openbare sleutel

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Downloaden, te controleren en RPM-Client installeren

Download: Voor RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Voor RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Controleren:

```bash
rpm -Kv azureclient.rpm
```

Controleer in de uitvoer die handtekening van het pakket is in orde

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

De RPM installeren

```bash
sudo rpm -U azureclient.rpm
```

Na voltooiing, Controleer of u toegang hebt tot Azure RHUI formulier de virtuele machine

### <a name="all-in-one-script-for-automating-the-preceding-task"></a>Alles in één script voor het automatiseren van de vorige bewerking
Gebruik het volgende script waar nodig voor het automatiseren van de taak voor het bijwerken van invloed op een virtuele machines naar de nieuwe Azure RHUI-servers.

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

## <a name="rhui-overview"></a>Overzicht van RHUI
[Red Hat Update-infrastructuur](https://access.redhat.com/products/red-hat-update-infrastructure) biedt een zeer schaalbare oplossing voor het beheren van inhoud van de opslagplaats yum voor Red Hat Enterprise Linux cloud-exemplaren die worden gehost door providers van Red Hat gecertificeerd Clouds. Op basis van de upstream Pulp-project, kunt RHUI cloudproviders lokaal spiegelen Red Hat gehost opslagplaats inhoud, aangepaste opslagplaatsen met hun eigen inhoud maken en deze opslagplaatsen beschikbaar te maken voor een grote groep met eindgebruikers via een taakverdeling systeem voor verzending van inhoud.

## <a name="regions-where-rhui-is-available"></a>Regio's waar RHUI beschikbaar is
RHUI is beschikbaar in alle regio's waar RHEL op aanvraag installatiekopieën beschikbaar zijn. Bevat momenteel alle openbare regio's die worden weergegeven op de [Azure status dashboard](https://azure.microsoft.com/status/) pagina Azure US Government en Duitse Azure-regio's. RHUI toegang voor virtuele machines die zijn ingericht van RHEL op aanvraag afbeeldingen is opgenomen in de prijs. Beschikbaarheid van extra regionale/national cloud worden bijgewerkt omdat we uitbreiding RHEL op aanvraag beschikbaar in de toekomst.

> [!NOTE]
> Toegang tot Azure gehoste RHUI is beperkt tot de virtuele machines binnen [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Updates downloaden van een andere update opslagplaats
Als u nodig hebt om updates te downloaden vanaf een andere update opslagplaats (in plaats van Azure gehoste RHUI), moet u eerst uw exemplaren van RHUI registratie. Vervolgens moet u opnieuw wilt registreren met de gewenste update-infrastructuur (zoals Red Hat satelliet of Red Hat Customer Portal CDN). U moet toepassing Red Hat abonnementen voor deze services en registratie voor [toegang tot de Cloud Red Hat in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

Volg deze stappen om het register te RHUI en Registreer opnieuw met uw update-infrastructuur:

1. /Etc/yum.repos.d/rh-cloud.repo bewerken en wijzig alle `enabled=1` naar `enabled=0`. Bijvoorbeeld:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. /Etc/yum/pluginconf.d/rhnplugin.conf bewerkt en wijzigt u `enabled=0` naar `enabled=1`.
3. Klik met de gewenste infrastructuur, zoals Red Hat Customer Portal registreren. Ga als volgt Red Hat solution guide op [registreren en een systeem voor Red Hat Customer Portal abonneren](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Toegang tot de Azure gehoste RHUI is opgenomen in de prijs van de installatiekopie RHEL betalen naar gebruik (Omslagstelsel). De registratie van een Omslagstelsel RHEL VM van de Azure gehoste RHUI, komt de virtuele machine niet converteren naar type Bring-Your-eigenaar-License (BYOL) VM. Als u dezelfde virtuele machine met een andere bron van updates registreert u dubbele kosten kan aangaan: de eerste keer dat voor Azure RHEL software kosten en de tweede keer voor Red Hat abonnementen. 
> 
> Als u consistent moet een update-infrastructuur dan gebruiken Azure gehoste RHUI kunt maken en implementeren van uw eigen installatiekopieën (BYOL-type), zoals beschreven in [maken en uploaden Red Hat virtuele-machinenaam voor Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artikel.
> 

## <a name="next-steps"></a>Volgende stappen
Een Red Hat Enterprise Linux VM maken vanuit Azure Marketplace betalen naar gebruik installatiekopie en gebruik Azure gehoste RHUI gaat u naar [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). U mag gebruiken `yum update` in uw exemplaar RHEL zonder aanvullende instellingen.

