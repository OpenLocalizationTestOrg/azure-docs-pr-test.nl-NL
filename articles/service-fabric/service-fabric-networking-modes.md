---
title: Netwerken modi voor services van Azure Service Fabric-container configureren | Microsoft Docs
description: Informatie over het instellen van de verschillende netwerken modi die ondersteuning biedt voor Azure Service Fabric.
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
ms.openlocfilehash: f792f9604a5d6e62551ed92c1049d6e2b4216417
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="5fb82-103">Netwerken modi voor service Fabric-container</span><span class="sxs-lookup"><span data-stu-id="5fb82-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="5fb82-104">De standaardwaarde netwerken modus in de Service Fabric-cluster voor containerservices aangeboden is de `nat` netwerken modus.</span><span class="sxs-lookup"><span data-stu-id="5fb82-104">The default networking mode offered in the Service Fabric cluster for container services is the `nat` networking mode.</span></span> <span data-ttu-id="5fb82-105">Met de `nat` netwerken met meer dan één containers service luistert naar de dezelfde poort leidt tot implementatiefouten modus.</span><span class="sxs-lookup"><span data-stu-id="5fb82-105">With the `nat` networking mode, having more than one containers service listening to the same port results in deployment errors.</span></span> <span data-ttu-id="5fb82-106">Voor verschillende uitgevoerd services die luisteren op dezelfde poort-, Service Fabric ondersteunt de `open` netwerken modus (versie 5.7 of hoger).</span><span class="sxs-lookup"><span data-stu-id="5fb82-106">For running several services that listen on the same port, Service Fabric supports the `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="5fb82-107">Met de `open` modus netwerken elke containerservice een dynamisch toegewezen IP-adres intern zodat meerdere services om te luisteren op dezelfde poort opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5fb82-107">With the `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services to listen to the same port.</span></span>   

<span data-ttu-id="5fb82-108">Dus met een type één service met een statische eindpunt gedefinieerd in het servicemanifest, nieuwe services kunnen worden gemaakt en verwijderd zonder implementatiefouten met behulp van de `open` netwerken modus.</span><span class="sxs-lookup"><span data-stu-id="5fb82-108">Thus, with a single service type with a static endpoint defined in the service manifest, new services may be created and deleted without deployment errors using the `open` networking mode.</span></span> <span data-ttu-id="5fb82-109">Op deze manier kunnen worden gebruikt dezelfde `docker-compose.yml` bestand met toewijzingen van statische poort voor het maken van meerdere services.</span><span class="sxs-lookup"><span data-stu-id="5fb82-109">Similarly, one can use the same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="5fb82-110">Met behulp van het dynamisch toegewezen IP-adres voor het detecteren van de services wordt niet aangeraden sinds de IP-adreswijzigingen wanneer de service opnieuw wordt gestart of verplaatst naar een ander knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5fb82-110">Using the dynamically assigned IP to discover services is not advisable since the IP address changes when the service restarts or moves to another node.</span></span> <span data-ttu-id="5fb82-111">Gebruik alleen de **Service Fabric Naming Service** of de **DNS-Service** voor servicedetectie.</span><span class="sxs-lookup"><span data-stu-id="5fb82-111">Only use the **Service Fabric Naming Service**  or the **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="5fb82-112">Alleen een totaal van 4096 IP-adressen per vNET in Azure zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="5fb82-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="5fb82-113">Dus de som van het aantal knooppunten en het aantal container service-exemplaren (met `open` netwerken) mag niet meer dan 4096 binnen een vNET.</span><span class="sxs-lookup"><span data-stu-id="5fb82-113">Thus, the sum of the number of nodes and the number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="5fb82-114">Voor dergelijke high-density scenario's, de `nat` netwerken modus wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="5fb82-114">For such high-density scenarios, the `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="5fb82-115">Open netwerken modus instellen</span><span class="sxs-lookup"><span data-stu-id="5fb82-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="5fb82-116">Instellen van de Azure Resource Manager-sjabloon te maken met DNS-Service en de IP-Provider onder `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="5fb82-116">Set up the Azure Resource Manager template by enabling DNS Service and the IP Provider under `fabricSettings`.</span></span> 

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

