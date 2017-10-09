## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Hoe toocreate een klassiek VNet met Azure CLI
U kunt uw Azure-resources via de opdrachtprompt Hallo vanaf elke computer met Windows, Linux of OS x hello Azure CLI toomanage. een VNet met behulp van Azure CLI Hallo toocreate Hallo volgende stappen.

1. Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../articles/cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.
2. Voer Hallo **azure network vnet maken** opdracht toocreate een VNet en een subnet, zoals hieronder wordt weergegeven. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Verwachte uitvoer:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Naam van Hallo VNet toobe gemaakt. In ons scenario *TestVNet*
   * **-e (of--adresruimte)**. VNet-adresruimte. In ons scenario *192.168.0.0*
   * **-i (of de cidr-)**. Het netwerkmasker in CIDR-notatie. In ons scenario *16*.
   * **-n (of--subnet naam**). Naam van het eerste subnet Hallo. In ons scenario *FrontEnd*.
   * **-p (of--begin-ip-subnet)**. IP-adres voor het subnet of subnetadresruimte wordt gestart. In ons scenario *192.168.1.0*.
   * **-r (of--subnet cidr)**. Het netwerkmasker in CIDR-indeling voor het subnet. In ons scenario *24*.
   * **-l (of --locatie)**. Azure-regio waar Hallo VNet wordt gemaakt. In ons scenario *VS-midden*.
3. Voer Hallo **azure network vnet subnet maken** opdracht toocreate een subnet, zoals hieronder wordt weergegeven. Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (of--vnet naam**. Naam van Hallo VNet waar Hallo subnet wordt gemaakt. In ons scenario *TestVNet*.
   * **-n (of --naam)**. Naam van nieuw subnet Hallo. In ons scenario *back-end*.
   * **-a (of --adresvoorvoegsel)**. Subnet CIDR-blok. Vier in ons scenario *192.168.2.0/24*.
4. Voer Hallo **azure network vnet show** opdracht tooview Hallo eigenschappen van nieuwe vnet hello, zoals hieronder wordt weergegeven.
   
            azure network vnet show
   
    Dit is verwacht Hallo uitvoer voor Hallo bovenstaande opdracht:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

