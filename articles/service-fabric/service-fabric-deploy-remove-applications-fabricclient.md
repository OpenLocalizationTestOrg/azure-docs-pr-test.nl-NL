---
title: aaaAzure implementatie voor Service Fabric-toepassing | Microsoft Docs
description: Hallo FabricClient APIs toodeploy gebruiken en verwijderen van toepassingen in Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Implementeren en toepassingen die gebruikmaken van FabricClient verwijderen
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient-API's](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Eenmaal een [toepassingstype zijn ingepakt][10], deze gereed is voor implementatie in een Azure Service Fabric-cluster. Implementatie omvat het Hallo drie stappen te volgen:

1. Hallo pakket toohello installatiekopie toepassingsarchief uploaden
2. Registratie van toepassingstype Hallo
3. Exemplaar van de toepassing hello maken

Nadat een toepassing wordt geïmplementeerd en een exemplaar in Hallo-cluster wordt uitgevoerd, kunt u Hallo toepassingsexemplaar en het toepassingstype verwijderen. toocompletely verwijderen een toepassing uit Hallo cluster omvat Hallo stappen te volgen:

1. Met een toepassingsexemplaar van de hello verwijderen (of verwijderen)
2. Hef de registratie van toepassingstype Hallo als u deze niet langer nodig hebt
3. Hallo-toepassingspakket verwijderen uit de installatiekopieopslag Hallo

Als u [Visual Studio voor het implementeren en foutopsporing in toepassingen](service-fabric-publish-app-remote-cluster.md) op uw lokaal ontwikkelcluster alle voorgaande stappen Hallo automatisch via een PowerShell-script worden verwerkt.  Dit script is gevonden in Hallo *Scripts* map van het toepassingsproject Hallo. Dit artikel vindt u achtergrond op script doet zodat u kunt uitvoeren Hallo dezelfde bewerkingen buiten Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Verbinding maken met cluster toohello
Verbinding maken met cluster toohello door het maken van een [FabricClient](/dotnet/api/system.fabric.fabricclient) exemplaar voordat u een van de Hallo codevoorbeelden in dit artikel. Voor voorbeelden van verbindende tooa lokaal ontwikkelcluster of een externe-cluster of -cluster beveiligd met Azure Active Directory, X509 certificaten of Windows Active Directory-Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). tooconnect toohello lokaal ontwikkelcluster, voert u de volgende Hallo:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Hallo-toepassingspakket uploaden
Stel dat u maakt en een toepassing met de naam van het pakket *Mijntoepassing* in Visual Studio. Standaard is Hallo naam van het toepassingstype die worden vermeld in Hallo ApplicationManifest.xml 'MyApplicationType'.  Hallo-toepassingspakket dat manifest van de benodigde toepassing hello, manifesten service en config-code-gegevens pakketten bevat, zich in *C:\Users\&lt; gebruikersnaam&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.

