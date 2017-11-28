---
title: HDInsight verbinden met uw on-premises netwerk - of Azure HDInsight | Microsoft Docs
description: Informatie over het maken van een HDInsight-cluster in een Azure-netwerk en maak verbinding met uw lokale netwerk. Informatie over het configureren van naamomzetting tussen HDInsight en uw on-premises netwerk via een aangepaste DNS-server.
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="77714-104">HDInsight verbinden met uw on-premises-netwerk</span><span class="sxs-lookup"><span data-stu-id="77714-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="77714-105">Informatie over het HDInsight verbinding met uw on-premises netwerk met behulp van Azure Virtual Networks en een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="77714-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="77714-106">Dit document bevat de planningsinformatie over:</span><span class="sxs-lookup"><span data-stu-id="77714-106">This document provides planning information on:</span></span>

* <span data-ttu-id="77714-107">HDInsight gebruikt in een Azure-netwerk die verbinding met uw on-premises netwerk maakt.</span><span class="sxs-lookup"><span data-stu-id="77714-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="77714-108">Configureren van DNS-naamomzetting tussen het virtuele netwerk en uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="77714-109">Configureren van netwerkbeveiligingsgroepen internettoegang tot HDInsight te beperken.</span><span class="sxs-lookup"><span data-stu-id="77714-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="77714-110">Poorten die zijn geleverd door HDInsight op het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="77714-111">De configuratie van het virtuele netwerk maken</span><span class="sxs-lookup"><span data-stu-id="77714-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77714-112">Als u zoekt Stapsgewijze instructies voor het verbinden van HDInsight met uw on-premises netwerk via een virtueel netwerk van Azure, raadpleegt u de [HDInsight verbinding maken met uw on-premises netwerk](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="77714-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="77714-113">Gebruik de volgende documenten voor meer informatie over het maken van een virtueel netwerk van Azure die is verbonden met uw on-premises netwerk:</span><span class="sxs-lookup"><span data-stu-id="77714-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="77714-114">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="77714-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="77714-115">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="77714-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="77714-116">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="77714-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="77714-117">Naamomzetting configureren</span><span class="sxs-lookup"><span data-stu-id="77714-117">Configure name resolution</span></span>

<span data-ttu-id="77714-118">Als u wilt toestaan HDInsight en bronnen in het gekoppelde netwerk om te communiceren met de naam, moet u de volgende acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="77714-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="77714-119">Maak een aangepaste DNS-server in het virtuele netwerk van Azure.</span><span class="sxs-lookup"><span data-stu-id="77714-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="77714-120">Het virtuele netwerk voor het gebruik van de aangepaste DNS-server in plaats van de standaard Azure recursieve naamomzetting configureren.</span><span class="sxs-lookup"><span data-stu-id="77714-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="77714-121">Configureren van forwarding tussen de aangepaste DNS-server en de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="77714-122">Deze configuratie kunt het volgende gedrag:</span><span class="sxs-lookup"><span data-stu-id="77714-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="77714-123">Aanvragen voor de volledig gekwalificeerde domeinnamen waarvoor het DNS-achtervoegsel __voor het virtuele netwerk__ worden doorgestuurd naar de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="77714-124">De aangepaste DNS-server stuurt vervolgens deze aanvragen aan de recursieve Resolver van Azure, waardoor het IP-adres geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="77714-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="77714-125">Alle andere aanvragen worden doorgestuurd naar de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="77714-126">Zelfs aanvragen voor het openbare internet-bronnen zoals microsoft.com worden doorgestuurd naar de lokale DNS-server voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="77714-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="77714-127">Groen regels zijn in het volgende diagram aanvragen voor bronnen die op de DNS-achtervoegsel van het virtuele netwerk eindigen.</span><span class="sxs-lookup"><span data-stu-id="77714-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="77714-128">Blauwe lijnen zijn aanvragen voor bronnen in de on-premises netwerk of op het openbare internet.</span><span class="sxs-lookup"><span data-stu-id="77714-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Diagram van hoe de DNS-aanvragen worden verwerkt in de configuratie die in dit document gebruikt](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="77714-130">Maken van een aangepaste DNS-server</span><span class="sxs-lookup"><span data-stu-id="77714-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77714-131">U moet maken en configureren van de DNS-server voordat u HDInsight installeert in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="77714-132">Maken van een Linux-VM die gebruikmaakt van de [binden](https://www.isc.org/downloads/bind/) DNS-software, gebruik de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="77714-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="77714-133">De volgende stappen uitvoeren om de [Azure-portal](https://portal.azure.com) voor het maken van een virtuele Machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="77714-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="77714-134">Zie voor andere manieren om te maken van een virtuele machine, de [VM maken, Azure CLI](../virtual-machines/linux/quick-create-cli.md) en [VM maken, Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documenten.</span><span class="sxs-lookup"><span data-stu-id="77714-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="77714-135">Van de [Azure-portal](https://portal.azure.com), selecteer  __+__ , __Compute__, en __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="77714-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Een virtuele Ubuntu-machine maken](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="77714-137">Van de __basisbeginselen__ sectie, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="77714-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="77714-138">__Naam__: een beschrijvende naam die deze virtuele machine wordt aangeduid.</span><span class="sxs-lookup"><span data-stu-id="77714-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="77714-139">Bijvoorbeeld: __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="77714-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="77714-140">__Gebruikersnaam__: de naam van het SSH-account.</span><span class="sxs-lookup"><span data-stu-id="77714-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="77714-141">__Openbare SSH-sleutel__ of __wachtwoord__: de verificatiemethode voor de SSH-account.</span><span class="sxs-lookup"><span data-stu-id="77714-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="77714-142">Wordt aangeraden met openbare sleutels, omdat ze beter te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="77714-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="77714-143">Zie voor meer informatie de [maken en gebruiken SSH-sleutels voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span><span class="sxs-lookup"><span data-stu-id="77714-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="77714-144">__Resourcegroep__: Selecteer __gebruik bestaande__, en selecteer vervolgens de resourcegroep waarin het virtuele netwerk eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="77714-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="77714-145">__Locatie__: Selecteer de dezelfde locatie als het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-145">__Location__: Select the same location as the virtual network.</span></span>

    ![Basisconfiguratie van de virtuele machine](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="77714-147">Andere items laat de standaardwaarden en selecteer vervolgens __OK__.</span><span class="sxs-lookup"><span data-stu-id="77714-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="77714-148">Van de __een grootte kiezen__ sectie, selecteert u de VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="77714-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="77714-149">Selecteer de optie waarbij de kleinste en de laagste kosten voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="77714-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="77714-150">Als u wilt doorgaan, gebruikt u de __Selecteer__ knop.</span><span class="sxs-lookup"><span data-stu-id="77714-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="77714-151">Van de __instellingen__ sectie, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="77714-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="77714-152">__Virtueel netwerk__: Selecteer het virtuele netwerk die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="77714-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="77714-153">__Subnet__: Selecteer de standaard-subnet voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="77714-154">Voer __niet__ selecteert u het subnet dat wordt gebruikt door de VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="77714-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="77714-155">__Opslagaccount voor diagnostische gegevens__: Selecteer een bestaand opslagaccount of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="77714-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Virtuele-netwerkinstellingen](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="77714-157">De andere vermeldingen laat de standaardwaarde en selecteer vervolgens __OK__ om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="77714-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="77714-158">Van de __aankoop__ sectie, selecteer de __aankoop__ om te maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="77714-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="77714-159">Wanneer de virtuele machine is gemaakt, de __overzicht__ sectie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="77714-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="77714-160">Selecteer in de lijst aan de linkerkant __eigenschappen__.</span><span class="sxs-lookup"><span data-stu-id="77714-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="77714-161">Sla de __openbaar IP-adres__ en __particuliere IP-adres__ waarden.</span><span class="sxs-lookup"><span data-stu-id="77714-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="77714-162">Deze wordt gebruikt in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="77714-162">It will be used in the next section.</span></span>

    ![Openbare en particuliere IP-adressen](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="77714-164">Installeren en configureren van de binding (DNS-software)</span><span class="sxs-lookup"><span data-stu-id="77714-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="77714-165">SSH gebruiken voor verbinding met de __openbaar IP-adres__ van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="77714-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="77714-166">Het volgende voorbeeld maakt verbinding met een virtuele machine op 40.68.254.142:</span><span class="sxs-lookup"><span data-stu-id="77714-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="77714-167">Vervang `sshuser` met het SSH-gebruikersaccount dat u hebt opgegeven bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="77714-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="77714-168">Er zijn tal van manieren verkrijgen van de `ssh` hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="77714-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="77714-169">Op Linux, Unix- en Mac OS, wordt dit geleverd als onderdeel van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="77714-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="77714-170">Als u van Windows gebruikmaakt, overweeg een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="77714-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="77714-171">Azure-Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="77714-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="77714-172">Bash op Ubuntu op Windows 10</span><span class="sxs-lookup"><span data-stu-id="77714-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="77714-173">GIT (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="77714-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="77714-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="77714-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="77714-175">Gebruik de volgende opdrachten bij de SSH-sessie voor het installeren van Bind:</span><span class="sxs-lookup"><span data-stu-id="77714-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="77714-176">Gebruik voor het configureren van de binding voor het doorsturen van aanvragen voor naamomzetting naar uw on-premises DNS-server de volgende tekst als de inhoud van de `/etc/bind/named.conf.options` bestand:</span><span class="sxs-lookup"><span data-stu-id="77714-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="77714-177">Vervang de waarden in de `goodclients` sectie met de IP-adresbereik van het virtuele netwerk en de on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="77714-178">Deze sectie worden de adressen die deze DNS-server aanvragen van accepteert gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="77714-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="77714-179">Vervang de `192.168.0.1` vermelding in de `forwarders` sectie met de IP-adres van uw lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="77714-180">Deze vermelding routeert DNS-aanvragen naar de lokale DNS-server voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="77714-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="77714-181">Dit bestand bewerken, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="77714-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="77714-182">Gebruiken om het bestand opslaat, __Ctrl + X__, __Y__, en vervolgens __Enter__.</span><span class="sxs-lookup"><span data-stu-id="77714-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="77714-183">Gebruik de volgende opdracht in de SSH-sessie:</span><span class="sxs-lookup"><span data-stu-id="77714-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="77714-184">Met deze opdracht retourneert een waarde die vergelijkbaar is met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="77714-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="77714-185">De `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` tekst is de __DNS-achtervoegsel__ voor dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="77714-186">Deze waarde niet opslaan omdat het wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77714-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="77714-187">Gebruik voor het configureren van DNS-namen omzetten voor resources binnen het virtuele netwerk is afhankelijk van de volgende tekst als de inhoud van de `/etc/bind/named.conf.local` bestand:</span><span class="sxs-lookup"><span data-stu-id="77714-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="77714-188">Vervang de `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` met de DNS-achtervoegsel dat u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="77714-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="77714-189">Dit bestand bewerken, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="77714-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="77714-190">Gebruiken om het bestand opslaat, __Ctrl + X__, __Y__, en vervolgens __Enter__.</span><span class="sxs-lookup"><span data-stu-id="77714-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="77714-191">Gebruik de volgende opdracht voor het starten van Bind:</span><span class="sxs-lookup"><span data-stu-id="77714-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="77714-192">Om te controleren die afhankelijk van de namen van bronnen in uw on-premises netwerk kunt oplossen, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="77714-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="77714-193">Vervang `dns.mynetwork.net` met de volledig gekwalificeerde domeinnaam (FQDN) van een resource in uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="77714-194">Vervang `10.0.0.4` met de __interne IP-adres__ van uw aangepaste DNS-server in het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="77714-195">Het antwoord ziet er ongeveer de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="77714-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="77714-196">Het virtuele netwerk voor het gebruik van de aangepaste DNS-server configureren</span><span class="sxs-lookup"><span data-stu-id="77714-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="77714-197">Gebruik de volgende stappen voor het configureren van het virtuele netwerk voor het gebruik van de aangepaste DNS-server in plaats van de Azure recursieve resolver:</span><span class="sxs-lookup"><span data-stu-id="77714-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="77714-198">In de [Azure-portal](https://portal.azure.com), selecteer het virtuele netwerk en selecteer vervolgens __DNS-Servers__.</span><span class="sxs-lookup"><span data-stu-id="77714-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="77714-199">Selecteer __aangepaste__, en voer de __interne IP-adres__ van de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="77714-200">Tot slot selecteert __opslaan__.</span><span class="sxs-lookup"><span data-stu-id="77714-200">Finally, select __Save__.</span></span>

    ![De aangepaste DNS-server voor het netwerk instellen](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="77714-202">De lokale DNS-server configureren</span><span class="sxs-lookup"><span data-stu-id="77714-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="77714-203">In de vorige sectie, moet u de aangepaste DNS-server voor het doorsturen van aanvragen naar de lokale DNS-server geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="77714-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="77714-204">Vervolgens configureert u de lokale DNS-server voor het doorsturen van aanvragen voor de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="77714-205">Raadpleeg de documentatie bij uw DNS-server-software voor specifieke stappen over het configureren van uw DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="77714-206">Zoekt u de stappen voor het configureren van een __voorwaardelijke doorstuurserver__.</span><span class="sxs-lookup"><span data-stu-id="77714-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="77714-207">Een voorwaardelijke voorwaartse verzendt alleen aanvragen voor een specifieke DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="77714-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="77714-208">In dit geval moet u een doorstuurserver voor het DNS-achtervoegsel van het virtuele netwerk configureren.</span><span class="sxs-lookup"><span data-stu-id="77714-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="77714-209">Aanvragen voor dit achtervoegsel moeten worden doorgestuurd naar het IP-adres van de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="77714-210">De volgende tekst is een voorbeeld van een voorwaardelijke doorstuurserver-configuratie voor de **binden** DNS-software:</span><span class="sxs-lookup"><span data-stu-id="77714-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="77714-211">Voor informatie over het gebruik van DNS op **Windows Server 2016**, Zie de [toevoegen DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentatie...</span><span class="sxs-lookup"><span data-stu-id="77714-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="77714-212">Wanneer u de lokale DNS-server hebt geconfigureerd, kunt u `nslookup` van de on-premises netwerk om te controleren dat u namen in het virtuele netwerk omzetten kan.</span><span class="sxs-lookup"><span data-stu-id="77714-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="77714-213">Het volgende voorbeeld</span><span class="sxs-lookup"><span data-stu-id="77714-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="77714-214">Dit voorbeeld wordt de lokale DNS-server op 196.168.0.4 omzetten van de naam van de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="77714-215">Het IP-adres vervangen door de voor de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="77714-216">Vervang de `dnsproxy` adres met de volledig gekwalificeerde domeinnaam van de aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="77714-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="77714-217">Optioneel: Besturingselement netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="77714-217">Optional: Control network traffic</span></span>

<span data-ttu-id="77714-218">U kunt netwerkbeveiligingsgroepen (NSG) of de gebruiker gedefinieerde routes (UDR) netwerkverkeer wordt beheerd.</span><span class="sxs-lookup"><span data-stu-id="77714-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="77714-219">Nsg's kunnen u binnenkomend en uitgaand verkeer filteren en toestaan of weigeren van het verkeer.</span><span class="sxs-lookup"><span data-stu-id="77714-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="77714-220">Udr's kunnen u bepalen hoe verkeersstromen tussen resources in het virtuele netwerk, internet en de on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="77714-221">HDInsight vereist binnenkomende toegang van specifieke IP-adressen in de Azure-cloud en onbeperkte uitgaande toegang.</span><span class="sxs-lookup"><span data-stu-id="77714-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="77714-222">Wanneer u nsg's of udr's om te bepalen van verkeer, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="77714-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="77714-223">De IP-adressen vinden voor de locatie waarin het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="77714-224">Zie voor een lijst met vereiste IP-adressen per locatie, [vereiste IP-adressen](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="77714-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="77714-225">Binnenkomend verkeer van de IP-adressen toestaan.</span><span class="sxs-lookup"><span data-stu-id="77714-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="77714-226">__NSG__: toestaan __inkomende__ verkeer op poort __443__ van de __Internet__.</span><span class="sxs-lookup"><span data-stu-id="77714-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="77714-227">__UDR__: Stel de __volgende Hop__ type van de route naar __Internet__.</span><span class="sxs-lookup"><span data-stu-id="77714-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="77714-228">Zie voor een voorbeeld van het gebruik van Azure PowerShell of Azure CLI voor het nsg's maken, de [HDInsight uitbreiden met Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span><span class="sxs-lookup"><span data-stu-id="77714-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="77714-229">Het HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="77714-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="77714-230">Voordat u HDInsight in het virtuele netwerk installeert, moet u de aangepaste DNS-server configureren.</span><span class="sxs-lookup"><span data-stu-id="77714-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="77714-231">Gebruik de stappen in de [maken van een HDInsight-cluster met de Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document om een HDInsight-cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="77714-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="77714-232">Tijdens het maken, moet u de locatie waarin het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="77714-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="77714-233">In de __geavanceerde instellingen__ deel van de configuratie, moet u het virtuele netwerk en subnet dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="77714-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="77714-234">Verbinding maken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="77714-234">Connecting to HDInsight</span></span>

<span data-ttu-id="77714-235">De meeste documentatie op HDInsight wordt ervan uitgegaan dat u toegang tot het cluster via internet hebt.</span><span class="sxs-lookup"><span data-stu-id="77714-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="77714-236">Bijvoorbeeld, u verbinding kunt maken met het cluster op https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="77714-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="77714-237">Dit adres wordt gebruikt voor de openbare-gateway niet beschikbaar is als u nsg's of udr's hebt gebruikt om toegang te beperken van het internet.</span><span class="sxs-lookup"><span data-stu-id="77714-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="77714-238">Om rechtstreeks verbinding maken met HDInsight via het virtuele netwerk, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="77714-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="77714-239">Gebruik een van de volgende methoden voor het detecteren van de interne FQDN-namen van de clusterknooppunten HDInsight:</span><span class="sxs-lookup"><span data-stu-id="77714-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="77714-240">Zie het vaststellen van de poort die een service is beschikbaar op de [poorten die worden gebruikt door de services van Hadoop op HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="77714-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="77714-241">Sommige services die worden gehost op de hoofdknooppunten zijn alleen actief is op één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="77714-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="77714-242">Als u probeert toegang tot een service op één hoofdknooppunt en dit mislukt, overschakelen naar het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="77714-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="77714-243">Bijvoorbeeld, is Ambari alleen actief op één hoofdknooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="77714-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="77714-244">Als u probeert toegang tot Ambari op één hoofdknooppunt en een 404-fout retourneert, wordt klikt u vervolgens deze uitgevoerd op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="77714-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77714-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77714-245">Next steps</span></span>

* <span data-ttu-id="77714-246">Zie voor meer informatie over het gebruik van HDInsight in een virtueel netwerk [HDInsight uitbreiden met behulp van Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="77714-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="77714-247">Zie voor meer informatie over virtuele netwerken in Azure, de [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77714-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="77714-248">Zie voor meer informatie over netwerkbeveiligingsgroepen [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="77714-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="77714-249">Zie voor meer informatie over de gebruiker gedefinieerde routes, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77714-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
