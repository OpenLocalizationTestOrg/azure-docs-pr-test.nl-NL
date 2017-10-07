---
title: Controlelijst voor de aaaAzure service fabric beveiliging | Microsoft Docs
description: In dit artikel biedt een reeks controlelijst voor beveiliging van de Azure-infrastructuur.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Controlelijst van Azure Service Fabric-beveiliging
Dit artikel bevat een controlelijst eenvoudig te gebruiken, waarmee u uw Azure Service Fabric-omgeving te beveiligen.

## <a name="introduction"></a>Inleiding
Azure Service Fabric is een platform voor gedistribueerde systemen waarmee u eenvoudig toopackage kunt, implementeren en beheren van schaalbare en betrouwbare microservices. Service Fabric ook een oplossing voor grote uitdagingen Hallo ontwikkelen en beheren van cloudtoepassingen. Ontwikkelaars en beheerders kunnen complexe infrastructuurproblemen voorkomen en zich concentreren op het implementeren van bedrijfsspecifieke, veeleisende werkbelastingen die schaalbaar, betrouwbaar en beheerbaar zijn.

## <a name="checklist"></a>Controlelijst
Gebruik Hallo controlelijst toohelp u ervoor zorgen dat u dit nog niet hebt over het hoofd eventuele belangrijke problemen in beheer en configuratie van een veilige Azure Service Fabric-oplossing gezien te volgen.


|Controlelijst categorie| Beschrijving |
| ------------ | -------- |
|[Op rollen gebaseerd toegangsbeheer (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Toegangsbeheer kunt Hallo beheerder toolimit toegang toocertain cluster clusterbewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken.</li><li>Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). </li><li>   Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.</li></ul>|
|[X.509-certificaten en Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>[Certificaten](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) gebruikt in clusters actief productieworkloads moeten worden gemaakt met behulp van een juist geconfigureerde service voor Windows Server-certificaat of verkregen van een goedgekeurde [certificeringsinstantie (CA)](https://en.wikipedia.org/wiki/Certificate_authority).</li><li>Gebruik nooit een [tijdelijke of certificaten testen](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) in productie die zijn gemaakt met hulpprogramma's zoals [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>U kunt een [zelf-ondertekend certificaat](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) maar moet alleen doen voor testclusters en niet in de productieomgeving.</li></ul>|
|[Clusterbeveiliging](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>Hallo cluster security scenario's omvatten knooppunt naar beveiliging, Client-naar-knooppunt, [op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Cluster-verificatie](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Verifieert [knooppunt naar communicatie](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) voor cluster Federatie. </li></ul>|
|[Server-verificatie](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Hallo verifieert [eindpunten voor beheer van cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa management-client.</li></ul>|
|[Toepassingsbeveiliging](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>Versleuteling en ontsleuteling van configuratiewaarden die van toepassing.</li><li> Codering van gegevens over knooppunten tijdens de replicatie.</li></ul>|
|[Cluster-certificaat](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Dit certificaat is vereist toosecure Hallo communicatie tussen knooppunten Hallo op een cluster.</li><li>  Hallo vingerafdruk van primaire certificaat voor Hallo in Hallo vingerafdruk sectie en instellen dat Hallo secundaire Hallo ThumbprintSecondary variabelen.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Dit certificaat wordt toohello client weergegeven als er wordt geprobeerd tooconnect toothis cluster. U kunt twee verschillende servercertificaten, een primaire en een secundaire voor een upgrade.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Dit is een set van certificaten die u tooinstall op Hallo geverifieerde clients wilt. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Hallo algemene naam van de eerste clientcertificaat Hallo voor Hallo CertificateCommonName instellen. Hallo CertificateIssuerThumbprint is Hallo vingerafdruk voor Hallo verlener van dit certificaat. </li></ul>|
|ReverseProxyCertificate| <ul><li>Dit is een optioneel certificaat dat kan worden opgegeven als u wilt dat toosecure uw [Reverse Proxy](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Key Vault| <ul><li>Toomanage certificaten gebruikt voor Service Fabric-clusters in Azure.  </li></ul>|


## <a name="next-steps"></a>Volgende stappen
- [Het upgradeproces service Fabric-Cluster en de verwachtingen van u](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Het beheren van uw Service Fabric-toepassingen in Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Status van de Fabric-service model inleiding](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
