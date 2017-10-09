---
title: aaaManaging geheimen in Service Fabric-toepassingen | Microsoft Docs
description: Dit artikel wordt beschreven hoe toosecure geheim waarden in een Service Fabric-toepassing.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>Het beheren van geheimen in Service Fabric-toepassingen
Deze handleiding leert u Hallo van het beheer van geheimen in een Service Fabric-toepassing. Geheimen mag gevoelige informatie, zoals de storage-verbindingsreeksen, wachtwoorden of andere waarden die niet moeten worden behandeld als tekst zonder opmaak.

Deze handleiding maakt gebruik van Azure Sleutelkluis toomanage sleutels en geheimen. Echter, *met* geheimen in een toepassing is cloud platform networkdirect tooallow toepassingen toobe geïmplementeerde tooa cluster gehost elke locatie. 

## <a name="overview"></a>Overzicht
Hallo configuratie-instellingen voor de service aanbevolen manier toomanage is via [service configuratiepakketten][config-package]. Configuratiepakketten zijn samengestelde en bij te werken via beheerde rollende upgrades met health-validatie en voor automatisch terugdraaien. Dit is voorkeur tooglobal configuratie vermindert Hallo kans op een globale Services uitvallen. Versleutelde geheimen zijn geen uitzondering. Service Fabric bevat ingebouwde functies voor het versleutelen en ontsleutelen van waarden in een pakket Settings.xml configuratiebestand met behulp van certificaatversleuteling.

Hallo illustreert volgende diagram Hallo-basisprincipes voor het beheer van de geheime in een Service Fabric-toepassing:

![overzicht van geheime management][overview]

Er zijn vier hoofdstappen in deze overdracht:

1. Verkrijgen van een certificaat voor het uitwisselen van gegevens.
2. Hallo-certificaat installeren in uw cluster.
3. Versleutelen geheime waarden bij het implementeren van een toepassing met Hallo-certificaat en injecteren van een service Settings.xml-configuratiebestand.
4. Alleen versleutelde waarden buiten Settings.xml door te ontsleutelen met Hallo hetzelfde uitwisselen certificaat. 

[Azure Sleutelkluis] [ key-vault-get-started] wordt hier gebruikt als een locatie voor de veilige opslag voor certificaten en als een manier tooget certificaten zijn geïnstalleerd op de Service Fabric-clusters in Azure. Als u geen tooAzure implementeert, hoeft u geen toouse Sleutelkluis toomanage geheimen in Service Fabric-toepassingen.

## <a name="data-encipherment-certificate"></a>Gegevens uitwisselen certificaat
Een certificaat voor het uitwisselen van gegevens wordt uitsluitend gebruikt voor versleuteling en ontsleuteling van de configuratie van de waarden in een service Settings.xml en wordt niet gebruikt voor de verificatie of het ondertekenen van de gecodeerde tekst. Hallo-certificaat moet voldoen aan Hallo volgens de vereisten:

