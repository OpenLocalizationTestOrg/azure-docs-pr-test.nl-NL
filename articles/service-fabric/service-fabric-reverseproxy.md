---
title: Service Fabric aaaAzure omgekeerde proxy | Microsoft Docs
description: Service Fabric van omgekeerde proxy gebruiken voor communicatie toomicroservices van binnen en buiten Hallo-cluster.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Azure Service Fabric-omgekeerde proxy
Hallo omgekeerde proxy die ingebouwd in Azure Service Fabric adressen microservices in Hallo Service Fabric-cluster dat toegang biedt tot HTTP-eindpunten.

## <a name="microservices-communication-model"></a>Microservices communicatiemodel
Microservices in Service Fabric wordt doorgaans uitgevoerd op een subset van virtuele machines in het Hallo-cluster en kunt verplaatsen van een virtuele machine tooanother om verschillende redenen. Hallo-eindpunten voor microservices kunnen dus dynamisch wijzigen. Hallo doorsnee patroon toocommunicate toohello microservice is Hallo volgende lus oplossen:

1. Los de servicelocatie Hallo in eerste instantie via Hallo naming service.
2. Verbinding maken met toohello-service.
3. Hallo-oorzaak van verbindingsfouten en Hallo servicelocatie opnieuw los indien nodig.

