---
title: Met behulp van dynamische DNS hostnamen registreren
description: Deze pagina geeft informatie over het instellen van dynamische DNS hostnamen in uw eigen DNS-servers registreren.
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
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="502d0-103">Met behulp van dynamische DNS hostnamen in uw eigen DNS-server registreren</span><span class="sxs-lookup"><span data-stu-id="502d0-103">Using Dynamic DNS to register hostnames in your own DNS server</span></span>
<span data-ttu-id="502d0-104">[Azure biedt naamomzetting](virtual-networks-name-resolution-for-vms-and-role-instances.md) voor virtuele machines (VM's) en rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="502d0-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="502d0-105">Wanneer uw naamomzetting moet verder dan die worden verstrekt door Azure, kunt u uw eigen DNS-servers opgeven.</span><span class="sxs-lookup"><span data-stu-id="502d0-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="502d0-106">Hierdoor kunt u de bevoegdheid om aan te passen van uw DNS-oplossing aanpassen aan uw eigen specifieke behoeften.</span><span class="sxs-lookup"><span data-stu-id="502d0-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="502d0-107">U wilt bijvoorbeeld toegang tot lokale bronnen via uw Active Directory-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="502d0-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="502d0-108">Wanneer uw aangepaste DNS-servers worden gehost als Azure virtuele machines kunt u de hostnaam van een query uitgevoerd naar hetzelfde vnet doorsturen naar Azure hostnamen omzetten.</span><span class="sxs-lookup"><span data-stu-id="502d0-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span></span> <span data-ttu-id="502d0-109">Als u niet deze route gebruikt wilt, kunt u uw VM hostnamen in uw DNS-server met behulp van dynamische DNS registreren.</span><span class="sxs-lookup"><span data-stu-id="502d0-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="502d0-110">Azure heeft de mogelijkheid (bijvoorbeeld referenties) geen rechtstreeks om records te maken in uw DNS-servers, zodat het alternatieve regelingen vaak nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="502d0-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="502d0-111">Hier volgen enkele algemene scenario's met alternatieven.</span><span class="sxs-lookup"><span data-stu-id="502d0-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="502d0-112">Windows-clients</span><span class="sxs-lookup"><span data-stu-id="502d0-112">Windows clients</span></span>
<span data-ttu-id="502d0-113">Niet-domein Windows-clients proberen onbeveiligde dynamische DNS-(DDNS) updates wanneer ze worden opgestart of wanneer hun IP-adres verandert.</span><span class="sxs-lookup"><span data-stu-id="502d0-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="502d0-114">De DNS-naam is de hostnaam plus het primaire DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="502d0-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="502d0-115">Azure worden de primaire DNS-achtervoegsel leeg gelaten, maar u kunt dit instellen in de virtuele machine de [UI](https://technet.microsoft.com/library/cc794784.aspx) of [met behulp van automatisering](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="502d0-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="502d0-116">Windows-clients domein voor het registreren van hun IP-adressen met de domeincontroller met behulp van beveiligde dynamische DNS.</span><span class="sxs-lookup"><span data-stu-id="502d0-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="502d0-117">Het lid van domein-proces wordt het primaire DNS-achtervoegsel op de client ingesteld en maakt en onderhoudt de vertrouwensrelatie.</span><span class="sxs-lookup"><span data-stu-id="502d0-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="502d0-118">Linux-clients</span><span class="sxs-lookup"><span data-stu-id="502d0-118">Linux clients</span></span>
<span data-ttu-id="502d0-119">Linux-clients in het algemeen niet registreren bij de DNS-server bij het opstarten, ze wordt ervan uitgegaan dat de DHCP-server dit doet.</span><span class="sxs-lookup"><span data-stu-id="502d0-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="502d0-120">Azure DHCP-servers beschikt niet over de mogelijkheid of referenties records te registreren bij uw DNS-server.</span><span class="sxs-lookup"><span data-stu-id="502d0-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span></span>  <span data-ttu-id="502d0-121">U kunt een hulpmiddel *nsupdate*, die is opgenomen in het pakket Bind, om het verzenden van dynamische DNS-updates.</span><span class="sxs-lookup"><span data-stu-id="502d0-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span></span> <span data-ttu-id="502d0-122">U kunt gebruiken omdat het dynamische DNS-protocol is gestandaardiseerd, *nsupdate* zelfs wanneer u niet gebruikt afhankelijk van de DNS-server.</span><span class="sxs-lookup"><span data-stu-id="502d0-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="502d0-123">U kunt de hooks die worden geleverd door de DHCP-client maken en onderhouden van de hostnaam vermelding in de DNS-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="502d0-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="502d0-124">Tijdens de cyclus DHCP, de client voert de scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="502d0-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="502d0-125">Dit kan worden gebruikt voor het registreren van het nieuwe IP-adres met behulp van *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="502d0-125">This can be used to register the new IP address by using *nsupdate*.</span></span> <span data-ttu-id="502d0-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="502d0-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
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

        
        

<span data-ttu-id="502d0-127">U kunt ook de *nsupdate* opdracht voor het uitvoeren van beveiligde dynamische DNS-updates.</span><span class="sxs-lookup"><span data-stu-id="502d0-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span></span> <span data-ttu-id="502d0-128">Bijvoorbeeld, wanneer u een Bind DNS-server, een openbaar / persoonlijk sleutelpaar is [gegenereerd](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="502d0-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="502d0-129">De DNS-server [geconfigureerd](http://linux.yyz.us/dns/ddns-server.html) met het openbare deel van de sleutel, zodat deze de handtekening van de aanvraag kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="502d0-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span></span> <span data-ttu-id="502d0-130">Moet u de *-k* optie in als u het sleutelpaar naar *nsupdate* bijwerken in volgorde voor de dynamische DNS-aanvraag moet worden ondertekend.</span><span class="sxs-lookup"><span data-stu-id="502d0-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span></span>

<span data-ttu-id="502d0-131">Als u een Windows-DNS-server gebruikt, kunt u Kerberos-verificatie met de *-g* parameter in *nsupdate* (niet beschikbaar in de Windows-versie van *nsupdate*).</span><span class="sxs-lookup"><span data-stu-id="502d0-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span></span> <span data-ttu-id="502d0-132">U doet dit door gebruik *kinit* laden de referenties (bijvoorbeeld van een [keytab-bestand](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="502d0-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="502d0-133">Vervolgens *nsupdate -g* gewoon door de referenties uit de cache.</span><span class="sxs-lookup"><span data-stu-id="502d0-133">Then *nsupdate -g* will pick up the credentials from the cache.</span></span>

<span data-ttu-id="502d0-134">Indien nodig, kunt u een DNS-zoekachtervoegsel toevoegen aan uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="502d0-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="502d0-135">Het DNS-achtervoegsel is opgegeven in de */etc/resolv.conf* bestand.</span><span class="sxs-lookup"><span data-stu-id="502d0-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="502d0-136">De meeste Linux-distributies beheren automatisch de inhoud van dit bestand, dus meestal niet worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="502d0-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="502d0-137">U kunt echter het achtervoegsel overschrijven met behulp van de DHCP-client *vervangen* opdracht.</span><span class="sxs-lookup"><span data-stu-id="502d0-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span></span> <span data-ttu-id="502d0-138">Hiervoor in */etc/dhcp/dhclient.conf*, toevoegen:</span><span class="sxs-lookup"><span data-stu-id="502d0-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

