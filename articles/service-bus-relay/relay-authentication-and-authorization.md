---
title: aaaAzure Relay-verificatie en autorisatie | Microsoft Docs
description: Overzicht van Shared Access Signature (SAS)-verificatie in Azure Relay
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Azure Relay-verificatie en autorisatie
Toepassingen kunnen verifiëren tooAzure Relay met Shared Access Signature (SAS)-verificatie. Vergelijkbare te[Service Bus-berichtenservice](../service-bus-messaging/service-bus-authentication-and-authorization.md), SAS-verificatie kunnen toepassingen tooauthenticate toohello Azure Relay-service met een toegangssleutel die is geconfigureerd op Hallo Relay-naamruimte. Vervolgens kunt u deze sleutel toogenerate een Shared Access Signature-token dat clients tooauthenticate toohello relay-service kunnen gebruiken.

## <a name="shared-access-signature-authentication"></a>Shared Access Signature-verificatie
[SAS verificatie](../service-bus-messaging/service-bus-sas.md) kunt u toogrant een gebruiker toegang tot tooAzure Relay bronnen met specifieke rechten. SAS-verificatie omvat het Hallo-configuratie van een cryptografische sleutel met de gekoppelde rechten van een resource. Clients krijgen vervolgens toegang toothat resource in de vorm van een SAS-token, die bestaat uit Hallo resource-URI wordt geopend en een ondertekend met Hallo verstrijken sleutel geconfigureerd.

U kunt de sleutels voor SA's configureren voor een Relay-naamruimte. In tegenstelling tot de Service Bus-berichtenservice [Relay hybride verbindingen](relay-hybrid-connections-protocol.md) onbevoegde of anonieme afzenders ondersteunt. U kunt anonieme toegang inschakelen voor Hallo entiteit bij het maken, zoals wordt weergegeven in de volgende schermopname van de portal Hallo Hallo:

![][0]

toouse SAS, kunt u een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) object op een Relay-naamruimte die uit de volgende Hallo bestaat:

* *KeyName* die Hallo regel identificeert.
* *PrimaryKey* is een cryptografische sleutel gebruikt toosign/valideren SAS-tokens.
* *Secundaire sleutel* is een cryptografische sleutel gebruikt toosign/valideren SAS-tokens.
* *Rechten* dat Hallo collectie Listen vertegenwoordigt, verzenden of beheren van rechten verleend.

Autorisatieregels geconfigureerd op het niveau van de naamruimte Hallo kunnen toegang verlenen toegang tooall relay-verbindingen in een naamruimte voor clients met tokens die zijn ondertekend met de bijbehorende sleutel Hallo. Up too12 kunnen dergelijke autorisatieregels worden geconfigureerd voor een Relay-naamruimte. Standaard een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) met alle rechten is geconfigureerd voor elke naamruimte als het eerst is ingericht.

tooaccess een entiteit Hallo-client vereist dat een SAS-token dat is gegenereerd met een specifieke [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Hallo SAS-token wordt gegenereerd op basis van hello HMAC-SHA256 van een resourcetekenreeks die uit Hallo resource URI toowhich toegang bestaat is aangevraagd en een verloopbewerking met een cryptografische sleutel die is gekoppeld aan het Hallo-autorisatieregel.

Ondersteuning van de SAS-verificatie voor Azure Relay is opgenomen in hello Azure .NET SDK-versies 2.0 en hoger. SAS biedt ondersteuning voor een [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Alle API's die een verbindingsreeks als een parameter accepteren onder meer ondersteuning voor SAS-verbindingsreeksen.

## <a name="next-steps"></a>Volgende stappen
- Blijven lezen [Service Bus-verificatie met Shared Access Signatures](../service-bus-messaging/service-bus-sas.md) voor meer informatie over SAS.
- Zie Hallo [Azure Relay hybride verbindingen protocol handleiding](relay-hybrid-connections-protocol.md) voor gedetailleerde informatie over Hallo mogelijkheid hybride verbindingen.
- Zie voor de bijbehorende informatie over Service Bus-berichtenservice verificatie en autorisatie, [Service Bus-verificatie en autorisatie](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png