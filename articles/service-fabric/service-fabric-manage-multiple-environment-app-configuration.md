---
title: aaaManage omgevingen met meerdere in Service Fabric | Microsoft Docs
description: "Service Fabric-toepassingen kunnen worden uitgevoerd op clusters die in grootte van één machine toothousands machines variëren. In sommige gevallen zult u tooconfigure uw toepassing anders voor deze uiteenlopende omgevingen. In dit artikel bevat informatie over hoe de andere toepassingsparameters toodefine per omgeving."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Parameters voor de toepassing voor omgevingen met meerdere beheren
U kunt Azure Service Fabric-clusters maken met behulp van een willekeurige plaats uit één toomany duizenden computers. Hoewel binaire bestanden van toepassingen zonder dat aanpassingen nodig over deze breed scala aan omgevingen uitvoeren kunnen, wilt u meestal tooconfigure Hallo toepassing anders, afhankelijk van het aantal machines die u implementeert op Hallo.

Een eenvoudig voorbeeld kunt u beter `InstanceCount` voor een stateless service. Wanneer u toepassingen in Azure uitvoert, doorgaans wilt u tooset deze speciale parameter toohello-waarde '1'. Deze configuratie zorgt ervoor dat uw service wordt uitgevoerd op elk knooppunt in het Hallo-cluster (of elk knooppunt in knooppunttype Hallo als u een beperking voor de plaatsing hebt ingesteld). Deze configuratie is echter niet geschikt voor een cluster met één computer omdat er meerdere processen luistert op Hallo dezelfde geen eindpunt op een enkele computer. In plaats daarvan doorgaans ingesteld `InstanceCount` te '1'.

## <a name="specifying-environment-specific-parameters"></a>Omgeving-specifieke parameters opgeven
Hallo oplossing toothis configuratieprobleem is een set met geparameteriseerde standaardservices en toepassingsbestanden parameter die de parameterwaarden van deze voor een bepaalde omgeving invullen. Standaardservices en de parameters voor de toepassing en worden geconfigureerd in de toepassing hello service manifesten. Hallo schemadefinitie voor Hallo ServiceManifest.xml en ApplicationManifest.xml bestanden is geïnstalleerd met Hallo Service Fabric SDK en hulpprogramma's te*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Standaard-services
Service Fabric-toepassingen bestaan uit een verzameling van service-exemplaren. Terwijl het is mogelijk dat u een lege toepassing toocreate en maak vervolgens alle service-exemplaren dynamisch, hebben de meeste toepassingen een set van core services die altijd moet worden gemaakt wanneer de toepassing hello wordt geïnstantieerd. Dit zijn waarnaar wordt verwezen tooas 'standaardservices'. Ze worden opgegeven in de toepassingsmanifest Hallo met tijdelijke aanduidingen voor de per-omgeving configuratie opgenomen tussen vierkante haken:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Elk van de benoemde parameters Hallo moet zijn gedefinieerd binnen Hallo Parameters element van het manifest van de toepassing hello:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

Hallo DefaultValue kenmerk geeft Hallo waarde toobe in Hallo afwezigheid van een meer specifieke parameter gebruikt voor een bepaalde omgeving.

> [!NOTE]
> Niet alle parameters van de service-exemplaar zijn geschikt voor configuratie van per-omgeving. Hallo bovenstaande voorbeeld Hallo LowKey en HighKey waarden voor het partitieschema Hallo-service zijn expliciet is gedefinieerd voor alle exemplaren van Hallo-service sinds Hallo partitiebereik een functie van Hallo gegevens domein, niet Hallo-omgeving is.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Configuratie-instellingen voor de per-omgeving
Hallo [Service Fabric-toepassingsmodel](service-fabric-application-model.md) schakelt services tooinclude configuratiepakketten met aangepaste sleutel-waardeparen die kunnen gelezen tijdens runtime worden. Hallo-waarden van deze instellingen kunnen ook worden onderscheiden door omgeving door te geven een `ConfigOverride` Hallo-toepassingsmanifest.

Stel dat u de volgende instelling in Hallo Config\Settings.xml bestand voor Hallo Hallo hebt `Stateful1` service:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
toooverride deze waarde voor de combinatie van een specifieke toepassingsomgeving, maak een `ConfigOverride` wanneer u Hallo servicemanifest in het toepassingsmanifest Hallo importeert.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Deze parameter kan vervolgens worden geconfigureerd door omgeving zoals hierboven. U kunt dit doen door het declareren in Hallo parameters gedeelte van het toepassingsmanifest Hallo en omgeving-specifieke waarden opgeven in de parameter toepassingsbestanden Hallo.

