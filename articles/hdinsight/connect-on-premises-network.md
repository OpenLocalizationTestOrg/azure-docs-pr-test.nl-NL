---
title: aaaConnect HDInsight tooyour on-premises netwerk - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate een HDInsight-cluster in een Azure-netwerk en sluit vervolgens tooyour on-premises netwerk. Meer informatie over hoe tooconfigure naamomzetting tussen HDInsight en uw on-premises netwerk via een aangepaste DNS-server.
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
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="797e1-104">HDInsight tooyour on-premises netwerk verbinden</span><span class="sxs-lookup"><span data-stu-id="797e1-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="797e1-105">Meer informatie over hoe tooconnect HDInsight tooyour on-premises netwerk door met behulp van Azure Virtual Networks en een VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="797e1-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="797e1-106">Dit document bevat de planningsinformatie over:</span><span class="sxs-lookup"><span data-stu-id="797e1-106">This document provides planning information on:</span></span>

* <span data-ttu-id="797e1-107">Gebruik HDInsight in een Azure-netwerk die verbinding tooyour maakt on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="797e1-108">Configureren van DNS-naamomzetting tussen Hallo virtuele netwerk en uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="797e1-109">Network security groepen toorestrict internet toegang tooHDInsight configureren.</span><span class="sxs-lookup"><span data-stu-id="797e1-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="797e1-110">Poorten die zijn geleverd door HDInsight op Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="797e1-111">Hallo-configuratie voor virtuele netwerken maken</span><span class="sxs-lookup"><span data-stu-id="797e1-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="797e1-112">Als u op zoek bent voor stapsgewijze instructies voor het verbinden van HDInsight tooyour lokaal netwerk met een virtueel netwerk van Azure, Zie Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="797e1-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="797e1-113">Gebruik Hallo volgende documenten toolearn hoe een Azure-netwerk dat is verbonden tooyour toocreate lokale netwerk:</span><span class="sxs-lookup"><span data-stu-id="797e1-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="797e1-114">Met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="797e1-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="797e1-115">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="797e1-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="797e1-116">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="797e1-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="797e1-117">Naamomzetting configureren</span><span class="sxs-lookup"><span data-stu-id="797e1-117">Configure name resolution</span></span>

