---
title: Service Bus aaaAzure verificatie en autorisatie | Microsoft Docs
description: Apps tooService Bus met Shared Access Signature (SAS)-verificatie worden geverifieerd.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Vereenvoudigde Service Bus-verificatie en -autorisatie

Toepassingen kunnen verifiëren tooAzure Service Bus Shared Access Signature (SAS) met verificatie. Shared Access Signature-verificatie kunnen toepassingen tooauthenticate tooService Bus met behulp van een toegangssleutel die is geconfigureerd op Hallo naamruimte of op Hallo entiteit waaraan de specifieke rechten zijn gekoppeld. Vervolgens kunt u deze sleutel toogenerate een Shared Access Signature-token dat clients tooauthenticate tooService Bus kunnen gebruiken.

> [!IMPORTANT]
> U moet SAS gebruiken in plaats van Azure Active Directory-toegangsbeheer (ook wel bekend als Access Control Service of ACS), zoals ACS wordt afgeschaft. SAS biedt een eenvoudige, flexibele en eenvoudig te gebruiken verificatieschema voor Service Bus. Toepassingen kunnen SAS gebruiken in scenario's waarin ze hoeven niet toomanage Hallo begrip van een geautoriseerde 'gebruiker'. Zie voor meer informatie [dit blogbericht](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Shared Access Signature-verificatie

[SAS verificatie](service-bus-sas.md) kunt u toogrant een gebruiker toegang tooService Bus-resources met specifieke rechten. SAS-verificatie in Service Bus omvat het Hallo-configuratie van een cryptografische sleutel met de gekoppelde rechten van een Service Bus-resource. Clients krijgen vervolgens toegang toothat resource in de vorm van een SAS-token, die bestaat uit Hallo resource-URI wordt geopend en een ondertekend met Hallo verstrijken sleutel geconfigureerd.

U kunt de sleutels voor SA's configureren voor een Service Bus-naamruimte. Hallo-sleutel is van toepassing tooall berichtentiteiten in waarmee de naamruimte. U kunt ook sleutels configureren over Service Bus-wachtrijen en onderwerpen. SAS wordt ook ondersteund op [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md).

toouse SAS, kunt u een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object op een naamruimte, wachtrij of onderwerp. Deze regel bestaat uit Hallo volgende elementen:

* *KeyName* die Hallo regel identificeert.
* *PrimaryKey* is een cryptografische sleutel gebruikt toosign/valideren SAS-tokens.
* *Secundaire sleutel* is een cryptografische sleutel gebruikt toosign/valideren SAS-tokens.
* *Rechten* dat Hallo collectie Listen vertegenwoordigt, verzenden of beheren van rechten verleend.

Autorisatieregels geconfigureerd op het niveau van de naamruimte Hallo kunnen toegang verlenen tooall entiteiten in een naamruimte voor clients met tokens die zijn ondertekend met een bijbehorende Hallo-sleutel. Up too12 kunnen dergelijke autorisatieregels worden geconfigureerd op een Service Bus-naamruimte, wachtrij of onderwerp. Standaard een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) met alle rechten is geconfigureerd voor elke naamruimte als het eerst is ingericht.

tooaccess een entiteit Hallo-client vereist dat een SAS-token dat is gegenereerd met een specifieke [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Hallo SAS-token wordt gegenereerd op basis van hello HMAC-SHA256 van een resourcetekenreeks die uit Hallo resource URI toowhich toegang bestaat is aangevraagd en een verloopbewerking met een cryptografische sleutel die is gekoppeld aan het Hallo-autorisatieregel.

Ondersteuning van de SAS-verificatie voor Service Bus is opgenomen in hello Azure .NET SDK-versies 2.0 en hoger. SAS biedt ondersteuning voor een [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Alle API's die een verbindingsreeks als een parameter accepteren onder meer ondersteuning voor SAS-verbindingsreeksen.

## <a name="next-steps"></a>Volgende stappen

- Blijven lezen [Service Bus-verificatie met Shared Access Signatures](service-bus-sas.md) voor meer informatie over SAS.
- [Wijzigingen tooACS ingeschakeld naamruimten.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Zie voor de bijbehorende informatie over Azure Relay-verificatie en autorisatie, [Azure Relay-verificatie en autorisatie](../service-bus-relay/relay-authentication-and-authorization.md). 

