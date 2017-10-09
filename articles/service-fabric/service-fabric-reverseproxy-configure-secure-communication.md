---
title: Service Fabric aaaAzure reverse proxy veilige communicatie | Microsoft Docs
description: Configureer de omgekeerde proxy tooenable veilige end-to-end communicatie.
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/10/2017
ms.author: kavyako
ms.openlocfilehash: e1248dffe2c324373ad0d09d3f5f094db74480d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a>Verbinding maken met veilige tooa-service met Hallo omgekeerde proxy

Dit artikel wordt uitgelegd hoe tooestablish beveiligde verbinding tussen Hallo omgekeerde proxy en services, waardoor u een beveiligd kanaal voor end-tooend.

Verbinding maken met toosecure services wordt alleen ondersteund als omgekeerde proxy geconfigureerd toolisten op HTTPS is. Rest van Hallo document wordt ervan uitgegaan dat Hallo geval is.
Raadpleeg te[omgekeerde proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure Hallo omgekeerde proxy in Service Fabric.

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a>Beveiligde verbinding tot stand brengen tussen Hallo omgekeerde proxy en services 

### <a name="reverse-proxy-authenticating-tooservices"></a>Omgekeerde proxy tooservices verifiëren:
Hallo omgekeerde proxy identificeert zichzelf tooservices met behulp van een certificaat opgegeven met ***reverseProxyCertificate*** eigenschap in Hallo **Cluster** [type resourcesectie](../azure-resource-manager/resource-group-authoring-templates.md). Services kunnen implementeren Hallo logica tooverify Hallo door aangeboden certificaat Hallo omgekeerde proxy. Hallo-services kunnen configuratie-instellingen in het configuratiepakket Hallo Hallo geaccepteerd client certificaatdetails opgeven. Dit kan worden gelezen tijdens runtime en toovalidate Hallo certificaat voor Hallo omgekeerde proxy gebruikt. Raadpleeg te[beheren toepassingsparameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd Hallo configuratie-instellingen. 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a>Omgekeerde proxy controleren Hallo-service-identiteit via aangeboden door de service Hallo Hallo-certificaat:
tooperform validatie van het servercertificaat Hallo-certificaten die worden aangeboden door Hallo-services, met omgekeerde proxy ondersteunt een Hallo volgende opties: None, ServiceCommonNameAndIssuer en ServiceCertificateThumbprints.
tooselect een van deze drie opties opgeven Hallo **ApplicationCertificateValidationPolicy** in Hallo parameters sectie van ApplicationGateway/Http-element onder [fabricSettings](service-fabric-cluster-fabric-settings.md).

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "None"
              }
            ]
          }
        ],
        ...
}
```

Raadpleeg de volgende sectie toohello voor meer informatie over aanvullende configuratie voor elk van deze opties.

### <a name="service-certificate-validation-options"></a>Validatie van opties voor service-certificaat 

- **Geen**: omgekeerde proxy verificatie van Hallo via proxy servicecertificaat overslaat en Hallo veilige verbinding tot stand brengt. Dit is standaardgedrag Hallo.
Geef Hallo **ApplicationCertificateValidationPolicy** met waarde **geen** in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.

- **ServiceCommonNameAndIssuer**: omgekeerde proxy verifieert Hallo certificaat aangeboden door Hallo-service op basis van de algemene naam van het certificaat en de directe verlener vingerafdruk: Geef Hallo **ApplicationCertificateValidationPolicy**  met waarde **ServiceCommonNameAndIssuer** in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCommonNameAndIssuer"
              }
            ]
          }
        ],
        ...
}
```

toospecify hello lijst met algemene servicenaam en de vingerafdrukken van de verlener, Voeg een **Http-ApplicationGateway/ServiceCommonNameAndIssuer** element onder fabricSettings, zoals hieronder wordt weergegeven. Meerdere algemene naam van certificaat en verlener vingerafdruk paren kunnen worden toegevoegd in matrixelement Hallo-parameters. 

Als omgekeerde proxy voor Hallo eindpunt verbinding maakt toopresents een certificaat die algemene naam en de verlener vingerafdruk overeenkomt met een van Hallo waarden die u hier opgeeft, SSL-kanaal tot stand is gebracht. Omgekeerde proxy mislukt bij storing toomatch Hallo certificaatdetails Hallo clientaanvraag met statuscode 502 (ongeldige Gateway). Hallo HTTP-statusregel bevat ook Hallo zinsnede "Ongeldig SSL-certificaat." 

```json
{
"fabricSettings": [
          ...
          {
             "name": "ApplicationGateway/Http/ServiceCommonNameAndIssuer",
            "parameters": [
              {
                "name": "WinFabric-Test-Certificate-CN1",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 b4 22 11"
              },
              {
                "name": "WinFabric-Test-Certificate-CN2",
                "value": "b3 44 9b 01 8d 0f 68 39 a2 c5 d6 2b 5b 6c 6a c8 22 11 33 44"
              }
            ]
          }
        ],
        ...
}
```