Uploaden van het Hallo-toepassingspakket plaatst het in een locatie die toegankelijk is voor Hallo interne Service Fabric-onderdelen. Service Fabric verifieert Hallo-toepassingspakket tijdens de registratie van het toepassingspakket Hallo Hallo. Als u wilt dat tooverify Hallo toepassingspakket lokaal (dat wil zeggen, voordat u uploadt), gebruiken Hallo [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Hallo [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploadt Hallo pakket toohello cluster installatiekopie toepassingsarchief. 

Als het Hallo-toepassingspakket is groot en/of veel bestanden, kunt u [comprimeert](service-fabric-package-apps.md#compress-a-package) en kopieer het toohello installatiekopieopslag met behulp van PowerShell. Hallo compressie vermindert Hallo grootte en het aantal bestanden Hallo.

Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.

## <a name="register-hello-application-package"></a>Hallo-toepassingspakket registreren
type van de toepassing Hello en versie gedeclareerd in het toepassingsmanifest Hallo komen beschikbaar voor gebruik wanneer het Hallo-toepassingspakket is geregistreerd. Hallo system Hallo pakket geüpload in de vorige stap Hallo leest, verifieert Hallo pakket Hallo pakketinhoud verwerkt en Hallo verwerkt pakket tooan intern systeemprobleem locatie kopieert.  

Hallo [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers Hallo toepassingstype in Hallo-cluster en het beschikbaar voor implementatie.

Hallo [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API bevat informatie over alle toepassingstypen is geregistreerd. U kunt deze API toodetermine gebruiken als het Hallo-registratie is voltooid.

## <a name="create-an-application-instance"></a>Maak een toepassingsinstantie
U kunt een toepassing vanuit elk toepassingstype dat is geregistreerd met behulp van Hallo instantiëren [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. Hallo-naam van elke toepassing moet beginnen met Hallo *"fabric: '* schema en moet uniek zijn voor elk toepassingsexemplaar (binnen een cluster). Alle services die standaard gedefinieerd in het toepassingsmanifest Hallo van type doeltoepassing Hallo worden ook gemaakt.

Meerdere exemplaren van een toepassing kunnen worden gemaakt voor een bepaalde versie van een geregistreerde toepassingstype. Elk toepassingsexemplaar wordt uitgevoerd in een geïsoleerde omgeving met een eigen werkmap en het aantal processen.

toosee die met de naam toepassingen en services worden uitgevoerd in de cluster Hallo Hallo uitvoeren [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) en [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API's.

## <a name="create-a-service-instance"></a>Een service-exemplaar maken
U kunt een service van een service met behulp van Hallo instantiëren [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Als Hallo-service is gedeclareerd als een standaardservice in het toepassingsmanifest hello, wordt Hallo service gemaakt wanneer de toepassing hello wordt geïnstantieerd.  Aanroepen Hallo [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API voor een service die al wordt geïnstantieerd wordt een uitzondering van type met een foutcode met een waarde van FabricErrorCode.ServiceAlreadyExists FabricException geretourneerd.

## <a name="remove-a-service-instance"></a>Verwijderen van een service-exemplaar
Wanneer een service-exemplaar niet langer nodig is, kunt u deze verwijderen uit met een toepassingsexemplaar van de door de aanroepende Hallo Hallo [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Deze bewerking kan niet ongedaan worden gemaakt en de status van service kan niet worden hersteld.

## <a name="remove-an-application-instance"></a>Verwijderen van instantie van een toepassing
Wanneer een toepassingsexemplaar niet meer nodig is, kunt u permanent verwijderen deze op naam Hallo met [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) alle services die deel uitmaken van toohello toepassing ook, permanent verwijderen van de status van alle service wordt automatisch verwijderd.

> [!WARNING]
> Deze bewerking kan niet ongedaan worden gemaakt en de status van toepassing kan niet worden hersteld.

## <a name="unregister-an-application-type"></a>Registratie van een toepassingstype
Wanneer een bepaalde versie van het type van een toepassing niet meer nodig is, moet u die bepaalde versie van het toepassingstype Hallo Hallo met registratie [Unregister ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Registratie ongebruikte versies van de toepassing typen releases opslagruimte die wordt gebruikt door Hallo image store. Een versie van het type van een toepassing kunt ongedaan worden gemaakt als geen toepassingen zijn gemaakt op basis van die versie van het type van de toepassing hello en er geen updates van toepassing op in behandeling die versie van het type van de toepassing hello verwijzen.

## <a name="remove-an-application-package-from-hello-image-store"></a>Een toepassingspakket verwijderen uit de installatiekopieopslag Hallo
Wanneer een toepassingspakket is niet langer nodig is, kunt u deze verwijderen uit Hallo image store toofree system resources met behulp van Hallo [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Kopiëren ServiceFabricApplicationPackage vraagt om een ImageStoreConnectionString
Hallo Service Fabric SDK omgeving moet al Hallo juiste standaardwaarden wordt ingesteld. Maar desgewenst Hallo ImageStoreConnectionString voor alle opdrachten moet overeenkomen met Hallo-waarde die Hallo Service Fabric-cluster wordt gebruikt. Hallo ImageStoreConnectionString vindt u in het clustermanifest Hallo opgehaald met Hallo [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) en Get-ImageStoreConnectionStringFromClusterManifest-opdrachten:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hallo **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet die deel uitmaakt van de Service Fabric SDK PowerShell-module hello, is de gebruikte tooget Hallo afbeelding verbindingsreeks te slaan.  tooimport hello SDK-module, uitvoeren:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


Hallo ImageStoreConnectionString is gevonden in clustermanifest Hallo:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Zie [begrijpen Hallo image store-verbindingsreeks](service-fabric-image-store-connection-string.md) voor aanvullende informatie over Hallo image store en afbeelding verbindingsreeks te slaan.

### <a name="deploy-large-application-package"></a>Grote toepassingspakket implementeren
Probleem: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API een time-out voor een groot pakket (in volgorde van GB).
Probeer een van:
- Geef een hogere time-out voor [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) methode met `timeout` parameter. Hallo-out is standaard 30 minuten.
- Controleer de netwerkverbinding Hallo tussen de bron- en cluster. Als Hallo verbinding langzaam is, kunt u overwegen een machine met een betere netwerkverbinding.
Hallo client-computer in een andere regio dan het Hallo-cluster, dan kunt u met behulp van een client-computer in een dichter of dezelfde regio als Hallo-cluster.
- Controleer als u externe beperking zijn raken. Wanneer de installatiekopieopslag Hallo geconfigureerde toouse azure storage, kunnen uploaden bijvoorbeeld kan worden beperkt.

Probleem: Upload-pakket is voltooid, maar [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API een time-out optreedt. Probeer een van:
- [Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert.
Hallo compressie Hallo verkleint en Hallo aantal bestanden, die op zijn beurt minder Hallo hoeveelheid verkeer en werkt deze Service Fabric moet uitvoeren. Hallo uploadbewerking mogelijk langzamer (met name als u Hallo compressie tijd opnemen), maar registreren en ongedaan maken van de registratie Hallo toepassingstype sneller.
- Geef een hogere time-out voor [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API met `timeout` parameter.

### <a name="deploy-application-package-with-many-files"></a>Toepassingspakket implementeren met veel bestanden
Probleem: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) time-out voor een toepassingspakket met veel bestanden (volgorde van duizendtallen).
Probeer een van:
- [Hallo pakket comprimeren](service-fabric-package-apps.md#compress-a-package) voordat u de installatiekopieopslag toohello kopieert. Hallo compressie vermindert het aantal bestanden Hallo.
- Geef een hogere time-out voor [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) met `timeout` parameter.

## <a name="code-example"></a>Voorbeeld van code
Hallo volgende voorbeeld gekopieerd van een toepassing pakket toohello image store, richt Hallo toepassingstype, instantie van een toepassing maakt, maakt een service-exemplaar, verwijdert Hallo toepassingsexemplaar, ongedaan maken met de bepalingen Hallo toepassingstype, en Hallo-toepassingspakket verwijdert uit de installatiekopieopslag Hallo.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Volgende stappen
[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)

[Service Fabric health Inleiding](service-fabric-health-introduction.md)

[Vaststellen en oplossen van een Service Fabric-service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Model van een toepassing in Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