> [!NOTE]
> In geval van configuratie-instellingen service Hallo er zijn drie locaties waar Hallo-waarde van een sleutel kan worden ingesteld: Hallo service configuratiepakket Hallo toepassingsmanifest en parameterbestand Hallo-toepassing. Service Fabric wordt altijd kiezen uit parameterbestand Hallo-toepassing eerst (indien opgegeven), vervolgens Hallo manifest van de toepassing en ten slotte Hallo configuratiepakket.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Instellen en het gebruik van omgevingsvariabelen 
U kunt opgeven en deze omgevingsvariabelen worden ingesteld in Hallo ServiceManifest.xml bestand en vervolgens uitschakelen in Hallo ApplicationManifest.xml bestand per exemplaar op basis van een.
Hallo voorbeeld hieronder ziet u twee omgevingsvariabelen, één met een waarde ingesteld en Hallo andere wordt overschreven. U kunt de parameters voor de toepassing tooset omgevingsvariabelen worden de waarden in Hallo dezelfde manier dat deze zijn gebruikt voor onderdrukkingen in configuratie gebruiken.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
toooverride hello environment variables in de Hallo ApplicationManifest.xml, verwijzing Hallo codepakket in Hallo ServiceManifest Hello `EnvironmentOverrides` element.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Zodra Hallo service-exemplaar met de naam is gemaakt, kunt u omgevingsvariabelen Hallo kunt openen vanaf code. bijvoorbeeld In C# kunt u doen Hallo volgende

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Service Fabric-omgevingsvariabelen
Service Fabric is ingebouwd in de omgevingsvariabelen instellen voor elke service-exemplaar. Hallo volledige lijst met omgevingsvariabelen is hieronder, waar hello toepassingsgroepen in vet weet Hallo toepassingsgroepen die u in uw service gebruiken wilt Hallo andere wordt gebruikt door de Service Fabric-runtime. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **TypeEndpoint Fabric_Endpoint_ [YourServiceName]**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Hallo code belows ziet u hoe toolist Service Fabric-omgevingsvariabelen Hallo
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Hallo hieronder vindt u voorbeelden van omgevingsvariabelen voor een toepassingstype aangeroepen `GuestExe.Application` aangeroepen met een servicetype `FrontEndService` wanneer uitvoeren op uw lokale dev-computer.

* **Fabric_ApplicationName fabric:/GuestExe.Application =**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName _Node_2 =**

### <a name="application-parameter-files"></a>Parameter voor toepassingsbestanden
Hallo Service Fabric-toepassingsproject kan een of meer parameter voor toepassingsbestanden bevatten. Elk van deze definieert specifieke waarden voor Hallo-parameters die zijn gedefinieerd in het toepassingsmanifest Hallo Hallo:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
Een nieuwe toepassing bevat drie parameter voor toepassingsbestanden, met de naam Local.1Node.xml Local.5Node.xml en Cloud.xml:

![Parameter voor toepassingsbestanden in Solution Explorer][app-parameters-solution-explorer]

een parameterbestand toocreate gewoon kopiëren en plakken van een bestaande en een nieuwe naam geven.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Omgeving-specifieke parameters identificeren tijdens de implementatie
Tijdens de implementatie moet u toochoose Hallo juiste parameter bestand tooapply met uw toepassing. U kunt dit doen via het dialoogvenster voor het publiceren van Hallo in Visual Studio of PowerShell.

### <a name="deploy-from-visual-studio"></a>Implementeren vanuit Visual Studio
U kunt kiezen uit Hallo lijst met beschikbare parameterbestanden wanneer u uw toepassing in Visual Studio publiceert.

![Kies een parameterbestand in Hallo publiceren dialoogvenster][publishdialog]

### <a name="deploy-from-powershell"></a>Implementeren vanaf PowerShell
Hallo `Deploy-FabricApplication.ps1` PowerShell-script is opgenomen in de projectsjabloon Hallo-toepassing een publicatieprofiel als een parameter accepteert en Hallo PublishProfile bevat een verwijzing toohello toepassingsbestand parameters.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over een aantal Hallo belangrijkste concepten die worden beschreven in dit onderwerp, Zie Hallo [technisch overzicht van Service Fabric](service-fabric-technical-overview.md). Zie voor meer informatie over de mogelijkheden van andere app-beheer die beschikbaar in Visual Studio zijn [beheren van uw Service Fabric-toepassingen in Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
