## <a name="load-balancer"></a><span data-ttu-id="ac976-101">Load balancer</span><span class="sxs-lookup"><span data-stu-id="ac976-101">Load Balancer</span></span>
<span data-ttu-id="ac976-102">Een load balancer wordt gebruikt wanneer u wilt schalen van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ac976-102">A load balancer is used when you want to scale your applications.</span></span> <span data-ttu-id="ac976-103">Typische implementatiescenario's hebben betrekking op toepassingen die worden uitgevoerd op meerdere VM-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ac976-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="ac976-104">VM-exemplaren zijn fronted door een load balancer die voor de distributie van netwerkverkeer naar de verschillende exemplaren.</span><span class="sxs-lookup"><span data-stu-id="ac976-104">The VM instances are fronted by a load balancer that helps to distribute network traffic to the various instances.</span></span> 

![NIC's op een enkele virtuele machine](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="ac976-106">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ac976-106">Property</span></span> | <span data-ttu-id="ac976-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ac976-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ac976-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="ac976-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="ac976-109">een Load balancer kan een of meer front-end IP-adressen, ook bekend als een virtueel IP-adressen (VIP's) bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac976-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="ac976-110">Deze IP-adressen kunnen fungeren als inkomend voor het verkeer en openbare IP-adres of privé-IP</span><span class="sxs-lookup"><span data-stu-id="ac976-110">These IP addresses serve as ingress for the traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="ac976-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="ac976-111">*backendAddressPools*</span></span> |<span data-ttu-id="ac976-112">Dit zijn IP-adressen die zijn gekoppeld aan de VM-NIC's die load worden gedistribueerd</span><span class="sxs-lookup"><span data-stu-id="ac976-112">these are IP addresses associated with the VM NICs to which load will be distributed</span></span> |
| <span data-ttu-id="ac976-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="ac976-113">*loadBalancingRules*</span></span> |<span data-ttu-id="ac976-114">de regeleigenschap van een wijst een opgegeven front-end-IP-poort aan een set van back-end-IP-adressen en poort.</span><span class="sxs-lookup"><span data-stu-id="ac976-114">a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="ac976-115">Met één definitie van een load balancer-bron, kunt u meerdere regels voor taakverdeling, elke regel als gevolg van een combinatie van een front end IP-adres en poort en back-end-IP- en de poort die is gekoppeld aan virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ac976-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="ac976-116">De regel is één poort in de front end-pool te veel virtuele machines in de groep back-end</span><span class="sxs-lookup"><span data-stu-id="ac976-116">The rule is one port in the front end pool to many virtual machines in the back end pool</span></span> |
| <span data-ttu-id="ac976-117">*Tests*</span><span class="sxs-lookup"><span data-stu-id="ac976-117">*Probes*</span></span> |<span data-ttu-id="ac976-118">tests kunnen u om de status van de VM-exemplaren bij te houden.</span><span class="sxs-lookup"><span data-stu-id="ac976-118">probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="ac976-119">Als u een health test mislukt, de instantie van de virtuele machine gaat buiten rotatie automatisch</span><span class="sxs-lookup"><span data-stu-id="ac976-119">If a health probe fails, the virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="ac976-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="ac976-120">*inboundNatRules*</span></span> |<span data-ttu-id="ac976-121">NAT-regels definiëren van het binnenkomende verkeer via de voorgrond IP beëindigen en gedistribueerd naar de back-end-IP op een specifieke virtuele machine-instantie.</span><span class="sxs-lookup"><span data-stu-id="ac976-121">NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP to a specific virtual machine instance.</span></span> <span data-ttu-id="ac976-122">NAT-regel is een poort in de front-end-pool aan een virtuele machine in de groep back-end</span><span class="sxs-lookup"><span data-stu-id="ac976-122">NAT rule is one port in the front end pool to one virtual machine in the back end pool</span></span> |

<span data-ttu-id="ac976-123">Voorbeeld van de load balancer-sjabloon in Json-indeling:</span><span class="sxs-lookup"><span data-stu-id="ac976-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location to deploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[parameters('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[parameters('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="ac976-124">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ac976-124">Additional resources</span></span>
<span data-ttu-id="ac976-125">Lees [netwerktaakverdeler REST-API](https://msdn.microsoft.com/library/azure/mt163651.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac976-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

