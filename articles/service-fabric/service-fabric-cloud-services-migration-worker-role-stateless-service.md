---
title: aaaConvert toomicroservices voor Azure Cloud Services-apps | Microsoft Docs
description: Deze handleiding vergelijkt Cloud Services-webserver en werkrollen en Service Fabric stateless services toohelp migreren van Cloudservices tooService Fabric.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Handleiding voor tooconverting Web- en werkrollen tooService Fabric stateless services
Dit artikel wordt beschreven hoe toomigrate uw Cloud Services-Web- en werkrollen tooService Fabric stateless services. Dit is de eenvoudigste migratiepad Hallo van Cloudservices tooService Fabric voor toepassingen waarvan de algehele architectuur toostay ongeveer gaat Hallo dezelfde.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Service-project tooService Fabric-toepassingsproject cloud
 Een Cloud Service-project en een Service Fabric-toepassing-project hebt een vergelijkbare structuur en beide vertegenwoordigen Hallo implementatie-eenheid voor uw toepassing - dat wil zeggen, ze elk voltooid Hallo-pakket dat geïmplementeerde toorun uw toepassing definiëren. Een Cloud Service-project bevat een of meer Web- of werkrollen. Een Service Fabric-toepassing-project bevat ook een of meer services. 

Hallo-verschil is dat Hallo Cloudservice project paren Hallo toepassingsimplementatie met een VM-implementatie en dus bevat VM-configuratie-instellingen in dit terwijl Hallo Service Fabric-toepassing project alleen definieert een toepassing die wordt geïmplementeerd tooa set bestaande virtuele machines in een Service Fabric-cluster. Hallo Service Fabric-cluster zelf wordt alleen geïmplementeerd als via een Resource Manager-sjabloon of via hello Azure-portal en meerdere Service Fabric-toepassingen zijn tooit geïmplementeerd.

![Vergelijking van service Fabric en Cloud Services-project][3]

## <a name="worker-role-toostateless-service"></a>De functieservice toostateless worker
Conceptueel gezien vertegenwoordigt een Werkrol een staatloze werkbelasting, wat betekent dat elke instantie van Hallo werkbelasting is identiek zijn en kunnen aanvragen gerouteerde tooany exemplaar op elk gewenst moment worden. Elk exemplaar is niet verwachte tooremember Hallo vorige aanvraag. Status van de werkbelasting Hallo werkt op wordt beheerd door een externe Statusopslag, zoals Azure Table Storage of Azure Documentdb. Dit soort werkbelasting is in Service Fabric vertegenwoordigd door een Stateless Service. Hallo eenvoudigste methode toomigrating een Werkrol tooService Fabric kan worden gedaan door de Werkrol code tooa staatloze Service converteren.

![Worker-rol tooStateless Service][4]

## <a name="web-role-toostateless-service"></a>De functieservice toostateless Web
Vergelijkbare tooWorker rol een Webrol ook vertegenwoordigt een staatloze werkbelasting, en zo in dat geval het te kan worden toegewezen tooa staatloze Service Fabric-service. Echter, in tegenstelling tot webrollen, Service Fabric ondersteunt geen IIS. toomigrate een webtoepassing van een Webrol tooa staatloze service vereist eerste verplaatsen tooa webframework die automatisch kan worden gehost en is niet afhankelijk van IIS of System.Web, zoals ASP.NET Core 1.

| **Toepassing** | **Ondersteund** | **Migratiepad** |
| --- | --- | --- |
| ASP.NET-webformulieren |Nee |Converteren tooASP.NET Core 1 MVC |
| ASP.NET MVC |Met migratie |Upgrade tooASP.NET Core 1 MVC |
| ASP.NET Web API |Met migratie |Automatische gehoste-server of ASP.NET Core 1 gebruiken |
| ASP.NET Core 1 |Ja |N.v.t. |

## <a name="entry-point-api-and-lifecycle"></a>Vermelding punt API en de levenscyclus
Werkrol en Service Fabric-service-API's bieden vergelijkbare toegangspunten: 

| **Toegangspunt** | **Werkrol** | **Service Fabric-service** |
| --- | --- | --- |
| Verwerking |`Run()` |`RunAsync()` |
| VM starten |`OnStart()` |N.v.t. |
| VM stoppen |`OnStop()` |N.v.t. |
| Open listener voor aanvragen van clients |N.v.t. |<ul><li> `CreateServiceInstanceListener()`voor stateless</li><li>`CreateServiceReplicaListener()`voor stateful</li></ul> |

### <a name="worker-role"></a>Werkrol
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Staatloze service Fabric-Service
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

