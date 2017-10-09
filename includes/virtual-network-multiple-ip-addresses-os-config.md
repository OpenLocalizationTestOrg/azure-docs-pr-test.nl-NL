## <span data-ttu-id="e5f65-101"><a name="os-config"></a>IP-adressen tooa VM-besturingssysteem toevoegen</span><span class="sxs-lookup"><span data-stu-id="e5f65-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="e5f65-102">Verbinding maken en aanmelding tooa VM die u hebt gemaakt met meerdere particuliere IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="e5f65-103">Alle Hallo privé IP-adressen (inclusief Hallo primair) dat u toohello VM hebt toegevoegd, moet u handmatig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="e5f65-104">Volgende stappen uit voor uw besturingssysteem VM Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="e5f65-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="e5f65-105">Windows</span><span class="sxs-lookup"><span data-stu-id="e5f65-105">Windows</span></span>

1. <span data-ttu-id="e5f65-106">Typ vanaf een opdrachtprompt *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="e5f65-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="e5f65-107">Ziet u alleen Hallo *primaire* privé IP-adres (via DHCP).</span><span class="sxs-lookup"><span data-stu-id="e5f65-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="e5f65-108">Type *ncpa.cpl* in Hallo opdrachtprompt tooopen hello **netwerkverbindingen** venster.</span><span class="sxs-lookup"><span data-stu-id="e5f65-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="e5f65-109">Open Eigenschappen voor de juiste adapter Hallo Hallo: **LAN-verbinding**.</span><span class="sxs-lookup"><span data-stu-id="e5f65-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="e5f65-110">Dubbelklik op Internet Protocol versie 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="e5f65-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="e5f65-111">Selecteer **gebruik Hallo volgende IP-adres** en voer de volgende waarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="e5f65-112">**IP-adres**: Voer Hallo *primaire* privé IP-adres</span><span class="sxs-lookup"><span data-stu-id="e5f65-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="e5f65-113">**Subnetmasker**: stel dit in op basis van uw subnet.</span><span class="sxs-lookup"><span data-stu-id="e5f65-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="e5f65-114">Bijvoorbeeld, als hello subnet is een/24-subnet en Hallo subnet subnetmasker 255.255.255.0 is.</span><span class="sxs-lookup"><span data-stu-id="e5f65-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="e5f65-115">**Standaard-gateway**: Hallo eerste IP-adres in Hallo subnet.</span><span class="sxs-lookup"><span data-stu-id="e5f65-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="e5f65-116">Als het subnet 10.0.0.0/24 is, is Hallo gateway IP-adres 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="e5f65-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="e5f65-117">Klik op **gebruik Hallo volgende DNS-serveradressen** en voer de volgende waarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="e5f65-118">**DNS-voorkeursserver**: als u niet uw eigen DNS-server gebruikt, voert u 168.63.129.16 in.</span><span class="sxs-lookup"><span data-stu-id="e5f65-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="e5f65-119">Als u uw eigen DNS-server gebruikt, voert u Hallo IP-adres voor uw server.</span><span class="sxs-lookup"><span data-stu-id="e5f65-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="e5f65-120">Klik op Hallo **Geavanceerd** knop en extra IP-adressen toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="e5f65-121">Elk Hallo secundaire privé IP-adressen die worden vermeld in stap 8 toohello NIC Hello hetzelfde subnet is opgegeven voor Hallo primaire IP-adres toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="e5f65-122">Als u bovenstaande stappen voor Hallo niet correct uitvoert, kunt u connectiviteit tooyour VM verliezen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="e5f65-123">Zorg ervoor dat Hallo-informatie voor stap 5 ingevoerd juist is voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="e5f65-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="e5f65-124">Klik op **OK** tooclose uit Hallo TCP/IP-instellingen en vervolgens **OK** opnieuw tooclose Hallo Adapterinstellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="e5f65-125">Uw RDP-verbinding wordt opnieuw tot stand gebracht.</span><span class="sxs-lookup"><span data-stu-id="e5f65-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="e5f65-126">Typ vanaf een opdrachtprompt *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="e5f65-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="e5f65-127">Alle IP-adressen die u hebt toegevoegd, worden weergegeven en DHCP is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e5f65-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="e5f65-128">Validatie (Windows)</span><span class="sxs-lookup"><span data-stu-id="e5f65-128">Validation (Windows)</span></span>

