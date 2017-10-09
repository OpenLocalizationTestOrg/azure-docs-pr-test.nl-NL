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
# <a name="connect-tooa-secure-service-with-hello-reverse-proxy"></a><span data-ttu-id="76a54-103">Verbinding maken met veilige tooa-service met Hallo omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="76a54-103">Connect tooa secure service with hello reverse proxy</span></span>

<span data-ttu-id="76a54-104">Dit artikel wordt uitgelegd hoe tooestablish beveiligde verbinding tussen Hallo omgekeerde proxy en services, waardoor u een beveiligd kanaal voor end-tooend.</span><span class="sxs-lookup"><span data-stu-id="76a54-104">This article explains how tooestablish secure connection between hello reverse proxy and services, thus enabling an end tooend secure channel.</span></span>

<span data-ttu-id="76a54-105">Verbinding maken met toosecure services wordt alleen ondersteund als omgekeerde proxy geconfigureerd toolisten op HTTPS is.</span><span class="sxs-lookup"><span data-stu-id="76a54-105">Connecting toosecure services is supported only when reverse proxy is configured toolisten on HTTPS.</span></span> <span data-ttu-id="76a54-106">Rest van Hallo document wordt ervan uitgegaan dat Hallo geval is.</span><span class="sxs-lookup"><span data-stu-id="76a54-106">Rest of hello document assumes this is hello case.</span></span>
<span data-ttu-id="76a54-107">Raadpleeg te[omgekeerde proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure Hallo omgekeerde proxy in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="76a54-107">Refer too[Reverse proxy in Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy) tooconfigure hello reverse proxy in Service Fabric.</span></span>

## <a name="secure-connection-establishment-between-hello-reverse-proxy-and-services"></a><span data-ttu-id="76a54-108">Beveiligde verbinding tot stand brengen tussen Hallo omgekeerde proxy en services</span><span class="sxs-lookup"><span data-stu-id="76a54-108">Secure connection establishment between hello reverse proxy and services</span></span> 

### <a name="reverse-proxy-authenticating-tooservices"></a><span data-ttu-id="76a54-109">Omgekeerde proxy tooservices verifiëren:</span><span class="sxs-lookup"><span data-stu-id="76a54-109">Reverse proxy authenticating tooservices:</span></span>
<span data-ttu-id="76a54-110">Hallo omgekeerde proxy identificeert zichzelf tooservices met behulp van een certificaat opgegeven met ***reverseProxyCertificate*** eigenschap in Hallo **Cluster** [type resourcesectie](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="76a54-110">hello reverse proxy identifies itself tooservices using its certificate, specified with ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="76a54-111">Services kunnen implementeren Hallo logica tooverify Hallo door aangeboden certificaat Hallo omgekeerde proxy.</span><span class="sxs-lookup"><span data-stu-id="76a54-111">Services can implement hello logic tooverify hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="76a54-112">Hallo-services kunnen configuratie-instellingen in het configuratiepakket Hallo Hallo geaccepteerd client certificaatdetails opgeven.</span><span class="sxs-lookup"><span data-stu-id="76a54-112">hello services can specify hello accepted client certificate details as configuration settings in hello configuration package.</span></span> <span data-ttu-id="76a54-113">Dit kan worden gelezen tijdens runtime en toovalidate Hallo certificaat voor Hallo omgekeerde proxy gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76a54-113">This can be read at runtime and used toovalidate hello certificate presented by hello reverse proxy.</span></span> <span data-ttu-id="76a54-114">Raadpleeg te[beheren toepassingsparameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd Hallo configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="76a54-114">Refer too[Manage application parameters](service-fabric-manage-multiple-environment-app-configuration.md) tooadd hello configuration settings.</span></span> 

### <a name="reverse-proxy-verifying-hello-services-identity-via-hello-certificate-presented-by-hello-service"></a><span data-ttu-id="76a54-115">Omgekeerde proxy controleren Hallo-service-identiteit via aangeboden door de service Hallo Hallo-certificaat:</span><span class="sxs-lookup"><span data-stu-id="76a54-115">Reverse proxy verifying hello service's identity via hello certificate presented by hello service:</span></span>
<span data-ttu-id="76a54-116">tooperform validatie van het servercertificaat Hallo-certificaten die worden aangeboden door Hallo-services, met omgekeerde proxy ondersteunt een Hallo volgende opties: None, ServiceCommonNameAndIssuer en ServiceCertificateThumbprints.</span><span class="sxs-lookup"><span data-stu-id="76a54-116">tooperform server certificate validation of hello certificates presented by hello services, reverse proxy supports one of hello following options: None, ServiceCommonNameAndIssuer, and ServiceCertificateThumbprints.</span></span>
<span data-ttu-id="76a54-117">tooselect een van deze drie opties opgeven Hallo **ApplicationCertificateValidationPolicy** in Hallo parameters sectie van ApplicationGateway/Http-element onder [fabricSettings](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="76a54-117">tooselect one of these three options, specify hello **ApplicationCertificateValidationPolicy** in hello parameters section of ApplicationGateway/Http element under [fabricSettings](service-fabric-cluster-fabric-settings.md).</span></span>

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

<span data-ttu-id="76a54-118">Raadpleeg de volgende sectie toohello voor meer informatie over aanvullende configuratie voor elk van deze opties.</span><span class="sxs-lookup"><span data-stu-id="76a54-118">Refer toohello next section for details about additional configuration for each of these options.</span></span>

### <a name="service-certificate-validation-options"></a><span data-ttu-id="76a54-119">Validatie van opties voor service-certificaat</span><span class="sxs-lookup"><span data-stu-id="76a54-119">Service certificate validation options</span></span> 

- <span data-ttu-id="76a54-120">**Geen**: omgekeerde proxy verificatie van Hallo via proxy servicecertificaat overslaat en Hallo veilige verbinding tot stand brengt.</span><span class="sxs-lookup"><span data-stu-id="76a54-120">**None**: Reverse proxy skips verification of hello proxied service certificate and establishes hello secure connection.</span></span> <span data-ttu-id="76a54-121">Dit is standaardgedrag Hallo.</span><span class="sxs-lookup"><span data-stu-id="76a54-121">This is hello default behavior.</span></span>
<span data-ttu-id="76a54-122">Geef Hallo **ApplicationCertificateValidationPolicy** met waarde **geen** in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.</span><span class="sxs-lookup"><span data-stu-id="76a54-122">Specify hello **ApplicationCertificateValidationPolicy** with value **None** in hello parameters section of ApplicationGateway/Http element.</span></span>

- <span data-ttu-id="76a54-123">**ServiceCommonNameAndIssuer**: omgekeerde proxy verifieert Hallo certificaat aangeboden door Hallo-service op basis van de algemene naam van het certificaat en de directe verlener vingerafdruk: Geef Hallo **ApplicationCertificateValidationPolicy**  met waarde **ServiceCommonNameAndIssuer** in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.</span><span class="sxs-lookup"><span data-stu-id="76a54-123">**ServiceCommonNameAndIssuer**: Reverse proxy verifies hello certificate presented by hello service based on certificate's common name and immediate issuer's thumbprint: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCommonNameAndIssuer** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="76a54-124">toospecify hello lijst met algemene servicenaam en de vingerafdrukken van de verlener, Voeg een **Http-ApplicationGateway/ServiceCommonNameAndIssuer** element onder fabricSettings, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="76a54-124">toospecify hello list of service common name and issuer thumbprints, add a **ApplicationGateway/Http/ServiceCommonNameAndIssuer** element under fabricSettings, as shown below.</span></span> <span data-ttu-id="76a54-125">Meerdere algemene naam van certificaat en verlener vingerafdruk paren kunnen worden toegevoegd in matrixelement Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="76a54-125">Multiple certificate common name and issuer thumbprint pairs can be added in hello parameters array element.</span></span> 

<span data-ttu-id="76a54-126">Als omgekeerde proxy voor Hallo eindpunt verbinding maakt toopresents een certificaat die algemene naam en de verlener vingerafdruk overeenkomt met een van Hallo waarden die u hier opgeeft, SSL-kanaal tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="76a54-126">If hello endpoint reverse proxy is connecting toopresents a certificate who's common name and  issuer thumbprint matches any of hello values specified here, SSL channel is established.</span></span> <span data-ttu-id="76a54-127">Omgekeerde proxy mislukt bij storing toomatch Hallo certificaatdetails Hallo clientaanvraag met statuscode 502 (ongeldige Gateway).</span><span class="sxs-lookup"><span data-stu-id="76a54-127">Upon failure toomatch hello certificate details, reverse proxy fails hello client's request with a 502 (Bad Gateway) status code.</span></span> <span data-ttu-id="76a54-128">Hallo HTTP-statusregel bevat ook Hallo zinsnede "Ongeldig SSL-certificaat."</span><span class="sxs-lookup"><span data-stu-id="76a54-128">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span> 

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


- <span data-ttu-id="76a54-129">**ServiceCertificateThumbprints**: omgekeerde proxy Hallo via proxy servicecertificaat op basis van de vingerafdruk wordt geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="76a54-129">**ServiceCertificateThumbprints**: Reverse proxy will verify hello proxied service certificate based on its thumbprint.</span></span> <span data-ttu-id="76a54-130">U kunt kiezen toogo deze route wanneer Hallo-services zijn geconfigureerd met zelfondertekende certificaten: Geef Hallo **ApplicationCertificateValidationPolicy** met waarde **ServiceCertificateThumbprints**in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.</span><span class="sxs-lookup"><span data-stu-id="76a54-130">You can choose toogo this route when hello services are configured with self signed certificates: Specify hello **ApplicationCertificateValidationPolicy** with value **ServiceCertificateThumbprints** in hello parameters section of ApplicationGateway/Http element.</span></span>

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

<span data-ttu-id="76a54-131">Geef ook op Hallo vingerafdrukken met een **ServiceCertificateThumbprints** item onder sectie opdrachtregelparameters van ApplicationGateway/HTTP-element.</span><span class="sxs-lookup"><span data-stu-id="76a54-131">Also specify hello thumbprints with a **ServiceCertificateThumbprints** entry under parameters section of ApplicationGateway/Http element.</span></span> <span data-ttu-id="76a54-132">Meerdere vingerafdrukken kunnen worden opgegeven als een door komma's gescheiden lijst in het veld waarde hello, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="76a54-132">Multiple thumbprints can be specified as a comma-separated list in hello value field, as shown below:</span></span>

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

<span data-ttu-id="76a54-133">Als Hallo vingerafdruk van het servercertificaat hello wordt vermeld in dit configuratie-item, lukt de omgekeerde proxy Hallo SSL-verbinding.</span><span class="sxs-lookup"><span data-stu-id="76a54-133">If hello thumbprint of hello server certificate is listed in this config entry, reverse proxy succeeds hello SSL connection.</span></span> <span data-ttu-id="76a54-134">Anders het Hallo-verbinding wordt beëindigd en mislukt Hallo van client-aanvraag met een 502 (ongeldige Gateway).</span><span class="sxs-lookup"><span data-stu-id="76a54-134">Otherwise, it terminates hello connection and fails hello client's request with a 502 (Bad Gateway).</span></span> <span data-ttu-id="76a54-135">Hallo HTTP-statusregel bevat ook Hallo zinsnede "Ongeldig SSL-certificaat."</span><span class="sxs-lookup"><span data-stu-id="76a54-135">hello HTTP status line will also contain hello phrase "Invalid SSL Certificate."</span></span>

## <a name="endpoint-selection-logic-when-services-expose-secure-as-well-as-unsecured-endpoints"></a><span data-ttu-id="76a54-136">Eindpunt selectie logica wanneer services beveiligd, evenals een onbeveiligde eindpunten weergeven</span><span class="sxs-lookup"><span data-stu-id="76a54-136">Endpoint selection logic when services expose secure as well as unsecured endpoints</span></span>
<span data-ttu-id="76a54-137">Service fabric ondersteunt meerdere eindpunten voor een service te configureren.</span><span class="sxs-lookup"><span data-stu-id="76a54-137">Service fabric supports configuring  multiple endpoints for a service.</span></span> <span data-ttu-id="76a54-138">Zie [Specify resources in a service manifest](service-fabric-service-manifest-resources.md) (Bronnen opgeven in een servicemanifest).</span><span class="sxs-lookup"><span data-stu-id="76a54-138">See [Specify resources in a service manifest](service-fabric-service-manifest-resources.md).</span></span>

<span data-ttu-id="76a54-139">Omgekeerde proxy selecteert een van de Hallo eindpunten tooforward Hallo aanvragen op basis van Hallo **ListenerName** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="76a54-139">Reverse proxy selects one of hello endpoints tooforward hello request based on hello  **ListenerName** query parameter.</span></span> <span data-ttu-id="76a54-140">Als dit niet is opgegeven, kan deze een willekeurig eindpunt in Hallo eindpunten lijst kiezen.</span><span class="sxs-lookup"><span data-stu-id="76a54-140">If this is not specified, it can pick any endpoint from hello endpoints list.</span></span> <span data-ttu-id="76a54-141">Dit is nu een HTTP of HTTPS-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="76a54-141">Now this can be an HTTP or HTTPS endpoint.</span></span> <span data-ttu-id="76a54-142">Er zijn mogelijk scenario's / vereisten waar u Hallo omgekeerde proxy toooperate in een 'veilige modus alleen' Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="76a54-142">There might be scenarios/requirements where you want hello reverse proxy toooperate in a "secure only mode", i.e</span></span> <span data-ttu-id="76a54-143">u wilt niet dat Hallo beveiligde omgekeerde proxy tooforward aanvragen toounsecured eindpunten.</span><span class="sxs-lookup"><span data-stu-id="76a54-143">you don't want hello secure reverse proxy tooforward requests toounsecured endpoints.</span></span> <span data-ttu-id="76a54-144">Dit kan worden bereikt door op te geven Hallo **SecureOnlyMode** configuratie-item met de waarde **true** in sectie van de parameters Hallo van ApplicationGateway/HTTP-element.</span><span class="sxs-lookup"><span data-stu-id="76a54-144">This can be achieved by specifying hello **SecureOnlyMode** configuration entry with value **true** in hello parameters section of ApplicationGateway/Http element.</span></span>   

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
> <span data-ttu-id="76a54-145">Als in **SecureOnlyMode**, als client heeft aangegeven dat een **ListenerName** tooan HTTP(unsecured) eindpunt overeenkomt, omgekeerde proxy mislukt Hallo-aanvraag met statuscode 404 HTTP (niet gevonden).</span><span class="sxs-lookup"><span data-stu-id="76a54-145">When operating in **SecureOnlyMode**, if client has specified a **ListenerName** corresponding tooan HTTP(unsecured) endpoint, reverse proxy fails hello request with a 404 (Not Found) HTTP status code.</span></span>

## <a name="setting-up-client-certificate-authentication-through-hello-reverse-proxy"></a><span data-ttu-id="76a54-146">Instellen van de verificatie van clientcertificaten via Hallo omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="76a54-146">Setting up client certificate authentication through hello reverse proxy</span></span>
<span data-ttu-id="76a54-147">SSL-beëindiging gebeurt op Hallo omgekeerde proxy en alle Hallo client certificaatgegevens verloren.</span><span class="sxs-lookup"><span data-stu-id="76a54-147">SSL termination happens at hello reverse proxy and all hello client certificate data is lost.</span></span> <span data-ttu-id="76a54-148">Voor Hallo services tooperform verificatie van clientcertificaten, stelt u Hallo **ForwardClientCertificate** instellen in de sectie van de parameters Hallo van ApplicationGateway/HTTP-element.</span><span class="sxs-lookup"><span data-stu-id="76a54-148">For hello services tooperform client certificate authentication, set hello **ForwardClientCertificate** setting in hello parameters section of ApplicationGateway/Http element.</span></span>

1. <span data-ttu-id="76a54-149">Wanneer **ForwardClientCertificate** te is ingesteld,**false**, reverse proxy niet vraagt de Hallo clientcertificaat tijdens de SSL-handshake met Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="76a54-149">When **ForwardClientCertificate** is set too**false**, reverse proxy will not request for hello client certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="76a54-150">Dit is standaardgedrag Hallo.</span><span class="sxs-lookup"><span data-stu-id="76a54-150">This is hello default behavior.</span></span>

2. <span data-ttu-id="76a54-151">Wanneer **ForwardClientCertificate** te is ingesteld,**true**, reverse Proxyaanvragen voor Hallo clientcertificaat tijdens de SSL-handshake met Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="76a54-151">When **ForwardClientCertificate** is set too**true**, reverse proxy requests for hello client's certificate during its SSL handshake with hello client.</span></span>
<span data-ttu-id="76a54-152">Wordt vervolgens doorgestuurd Hallo client certificaatgegevens in een aangepaste HTTP-header met de naam **X-clientcertificaat**.</span><span class="sxs-lookup"><span data-stu-id="76a54-152">It will then forward hello client certificate data in a custom HTTP header named **X-Client-Certificate**.</span></span> <span data-ttu-id="76a54-153">Hallo-kopwaarde is Hallo base64-gecodeerd PEM-indelingstekenreeks van Hallo clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="76a54-153">hello header value is hello base64 encoded PEM format string of hello client's certificate.</span></span> <span data-ttu-id="76a54-154">Hallo-service kan slagen/mislukken Hallo-aanvraag met de juiste statuscode na het Hallo-certificaatgegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="76a54-154">hello service can succeed/fail hello request with appropriate status code after inspecting hello certificate data.</span></span>
<span data-ttu-id="76a54-155">Hallo-client heeft een certificaat niet aanwezig omgekeerde proxy stuurt de header van een leeg als Hallo service ingang Hallo geval laten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76a54-155">If hello client does not present a certificate, reverse proxy forwards an empty header and let hello service handle hello case.</span></span>

> <span data-ttu-id="76a54-156">Omgekeerde proxy is een alleen-doorstuurserver.</span><span class="sxs-lookup"><span data-stu-id="76a54-156">Reverse proxy is a mere forwarder.</span></span> <span data-ttu-id="76a54-157">Een validatie van Hallo clientcertificaat wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="76a54-157">It will not perform any validation of hello client's certificate.</span></span>


## <a name="next-steps"></a><span data-ttu-id="76a54-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76a54-158">Next steps</span></span>
* <span data-ttu-id="76a54-159">Raadpleeg te[omgekeerde proxy tooconnect toosecure services configureren](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) voor Azure Resource Manager-sjabloon voorbeelden tooconfigure beveiligde omgekeerde proxy met Hallo andere service-certificaatopties voor validatie.</span><span class="sxs-lookup"><span data-stu-id="76a54-159">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="76a54-160">Een voorbeeld bekijken van HTTP-communicatie tussen services in een [voorbeeldproject op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="76a54-160">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="76a54-161">Externe procedureaanroepen weer dat met Reliable Services voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="76a54-161">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="76a54-162">Web-API die gebruikmaakt van OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="76a54-162">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="76a54-163">Clustercertificaten beheren</span><span class="sxs-lookup"><span data-stu-id="76a54-163">Manage cluster certificates</span></span>](service-fabric-cluster-security-update-certs-azure.md)
