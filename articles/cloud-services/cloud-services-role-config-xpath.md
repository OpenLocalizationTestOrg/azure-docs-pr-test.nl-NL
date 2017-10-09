---
title: aaaCloud Services-rol config XPath-referentieoverzicht | Microsoft Docs
description: Hallo diverse XPath-instellingen die u in de tooexpose instellingen voor de configuratie van Hallo cloud service-functie als een omgevingsvariabele gebruiken kunt.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Configuratie-rolinstellingen weergeven als een omgevingsvariabele met XPath
In Hallo cloud service worker of web rol servicedefinitiebestand kan configuratiewaarden runtime worden blootgesteld als omgevingsvariabelen. Hallo volgende XPath waarden worden ondersteund (die overeenkomt met tooAPI waarden).

Deze XPath-waarden zijn ook beschikbaar via Hallo [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) bibliotheek. 

## <a name="app-running-in-emulator"></a>App uitgevoerd in de emulator
Hiermee wordt aangegeven dat die Hallo-app wordt uitgevoerd in Hallo-emulator.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/Deployment/@emulated" |
| Code |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>Implementatie-ID
Hallo implementatie-ID voor Hallo-exemplaar wordt opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/Deployment/@id" |
| Code |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>Rol-ID
Hallo huidige rol-ID voor Hallo-exemplaar wordt opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@id" |
| Code |var-id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>Bijwerken van domein
Hallo updatedomein van Hallo-exemplaar wordt opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@updateDomain" |
| Code |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Foutdomein
Hiermee haalt u foutdomein op Hallo van Hallo-exemplaar.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@faultDomain" |
| Code |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Rolnaam
De rolnaam Hallo Hallo exemplaren van opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/RoleEnvironment/CurrentInstance/@roleName" |
| Code |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Configuratie-instelling
Haalt Hallo waarde Hallo opgegeven configuratie-instelling.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting [@name= 'Setting1']/@value' |
| Code |de instelling var = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Pad voor lokale opslag
Hallo lokale opslagpad voor Hallo-exemplaar wordt opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name= 'LocalStore1']/@path' |
| Code |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1"). RootPath; |

## <a name="local-storage-size"></a>De grootte van de lokale opslag
Haalt de grootte op Hallo van lokale opslag Hallo voor Hallo-exemplaar.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/CurrentInstance/LocalResources/LocalResource [@name= 'LocalStore1']/@sizeInMB' |
| Code |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1"). MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Protocol voor eindpunt
Hallo eindpunt protocol voor het Hallo-exemplaar wordt opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@protocol' |
| Code |var b RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. Protocol; |

## <a name="endpoint-ip"></a>Eindpunt IP
Hallo opgehaald van het eindpunt IP-adres opgegeven.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@address' |
| Code |adres var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. IPEndpoint.Address |

## <a name="endpoint-port"></a>Eindpuntpoort
Hallo eindpuntpoort voor Hallo-exemplaar wordt opgehaald.

| Type | Voorbeeld |
| --- | --- |
| XPath |XPath = "/ RoleEnvironment/CurrentInstance/eindpunten/het eindpunt [@name= '1']/@port' |
| Code |poort var RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1 = ']. IPEndpoint.Port; |

## <a name="example"></a>Voorbeeld
Hier volgt een voorbeeld van een werkrol die u een taak starten met een omgevingsvariabele maakt `TestIsEmulated` ingesteld toohello [ @emulated xpath-waarde](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Volgende stappen
Meer informatie over Hallo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) bestand.

Maak een [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) pakket.

Schakel [extern bureaublad](cloud-services-role-enable-remote-desktop.md) voor een rol.