<span data-ttu-id="e5f65-129">tooensure kunnen tooconnect toohello internet vanaf de secundaire IP-configuratie via Hallo openbare IP-adres dat is gekoppeld, nadat u hebt toegevoegd correct met behulp van de stappen hierboven, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e5f65-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="e5f65-130">U kunt alleen toohello Internet pingen secundaire IP-configuraties als Hallo configuratie een openbaar IP-adres dat is gekoppeld heeft.</span><span class="sxs-lookup"><span data-stu-id="e5f65-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="e5f65-131">Primaire IP-configuraties is een openbare IP-adres niet vereist tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="e5f65-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e5f65-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e5f65-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="e5f65-133">Open een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="e5f65-133">Open a terminal window.</span></span>
2. <span data-ttu-id="e5f65-134">Zorg ervoor dat u de hoofdgebruiker Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="e5f65-134">Make sure you are hello root user.</span></span> <span data-ttu-id="e5f65-135">Als u niet het geval is, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e5f65-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="e5f65-136">Hallo-configuratiebestand van netwerkinterface hello (ervan uitgaande dat 'eth0') bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e5f65-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="e5f65-137">Houd Hallo bestaande line-item voor dhcp.</span><span class="sxs-lookup"><span data-stu-id="e5f65-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="e5f65-138">Hallo primaire IP-adres blijft geconfigureerde als voorheen.</span><span class="sxs-lookup"><span data-stu-id="e5f65-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="e5f65-139">Een configuratie voor een extra statische IP-adres met de volgende opdrachten Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e5f65-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="e5f65-140">U moet een .CFG-bestand zien.</span><span class="sxs-lookup"><span data-stu-id="e5f65-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="e5f65-141">Open Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="e5f65-141">Open hello file.</span></span> <span data-ttu-id="e5f65-142">U ziet de volgende regels aan Hallo einde van bestand Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="e5f65-143">Hallo volgende regels na Hallo-regels die zijn opgenomen in dit bestand toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e5f65-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="e5f65-144">Hallo-bestand opslaan met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="e5f65-145">Opnieuw instellen van netwerkinterface Hallo Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e5f65-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e5f65-146">Zowel ifdown als ifup in dezelfde regel als een externe verbinding Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e5f65-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="e5f65-147">Controleer of Hallo IP-adres toohello netwerkinterface met de volgende opdracht Hallo is toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="e5f65-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="e5f65-148">U ziet Hallo IP mailadres dat u hebt toegevoegd als onderdeel van het Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="e5f65-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="e5f65-149">Linux (Redhat, CentOS en anderen)</span><span class="sxs-lookup"><span data-stu-id="e5f65-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="e5f65-150">Open een terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="e5f65-150">Open a terminal window.</span></span>
2. <span data-ttu-id="e5f65-151">Zorg ervoor dat u de hoofdgebruiker Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="e5f65-151">Make sure you are hello root user.</span></span> <span data-ttu-id="e5f65-152">Als u niet het geval is, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e5f65-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="e5f65-153">Voer uw wachtwoord in en volg de instructies.</span><span class="sxs-lookup"><span data-stu-id="e5f65-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="e5f65-154">Wanneer u de hoofdgebruiker Hallo bent, gaat u toohello scripts netwerkmap Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e5f65-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="e5f65-155">Lijst Hallo verwante ifcfg bestanden met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="e5f65-156">U ziet *ifcfg eth0* als een Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e5f65-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="e5f65-157">tooadd een IP-adres voor een configuratiebestand maken zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e5f65-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="e5f65-158">Houd er rekening mee dat er voor elke IP-configuratie één bestand moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e5f65-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="e5f65-159">Open Hallo *ifcfg-eth0:0* bestand met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="e5f65-160">Inhoud toohello-bestand toevoegen *eth0:0* in dit geval met volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="e5f65-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="e5f65-161">Worden ervoor tooupdate informatie op basis van uw IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e5f65-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="e5f65-162">Hallo-bestand opslaan met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e5f65-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="e5f65-163">Hallo network services opnieuw starten en zorg ervoor dat Hallo wijzigingen zijn voltooid door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="e5f65-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="e5f65-164">U ziet Hallo IP mailadres dat u hebt toegevoegd, *eth0:0*, in Hallo lijst geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e5f65-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="e5f65-165">Validatie (Linux)</span><span class="sxs-lookup"><span data-stu-id="e5f65-165">Validation (Linux)</span></span>

<span data-ttu-id="e5f65-166">tooensure zijn van kunnen tooconnect toohello internet vanaf de secundaire IP-configuratie via openbare IP-adres Hallo gekoppeld, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e5f65-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="e5f65-167">U kunt alleen toohello Internet pingen secundaire IP-configuraties als Hallo configuratie een openbaar IP-adres dat is gekoppeld heeft.</span><span class="sxs-lookup"><span data-stu-id="e5f65-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="e5f65-168">Primaire IP-configuraties is een openbare IP-adres niet vereist tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="e5f65-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="e5f65-169">Voor Linux VM's wanneer u probeert toovalidate uitgaande verbinding van een secundaire NIC, moet u de juiste routes tooadd.</span><span class="sxs-lookup"><span data-stu-id="e5f65-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="e5f65-170">Er zijn veel manieren toodo dit.</span><span class="sxs-lookup"><span data-stu-id="e5f65-170">There are many ways toodo this.</span></span> <span data-ttu-id="e5f65-171">Zie de relevante documentatie voor uw Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="e5f65-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="e5f65-172">Hallo volgende is een methode tooaccomplish dit:</span><span class="sxs-lookup"><span data-stu-id="e5f65-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="e5f65-173">Ervoor tooreplace zijn:</span><span class="sxs-lookup"><span data-stu-id="e5f65-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="e5f65-174">**10.0.0.5** met Hallo persoonlijke IP-adres met een openbare IP-adres gekoppeld tooit adres</span><span class="sxs-lookup"><span data-stu-id="e5f65-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="e5f65-175">**10.0.0.1** tooyour standaardgateway</span><span class="sxs-lookup"><span data-stu-id="e5f65-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="e5f65-176">**eth2** toohello-naam van uw secundaire NIC.</span><span class="sxs-lookup"><span data-stu-id="e5f65-176">**eth2** toohello name of your secondary NIC</span></span>
