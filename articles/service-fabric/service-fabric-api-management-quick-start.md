---
title: Service Fabric aaaAzure met API Management snel aan de slag | Microsoft Docs
description: Deze handleiding wordt getoond hoe tooquickly aan de slag met Azure API Management en Service Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Service Fabric met Azure API Management snel starten

Deze handleiding laat zien u hoe tooset Azure API Management met Service Fabric-up maken van en het configureren van uw eerste API bewerking toosend verkeer tooback-end-services in Service Fabric. toolearn meer informatie over Azure API Management-scenario's met Service Fabric Zie Hallo [overzicht](service-fabric-api-management-overview.md) artikel. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>API Management en Service Fabric tooAzure implementeren

de eerste stap Hallo is toodeploy API Management en een tooAzure Service Fabric-cluster in een gedeelde virtuele netwerk. Hiermee kunt API Management toocommunicate rechtstreeks met Service Fabric zodat deze kan direct tooany back-end-service in Service Fabric detectie-service, service partitie resolutie en voorwaarts verkeer uitvoeren.

### <a name="topology"></a>Topologie

Deze handleiding implementeert Hallo volgende topologie tooAzure waarin API Management en Service Fabric zijn in de subnetten van Hallo hetzelfde virtuele netwerk:

 ![Een bijschrift][sf-apim-topology-overview]