Een onderdrukking primaire 'uitvoeren' hebben beide in welke toobegin-verwerking. Service Fabric-services combineren `Run`, `Start`, en `Stop` in een enkel toegangspunt `RunAsync`. De service moet beginnen met werken wanneer `RunAsync` wordt gestart en mag niet meer werken wanneer hello `RunAsync` van de methode CancellationToken ontvangt een signaal. 

Er zijn enkele belangrijke verschillen tussen Hallo lifecycle en levensduur van Service Fabric- en werkrollen services:

* **Levenscyclus:** Hallo grootste verschil is dat een Werkrol een virtuele machine is en dus de levenscyclus gebonden toohello VM, waaronder gebeurtenissen voor wanneer Hallo VM wordt gestart en gestopt. Een Service Fabric-service heeft een levenscyclus dat is gescheiden van Hallo VM levensduur, zodat deze bevat geen gebeurtenissen voor als Hallo host, VM of machine wordt gestart en gestopt, omdat ze niet zijn gerelateerd.
* **Levensduur:** een Werkrol-exemplaar wordt gerecycled als hello `Run` methode afgesloten. Hallo `RunAsync` methode in een Service Fabric-service evenwel toocompletion kunt uitvoeren en service-exemplaar Hallo blijven. 

Service Fabric bevat een toegangspunt optionele communicatie-instellingen voor services die naar aanvragen van clients luisteren. Zowel Hallo RunAsync en communicatie toegangspunt zijn optionele onderdrukkingen in Service Fabric-services - uw service kan kiezen tooonly listen tooclient aanvragen of een lus verwerking of beide alleen worden uitgevoerd - dat is waarom Hallo RunAsync-methode tooexit zonder is toegestaan opnieuw starten van Hallo service-exemplaar, omdat deze toolisten voor clientaanvragen blijven mogelijk.

## <a name="application-api-and-environment"></a>Application-API en de omgeving
Hallo Cloud Services-omgeving API biedt informatie en -functionaliteit voor de huidige VM-instantie hello, evenals informatie over andere VM-rolexemplaren. Service Fabric bevat informatie over de runtime tooits en enige informatie over het Hallo-knooppunt een service die momenteel wordt uitgevoerd op. 

| **Taak omgeving** | **Cloud Services** | **Service Fabric** |
| --- | --- | --- |
| Configuratie-instellingen en Wijzigingsmelding |`RoleEnvironment` |`CodePackageActivationContext` |
| Lokale opslag |`RoleEnvironment` |`CodePackageActivationContext` |
| Informatie over endpoint |`RoleInstance` <ul><li>Huidige instantie:`RoleEnvironment.CurrentRoleInstance`</li><li>Andere functies en -exemplaar:`RoleEnvironment.Roles`</li> |<ul><li>`NodeContext`voor het huidige knooppuntadres</li><li>`FabricClient`en `ServicePartitionResolver` voor detectie van de service-eindpunt</li> |
| Omgeving emulatie |`RoleEnvironment.IsEmulated` |N.v.t. |
| Gelijktijdige wijzigingsgebeurtenis |`RoleEnvironment` |N.v.t. |

## <a name="configuration-settings"></a>Configuratie-instellingen
Configuratie-instellingen in de Cloud-Services worden ingesteld voor een VM-rol en tooall exemplaren van die VM-rol van toepassing. Deze instellingen zijn ingesteld in ServiceConfiguration.*.cscfg bestanden sleutel-waardeparen en toegankelijk zijn via RoleEnvironment. In Service Fabric toepassen instellingen afzonderlijk tooeach service en tooeach toepassing, in plaats van tooa VM, omdat een virtuele machine kan meerdere services en toepassingen hosten. Een service bestaat uit drie pakketten:

* **Code:** Hallo service uitvoerbare bestanden, binaire bestanden, dll's en andere bestanden bevat een service nodig heeft toorun.
* **Config:** alle configuratiebestanden en instellingen voor een service.
* **Gegevens:** statische gegevensbestanden die zijn gekoppeld aan het Hallo-service.

Elk van deze pakketten zijn onafhankelijk samengestelde en bijgewerkte. Soortgelijke tooCloud diensten, een configuratiepakket programmatisch kunnen worden geopend via een API en gebeurtenissen zijn beschikbaar toonotify Hallo-service van een pakket configuratiewijziging. Een bestand Settings.xml kan worden gebruikt voor de sleutel / waarde-configuratie en toegang op programmeerniveau vergelijkbare toohello app sectie instellingen van een App.config-bestand. In tegenstelling tot Cloud-Services, kan een Service Fabric-configuratiepakket echter bevatten alle configuratiebestanden in een willekeurige indeling, of het XML, JSON, YAML of een aangepaste binaire indeling. 

