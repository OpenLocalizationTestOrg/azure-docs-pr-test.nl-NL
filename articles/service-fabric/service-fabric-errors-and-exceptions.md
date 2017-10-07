---
title: aaaCommon FabricClient uitzonderingen | Microsoft Docs
description: Beschrijft Hallo algemene uitzonderingen en fouten die door Hallo FabricClient APIs kunnen worden gegenereerd tijdens het uitvoeren van beheerbewerkingen toepassing en het cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Algemene uitzonderingen en fouten bij het werken met Hallo FabricClient APIs
Hallo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) -API's kunnen cluster en de toepassing beheerders tooperform administratieve taken op een Service Fabric-toepassing, een service of een cluster. Bijvoorbeeld: toepassingsimplementatie, upgrade en verwijderen van een service te testen of controleren Hallo health een cluster. Softwareontwikkelaars en clusterbeheerders kunnen Hallo FabricClient API's toodevelop hulpprogramma's gebruiken voor het beheren van Hallo Service Fabric-cluster en toepassingen.

Er zijn veel verschillende soorten bewerkingen waarvoor kunnen worden uitgevoerd met behulp van FabricClient.  Elke methode kunt uitzonderingen voor fouten vanwege tooincorrect invoer, runtime-fouten of problemen van voorbijgaande aard infrastructuur genereren.  Zie Hallo API reference documentatie toofind welke uitzonderingen worden veroorzaakt door een specifieke methode. Er zijn enkele uitzonderingen, maar die kunnen worden gegenereerd door veel verschillende [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API's. Hallo bevat volgende tabel Hallo uitzonderingen die door Hallo FabricClient APIs gedeeld worden.

| Uitzondering | Gegenereerd wanneer |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Hallo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) bevindt zich in een gesloten. Buitengebruikstelling van Hallo [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) object u gebruikt en een nieuwe [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) object. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |Er is een time-out opgetreden bij het Hallo-bewerking. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) wordt geretourneerd wanneer het Hallo-bewerking duurt langer dan MaxOperationTimeout toocomplete. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Hallo toegangscontrole voor Hallo-bewerking is mislukt. E_ACCESSDENIED wordt geretourneerd. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Een runtime-fout is opgetreden tijdens het Hallo-bewerking uitvoeren. Hallo FabricClient methoden kunt mogelijk de throw [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), Hallo [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) eigenschap geeft Hallo exacte oorzaak van Hallo-uitzondering. Foutcodes zijn gedefinieerd in Hallo [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) opsomming. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |Hallo-bewerking is mislukt vanwege een tijdelijke fout tooa type. Bijvoorbeeld: een bewerking mislukken omdat een quorum van replica's tijdelijk niet bereikbaar is. Tijdelijke uitzonderingen komen overeen toofailed bewerkingen die kunnen opnieuw worden uitgevoerd. |

Sommige algemene [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) fouten die kunnen worden geretourneerd in een [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException):

| Fout | Voorwaarde |
| --- |:--- |
| CommunicationError |Een communicatiefout is Hallo bewerking toofail, Hallo opnieuw. |
| InvalidCredentialType |Hallo referentietype is ongeldig. |
| InvalidX509FindType |Hallo X509FindType is ongeldig. |
| InvalidX509StoreLocation |Hallo X509 opslaglocatie is ongeldig. |
| InvalidX509StoreName |Hallo X509 Opslagnaam is ongeldig. |
| InvalidX509Thumbprint |Hallo X509 certificaat vingerafdruk tekenreeks is ongeldig. |
| InvalidProtectionLevel |Hallo beveiligingsniveau is ongeldig. |
| InvalidX509Store |Hallo X509 certificaatarchief kan niet worden geopend. |
| InvalidSubjectName |Hallo-objectnaam is ongeldig. |
| InvalidAllowedCommonNameList |Hallo-indeling van tekenreeks voor de algemene lijst is ongeldig. Deze moet een door komma's gescheiden lijst. |