2. <span data-ttu-id="5fb82-117">De sectie network profiel instellen voor het toestaan van meerdere IP-adressen worden geconfigureerd op elk knooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="5fb82-117">Set up the network profile section to allow multiple IP addresses to be configured on each node of the cluster.</span></span> <span data-ttu-id="5fb82-118">Het volgende voorbeeld wordt een vijf IP-adressen per knooppunt (dus kunt u vijf service-exemplaren die luisteren naar de poort op elk knooppunt hebt) voor een Windows-Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="5fb82-118">The following example sets up five IP addresses per node (thus you can have five service instances listening to the port on each node) for a Windows Service Fabric cluster.</span></span>

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

    <span data-ttu-id="5fb82-119">Voor Linux-clusters, wordt een extra openbare IP-configuratie toegevoegd aan het toestaan van uitgaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="5fb82-119">For Linux clusters, an additional public IP configuration is added to allow outbound connectivity.</span></span> <span data-ttu-id="5fb82-120">Het volgende fragment stelt u vijf IP-adressen per knooppunt voor een Linux-cluster:</span><span class="sxs-lookup"><span data-stu-id="5fb82-120">The following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

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

3. <span data-ttu-id="5fb82-121">Voor Windows clusters, stelt u een NSG regel openen van UDP/53-poort voor het vNET met de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="5fb82-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for the vNET with the following values:</span></span>

   | <span data-ttu-id="5fb82-122">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="5fb82-122">Priority</span></span> |    <span data-ttu-id="5fb82-123">Naam</span><span class="sxs-lookup"><span data-stu-id="5fb82-123">Name</span></span>    |    <span data-ttu-id="5fb82-124">Bron</span><span class="sxs-lookup"><span data-stu-id="5fb82-124">Source</span></span>      |  <span data-ttu-id="5fb82-125">Doel</span><span class="sxs-lookup"><span data-stu-id="5fb82-125">Destination</span></span>   |   <span data-ttu-id="5fb82-126">Service</span><span class="sxs-lookup"><span data-stu-id="5fb82-126">Service</span></span>    | <span data-ttu-id="5fb82-127">Actie</span><span class="sxs-lookup"><span data-stu-id="5fb82-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="5fb82-128">2000</span><span class="sxs-lookup"><span data-stu-id="5fb82-128">2000</span></span> | <span data-ttu-id="5fb82-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="5fb82-129">Custom_Dns</span></span> | <span data-ttu-id="5fb82-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5fb82-130">VirtualNetwork</span></span> | <span data-ttu-id="5fb82-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5fb82-131">VirtualNetwork</span></span> | <span data-ttu-id="5fb82-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="5fb82-132">DNS (UDP/53)</span></span> | <span data-ttu-id="5fb82-133">Toestaan</span><span class="sxs-lookup"><span data-stu-id="5fb82-133">Allow</span></span>  |


4. <span data-ttu-id="5fb82-134">Geef de modus voor netwerken in het app-manifest voor elke service `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="5fb82-134">Specify the networking mode in the app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="5fb82-135">De modus `open` resulteert in de service een toegewijde IP-adres ophalen.</span><span class="sxs-lookup"><span data-stu-id="5fb82-135">The mode `open` results in the service getting a dedicated IP address.</span></span> <span data-ttu-id="5fb82-136">Als een modus niet is opgegeven, wordt het basic standaard `nat` modus.</span><span class="sxs-lookup"><span data-stu-id="5fb82-136">If a mode isn't specified, it defaults to the basic `nat` mode.</span></span> <span data-ttu-id="5fb82-137">Dus in het volgende voorbeeld manifest `NodeContainerServicePackage1` en `NodeContainerServicePackage2` kan elke luisteren op dezelfde poort (beide services luisteren `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="5fb82-137">Thus, in the following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen to the same port (both services are listening on `Endpoint1`).</span></span>

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
<span data-ttu-id="5fb82-138">U kunt combineren en overeenkomen met verschillende netwerken modi alle services in een toepassing voor een Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="5fb82-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="5fb82-139">U kunt dus sommige services hebben op `open` modus en sommige op `nat` netwerken modus.</span><span class="sxs-lookup"><span data-stu-id="5fb82-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="5fb82-140">Als een service is geconfigureerd met `nat`, de poort die wordt geluisterd naar moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="5fb82-140">When a service is configured with `nat`, the port it is listening to must be unique.</span></span> <span data-ttu-id="5fb82-141">De combinatie van netwerken modi voor verschillende services wordt niet ondersteund op Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="5fb82-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5fb82-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5fb82-142">Next steps</span></span>
<span data-ttu-id="5fb82-143">In dit artikel hebt u geleerd over netwerken modi die worden aangeboden door de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5fb82-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="5fb82-144">Service Fabric-toepassingsmodel</span><span class="sxs-lookup"><span data-stu-id="5fb82-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="5fb82-145">Service Fabric-service manifest resources</span><span class="sxs-lookup"><span data-stu-id="5fb82-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="5fb82-146">Een Windows-container implementeren op Service Fabric op Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5fb82-146">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="5fb82-147">Implementeert een Docker-container op Service Fabric op Linux</span><span class="sxs-lookup"><span data-stu-id="5fb82-147">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