Dit proces omvat doorgaans wrapping communicatie van client-side '-bibliotheken in een herhalingslus waarmee service Hallo-beleid oplossen en probeer het opnieuw.
Zie voor meer informatie [Connect en communiceren met services](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>Communicatie met behulp van Hallo omgekeerde proxy
Hallo omgekeerde proxy in Service Fabric wordt uitgevoerd op alle Hallo-knooppunten in het Hallo-cluster. Het Hallo hele service omzettingsproces namens een client uitvoert en stuurt Hallo clientaanvraag. Clients die worden uitgevoerd op Hallo cluster kunnen dus een client-side HTTP-communicatie bibliotheken tootalk toohello target-service gebruiken via Hallo omgekeerde proxy of lokaal uitgevoerd op hetzelfde knooppunt Hallo.

![Interne communicatie][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Microservices uit externe Hallo-cluster is bereikt
Hallo standaard externe communicatiemodel voor microservices is een opt-in-model waarbij elke service rechtstreeks van externe clients kan niet worden geopend. [Azure Load Balancer](../load-balancer/load-balancer-overview.md), dit is een netwerkgrens tussen microservices en externe clients voert netwerkadresomzetting en forwards externe aanvragen toointernal IP: poort eindpunten. toomake een microservice eindpunt rechtstreeks toegankelijk tooexternal clients, moet u eerst configureren Load Balancer tooforward verkeer tooeach poort die Hallo service gebruikt in Hallo-cluster. De meeste microservices, met name stateful microservices live niet bovendien op alle knooppunten van het Hallo-cluster. Hallo microservices kunt verplaatsen tussen knooppunten op failover. In dergelijke gevallen Load Balancer effectief Hallo locatie kan niet bepalen van het doelknooppunt Hallo van Hallo replica's toowhich moet het doorsturen van verkeer.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Microservices via een omgekeerde proxy uit cluster buiten Hallo Hallo bereikt
U kunt in plaats van het Hallo-poort van een afzonderlijke service wordt geconfigureerd in de Load Balancer, net Hallo poort van Hallo reverse proxy configureren in de Load Balancer. Deze configuratie kiest, kunnen clients buiten Hallo cluster services in de cluster Hallo bereiken met behulp van de omgekeerde proxy Hallo zonder aanvullende configuratie.

![Externe communicatie][0]

> [!WARNING]
> Wanneer u Hallo reverse proxy-poort in de Load Balancer configureert, zijn alle microservices in Hallo cluster die een HTTP-eindpunt adresseerbare van buiten Hallo-cluster.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>URI-indeling voor het adresseren van services met behulp van Hallo omgekeerde proxy
Hallo omgekeerde proxy gebruikt met die een specifieke uniform resource identifier (URI)-indeling tooidentify Hallo partitie toowhich Hallo binnenkomende serviceaanvraag moet worden doorgestuurd:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **HTTP (s):** Hallo omgekeerde proxy kan worden geconfigureerde tooaccept HTTP of HTTPS-verkeer. Voor het doorsturen van HTTPS, Raadpleeg te[secure tooa-service verbinding met de reverse proxy Hallo](service-fabric-reverseproxy-configure-secure-communication.md) zodra u omgekeerde proxy setup toolisten op HTTPS.
* **Cluster volledig gekwalificeerde domeinnaam (FQDN) | intern IP-adres:** voor externe clients, kunt u omgekeerde proxy Hallo configureren zodat deze bereikbaar is via Hallo clusterdomein, zoals mycluster.eastus.cloudapp.azure.com. Hallo omgekeerde proxy wordt standaard uitgevoerd op elk knooppunt. Voor interne verkeer worden Hallo reverse proxy bereikt op localhost of op een knooppunt van interne IP-adres bijvoorbeeld 10.0.0.1.
* **Poort:** dit Hallo-poort, zoals 19081, die is opgegeven voor de reverse proxy Hallo is.
* **ServiceInstanceName:** volledig gekwalificeerde naam op Hallo van Hallo geïmplementeerd service-exemplaar dat u tooreach zonder Hallo probeert "fabric: / ' schema. Bijvoorbeeld: tooreach hello *fabric: / myapp/MijnService/* service, die u wilt gebruiken *myapp/MijnService*.

    Hallo exemplaar servicenaam is hoofdlettergevoelig. Gebruik een ander hoofdlettergebruik voor Hallo-exemplaarnaam in Hallo-URL zorgt ervoor dat Hallo aanvragen toofail met 404 (niet gevonden).
* **Achtervoegsel-pad:** dit Hallo werkelijke URL-pad, zoals is *myapi/waarden/toevoegen/3*, voor Hallo-service die u wilt dat tooconnect naar.
* **PartitionKey:** voor een gepartitioneerde service, is dit Hallo berekende partitiesleutel van dat u wilt dat tooreach Hallo-partitie. Dit is *niet* Hallo partitie-ID GUID. Deze parameter is niet vereist voor services die gebruikmaken van Hallo singleton-partitieschema.
* **PartitionKind:** dit partitieschema Hallo-service is. Dit kan zijn 'Int64Range' of 'Met de naam'. Deze parameter is niet vereist voor services die gebruikmaken van Hallo singleton-partitieschema.
* **ListenerName** Hallo eindpunten van Hallo-service zijn Hallo vorm {"Eindpunten": {'Listener1': '1', 'Listener2': 'Endpoint2'...}}. Wanneer het Hallo-service geeft meerdere eindpunten, Hallo eindpunt herkent hieraan die clientaanvraag Hallo moet worden doorgestuurd. Dit kan worden weggelaten als Hallo-service slechts één listener heeft.
* **TargetReplicaSelector** Hiermee wordt aangegeven hoe Hallo doelreplica of instantie moet worden geselecteerd.
  * Wanneer de doelservice Hallo stateful is, Hallo TargetReplicaSelector kan bestaan uit een van de volgende Hallo: 'PrimaryReplica', 'RandomSecondaryReplica' of 'RandomReplica'. Als deze parameter niet is opgegeven, is standaard Hallo 'PrimaryReplica'.
  * Wanneer de doelservice Hallo staatloze, hervat omgekeerde proxy een willekeurig exemplaar van Hallo partitie tooforward Hallo serviceaanvraag aan.
* **Time-out:** Hiermee Hallo time-out voor gemaakt door Hallo omgekeerde proxy toohello service namens de clientaanvraag Hallo Hallo HTTP-aanvraag. Hallo-standaardwaarde is 60 seconden. Dit is een optionele parameter.

### <a name="example-usage"></a>Voorbeeld van syntaxis
Als u bijvoorbeeld eens Hallo *fabric: / MyApp/MyService* service die Hiermee opent u een HTTP-listener op Hallo URL te volgen:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Hieronder vindt u Hallo informatiebronnen voor Hallo-service:

* `/index.html`
* `/api/users/<userId>`

Als Hallo-service Hallo singleton partitieschema gebruikt, Hallo *PartitionKey* en *PartitionKind* queryreeksparameters zijn niet vereist en het Hallo-service kan worden bereikt met behulp van de gateway Hallo als:

* Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Intern:`http://localhost:19081/MyApp/MyService`

Als Hallo-service Hallo Uniform Int64 partitieschema gebruikt, Hallo *PartitionKey* en *PartitionKind* queryreeksparameters gebruikte tooreach een partitie van Hallo-service moeten zijn:

* Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Intern:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

Hallo bronpad tooreach Hallo resources die Hallo-service geeft, geplaatst na de servicenaam Hallo Hallo URL:

* Extern:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Intern:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

Hallo gateway stuurt vervolgens deze aanvragen toohello-service-URL:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Speciale verwerking voor het delen van poort services
Azure Application Gateway probeert tooresolve een service adres opnieuw en probeer Hallo aanvraag als een service kan niet worden bereikt. Dit is een belangrijk voordeel van Application Gateway omdat clientcode niet tooimplement een eigen service-oplossing nodig en omzetten van de lus.

In het algemeen als een service kan niet worden bereikt, is Hallo service-exemplaar of de replica verplaatst tooa ander knooppunt als onderdeel van de normale levenscyclus. Als dit gebeurt, kan een netwerk verbinding fout die aangeeft dat een eindpunt is dat niet langer openen op Hallo opgelost oorspronkelijk adres Application Gateway ontvangen.

Echter replica's of service-exemplaren kunnen delen een hostproces verstrekt en mogelijk ook delen van een poort wanneer deze wordt gehost door een op basis van het http.sys-webserver, met inbegrip van:

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET Core WebListener](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

In dit geval is het waarschijnlijk dat Hallo webserver is beschikbaar in het hostproces van Hallo en toorequests, maar Hallo opgelost service-exemplaar of replica is niet meer beschikbaar op Hallo host reageert. Hallo gateway ontvangt in dit geval een HTTP 404-respons van Hallo-webserver. Een HTTP 404 is dus twee verschillende betekenis:

- Case #1: adres van de Hallo-service correct is, maar Hallo resource die Hallo aangevraagde gebruiker bestaat niet.
- Case #2: serviceadres Hallo is onjuist en Hallo resource die Hallo aangevraagde gebruiker bestaat mogelijk op een ander knooppunt.

het eerste geval Hallo is een normale HTTP 404, wordt beschouwd als een gebruikersfout opgetreden. Hallo gebruiker heeft echter in de tweede geval Hallo aangevraagd een resource die bestaat. Application Gateway is toolocate die deze omdat het Hallo-service zelf is verplaatst. Toepassing behoeften tooresolve Hallo gatewayadres opnieuw en probeer het opnieuw Hallo-aanvraag.

Toepassingsgateway moet dus een toodistinguish manier tussen deze twee gevallen. toomake dat onderscheid, een hint van Hallo-server vereist is.

* Standaard Application Gateway wordt ervan uitgegaan dat het geval #2 en tooresolve en probleem Hallo aanvraag opnieuw probeert.
* tooindicate geval #1 tooApplication Gateway Hallo-service moet Hallo volgende HTTP-antwoordheader retourneren:

  `X-ServiceFabric : ResourceNotFound`

Deze HTTP-antwoordheader geeft een situatie met een normale HTTP 404 in welke Hallo aangevraagde resource niet bestaat en Application Gateway tooresolve Hallo-serviceadres niet opnieuw proberen.

## <a name="setup-and-configuration"></a>Installatie en configuratie

### <a name="enable-reverse-proxy-via-azure-portal"></a>Inschakelen van omgekeerde proxy via Azure portal

Azure portal biedt een optie tooenable omgekeerde proxy tijdens het maken van een nieuwe Service Fabric-cluster.
Onder **maken Service Fabric-cluster**, stap 2: clusterconfiguratie, configuratie van het type, Hallo selectievakje te selecteren 'Enable reverse proxy'.
Voor het configureren van beveiligde omgekeerde proxy SSL-certificaat kan worden opgegeven in stap 3: beveiliging, beveiligingsinstellingen voor het cluster configureren, selecteer Hallo selectievakje te 'Bevatten een SSL-certificaat voor reverse proxy' en Voer Hallo Certificaatdetails.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Inschakelen van omgekeerde proxy via Azure Resource Manager-sjablonen

U kunt Hallo [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) tooenable Hallo omgekeerde proxy in Service Fabric voor Hallo-cluster.

Raadpleeg te[HTTPS Reverse Proxy configureren in een beveiligde cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) voor Azure Resource Manager-sjabloon tooconfigure beveiligde omgekeerde proxy met een certificaat en verwerking van certificaat rollover voorbeelden.

Eerst, ontvangt u Hallo-sjabloon voor Hallo-cluster dat u wilt dat toodeploy. U kunt voorbeeldsjablonen hello gebruiken of een aangepaste Resource Manager-sjabloon maken. Vervolgens kunt u omgekeerde proxy Hallo inschakelen met behulp van Hallo stappen te volgen:

1. Een poort voor de reverse proxy Hallo definiëren in Hallo [gedeelte Parameters](../azure-resource-manager/resource-group-authoring-templates.md) van Hallo-sjabloon.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Hallo-poort opgeven voor elke Hallo nodetype objecten in Hallo **Cluster** [resourcesectie type](../azure-resource-manager/resource-group-authoring-templates.md).

    Hallo-poort wordt aangeduid met parameternamen hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. tooaddress hello omgekeerde proxy van externe hello Azure cluster hello Azure Load Balancer regels voor Hallo-poort die u hebt opgegeven in stap 1 instellen.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. SSL-certificaten op Hallo-poort voor de reverse proxy Hallo tooconfigure toevoegen Hallo certificaat toohello ***reverseProxyCertificate*** eigenschap in Hallo **Cluster** [type resourcesectie](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Ondersteuning van een reverse proxycertificaat dat afwijkt van Hallo cluster certificaat
 Als Hallo reverse proxy-certificaat af van het Hallo-certificaat dat Hallo cluster beveiligt wijkt, moeten Hallo eerder opgegeven certificaat moet worden geïnstalleerd op Hallo virtuele machine en toohello toegangsbeheerlijst (ACL) toegevoegd zodat Service Fabric kunt toegang tot dit. Dit kan worden gedaan in Hallo **virtualMachineScaleSets** [resourcesectie type](../resource-group-authoring-templates.md). Voor installatie, voegt u dat certificaat toohello osProfile. Hallo-extensie-gedeelte van Hallo sjabloon kunt Hallo certificaat in Hallo ACL bijwerken.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Wanneer u certificaten die afwijken van Hallo cluster certificaat tooenable Hallo omgekeerde proxy op een bestaand cluster gebruikt, Hallo reverse proxy-certificaat installeren en bijwerken Hallo ACL op Hallo cluster voordat u Hallo omgekeerde proxy inschakelt. Volledige Hallo [Azure Resource Manager-sjabloon](service-fabric-cluster-creation-via-arm.md) implementatie met behulp van Hallo instellingen vermeld eerder voordat u begint met een omgekeerde proxy voor implementatie tooenable Hallo in stap 1-4.

## <a name="next-steps"></a>Volgende stappen
* Een voorbeeld bekijken van HTTP-communicatie tussen services in een [voorbeeldproject op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Toosecure HTTP-service doorsturen met de reverse proxy Hallo](service-fabric-reverseproxy-configure-secure-communication.md)
* [Externe procedureaanroepen weer dat met Reliable Services voor externe toegang](service-fabric-reliable-services-communication-remoting.md)
* [Web-API die gebruikmaakt van OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [WCF-communicatie met behulp van Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* Raadpleeg voor aanvullende reverse proxy-configuratie-opties ApplicationGateway/Http-sectie in [aanpassen Service Fabric-clusterinstellingen](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