- **ServiceCertificateThumbprints**: omgekeerde proxy Hallo via proxy servicecertificaat op basis van de vingerafdruk wordt geverifieerd. U kunt kiezen toogo deze route wanneer Hallo-services zijn geconfigureerd met zelfondertekende certificaten: Geef Hallo **ApplicationCertificateValidationPolicy** met waarde **ServiceCertificateThumbprints**in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
              {
                "name": "ApplicationCertificateValidationPolicy",
                "value": "ServiceCertificateThumbprints"
              }
            ]
          }
        ],
        ...
}
```

Geef ook op Hallo vingerafdrukken met een **ServiceCertificateThumbprints** item onder sectie opdrachtregelparameters van ApplicationGateway/HTTP-element. Meerdere vingerafdrukken kunnen worden opgegeven als een door komma's gescheiden lijst in het veld waarde hello, zoals hieronder wordt weergegeven:

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "ServiceCertificateThumbprints",
                "value": "78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 bf,78 12 20 5a 39 d2 23 76 da a0 37 f0 5a ed e3 60 1a 7e 64 b9"
              }
            ]
          }
        ],
        ...
}
```

Als Hallo vingerafdruk van het servercertificaat hello wordt vermeld in dit configuratie-item, lukt de omgekeerde proxy Hallo SSL-verbinding. Anders het Hallo-verbinding wordt beëindigd en mislukt Hallo van client-aanvraag met een 502 (ongeldige Gateway). Hallo HTTP-statusregel bevat ook Hallo zinsnede "Ongeldig SSL-certificaat."

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a>Eindpunt selectie logica wanneer services beveiligd, evenals een onbeveiligde eindpunten weergeven
Service fabric ondersteunt meerdere eindpunten voor een service te configureren. Zie [Specify resources in a service manifest](service-fabric-service-manifest-resources.md) (Bronnen opgeven in een servicemanifest).

Omgekeerde proxy selecteert een van de Hallo eindpunten tooforward Hallo aanvragen op basis van Hallo **ListenerName** queryparameter. Als dit niet is opgegeven, kan deze een willekeurig eindpunt in Hallo eindpunten lijst kiezen. Dit is nu een HTTP of HTTPS-eindpunt. Er zijn mogelijk scenario's / vereisten waar u Hallo omgekeerde proxy toooperate in een 'veilige modus alleen' Internet Explorer u wilt niet dat Hallo beveiligde omgekeerde proxy tooforward aanvragen toounsecured eindpunten. Dit kan worden bereikt door op te geven Hallo **SecureOnlyMode** configuratie-item met de waarde **true** in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.   

```json
{
"fabricSettings": [
          ...
          {
            "name": "ApplicationGateway/Http",
            "parameters": [
                ...
              {
                "name": "SecureOnlyMode",
                "value": true
              }
            ]
          }
        ],
        ...
}
```

> 
> Als in **SecureOnlyMode**, als client heeft aangegeven dat een **ListenerName** tooan HTTP(unsecured) eindpunt overeenkomt, omgekeerde proxy mislukt Hallo-aanvraag met statuscode 404 HTTP (niet gevonden).

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a>Instellen van de verificatie van clientcertificaten via Hallo omgekeerde proxy
SSL-beëindiging gebeurt op Hallo omgekeerde proxy en alle Hallo client certificaatgegevens verloren. Voor Hallo services tooperform verificatie van clientcertificaten, stelt u Hallo **ForwardClientCertificate** instellen in de sectie van de parameters Hallo van ApplicationGateway/HTTP-element.

1. Wanneer **ForwardClientCertificate** te is ingesteld,**false**, reverse proxy niet vraagt de Hallo clientcertificaat tijdens de SSL-handshake met Hallo-client.
Dit is standaardgedrag Hallo.

2. Wanneer **ForwardClientCertificate** te is ingesteld,**true**, reverse Proxyaanvragen voor Hallo clientcertificaat tijdens de SSL-handshake met Hallo-client.
Wordt vervolgens doorgestuurd Hallo client certificaatgegevens in een aangepaste HTTP-header met de naam **X-clientcertificaat**. Hallo-kopwaarde is Hallo base64-gecodeerd PEM-indelingstekenreeks van Hallo clientcertificaat. Hallo-service kan slagen/mislukken Hallo-aanvraag met de juiste statuscode na het Hallo-certificaatgegevens te bekijken.
Hallo-client heeft een certificaat niet aanwezig omgekeerde proxy stuurt de header van een leeg als Hallo service ingang Hallo geval laten gebruiken.

> Omgekeerde proxy is een alleen-doorstuurserver. Een validatie van Hallo clientcertificaat wordt niet uitgevoerd.


## <a name="next-steps"></a>Volgende stappen
* Raadpleeg te[omgekeerde proxy tooconnect toosecure services configureren](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) voor Azure Resource Manager-sjabloon voorbeelden tooconfigure beveiligde omgekeerde proxy met Hallo andere service-certificaatopties voor validatie.
* Een voorbeeld bekijken van HTTP-communicatie tussen services in een [voorbeeldproject op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Externe procedureaanroepen weer dat met Reliable Services voor externe toegang](service-fabric-reliable-services-communication-remoting.md)
* [Web-API die gebruikmaakt van OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Clustercertificaten beheren](service-fabric-cluster-security-update-certs-azure.md)
