---
title: Service Fabric-container beveiliging aaaAzure | Microsoft Docs
description: Meer informatie over nu toosecure containerservices.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>Beveiliging van de container

Service Fabric biedt een mechanisme voor services binnen een container tooaccess een certificaat dat is geïnstalleerd op het Hallo-knooppunten in een Windows- of Linux-cluster (versie 5.7 of hoger). Service Fabric ondersteunt bovendien ook gMSA (groep beheerde serviceaccounts) voor Windows-containers. 

## <a name="certificate-management-for-containers"></a>Certificaatbeheer voor containers

U kunt uw containerservices beveiligen door te geven van een certificaat. Hallo-certificaat moet worden geïnstalleerd op Hallo knooppunten van het Hallo-cluster. Hallo certificaatinformatie vindt u in het toepassingsmanifest Hallo onder Hallo `ContainerHostPolicies` label als Hallo volgende codefragment bevat:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Bij het starten van de toepassing hello wordt Hallo runtime Hallo certificaten leest en genereert een PFX-bestand en het wachtwoord voor elk certificaat. Deze PFX-bestand en het wachtwoord zijn toegankelijk binnen Hallo-container met Hallo omgevingsvariabelen te volgen: 

* **Certificate_ [CodePackageName] _ [CertName] _PFX**
* **Certificate_ [CodePackageName] _ [CertName] _Password**

Hallo containerservice of het proces is verantwoordelijk voor het importeren van Hallo PFX-bestand in container Hallo. tooimport hello certificaat, kunt u `setupentrypoint.sh` scripts of aangepaste code binnen Hallo container proces uitgevoerd. Hier volgt de voorbeeldcode in C# voor het importeren van Hallo PFX-bestand:

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
Dit PFX-certificaat kan worden gebruikt voor verificatie Hallo toepassing of service of beveiligde commmunication met andere services.


## <a name="set-up-gmsa-for-windows-containers"></a>Instellen van gMSA voor Windows-containers

tooset van gMSA (groep beheerde serviceaccounts), een referentie specification-bestand (`credspec`) op alle knooppunten in cluster hello wordt geplaatst. Hallo-bestand kan worden gekopieerd op alle knooppunten met behulp van een VM-extensie.  Hallo `credspec` bestand moet Hallo gMSA-accountgegevens bevatten. Voor meer informatie over Hallo `credspec` bestand, Zie [serviceaccounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Hallo referentie-specificatie en Hallo `Hostname` label in het toepassingsmanifest Hallo zijn opgegeven. Hallo `Hostname` label moet overeenkomen met de Hallo gMSA accountnaam op die Hallo onder container wordt uitgevoerd.  Hallo `Hostname` tag kan Hallo container tooauthenticate zelf tooother services in Hallo domein Kerberos-verificatie gebruiken.  Een voorbeeld voor het opgeven van Hallo `Hostname` en Hallo `credspec` in Hallo toepassingsmanifest wordt weergegeven in het volgende codefragment Hallo:

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Volgende stappen

* [Een Windows-container tooService Fabric op Windows Server 2016 implementeren](service-fabric-get-started-containers.md)
* [Implementeert een Docker-container tooService Fabric op Linux](service-fabric-get-started-containers-linux.md)