* Hallo-certificaat moet een persoonlijke sleutel bevatten.
* Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.
* Hallo certificaat sleutelgebruik gegevenscodering (10) moet bevatten en mag geen serververificatie of clientverificatie bevatten. 
  
  Bijvoorbeeld bij het maken van een zelfondertekend certificaat met behulp van PowerShell Hallo `KeyUsage` moet de vlag te instellen`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Hallo-certificaat installeren in het cluster
Dit certificaat moet worden geïnstalleerd op elk knooppunt in het Hallo-cluster. Deze wordt gebruikt tijdens runtime toodecrypt waarden in een service Settings.xml zijn opgeslagen. Zie [hoe toocreate een cluster met Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] voor installatie-instructies. 

## <a name="encrypt-application-secrets"></a>Toepassing geheimen versleutelen
Hallo Service Fabric SDK bevat ingebouwde geheime versleuteling en ontsleuteling functies. Geheime waarden kunnen worden versleuteld op het moment van gebouwd ontsleuteld en gelezen via een programma in de servicecode. 

Hallo volgende PowerShell-opdracht is gebruikte tooencrypt een geheim. Met deze opdracht versleutelt alleen Hallo value; Dit gebeurt **niet** ondertekenen Hallo gecodeerde tekst. Hallo moet u hetzelfde certificaat voor uitwisselen die is geïnstalleerd in uw cluster tooproduce gecodeerde tekst voor geheime waarden:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Hallo resulterende base 64-tekenreeks bevat zowel geheime gecodeerde tekst hello, evenals informatie over het Hallo-certificaat dat gebruikt tooencrypt is deze.  Hallo Base64-gecodeerde tekenreeks kan worden ingevoegd in een parameter in het configuratiebestand van uw service Settings.xml Hello `IsEncrypted` kenmerkset te`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Toepassing geheimen invoeren in toepassingsexemplaren
Implementatie toodifferent omgevingen moeten in het ideale geval als geautomatiseerde mogelijk. Dit kan worden bereikt door geheime versleuteling uitvoeren in een build-omgeving en het leveren van geheimen Hallo versleuteld als parameters bij het maken van exemplaren van een toepassing.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Onderdrukbare parameters in Settings.xml gebruiken
Hallo Settings.xml configuratiebestand kunt overschrijfbare parameters die tijdens de aanmaak van de toepassing kunnen worden opgegeven. Gebruik Hallo `MustOverride` kenmerk in plaats van een waarde voor een parameter op te geven:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

toooverride waarden in Settings.xml, declareren een overrideparameter voor Hallo-service in ApplicationManifest.xml:

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

Nu het Hallo-waarde kan worden opgegeven als een *toepassing parameter* bij het maken van een exemplaar van de toepassing hello. Maken van een toepassingsexemplaar kan scripts worden gebruikt met behulp van PowerShell, of geschreven in C#, voor eenvoudige integratie in een buildproces.

Met behulp van PowerShell, Hallo parameter wordt opgegeven toohello `New-ServiceFabricApplication` opdracht als een [hash-tabel](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Met C#, parameters voor de toepassing zijn opgegeven in een `ApplicationDescription` als een `NameValueCollection`:

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>Ontsleutelen van geheimen van servicecode
Services in Service Fabric onder netwerkservice standaard uitgevoerd in Windows en geen toegang toocertificates op hebt geïnstalleerd Hallo-knooppunt zonder extra instellingen opgeven.

Wanneer u een certificaat voor het uitwisselen van gegevens, moet u ervoor dat netwerkservice of de gebruiker account Hallo-service wordt uitgevoerd onder de persoonlijke sleutel toegang toohello certificaat toomake. Service Fabric, het verlenen van toegang voor uw service automatisch als u deze toodo dus configureren verwerkt. Deze configuratie kan worden gedaan in ApplicationManifest.xml door gebruikers- en beveiligingsbeleid voor certificaten te definiëren. Hallo Netwerkservice-account in Hallo voorbeeld te volgen, krijgt leestoegang tooa certificaat gedefinieerd door de vingerafdruk:

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> Bij het kopiëren van een certificaatvingerafdruk opslaan van Hallo-certificaat-module voor Windows, een onzichtbare teken aan begin Hallo van Hallo vingerafdruk tekenreeks geplaatst. Dit onzichtbaar teken kan leiden tot een fout opgetreden bij het toolocate een certificaat met vingerafdruk, dus worden toodelete ervoor dat deze extra tekens.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Gebruik application geheimen in servicecode
Hallo API voor het openen van configuratiewaarden uit Settings.xml in een configuratiepakket kunt u eenvoudig ontsleutelen van waarden die Hallo hebben `IsEncrypted` kenmerkset te`true`. Omdat Hallo versleuteld tekst informatie over Hallo certificaat gebruikt voor versleuteling bevat, hoeft u geen toomanually zoeken Hallo certificaat. Hallo-certificaat moet net toobe op Hallo-knooppunt dat Hallo-service wordt uitgevoerd op is geïnstalleerd. Hallo te roepen `DecryptValue()` methode tooretrieve Hallo oorspronkelijke geheime waarde:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [met toepassingen met andere machtigingen](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
