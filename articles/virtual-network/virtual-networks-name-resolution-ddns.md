---
title: Dynamische DNS-tooregister hostnamen aaaUsing
description: Deze pagina geeft informatie over hoe tooset van dynamische DNS-tooregister hostnamen in uw eigen DNS-servers.
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="3cebd-103">Gebruik van dynamische DNS-tooregister hostnamen in uw eigen DNS-server</span><span class="sxs-lookup"><span data-stu-id="3cebd-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="3cebd-104">[Azure biedt naamomzetting](virtual-networks-name-resolution-for-vms-and-role-instances.md) voor virtuele machines (VM's) en rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="3cebd-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="3cebd-105">Wanneer uw naamomzetting moet verder dan die worden verstrekt door Azure, kunt u uw eigen DNS-servers opgeven.</span><span class="sxs-lookup"><span data-stu-id="3cebd-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="3cebd-106">Dit biedt u de DNS-oplossing toosuit power tootailor Hallo uw eigen specifieke behoeften.</span><span class="sxs-lookup"><span data-stu-id="3cebd-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="3cebd-107">Bijvoorbeeld, moet u mogelijk tooaccess lokale bronnen via uw Active Directory-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="3cebd-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="3cebd-108">Wanneer uw aangepaste DNS-servers worden gehost als Azure virtuele machines kunnen worden doorgestuurd hostnaam query's voor Hallo hetzelfde vnet tooAzure tooresolve hostnamen.</span><span class="sxs-lookup"><span data-stu-id="3cebd-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="3cebd-109">Als u niet toouse deze route wenst, kunt u uw VM hostnamen in uw DNS-server met behulp van dynamische DNS registreren.</span><span class="sxs-lookup"><span data-stu-id="3cebd-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="3cebd-110">Azure heeft geen Hallo mogelijkheid (bijvoorbeeld referenties) toodirectly records maken in uw DNS-servers, zodat het alternatieve regelingen vaak nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="3cebd-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="3cebd-111">Hier volgen enkele algemene scenario's met alternatieven.</span><span class="sxs-lookup"><span data-stu-id="3cebd-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="3cebd-112">Windows-clients</span><span class="sxs-lookup"><span data-stu-id="3cebd-112">Windows clients</span></span>
<span data-ttu-id="3cebd-113">Niet-domein Windows-clients proberen onbeveiligde dynamische DNS-(DDNS) updates wanneer ze worden opgestart of wanneer hun IP-adres verandert.</span><span class="sxs-lookup"><span data-stu-id="3cebd-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="3cebd-114">Hallo DNS-naam is Hallo hostnaam plus Hallo primaire DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="3cebd-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="3cebd-115">Azure Hallo primaire DNS-achtervoegsel leeg laat, maar u kunt dit instellen in Hallo VM, via Hallo [UI](https://technet.microsoft.com/library/cc794784.aspx) of [met behulp van automatisering](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="3cebd-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="3cebd-116">Domein van de Windows-clients voor het registreren van hun IP-adressen met Hallo-domeincontroller met behulp van beveiligde dynamische DNS.</span><span class="sxs-lookup"><span data-stu-id="3cebd-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="3cebd-117">Hallo lid van domein proces Hallo primaire DNS-achtervoegsel op Hallo client ingesteld en maakt en onderhoudt Hallo-vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="3cebd-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="3cebd-118">Linux-clients</span><span class="sxs-lookup"><span data-stu-id="3cebd-118">Linux clients</span></span>
<span data-ttu-id="3cebd-119">Linux-clients in het algemeen niet registreren bij Hallo DNS-server bij het opstarten, ze wordt ervan uitgegaan dat Hallo DHCP-server heeft het.</span><span class="sxs-lookup"><span data-stu-id="3cebd-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="3cebd-120">Azure DHCP-servers geen Hallo mogelijkheid of referenties tooregister records in uw DNS-server.</span><span class="sxs-lookup"><span data-stu-id="3cebd-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="3cebd-121">U kunt een hulpmiddel *nsupdate*, die is opgenomen in Hallo Bind pakket, toosend dynamische DNS-updates.</span><span class="sxs-lookup"><span data-stu-id="3cebd-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="3cebd-122">Aangezien Hallo dynamische DNS-protocol is gestandaardiseerd, kunt u *nsupdate* zelfs wanneer u gebruikt geen binding op Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="3cebd-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="3cebd-123">U kunt Hallo hooks die worden geleverd door Hallo DHCP-client toocreate gebruiken en onderhouden van Hallo hostnaam Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="3cebd-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="3cebd-124">Tijdens de cyclus van een DHCP-hello, Hallo-client wordt uitgevoerd Hallo-scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="3cebd-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="3cebd-125">Dit kan zijn tooregister Hallo nieuwe IP-adres gebruikt met behulp van *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="3cebd-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="3cebd-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3cebd-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

<span data-ttu-id="3cebd-127">U kunt ook Hallo *nsupdate* opdracht tooperform beveiligde dynamische DNS-updates.</span><span class="sxs-lookup"><span data-stu-id="3cebd-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="3cebd-128">Bijvoorbeeld, wanneer u een Bind DNS-server, een openbaar / persoonlijk sleutelpaar is [gegenereerd](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="3cebd-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="3cebd-129">Hallo DNS-server is [geconfigureerd](http://linux.yyz.us/dns/ddns-server.html) met openbare onderdeel Hallo van Hallo sleutel zodat die er het Hallo-handtekening op Hallo aanvraag kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="3cebd-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="3cebd-130">Moet u Hallo *-k* optie tooprovide Hallo sleutelpaar-te*nsupdate* om Hallo update dynamische DNS-aanvraag toobe ondertekend.</span><span class="sxs-lookup"><span data-stu-id="3cebd-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="3cebd-131">Wanneer u een Windows-DNS-server gebruikt, kunt u Kerberos-verificatie gebruiken Hello *-g* parameter in *nsupdate* (niet beschikbaar in Windows-versie van Hallo *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="3cebd-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="3cebd-132">toodo dit, gebruik *kinit* tooload Hallo referenties (bijvoorbeeld van een [keytab-bestand](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="3cebd-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="3cebd-133">Vervolgens *nsupdate -g* Hallo referenties uit de cache Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="3cebd-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="3cebd-134">Indien nodig, kunt u een DNS-zoekopdracht achtervoegsel tooyour VM's kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3cebd-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="3cebd-135">Hallo DNS-achtervoegsel is opgegeven in Hallo */etc/resolv.conf* bestand.</span><span class="sxs-lookup"><span data-stu-id="3cebd-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="3cebd-136">De meeste Linux-distributies beheren automatisch Hallo inhoud van dit bestand, dus meestal niet worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="3cebd-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="3cebd-137">U kunt echter Hallo achtervoegsel overschrijven met behulp van Hallo DHCP-client *vervangen* opdracht.</span><span class="sxs-lookup"><span data-stu-id="3cebd-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="3cebd-138">toodo dit in */etc/dhcp/dhclient.conf*, toevoegen:</span><span class="sxs-lookup"><span data-stu-id="3cebd-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

