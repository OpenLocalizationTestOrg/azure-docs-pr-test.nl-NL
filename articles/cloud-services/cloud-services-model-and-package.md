---
title: aaaWhat is een Service in de Cloud-model en het pakket | Microsoft Docs
description: Beschrijft Hallo cloudservicemodel (csdef, cscfg-bestand) en -pakket (.cspkg) in Azure
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>Wat is Hallo Cloud Service-model en hoe ik dit pakket?
Een cloudservice is gemaakt op basis van drie onderdelen, Hallo servicedefinitie *(.csdef)*, van de serviceconfiguratie Hallo *(.cscfg)*, en een servicepakket *(.cspkg)*. Beide Hallo **ServiceDefinition.csdef** en **ServiceConfig.cscfg** bestanden zijn XML- en beschrijven Hallo-structuur van het Hallo-cloudservice en de manier waarop deze geconfigureerd; gezamenlijk Hallo-model genoemd. Hallo **ServicePackage.cspkg** is een zipbestand dat is gegenereerd op basis van Hallo **ServiceDefinition.csdef** en bevat onder andere alle Hallo vereist op basis van een binair afhankelijkheden. Azure maakt een cloudservice van beide Hallo **ServicePackage.cspkg** en Hallo **ServiceConfig.cscfg**.

Zodra het Hallo-cloudservice wordt uitgevoerd in Azure, kunt u deze configureren via Hallo **ServiceConfig.cscfg** bestand, maar kan Hallo-definitie niet wijzigen.

