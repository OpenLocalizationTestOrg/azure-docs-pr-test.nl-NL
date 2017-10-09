---
title: modi voor services van Azure Service Fabric-container networking aaaConfigure | Microsoft Docs
description: Meer informatie over hoe toosetup Hallo verschillende netwerken modi die Azure Service Fabric ondersteunt.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="72288-103">Netwerken modi voor service Fabric-container</span><span class="sxs-lookup"><span data-stu-id="72288-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="72288-104">Hallo netwerken standaardmodus wordt aangeboden op Hallo Service Fabric-cluster voor containerservices is Hallo `nat` netwerken modus.</span><span class="sxs-lookup"><span data-stu-id="72288-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="72288-105">Hello `nat` networking-modus met meer dan één containers service luisterende toohello resulteert in een implementatiefouten dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="72288-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="72288-106">Voor het uitvoeren van verschillende services die luisteren op dezelfde poort, Service Fabric ondersteunt Hallo Hallo `open` netwerken modus (versie 5.7 of hoger).</span><span class="sxs-lookup"><span data-stu-id="72288-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="72288-107">Hello `open` modus netwerken elke containerservice een dynamisch toegewezen IP-adres intern dezelfde poort zodat meerdere services toolisten toohello opgehaald.</span><span class="sxs-lookup"><span data-stu-id="72288-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="72288-108">Dus met een enkele servicetype met een statische eindpunt gedefinieerd in Hallo servicemanifest nieuwe services kunnen worden gemaakt en verwijderd zonder implementatiefouten bij het gebruik van Hallo `open` netwerken modus.</span><span class="sxs-lookup"><span data-stu-id="72288-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="72288-109">Op deze manier kunnen worden gebruikt dezelfde Hallo `docker-compose.yml` bestand met toewijzingen van statische poort voor het maken van meerdere services.</span><span class="sxs-lookup"><span data-stu-id="72288-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="72288-110">Met behulp van Hallo dynamisch toegewezen IP-toodiscover services wordt niet aangeraden sinds Hallo IP-adreswijzigingen als Hallo-service opnieuw wordt opgestart of tooanother knooppunt wordt bewogen.</span><span class="sxs-lookup"><span data-stu-id="72288-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="72288-111">Gebruik alleen Hallo **Service Fabric Naming Service** of Hallo **DNS-Service** voor servicedetectie.</span><span class="sxs-lookup"><span data-stu-id="72288-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="72288-112">Alleen een totaal van 4096 IP-adressen per vNET in Azure zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="72288-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="72288-113">Dus Hallo som van het aantal knooppunten Hallo en Hallo aantal container service-exemplaren (met `open` netwerken) mag niet meer dan 4096 binnen een vNET.</span><span class="sxs-lookup"><span data-stu-id="72288-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="72288-114">Voor zulke gevallen high-density Hallo `nat` netwerken modus wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="72288-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="72288-115">Open netwerken modus instellen</span><span class="sxs-lookup"><span data-stu-id="72288-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="72288-116">Hello Azure Resource Manager-sjabloon instellen door in te schakelen van DNS-Service en IP-Provider onder Hallo `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="72288-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="72288-117">Hallo netwerk profiel sectie tooallow meerdere IP-geconfigureerd op elk knooppunt van Hallo toobe adressen instellen.</span><span class="sxs-lookup"><span data-stu-id="72288-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="72288-118">Hallo volgende voorbeeld wordt een vijf IP-adressen per knooppunt (dus kunt u vijf exemplaren van de service toohello luisterpoort op elk knooppunt hebt) voor een Windows-Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="72288-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="72288-119">Voor Linux-clusters, wordt een extra openbare IP-configuratie tooallow uitgaande verbinding toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="72288-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="72288-120">Hallo stelt volgende fragment vijf IP-adressen per knooppunt voor een Linux-cluster:</span><span class="sxs-lookup"><span data-stu-id="72288-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="72288-121">Voor Windows-clusters, van een NSG instellen regel openen van poort UDP/53 Hallo vNET Hello volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="72288-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="72288-122">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="72288-122">Priority</span></span> |    <span data-ttu-id="72288-123">Naam</span><span class="sxs-lookup"><span data-stu-id="72288-123">Name</span></span>    |    <span data-ttu-id="72288-124">Bron</span><span class="sxs-lookup"><span data-stu-id="72288-124">Source</span></span>      |  <span data-ttu-id="72288-125">Doel</span><span class="sxs-lookup"><span data-stu-id="72288-125">Destination</span></span>   |   <span data-ttu-id="72288-126">Service</span><span class="sxs-lookup"><span data-stu-id="72288-126">Service</span></span>    | <span data-ttu-id="72288-127">Actie</span><span class="sxs-lookup"><span data-stu-id="72288-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="72288-128">2000</span><span class="sxs-lookup"><span data-stu-id="72288-128">2000</span></span> | <span data-ttu-id="72288-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="72288-129">Custom_Dns</span></span> | <span data-ttu-id="72288-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="72288-130">VirtualNetwork</span></span> | <span data-ttu-id="72288-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="72288-131">VirtualNetwork</span></span> | <span data-ttu-id="72288-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="72288-132">DNS (UDP/53)</span></span> | <span data-ttu-id="72288-133">Toestaan</span><span class="sxs-lookup"><span data-stu-id="72288-133">Allow</span></span>  |


4. <span data-ttu-id="72288-134">Hallo netwerken modus opgeven in de app-manifest Hallo voor elke service `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="72288-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="72288-135">Hallo modus `open` resulteert in het Hallo-service ophalen van een vast IP-adres.</span><span class="sxs-lookup"><span data-stu-id="72288-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="72288-136">Als u een modus niet is opgegeven, wordt standaard toohello basic `nat` modus.</span><span class="sxs-lookup"><span data-stu-id="72288-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="72288-137">Dus in Hallo manifest bijvoorbeeld na `NodeContainerServicePackage1` en `NodeContainerServicePackage2` kan elke toohello luisteren naar dezelfde poort (beide services luisteren `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="72288-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="72288-138">U kunt combineren en overeenkomen met verschillende netwerken modi alle services in een toepassing voor een Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="72288-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="72288-139">U kunt dus sommige services hebben op `open` modus en sommige op `nat` netwerken modus.</span><span class="sxs-lookup"><span data-stu-id="72288-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="72288-140">Als een service is geconfigureerd met `nat`, Hallo-poort luistert toomust is uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="72288-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="72288-141">De combinatie van netwerken modi voor verschillende services wordt niet ondersteund op Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="72288-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="72288-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72288-142">Next steps</span></span>
<span data-ttu-id="72288-143">In dit artikel hebt u geleerd over netwerken modi die worden aangeboden door de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="72288-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="72288-144">Service Fabric-toepassingsmodel</span><span class="sxs-lookup"><span data-stu-id="72288-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="72288-145">Service Fabric-service manifest resources</span><span class="sxs-lookup"><span data-stu-id="72288-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="72288-146">Een Windows-container tooService Fabric op Windows Server 2016 implementeren</span><span class="sxs-lookup"><span data-stu-id="72288-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="72288-147">Implementeert een Docker-container tooService Fabric op Linux</span><span class="sxs-lookup"><span data-stu-id="72288-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