tooget aan de slag wilt, zijn Resource Manager-sjablonen beschikbaar voor elke stap van de implementatie:

 - Netwerktopologie:
    - [Network.JSON][network-arm]
    - [Network.parameters.JSON][network-parameters-arm]
 - Service Fabric-cluster:
    - [cluster.JSON][cluster-arm]
    - [cluster.parameters.JSON][cluster-parameters-arm]
 - API Management:
    - [APIM.JSON][apim-arm]
    - [APIM.parameters.JSON][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>TooAzure aanmelden en uw abonnement te selecteren

Maakt gebruik van deze handleiding [Azure PowerShell][azure-powershell]. Wanneer u een nieuwe PowerShell-sessie start, meld u aan tooyour Azure-account en uw abonnement te selecteren voordat u Azure-opdrachten uitvoeren.
 
Meld u aan tooyour Azure-account:

```powershell
PS > Login-AzureRmAccount
```

Selecteer uw abonnement:

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een nieuwe resourcegroep voor uw implementatie. Geef deze een naam en een locatie.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Hallo netwerktopologie implementeren

de eerste stap Hallo is tooset up Hallo netwerk topologie toowhich API Management en Hallo Service Fabric-cluster wordt geïmplementeerd. Hallo [network.json] [ network-arm] Resource Manager-sjabloon is geconfigureerd toocreate een virtueel netwerk (VNET) met twee subnetten en twee Netwerkbeveiligingsgroep groepen (NSG). 

Hallo [network.parameters.json] [ network-parameters-arm] parameterbestand Hallo namen bevat van Hallo subnetten en nsg's die API Management en Service Fabric om te worden geïmplementeerd. Voor deze handleiding hoeft Hallo parameterwaarden niet toobe gewijzigd. Hallo API Management en Service Fabric-Resource Manager-sjablonen gebruiken deze waarden, zodat als ze hier zijn gewijzigd, moet u wijzigen in de andere Resource Manager-sjablonen dienovereenkomstig Hallo. 

 1. Download Hallo Resource Manager-sjabloon en de parameters-bestand te volgen:

    - [Network.JSON][network-arm]
    - [Network.parameters.JSON][network-parameters-arm]

 2. Gebruik Hallo volgende PowerShell-opdracht toodeploy Hallo Resource Manager-sjabloon en de parameter bestanden voor Hallo netwerk instellen:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Hallo Service Fabric-cluster implementeren

Zodra de netwerkbronnen Hallo hebt implementeren, Hallo volgende stap is een Service Fabric-cluster toohello VNET in Hallo subnet toodeploy en NSG voor Hallo Service Fabric-cluster is aangewezen. Hallo Service Fabric-Resource Manager-sjabloon is voor deze zelfstudie vooraf geconfigureerde toouse Hallo namen van Hallo VNET, subnet en NSG die u hebt ingesteld in de vorige stap Hallo. 

Hallo Service Fabric-cluster Resource Manager-sjabloon is geconfigureerd toocreate een beveiligde cluster met Certificaatbeveiliging. Hallo-certificaat is gebruikte toosecure knooppunt naar communicatie voor uw cluster en toomanage gebruiker toegang tooyour Service Fabric-cluster. Dit certificaat tooaccess Hallo Service Fabric Naming Service API Management gebruikt voor servicedetectie.

Deze stap is vereist dat u een certificaat in de Sleutelkluis voor clusterbeveiliging. Zie voor meer informatie over het instellen van een beveiligde cluster met Sleutelkluis [in deze handleiding over het maken van een cluster in Azure Resource Manager gebruiken](service-fabric-cluster-creation-via-arm.md)

> [!NOTE]
> U kunt Azure Active Directory-verificatie in toevoeging toohello certificaat gebruikt voor toegang tot cluster toevoegen. Azure Active Directory is de aanbevolen manier toomanage gebruiker toegang tooyour Service Fabric-cluster hello, maar is niet nodig toocomplete in deze zelfstudie. Een certificaat is vereist in beide gevallen voor cluster knooppunt naar beveiliging en Azure API Management-verificatie op dit moment biedt geen ondersteuning voor verificatie met Azure Active Directory voor een Service Fabric-back-end.

 1. Download Hallo Resource Manager-sjabloon en de parameters-bestand te volgen:
 
    - [cluster.JSON][cluster-arm]
    - [cluster.parameters.JSON][cluster-parameters-arm]

 2. Vul Hallo leeg parameters in Hallo `cluster.parameters.json` bestand voor uw implementatie, met inbegrip van Hallo [Sleutelkluis informatie](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) voor uw cluster-certificaat.

 3. Hallo volgende PowerShell-opdracht toodeploy Hallo Resource Manager-sjabloon en de parameter bestanden toocreate Hallo Service Fabric-cluster gebruiken:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Implementeren van API Management

Ten slotte implementeren API Management toohello VNET in Hallo subnet en NSG die is aangewezen voor API Management. U hoeft niet toowait voor Hallo Service Fabric-cluster implementatie toofinish voordat u implementeert API Management. 

Hallo API Management-Resource Manager-sjabloon is voor deze zelfstudie vooraf geconfigureerde toouse Hallo namen van Hallo VNET, subnet en NSG die u hebt ingesteld in de vorige stap Hallo. 

 1. Download Hallo Resource Manager-sjabloon en de parameters-bestand te volgen:
 
    - [APIM.JSON][apim-arm]
    - [APIM.parameters.JSON][apim-parameters-arm]

 2. Vul Hallo leeg parameters in Hallo `apim.parameters.json` voor uw implementatie.

 3. Hallo volgende PowerShell-opdracht toodeploy Hallo Resource Manager-sjabloon en de parameter bestanden voor API Management gebruiken:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>API Management configureren

Zodra uw API Management en Service Fabric-cluster worden geïmplementeerd, kunt u een Service Fabric-back-end kunt configureren in API Management. Hiermee kunt u toocreate een back-end-service-beleid waarmee verkeer tooyour Service Fabric-cluster worden verzonden.

### <a name="api-management-security"></a>Beveiliging van API Management

tooconfigure hello Service Fabric-back-end, moet u eerst tooconfigure API Management-beveiligingsinstellingen. tooconfigure beveiligingsinstellingen, gaat u tooyour API Management-service in hello Azure-portal.

#### <a name="enable-hello-api-management-rest-api"></a>Hallo API Management REST API inschakelen

Hallo API Management REST API is momenteel Hallo alleen manier tooconfigure een back-endservice. de eerste stap Hallo tooenable Hallo API Management REST API is en beveilig deze.

 1. Selecteer in de Hallo API Management-service, **Management-API - voorbeeld** onder **beveiliging**.
 2. Controleer de Hallo **API Management REST API inschakelen** selectievakje.
 3. Hallo Management API URL Opmerking: dit is Hallo URL gebruiken we later tooset up Hallo Service Fabric-back-end
 4. Genereren een **toegangstoken** als u een vervaldatum en een sleutel selecteert, klikt u vervolgens op Hallo **genereren** knop naar de onderkant Hallo van Hallo pagina.
 5. Kopiëren Hallo **toegangstoken** en sla deze - kun je in Hallo stappen te volgen. Houd er rekening mee dat deze verschilt van Hallo primaire en secundaire sleutel.

#### <a name="upload-a-service-fabric-client-certificate"></a>Een Service Fabric-client-certificaat uploaden

API Management moet verifiëren met uw Service Fabric-cluster voor detectie van de service met behulp van een clientcertificaat dat toegang tooyour cluster heeft. Ter vereenvoudiging Hallo deze zelfstudie maakt gebruik van uw cluster hetzelfde certificaat bij het maken van de Service Fabric-cluster hello, die standaard gebruikte tooaccess kan worden opgegeven.

 1. Selecteer in de Hallo API Management-service, **clientcertificaten - PREVIEW** onder **beveiliging**.
 2. Klik op Hallo **+ toevoegen** knop
 2. Selecteer Hallo persoonlijke sleutelbestand (.pfx) van Hallo cluster certificaat dat u hebt opgegeven bij het maken van uw Service Fabric-cluster, een naam geven en Hallo-wachtwoord voor persoonlijke sleutel bevatten.

> [!NOTE]
> Deze zelfstudie wordt Hallo hetzelfde certificaat voor verificatie en cluster knooppunt naar de clientbeveiligingssessie. U kunt een afzonderlijke clientcertificaat hebt u een geconfigureerde tooaccess Service Fabric-cluster.

### <a name="configure-hello-backend"></a>Hallo back-end configureren

Nu dat API Management-beveiliging is geconfigureerd, kunt u Hallo Service Fabric-back-end kunt configureren. Hallo Service Fabric-cluster is voor Service Fabric-back-ends, Hallo backend, in plaats van een specifieke Service Fabric-service. Hiermee wordt een enkele beleidsregel tooroute toomore dan één service in Hallo-cluster.

Deze stap is vereist Hallo-toegangstoken die u eerder hebt gegenereerd en vingerafdruk voor uw cluster-certificaat dat u hebt geüpload tooAPI Management in de vorige stap Hallo Hallo.

> [!NOTE]
> Als u een afzonderlijke clientcertificaat in de vorige stap Hallo voor API Management gebruikt, moet u de vingerafdruk van het Hallo voor Hallo clientcertificaat in toevoeging toohello cluster certificaatvingerafdruk in deze stap.

Verzenden Hallo HTTP PUT-aanvraag toohello API Management-API-URL die u eerder hebt genoteerd bij het inschakelen van Hallo API Management REST API tooconfigure Hallo Service Fabric back-endservice te volgen. U ziet een `HTTP 201 Created` antwoord als Hallo-opdracht is geslaagd. Zie voor meer informatie over elk veld Hallo API Management [back-end voor API-naslagdocumentatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

HTTP-opdracht en URL:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

Headers voor aanvraag:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Hoofdtekst van de aanvraag:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Hallo **url** parameter hier is een volledig gekwalificeerde servicenaam van een service in het cluster die alle aanvragen zijn doorgestuurd tooby standaard als er geen servicenaam is opgegeven in een back-end-beleid. U kunt de naam van een valse service, zoals "fabric: / valse/service ' als u niet van plan toohave een fallback-service bent.

Raadpleeg toohello API Management [back-end voor API-naslagdocumentatie](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) voor meer informatie over elk veld.

#### <a name="example"></a>Voorbeeld

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Een Service Fabric-back-end-service implementeren

Nu dat u Service Fabric geconfigureerd als een back-end tooAPI Management Hallo hebt, kunt u back-end-beleid schrijven voor uw API's die verkeer tooyour Service Fabric-services verzenden. Maar u moet eerst een service die wordt uitgevoerd in Service Fabric tooaccept aanvragen.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Een Service Fabric-service met een HTTP-eindpunt maken

Voor deze zelfstudie maken we een eenvoudige staatloze ASP.NET Core betrouwbare Service met Web-API Hallo-project standaardsjabloon. Hiermee maakt u een HTTP-eindpunt voor uw service, die u via Azure API Management gebruiken zult:

```
/api/values
```

Start [instellen van uw ontwikkelomgeving voor het ontwikkelen van ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Zodra uw ontwikkelomgeving is ingesteld, start Visual Studio als beheerder en maak een ASP.NET Core-service:

 1. In Visual Studio-Selecteer-Bestand > Nieuw Project.
 2. Selecteer Hallo Service Fabric-toepassing sjabloon onder Cloud en geef deze de naam **'ApiApplication'**.
 3. Selecteer Hallo ASP.NET Core-servicesjabloon en naam Hallo project **'WebApiService'**.
 4. Hallo Web API ASP.NET Core 1.1-projectsjabloon selecteren.
 5. Zodra het Hallo-project is gemaakt, opent u `PackageRoot\ServiceManifest.xml` en verwijder Hallo `Port` kenmerk van de eindpuntconfiguratie resource Hallo:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    Hierdoor kunnen Service Fabric toospecify een poort dynamisch van Hallo toepassingspoortbereik, dat wordt geopend via Hallo Netwerkbeveiligingsgroep in Hallo cluster Resource Manager-sjabloon, zodat u verkeer tooflow tooit van API Management.
 
 6. Druk op F5 in Visual Studio tooverify Hallo web-API is lokaal beschikbaar. 

    Service Fabric Explorer te openen en inzoomen tooa specifieke instantie van Hallo ASP.NET Core service toosee Hallo basisadres Hallo service luistert op. Voeg `/api/values` toohello basisadres en geopend in een browser. Hiermee wordt de Hallo Get-methode op Hallo ValuesController in Hallo Web API-sjabloon. Deze retourneert Hallo standaardreactie die wordt geleverd door het Hallo-sjabloon, een JSON-matrix die twee tekenreeksen bevat:

    ```json
    ["value1", "value2"]`
    ```

    Dit is Hallo-eindpunt dat u via API Management in Azure gebruiken zult.

 7. Ten slotte Hallo toepassing tooyour cluster in Azure implementeren. [Met Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), met de rechtermuisknop op Hallo Application-project en selecteer **publiceren**. Geef uw clustereindpunt (bijvoorbeeld `mycluster.westus.cloudapp.azure.com:19000`) toodeploy Hallo toepassing tooyour Service Fabric-cluster in Azure.

Een stateless service met de naam van ASP.NET Core `fabric:/ApiApplication/WebApiService` moet nu worden uitgevoerd in het Service Fabric-cluster in Azure.

## <a name="create-an-api-operation"></a>Een API-bewerking maken

Nu we klaar toocreate een bewerking in API Management Hallo die toocommunicate voor het gebruik van externe clients met ASP.NET Core staatloze service wordt uitgevoerd op Hallo Service Fabric-cluster.

 1. Meld u bij toohello Azure-portal en navigeer tooyour API Management service-implementatie.
 2. Selecteer in de blade voor Hallo API Management-service, **-API's - Preview**
 3. Een nieuwe API toevoegen door te klikken op Hallo **leeg API** vak en invullen van het dialoogvenster Hallo:

     - **Webservice-URL**: voor Service Fabric-back-ends, deze URL-waarde niet wordt gebruikt. Hier kunt u een willekeurige waarde plaatsen. Gebruik voor deze zelfstudie: `http://servicefabric`.
     - **Naam**: Geef een naam op voor uw API. Gebruik voor deze zelfstudie `Service Fabric App`.
     - **URL-schema**: Selecteer HTTP, HTTPS of beide. Gebruik voor deze zelfstudie `both`.
     - **Achtervoegsel voor API-URL**: Geef een achtervoegsel voor de API. Gebruik voor deze zelfstudie `myapp`.
 
 4. Zodra het Hallo-API is gemaakt, klikt u op **+ toevoegbewerking** tooadd een front-API-bewerking. Vul Hallo waarden:
    
     - **URL**: Selecteer `GET` en een URL-pad opgeven voor Hallo API. Gebruik voor deze zelfstudie `/api/values`.
     
       Standaard worden Hallo URL-pad hier opgegeven URL-pad Hallo toohello backend Service Fabric-service verzonden. Als u Hallo dezelfde URL-pad hier uw service in dit geval gebruikt `/api/values`, vervolgens Hallo-bewerking werkt zonder verdere aanpassing. U kunt ook een URL-pad hier die verschilt van Hallo URL-pad gebruikt door uw back-end Service Fabric-service opgeven in dat geval u ziet ook nodig toospecify herschrijven van een pad in uw beleid voor de bewerking later.
     - **Weergavenaam**: Geef een naam op voor Hallo API. Gebruik voor deze zelfstudie `Values`.

## <a name="configure-a-backend-policy"></a>Een back-end-beleid configureren

Hallo back-end van beleid koppelt alles bij elkaar. Dit is waar het configureren van Hallo back-end Service Fabric toowhich serviceaanvragen worden gerouteerd. U kunt deze bewerking beleid tooany API toepassen. Hallo [back-endconfiguratie voor Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) Hallo volgende aanvragen routering besturingselementen bevat: 
 - Service-exemplaar selecteren door op te geven van een naam in Service Fabric-service-exemplaar, ofwel hardcoded (bijvoorbeeld `"fabric:/myapp/myservice"`) of gegenereerd op basis van Hallo HTTP-aanvraag (bijvoorbeeld `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Omzetting van de partitie een partitiesleutel met behulp van een Service Fabric-partitieschema te genereren.
 - De selectie van de replica voor stateful services.
 - Resolutie voorwaarden waarmee u toospecify Hallo voorwaarden voor een servicelocatie opnieuw op te lossen en het opnieuw verzenden van een aanvraag opnieuw.

Voor deze zelfstudie maakt u een back-end-beleid routes aanvragen rechtstreeks toohello ASP.NET Core staatloze service eerder hebt geïmplementeerd:

 1. Selecteren en bewerken van Hallo **inkomende beleidsregels** voor Hallo `Values` bewerking door te klikken op het bewerkingspictogram Hallo en vervolgens te klikken op **codeweergave**.
 2. Hallo beleid code-editor, Voeg een `set-backend-service` beleid onder inkomende beleidsregels, zoals hier wordt weergegeven en klik op Hallo **opslaan** knop:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Raadpleeg voor een volledige set van kenmerken voor Service Fabric-back-end beleid toohello [back-end-documentatie voor API Management](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Hallo API tooa product toevoegen. 

Voordat u Hallo API aanroepen kunt, moet worden deze tooa product waar u toousers toegang kunt geven toegevoegd. 

 1. Selecteer in de Hallo API Management-service, **producten - PREVIEW**.
 2. Standaard API Management providers twee producten: Starter en onbeperkt. Selecteer Hallo onbeperkte product.
 3. Selecteer de API's.
 4. Klik op Hallo **+ toevoegen** knop.
 5. Selecteer Hallo `Service Fabric App` API die u hebt gemaakt in de vorige stappen Hallo en klikt u op Hallo **Selecteer** knop.

### <a name="test-it"></a>Testen

U kunt nu verzenden van een aanvraag tooyour back-endservice in Service Fabric via API Management rechtstreeks vanuit hello Azure-portal.

 1. Selecteer in de Hallo API Management-service, **API - voorbeeld**.
 2. In Hallo `Service Fabric App` API die u hebt gemaakt in de vorige stappen hello, selecteer Hallo **Test** tabblad.
 3. Klik op Hallo **verzenden** knop toosend een test aanvraag toohello back-endservice.

## <a name="next-steps"></a>Volgende stappen

U hebt op dit moment een basisinstellingen met Service Fabric en API Management.

Deze zelfstudie wordt verificatie op basis van certificaten basisgebruiker voor uw Service Fabric-cluster tooget die u snel instellen. Meer geavanceerde gebruikersverificatie voor uw Service Fabric-cluster heeft de voorkeur boven met [Azure Active Directory-verificatie](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Vervolgens [maken en configureren van geavanceerde productinstellingen in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare uw toepassing op concrete verkeer.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