<span data-ttu-id="797e1-118">tooallow HDInsight en resources die lid zijn van Hallo netwerk toocommunicate met de naam, moet u de volgende activiteiten Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="797e1-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="797e1-119">Maak een aangepaste DNS-server in hello Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="797e1-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="797e1-120">Hallo virtueel netwerk toouse Hallo aangepaste DNS-server in plaats van Hallo standaard Azure recursieve naamomzetting configureren.</span><span class="sxs-lookup"><span data-stu-id="797e1-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="797e1-121">Configureren van forwarding tussen Hallo aangepaste DNS-server en de lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="797e1-122">Deze configuratie kunt Hallo volgende gedrag:</span><span class="sxs-lookup"><span data-stu-id="797e1-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="797e1-123">Aanvragen voor de volledig gekwalificeerde domeinnamen met Hallo DNS-achtervoegsel __voor het virtuele netwerk Hallo__ toohello aangepaste DNS-server worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="797e1-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="797e1-124">Hallo aangepaste DNS-server stuurt vervolgens deze aanvragen toohello Azure recursieve Resolver, die als resultaat Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="797e1-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="797e1-125">Alle andere aanvragen worden doorgestuurd toohello lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="797e1-126">Zelfs aanvragen voor het openbare internet-bronnen zoals microsoft.com doorgestuurd toohello lokale DNS-server voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="797e1-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="797e1-127">Groen regels zijn in Hallo diagram te volgen, aanvragen voor bronnen die op Hallo DNS-achtervoegsel van het virtuele netwerk Hallo eindigen.</span><span class="sxs-lookup"><span data-stu-id="797e1-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="797e1-128">Blauwe lijnen zijn aanvragen voor bronnen in Hallo on-premises netwerk of op Hallo openbare internet.</span><span class="sxs-lookup"><span data-stu-id="797e1-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Diagram van hoe de DNS-aanvragen worden verwerkt in Hallo-configuratie gebruikt in dit document](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="797e1-130">Maken van een aangepaste DNS-server</span><span class="sxs-lookup"><span data-stu-id="797e1-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="797e1-131">U moet maken en configureren van Hallo DNS-server voordat u HDInsight in Hallo virtueel netwerk installeert.</span><span class="sxs-lookup"><span data-stu-id="797e1-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="797e1-132">een Linux-VM die gebruikmaakt van Hallo toocreate [binden](https://www.isc.org/downloads/bind/) DNS-software, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="797e1-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="797e1-133">Hallo volgende stappen gebruikt Hallo [Azure-portal](https://portal.azure.com) toocreate een virtuele Machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="797e1-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="797e1-134">Zie voor andere toocreate manieren een virtuele machine Hallo [VM maken, Azure CLI](../virtual-machines/linux/quick-create-cli.md) en [VM maken, Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documenten.</span><span class="sxs-lookup"><span data-stu-id="797e1-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="797e1-135">Van Hallo [Azure-portal](https://portal.azure.com), selecteer  __+__ , __Compute__, en __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="797e1-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Een virtuele Ubuntu-machine maken](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="797e1-137">Van Hallo __basisbeginselen__ sectie, voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="797e1-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="797e1-138">__Naam__: een beschrijvende naam die deze virtuele machine wordt aangeduid.</span><span class="sxs-lookup"><span data-stu-id="797e1-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="797e1-139">Bijvoorbeeld: __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="797e1-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="797e1-140">__Gebruikersnaam__: naam Hallo Hallo SSH-account.</span><span class="sxs-lookup"><span data-stu-id="797e1-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="797e1-141">__Openbare SSH-sleutel__ of __wachtwoord__: Hallo verificatiemethode voor Hallo SSH-account.</span><span class="sxs-lookup"><span data-stu-id="797e1-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="797e1-142">Wordt aangeraden met openbare sleutels, omdat ze beter te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="797e1-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="797e1-143">Zie voor meer informatie, Hallo [maken en gebruiken SSH-sleutels voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span><span class="sxs-lookup"><span data-stu-id="797e1-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="797e1-144">__Resourcegroep__: Selecteer __gebruik bestaande__, en selecteer vervolgens de resourcegroep Hallo met Hallo virtueel netwerk eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="797e1-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="797e1-145">__Locatie__: Selecteer dezelfde locatie als het virtuele netwerk Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="797e1-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Basisconfiguratie van de virtuele machine](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="797e1-147">Laat de andere vermeldingen op Hallo standaardwaarden en selecteer vervolgens __OK__.</span><span class="sxs-lookup"><span data-stu-id="797e1-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="797e1-148">Van Hallo __een grootte kiezen__ sectie, selecteer Hallo VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="797e1-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="797e1-149">Voor deze zelfstudie Hallo kleinste selecteren en de laagste kosten optie.</span><span class="sxs-lookup"><span data-stu-id="797e1-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="797e1-150">toocontinue, gebruik Hallo __Selecteer__ knop.</span><span class="sxs-lookup"><span data-stu-id="797e1-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="797e1-151">Van Hallo __instellingen__ sectie, voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="797e1-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="797e1-152">__Virtueel netwerk__: Selecteer Hallo virtueel netwerk dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="797e1-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="797e1-153">__Subnet__: Hallo standaard subnet voor het virtuele netwerk Hallo selecteert.</span><span class="sxs-lookup"><span data-stu-id="797e1-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="797e1-154">Voer __niet__ Selecteer Hallo subnet dat wordt gebruikt door Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="797e1-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="797e1-155">__Opslagaccount voor diagnostische gegevens__: Selecteer een bestaand opslagaccount of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="797e1-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Virtuele-netwerkinstellingen](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="797e1-157">Hallo andere vermeldingen laten op het Hallo-standaardwaarde, selecteert u vervolgens __OK__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="797e1-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="797e1-158">Van Hallo __aankoop__ sectie, selecteer Hallo __aankoop__ knop toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="797e1-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="797e1-159">Zodra Hallo virtuele machine is gemaakt, de __overzicht__ sectie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="797e1-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="797e1-160">Selecteer in lijst aan de linkerkant Hallo Hallo __eigenschappen__.</span><span class="sxs-lookup"><span data-stu-id="797e1-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="797e1-161">Hallo opslaan __openbaar IP-adres__ en __particuliere IP-adres__ waarden.</span><span class="sxs-lookup"><span data-stu-id="797e1-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="797e1-162">Deze wordt gebruikt in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="797e1-162">It will be used in hello next section.</span></span>

    ![Openbare en particuliere IP-adressen](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="797e1-164">Installeren en configureren van de binding (DNS-software)</span><span class="sxs-lookup"><span data-stu-id="797e1-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="797e1-165">Gebruik van SSH tooconnect toohello __openbaar IP-adres__ van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="797e1-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="797e1-166">Hallo volgende voorbeeld maakt tooa virtuele machine op 40.68.254.142 verbinding:</span><span class="sxs-lookup"><span data-stu-id="797e1-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="797e1-167">Vervang `sshuser` Hello SSH gebruikersaccount die u hebt opgegeven bij het maken van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="797e1-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="797e1-168">Er zijn tal van manieren tooobtain hello `ssh` hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="797e1-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="797e1-169">Op Linux, Unix- en Mac OS, wordt dit geleverd als onderdeel van het Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="797e1-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="797e1-170">Als u van Windows gebruikmaakt, overweeg dan een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="797e1-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="797e1-171">Azure-Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="797e1-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="797e1-172">Bash op Ubuntu op Windows 10</span><span class="sxs-lookup"><span data-stu-id="797e1-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="797e1-173">GIT (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="797e1-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="797e1-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="797e1-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="797e1-175">tooinstall binding, gebruik Hallo volgende opdrachten uit Hallo SSH-sessie:</span><span class="sxs-lookup"><span data-stu-id="797e1-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="797e1-176">tooconfigure Bind tooforward aanvragen tooyour on-premises DNS-server voor naamomzetting, gebruiken na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.options` bestand:</span><span class="sxs-lookup"><span data-stu-id="797e1-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="797e1-177">Vervang de waarden Hallo in Hallo `goodclients` sectie met Hallo IP-adresbereik van Hallo virtueel netwerk en on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="797e1-178">Deze sectie definieert hello-mailadressen die deze DNS-server aanvragen van accepteert.</span><span class="sxs-lookup"><span data-stu-id="797e1-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="797e1-179">Vervang Hallo `192.168.0.1` vermelding in Hallo `forwarders` sectie met Hallo IP-adres van uw lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="797e1-180">Deze vermelding routes DNS-aanvragen tooyour lokale DNS-server voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="797e1-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="797e1-181">tooedit dit bestand, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="797e1-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="797e1-182">Gebruik-bestand Hallo toosave __Ctrl + X__, __Y__, en vervolgens __Enter__.</span><span class="sxs-lookup"><span data-stu-id="797e1-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="797e1-183">Gebruik van Hallo SSH-sessie, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="797e1-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="797e1-184">Met deze opdracht retourneert een waarde van een vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="797e1-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="797e1-185">Hallo `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` tekst hello is __DNS-achtervoegsel__ voor dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="797e1-186">Deze waarde niet opslaan omdat het wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="797e1-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="797e1-187">tooconfigure Bind tooresolve DNS-namen voor resources binnen het virtuele netwerk hello, gebruiken na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.local` bestand:</span><span class="sxs-lookup"><span data-stu-id="797e1-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="797e1-188">Vervang Hallo `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` met Hallo DNS-achtervoegsel die u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="797e1-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="797e1-189">tooedit dit bestand, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="797e1-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="797e1-190">Gebruik-bestand Hallo toosave __Ctrl + X__, __Y__, en vervolgens __Enter__.</span><span class="sxs-lookup"><span data-stu-id="797e1-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="797e1-191">toostart binding, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="797e1-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="797e1-192">tooverify die binden kunt oplossen Hallo namen van resources in uw on-premises netwerk, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="797e1-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="797e1-193">Vervang `dns.mynetwork.net` met Hallo volledig gekwalificeerde domeinnaam (FQDN) van een bron in uw on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="797e1-194">Vervang `10.0.0.4` Hello __interne IP-adres__ van uw aangepaste DNS-server in het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="797e1-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="797e1-195">antwoord Hallo verschijnt vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="797e1-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="797e1-196">Hallo virtueel netwerk toouse Hallo aangepaste DNS-server configureren</span><span class="sxs-lookup"><span data-stu-id="797e1-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="797e1-197">tooconfigure hello virtueel netwerk toouse Hallo aangepaste DNS-server in plaats van hello Azure recursieve resolver, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="797e1-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="797e1-198">In Hallo [Azure-portal](https://portal.azure.com)Hallo virtueel netwerk selecteert en selecteer vervolgens __DNS-Servers__.</span><span class="sxs-lookup"><span data-stu-id="797e1-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="797e1-199">Selecteer __aangepaste__, en Voer Hallo __interne IP-adres__ van Hallo aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="797e1-200">Tot slot selecteert __opslaan__.</span><span class="sxs-lookup"><span data-stu-id="797e1-200">Finally, select __Save__.</span></span>

    ![Hallo aangepaste DNS-server voor Hallo netwerk instellen](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="797e1-202">Hallo lokale DNS-server configureren</span><span class="sxs-lookup"><span data-stu-id="797e1-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="797e1-203">In de vorige sectie hello, moet u Hallo aangepaste DNS-server tooforward aanvragen toohello lokale DNS-server geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="797e1-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="797e1-204">Vervolgens configureert u Hallo lokale DNS-server tooforward aanvragen toohello aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="797e1-205">Voor specifieke stappen over het tooconfigure uw DNS-server, Raadpleeg de documentatie van de Hallo voor uw DNS-server-software.</span><span class="sxs-lookup"><span data-stu-id="797e1-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="797e1-206">Zoek naar Hallo Stapsgewijze instructies voor het tooconfigure een __voorwaardelijke doorstuurserver__.</span><span class="sxs-lookup"><span data-stu-id="797e1-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="797e1-207">Een voorwaardelijke voorwaartse verzendt alleen aanvragen voor een specifieke DNS-achtervoegsel.</span><span class="sxs-lookup"><span data-stu-id="797e1-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="797e1-208">In dit geval moet u een doorstuurserver voor Hallo DNS-achtervoegsel van het virtuele netwerk Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="797e1-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="797e1-209">Aanvragen voor dit achtervoegsel moeten toohello IP-adres van Hallo aangepaste DNS-server worden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="797e1-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="797e1-210">Hallo volgende tekst is een voorbeeld van een voorwaardelijke doorstuurserver-configuratie voor Hallo **binden** DNS-software:</span><span class="sxs-lookup"><span data-stu-id="797e1-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="797e1-211">Voor informatie over het gebruik van DNS op **Windows Server 2016**, Zie Hallo [toevoegen DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentatie...</span><span class="sxs-lookup"><span data-stu-id="797e1-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="797e1-212">Wanneer u Hallo lokale DNS-server hebt geconfigureerd, kunt u `nslookup` van Hallo lokale netwerk tooverify in Hallo virtueel netwerk dat u het kunt oplossen namen.</span><span class="sxs-lookup"><span data-stu-id="797e1-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="797e1-213">Hallo voorbeeld te volgen</span><span class="sxs-lookup"><span data-stu-id="797e1-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="797e1-214">In dit voorbeeld maakt gebruik van de lokale DNS-server op 196.168.0.4 Hallo tooresolve Hallo-naam van Hallo aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="797e1-215">Hallo IP-adres vervangen door Hallo voor Hallo lokale DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="797e1-216">Vervang Hallo `dnsproxy` adres met de volledig gekwalificeerde domeinnaam Hallo van Hallo aangepaste DNS-server.</span><span class="sxs-lookup"><span data-stu-id="797e1-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="797e1-217">Optioneel: Besturingselement netwerkverkeer</span><span class="sxs-lookup"><span data-stu-id="797e1-217">Optional: Control network traffic</span></span>

<span data-ttu-id="797e1-218">U kunt de netwerkbeveiligingsgroepen (NSG) of de gebruiker gedefinieerde routes (UDR) toocontrol-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="797e1-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="797e1-219">Nsg's kunnen u toofilter binnenkomend en uitgaand verkeer, en verkeer toestaan of weigeren Hallo.</span><span class="sxs-lookup"><span data-stu-id="797e1-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="797e1-220">Udr's kunnen u toocontrol hoe tussen resources in het virtuele netwerk Hallo verkeersstromen Hallo van internet en Hallo on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="797e1-221">HDInsight vereist binnenkomende toegang van specifieke IP-adressen in hello Azure-cloud en onbeperkte uitgaande toegang.</span><span class="sxs-lookup"><span data-stu-id="797e1-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="797e1-222">Wanneer u nsg's of udr's toocontrol-verkeer gebruikt, moet u Hallo stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="797e1-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="797e1-223">Hallo IP-adressen voor Hallo locatie waarin het virtuele netwerk zoeken.</span><span class="sxs-lookup"><span data-stu-id="797e1-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="797e1-224">Zie voor een lijst met vereiste IP-adressen per locatie, [vereiste IP-adressen](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="797e1-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="797e1-225">Binnenkomend verkeer van Hallo IP-adressen toestaan.</span><span class="sxs-lookup"><span data-stu-id="797e1-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="797e1-226">__NSG__: toestaan __inkomende__ verkeer op poort __443__ van Hallo __Internet__.</span><span class="sxs-lookup"><span data-stu-id="797e1-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="797e1-227">__UDR__: Set Hallo __volgende Hop__ Hallo route too__Internet__ type.</span><span class="sxs-lookup"><span data-stu-id="797e1-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="797e1-228">Zie voor een voorbeeld van het gebruik van Azure PowerShell of hello Azure CLI toocreate nsg's Hallo [HDInsight uitbreiden met Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span><span class="sxs-lookup"><span data-stu-id="797e1-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="797e1-229">Hallo HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="797e1-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="797e1-230">Hallo aangepaste DNS-server moet u configureren voordat u HDInsight in het virtuele netwerk Hallo installeert.</span><span class="sxs-lookup"><span data-stu-id="797e1-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="797e1-231">Gebruik Hallo stappen voor het Hallo [maken van een HDInsight-cluster met behulp van Azure-portal Hallo](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="797e1-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="797e1-232">Tijdens het maken, moet u Hallo locatie waarin het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="797e1-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="797e1-233">In Hallo __geavanceerde instellingen__ deel van de configuratie, moet u Hallo virtueel netwerk en subnet dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="797e1-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="797e1-234">Verbinding maken met tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="797e1-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="797e1-235">De meeste documentatie op HDInsight wordt ervan uitgegaan dat u toegang toohello cluster via Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="797e1-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="797e1-236">Bijvoorbeeld, kunt u de cluster toohello op https://CLUSTERNAME.azurehdinsight.net koppelen.</span><span class="sxs-lookup"><span data-stu-id="797e1-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="797e1-237">Dit adres Hallo openbare-gateway niet beschikbaar is als u nsg's hebt gebruikt of udr's toorestrict toegang vanaf internet Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="797e1-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="797e1-238">toodirectly tooHDInsight via Hallo virtueel netwerk verbinding maken, gebruikt u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="797e1-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="797e1-239">toodiscover hello interne FQDN-namen van de clusterknooppunten Hallo HDInsight, een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="797e1-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

2. <span data-ttu-id="797e1-240">toodetermine hello poort die een service is beschikbaar op, Zie Hallo [poorten die worden gebruikt door de services van Hadoop op HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="797e1-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="797e1-241">Sommige services die worden gehost op Hallo hoofdknooppunten zijn alleen actief is op één knooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="797e1-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="797e1-242">Als u probeert toegang tot een service op één hoofdknooppunt en dit mislukt, overschakelen toohello andere hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="797e1-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="797e1-243">Bijvoorbeeld, is Ambari alleen actief op één hoofdknooppunt tegelijk.</span><span class="sxs-lookup"><span data-stu-id="797e1-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="797e1-244">Als u probeert toegang tot Ambari op één hoofdknooppunt en een 404-fout, retourneert en vervolgens deze wordt uitgevoerd op Hallo andere hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="797e1-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="797e1-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="797e1-245">Next steps</span></span>

* <span data-ttu-id="797e1-246">Zie voor meer informatie over het gebruik van HDInsight in een virtueel netwerk [HDInsight uitbreiden met behulp van Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="797e1-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="797e1-247">Zie voor meer informatie over virtuele netwerken van Azure Hallo [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="797e1-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="797e1-248">Zie voor meer informatie over netwerkbeveiligingsgroepen [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="797e1-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="797e1-249">Zie voor meer informatie over de gebruiker gedefinieerde routes, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="797e1-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