## <a name="what-would-you-like-tooknow-more-about"></a>Wat wilt u meer informatie over tooknow?
* Ik wil meer informatie over Hallo tooknow [ServiceDefinition.csdef](#csdef) en [ServiceConfig.cscfg](#cscfg) bestanden.
* Ik heb al weet over die, geef me [enkele voorbeelden](#next-steps) op ik kunt configureren.
* Ik wil toocreate hello [ServicePackage.cspkg](#cspkg).
* Ik gebruik Visual Studio en ik wil...
  * [Maak een cloudservice][vs_create]
  * [Configureren van een bestaande cloudservice][vs_reconfigure]
  * [Een Cloud Service-project implementeert][vs_deploy]
  * [Extern bureaublad in een cloud service-exemplaar][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Hallo **ServiceDefinition.csdef** bestand geeft Hallo-instellingen die worden gebruikt door Azure tooconfigure een cloudservice. Hallo [Azure Service definitie Schema (.csdef-bestand)](https://msdn.microsoft.com/library/azure/ee758711.aspx) Hallo toegestane indeling biedt voor een servicedefinitiebestand. Hallo toont volgende voorbeeld Hallo-instellingen die kunnen worden gedefinieerd voor hello Web- en werkrollen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

U kunt verwijzen toohello [Service definitie Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) voor een beter begrip van XML-schema Hallo hier gebruikt, maar hier volgt een korte uitleg van een aantal Hallo elementen:

**Sites**  
Bevat de definities Hallo voor websites of web-toepassingen die worden gehost in IIS7.

**InputEndpoints**  
Bevat definities voor eindpunten die zijn Hallo toocontact hello cloudservice gebruikt.

**InternalEndpoints**  
Bevat de definities Hallo voor eindpunten die worden gebruikt door de functie instanties toocommunicate met elkaar.

**ConfigurationSettings**  
Hallo instellingsdefinities voor de functies van een specifieke functie bevat.

**Certificaten**  
Bevat de definities Hallo voor certificaten die nodig zijn voor een rol. Hallo vorige codevoorbeeld ziet u een certificaat dat wordt gebruikt voor het Hallo-configuratie van de Azure-verbinding.

**LocalResources**  
Bevat de definities Hallo voor resources voor lokale opslag. Een lokale opslagbron is een gereserveerde map op het bestandssysteem Hallo van Hallo virtuele machine waarop een exemplaar van een rol wordt uitgevoerd.

**Invoer**  
Bevat de definities Hallo voor geïmporteerde modules. Hallo vorige codevoorbeeld toont Hallo-modules voor verbinding met extern bureaublad en Azure-verbinding.

**Opstarten**  
Bevat taken die worden uitgevoerd wanneer het Hallo-rol wordt gestart. Hallo-taken zijn gedefinieerd in een .cmd of uitvoerbaar bestand.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
Hallo-configuratie van Hallo-instellingen voor uw cloudservice wordt bepaald door de waarden Hallo in Hallo **ServiceConfiguration.cscfg** bestand. U opgeven Hallo aantal instanties dat u toodeploy voor elke rol in dit bestand wilt. Hallo-waarden voor Hallo configuratie-instellingen die u hebt gedefinieerd in het servicedefinitiebestand hello, toohello serviceconfiguratiebestand worden toegevoegd. Hallo vingerafdrukken instellen voor van beheercertificaten die gekoppeld aan de cloudservice Hallo zijn ook toohello bestand toegevoegd. Hallo [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx) Hallo toegestane indeling voorziet in een configuratiebestand voor de service.

Hallo serviceconfiguratiebestand wordt niet geleverd met de toepassing hello, maar is geüploade tooAzure als een afzonderlijk bestand en wordt gebruikte tooconfigure hello cloudservice. U kunt een nieuwe service-configuratiebestand zonder uw cloudservice opnieuw uploaden. Hallo configuratiewaarden voor Hallo cloudservice kunnen worden gewijzigd terwijl Hallo cloudservice wordt uitgevoerd. Hallo toont volgende voorbeeld Hallo configuratie-instellingen die kunnen worden gedefinieerd voor hello Web- en werkrollen:

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Raadpleegt u toohello [Service configuratieschema](https://msdn.microsoft.com/library/azure/ee758710.aspx) voor een beter begrip Hallo XML-schema hier gebruikt, hier is echter een korte uitleg van Hallo elementen:

**Exemplaren**  
Hiermee configureert u Hallo aantal actieve exemplaren voor Hallo-rol. tooprevent uw cloud-service niet langer mogelijk niet beschikbaar tijdens upgrades, is het aanbevolen dat u meer dan één exemplaar van de functies van uw web gerichte implementeert. Door het implementeren van meer dan één exemplaar u toohello richtlijnen in Hallo voldoet [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), die wordt gegarandeerd dat externe connectiviteit van 99,95% voor internetgerichte rollen wanneer twee of meer rol exemplaren worden geïmplementeerd voor een service.

**ConfigurationSettings**  
Hallo-instellingen voor Hallo actieve exemplaren voor een functie configureert. Hallo-naam van Hallo `<Setting>` elementen moeten overeenkomen met de definities in het servicedefinitiebestand Hallo Hallo.

**Certificaten**  
Hallo-certificaten die worden gebruikt door Hallo service configureert. Hallo vorige codevoorbeeld ziet u hoe toodefine Hallo certificaat voor Hallo RemoteAccess-module. waarde van Hallo Hallo *vingerafdruk* kenmerk toohello vingerafdruk van Hallo certificaat toouse moet worden ingesteld.

<p/>

> [!NOTE]
> Hallo vingerafdruk voor Hallo certificaat kan configuratiebestand toohello worden toegevoegd met een teksteditor. Of het Hallo-waarde kan worden toegevoegd op Hallo **certificaten** tabblad Hallo **eigenschappen** pagina van de rol Hallo in Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Poorten voor rolinstanties definiëren
Azure kan slechts één vermelding punt tooa-Webrol. Dit betekent dat alle verkeer vindt plaats via één IP-adres. U kunt uw websites tooshare een poort configureren door Hallo host-header toodirect Hallo aanvraag toohello juiste locatie te configureren. U kunt ook uw toepassingen toolisten toowell bekende poorten op Hallo IP-adres configureren.

Hallo toont volgende voorbeeld Hallo-configuratie voor een Webrol aan een toepassing website en webtoepassingen. Hallo-website is geconfigureerd als Hallo standaardlocatie vermelding op poort 80 en Hallo webtoepassingen zijn geconfigureerde tooreceive aanvragen van een andere host-header 'mail.mysite.cloudapp.net' wordt genoemd.

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>Hallo-configuratie van een rol wijzigen
U kunt Hallo configuratie van uw cloudservice bijwerken terwijl deze wordt uitgevoerd in Azure, zonder Hallo service offline te halen. toochange configuratiegegevens, kunt u ofwel een nieuw configuratiebestand uploaden of het Hallo-configuratiebestand bewerken in plaatsen en dit toepassen tooyour waarop service wordt uitgevoerd. wijzigingen Hallo volgende kunnen worden aangebracht toohello configuratie van een service:

* **Hallo-waarden van configuratie-instellingen wijzigen**  
  Als er een configuratie kunt Instellingswijzigingen, een rolinstantie kiezen tooapply Hallo wijzigen tijdens het Hallo-exemplaar is online of toorecycle Hallo exemplaar probleemloos en Hallo wijziging toepassen tijdens het Hallo-exemplaar is offline.
* **Hallo service topologie rolinstanties wijzigen**  
  Wijzigingen in de netwerktopologie hebben geen invloed op de exemplaren die worden uitgevoerd, behalve wanneer een exemplaar wordt verwijderd. Alle overige exemplaren moeten in het algemeen niet toobe gerecycled; u kunt echter toorecycle rolinstanties antwoord tooa topologiewijziging in.
* **Hallo certificaatvingerafdruk wijzigen**  
  U kunt een certificaat alleen bijwerken wanneer een rolinstantie offline is. Als een certificaat is toegevoegd, verwijderd of gewijzigd terwijl een rolinstantie online is, wordt Azure probleemloos Hallo exemplaar offline tooupdate Hallo certificaat nodig en deze weer online brengen nadat Hallo wijziging is aangebracht.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Wijzigingen in de configuratie met gebeurtenissen van de Runtime-Service verwerken
Hallo [Azure-Runtime-bibliotheek](https://msdn.microsoft.com/library/azure/mt419365.aspx) Hallo omvat [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) naamruimte, waardoor de klassen voor interactie met hello Azure-omgeving van een rol. Hallo [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) klasse definieert Hallo gebeurtenissen die worden gegenereerd voor en na een wijziging in de configuratie te volgen:

* **[Het wijzigen van](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) gebeurtenis**  
  Dit vindt plaats voordat de configuratiewijziging Hallo toegepaste tooa opgegeven exemplaar van een rol zodat u een kans tootake omlaag Hallo rolinstanties indien nodig.
* **[Gewijzigd](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) gebeurtenis**  
  Deze gebeurtenis treedt op nadat Hallo configuratiewijziging toegepaste tooa opgegeven exemplaar van een rol is.

> [!NOTE]
> Omdat wijzigingen certificaat altijd Hallo exemplaren van een rol offline halen, beter ze Hallo RoleEnvironment.Changing of RoleEnvironment.Changed gebeurtenissen niet verhogen.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy een toepassing als een cloudservice in Azure, moet u de eerste pakket Hallo-toepassing in de juiste notatie Hallo. Kunt u Hallo **CSPack** opdrachtregelprogramma (geïnstalleerd met Hallo [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate Hallo pakketbestand als een alternatieve tooVisual Studio.

**CSPack** gebruikt Hallo inhoud Hallo service definitie bestands- en configuratie toodefine Hallo bestandsinhoud van Hallo-pakket. **CSPack** genereert een toepassingspakketbestand (.cspkg) dat u tooAzure kunt uploaden via Hallo [Azure-portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). Standaard Hallo pakket heet `[ServiceDefinitionFileName].cspkg`, maar u kunt een andere naam opgeven met behulp van Hallo `/out` optie **CSPack**.

**CSPack** bevindt zich op  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (op windows) is beschikbaar door het uitvoeren van Hallo **Microsoft Azure-opdrachtprompt** snelkoppeling die is geïnstalleerd met Hallo SDK.  
> 
> Hallo CSPack.exe programma zelfstandig toosee documentatie over alle mogelijke Hallo-switches en opdrachten uitvoeren.
> 
> 

<p />

> [!TIP]
> Lokaal uitvoeren van de cloudservice in Hallo **Microsoft Azure Compute-Emulator**, gebruik Hallo **/copyonly** optie. Deze optie kopieert Hallo binaire bestanden voor Hallo tooa directory indeling van de toepassing waaruit ze kunnen worden uitgevoerd in Hallo rekenemulator.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Voorbeeld van de opdracht toopackage een cloudservice
Hallo wordt volgende voorbeeld een toepassingspakket met daarin Hallo-informatie voor een Webrol. Hallo-opdracht geeft Hallo service definitie bestand toouse, Hallo directory waar de binaire bestanden kunnen worden gevonden en de naam van het pakketbestand Hallo Hallo.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Als de toepassing hello zowel een Webrol en een werkrol bevat, wordt hello volgende opdracht gebruikt:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Waar Hallo variabelen worden als volgt gedefinieerd:

| Variabele | Waarde |
| --- | --- |
| \[DirectoryName\] |Hallo submap onder Hallo project hoofdmap die Hallo csdef-bestand van hello Azure-project bevat. |
| \[ServiceDefinition\] |Hallo-naam van het servicedefinitiebestand Hallo. Standaard is dit bestand ServiceDefinition.csdef naam. |
| \[OutputFileName\] |Hallo-naam voor Hallo gegenereerd pakketbestand. Dit is normaal gesproken toohello naam van de toepassing hello ingesteld. Als geen bestandsnaam is opgegeven, Hallo toepassingspakket is gemaakt als \[ApplicationName\].cspkg. |
| \[Rolnaam\] |Hallo-naam van Hallo rol zoals gedefinieerd in het servicedefinitiebestand Hallo. |
| \[RoleBinariesDirectory] |Hallo-locatie van de binaire bestanden voor de rol Hallo Hallo. |
| \[VirtualPath\] |Hallo fysieke mappen voor elke virtuele pad gedefinieerd in Hallo sectie Sites van Hallo servicedefinitie. |
| \[PhysicalPath\] |Hallo fysieke mappen van inhoud voor elke virtuele pad dat is gedefinieerd in Hallo siteknooppunt van de servicedefinitie Hallo Hallo. |
| \[RoleAssemblyName\] |Hallo-naam van binair bestand voor de rol Hallo Hallo. |

## <a name="next-steps"></a>Volgende stappen
Ik ben een cloud service-pakket maken en ik wil...

* [Extern bureaublad instellen voor een cloud service-exemplaar][remotedesktop]
* [Een Cloud Service-project implementeert][deploy]

Ik gebruik Visual Studio en ik wil...

* [Maak een nieuwe cloudservice][vs_create]
* [Configureren van een bestaande cloudservice][vs_reconfigure]
* [Een Cloud Service-project implementeert][vs_deploy]
* [Extern bureaublad instellen voor een cloud service-exemplaar][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