### <a name="accessing-configuration"></a>Toegang tot configuratie
#### <a name="cloud-services"></a>Cloudservices
Configuratie-instellingen van ServiceConfiguration.*.cscfg toegankelijk zijn via `RoleEnvironment`. Deze instellingen zijn algemeen beschikbaar tooall rolinstanties in Hallo dezelfde Cloud Service-implementatie.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Elke service heeft een eigen afzonderlijke configuratie-pakket. Er is geen ingebouwde methode voor globale configuratie-instellingen toegankelijk door alle toepassingen in een cluster. Wanneer u Service-Fabric speciale Settings.xml configuratiebestand binnen een configuratiepakket gebruikt, kunnen waarden in Settings.xml worden overschreven op toepassingsniveau hello, die op toepassingsniveau configuratie-instellingen mogelijk te maken.

Configuratie-instellingen zijn toegangspogingen binnen elk service-exemplaar via Hallo-service `CodePackageActivationContext`.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>Update-Configuratiegebeurtenissen
#### <a name="cloud-services"></a>Cloudservices
Hallo `RoleEnvironment.Changed` gebeurtenis gebruikte toonotify alle rolinstanties wanneer een wijziging optreedt in Hallo-omgeving, zoals een wijziging in de configuratie is. Dit is de gebruikte tooconsume configuratie-updates zonder rolinstanties recycling of opnieuw starten van een werkproces.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Elk van de drie pakkettypen Hallo in een service - Code, configuratie en gegevens - gebeurtenissen die een service-exemplaar wordt gewaarschuwd wanneer er een pakket wordt bijgewerkt, toegevoegd of verwijderd hebben. Een service, kan meerdere pakketten van elk type bevatten. Een service kan bijvoorbeeld meerdere config pakketten elk afzonderlijk samengestelde en kan worden uitgebreid. 

Deze gebeurtenissen zijn beschikbaar tooconsume wijzigingen in servicepakketten zonder Hallo service-exemplaar opnieuw te starten.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Starten van de taken
Starten van de taken zijn acties die worden uitgevoerd voordat een toepassing wordt gestart. Een taak starten is gewoonlijk gebruikte toorun setup scripts met verhoogde bevoegdheden. Ondersteuning voor opstarten taken zowel Cloudservices als Service Fabric. Hallo belangrijkste verschil is dat in Cloud-Services, een starten van de taak is gebonden tooa VM omdat deze deel uitmaakt van een rolinstantie terwijl een taak starten in Service Fabric gebonden tooa-service niet gebonden tooany is bepaalde VM.

| Cloudservices | Service Fabric |
| --- | --- | --- |
| Locatie van de configuratie |ServiceDefinition.csdef |
| Bevoegdheden |'beperkt' of 'verhoogde' |
| Sequentiëren |'eenvoudige', 'achtergrond', 'voorgrond' |

### <a name="cloud-services"></a>Cloudservices
In de Cloud Services een toegangspunt opstarten geconfigureerd per rol in ServiceDefinition.csdef. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
In Service Fabric is een toegangspunt starten van de per-service in ServiceManifest.xml geconfigureerd:

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>Een opmerking over ontwikkelomgeving
Zowel Cloudservices als Service Fabric zijn geïntegreerd met Visual Studio met projectsjablonen en ondersteuning voor foutopsporing, configureren en implementeren van zowel lokaal en tooAzure. Zowel Cloudservices als Service Fabric bieden ook een runtime-omgeving voor lokale ontwikkeling. Hallo is verschil dat terwijl hello Service in de Cloud emuleert ontwikkeling runtime hello Azure-omgeving waarop deze wordt uitgevoerd, een emulator maakt geen gebruik van Service Fabric - Hallo volledige Service Fabric-runtime wordt gebruikt. Hallo Hallo Service Fabric-omgeving u op uw lokale ontwikkelcomputer uitvoeren dezelfde omgeving die wordt uitgevoerd in de productieomgeving.

## <a name="next-steps"></a>Volgende stappen
Lees meer over Service Fabric Reliable Services en Hallo fundamentele verschillen tussen Cloud Services en de Service Fabric-toepassing architectuur toounderstand hoe tootake profiteren van Hallo volledige van Service Fabric-onderdelen set.

* [Aan de slag met Service Fabric Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Conceptuele handleiding toohello verschillen tussen Cloudservices en Service Fabric](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
