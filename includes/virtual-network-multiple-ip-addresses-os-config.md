## <a name="os-config"></a>IP-adressen tooa VM-besturingssysteem toevoegen

Verbinding maken en aanmelding tooa VM die u hebt gemaakt met meerdere particuliere IP-adressen. Alle Hallo privé IP-adressen (inclusief Hallo primair) dat u toohello VM hebt toegevoegd, moet u handmatig toevoegen. Volgende stappen uit voor uw besturingssysteem VM Hallo voltooien:

### <a name="windows"></a>Windows

1. Typ vanaf een opdrachtprompt *ipconfig /all*.  Ziet u alleen Hallo *primaire* privé IP-adres (via DHCP).
2. Type *ncpa.cpl* in Hallo opdrachtprompt tooopen hello **netwerkverbindingen** venster.
3. Open Eigenschappen voor de juiste adapter Hallo Hallo: **LAN-verbinding**.
4. Dubbelklik op Internet Protocol versie 4 (IPv4).
5. Selecteer **gebruik Hallo volgende IP-adres** en voer de volgende waarden Hallo:

    * **IP-adres**: Voer Hallo *primaire* privé IP-adres
    * **Subnetmasker**: stel dit in op basis van uw subnet. Bijvoorbeeld, als hello subnet is een/24-subnet en Hallo subnet subnetmasker 255.255.255.0 is.
    * **Standaard-gateway**: Hallo eerste IP-adres in Hallo subnet. Als het subnet 10.0.0.0/24 is, is Hallo gateway IP-adres 10.0.0.1.
    * Klik op **gebruik Hallo volgende DNS-serveradressen** en voer de volgende waarden Hallo:
        * **DNS-voorkeursserver**: als u niet uw eigen DNS-server gebruikt, voert u 168.63.129.16 in.  Als u uw eigen DNS-server gebruikt, voert u Hallo IP-adres voor uw server.
    * Klik op Hallo **Geavanceerd** knop en extra IP-adressen toe te voegen. Elk Hallo secundaire privé IP-adressen die worden vermeld in stap 8 toohello NIC Hello hetzelfde subnet is opgegeven voor Hallo primaire IP-adres toevoegen.
        >[!WARNING] 
        >Als u bovenstaande stappen voor Hallo niet correct uitvoert, kunt u connectiviteit tooyour VM verliezen. Zorg ervoor dat Hallo-informatie voor stap 5 ingevoerd juist is voordat u doorgaat.

    * Klik op **OK** tooclose uit Hallo TCP/IP-instellingen en vervolgens **OK** opnieuw tooclose Hallo Adapterinstellingen wijzigen. Uw RDP-verbinding wordt opnieuw tot stand gebracht.

6. Typ vanaf een opdrachtprompt *ipconfig /all*. Alle IP-adressen die u hebt toegevoegd, worden weergegeven en DHCP is uitgeschakeld.


### <a name="validation-windows"></a>Validatie (Windows)

tooensure kunnen tooconnect toohello internet vanaf de secundaire IP-configuratie via Hallo openbare IP-adres dat is gekoppeld, nadat u hebt toegevoegd correct met behulp van de stappen hierboven, Hallo volgende opdracht gebruiken:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>U kunt alleen toohello Internet pingen secundaire IP-configuraties als Hallo configuratie een openbaar IP-adres dat is gekoppeld heeft. Primaire IP-configuraties is een openbare IP-adres niet vereist tooping toohello Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Open een terminalvenster.
2. Zorg ervoor dat u de hoofdgebruiker Hallo zijn. Als u niet het geval is, Voer Hallo volgende opdracht:

    ```bash
    sudo -i
    ```

3. Hallo-configuratiebestand van netwerkinterface hello (ervan uitgaande dat 'eth0') bijwerken.

    * Houd Hallo bestaande line-item voor dhcp. Hallo primaire IP-adres blijft geconfigureerde als voorheen.
    * Een configuratie voor een extra statische IP-adres met de volgende opdrachten Hallo toevoegen:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    U moet een .CFG-bestand zien.
4. Open Hallo-bestand. U ziet de volgende regels aan Hallo einde van bestand Hallo Hallo:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Hallo volgende regels na Hallo-regels die zijn opgenomen in dit bestand toevoegen:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Hallo-bestand opslaan met behulp van de volgende opdracht Hallo:

    ```bash
    :wq
    ```

7. Opnieuw instellen van netwerkinterface Hallo Hello volgende opdracht:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Zowel ifdown als ifup in dezelfde regel als een externe verbinding Hallo uitgevoerd.
    >

8. Controleer of Hallo IP-adres toohello netwerkinterface met de volgende opdracht Hallo is toegevoegd:

    ```bash
    ip addr list eth0
    ```

    U ziet Hallo IP mailadres dat u hebt toegevoegd als onderdeel van het Hallo-lijst.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS en anderen)

1. Open een terminalvenster.
2. Zorg ervoor dat u de hoofdgebruiker Hallo zijn. Als u niet het geval is, Voer Hallo volgende opdracht:

    ```bash
    sudo -i
    ```

3. Voer uw wachtwoord in en volg de instructies. Wanneer u de hoofdgebruiker Hallo bent, gaat u toohello scripts netwerkmap Hello volgende opdracht:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Lijst Hallo verwante ifcfg bestanden met behulp van de volgende opdracht Hallo:

    ```bash
    ls ifcfg-*
    ```

    U ziet *ifcfg eth0* als een Hallo-bestanden.

5. tooadd een IP-adres voor een configuratiebestand maken zoals hieronder wordt weergegeven. Houd er rekening mee dat er voor elke IP-configuratie één bestand moet worden gemaakt.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Open Hallo *ifcfg-eth0:0* bestand met de volgende opdracht Hallo:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Inhoud toohello-bestand toevoegen *eth0:0* in dit geval met volgende opdracht Hallo. Worden ervoor tooupdate informatie op basis van uw IP-adres.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Hallo-bestand opslaan met Hallo volgende opdracht:

    ```bash
    :wq
    ```

9. Hallo network services opnieuw starten en zorg ervoor dat Hallo wijzigingen zijn voltooid door het uitvoeren van de volgende opdrachten Hallo:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    U ziet Hallo IP mailadres dat u hebt toegevoegd, *eth0:0*, in Hallo lijst geretourneerd.

### <a name="validation-linux"></a>Validatie (Linux)

tooensure zijn van kunnen tooconnect toohello internet vanaf de secundaire IP-configuratie via openbare IP-adres Hallo gekoppeld, Hallo volgende opdracht gebruiken:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>U kunt alleen toohello Internet pingen secundaire IP-configuraties als Hallo configuratie een openbaar IP-adres dat is gekoppeld heeft. Primaire IP-configuraties is een openbare IP-adres niet vereist tooping toohello Internet.

Voor Linux VM's wanneer u probeert toovalidate uitgaande verbinding van een secundaire NIC, moet u de juiste routes tooadd. Er zijn veel manieren toodo dit. Zie de relevante documentatie voor uw Linux-distributie. Hallo volgende is een methode tooaccomplish dit:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Ervoor tooreplace zijn:
    - **10.0.0.5** met Hallo persoonlijke IP-adres met een openbare IP-adres gekoppeld tooit adres
    - **10.0.0.1** tooyour standaardgateway
    - **eth2** toohello-naam van uw secundaire NIC.
