---
title: aaaAMQP 1.0 in Azure Service Bus-bewerkingen op basis van aanvraag-antwoord | Microsoft Docs
description: Lijst met Microsoft Azure Service Bus-aanvraag/antwoord-bewerkingen.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>AMQP 1.0 in Microsoft Azure Service Bus: aanvraag-antwoord-bewerkingen

In dit onderwerp definieert Hallo lijst met Microsoft Azure Service Bus-aanvraag/antwoord-bewerkingen. Deze informatie is gebaseerd op Hallo AMQP Management versie 1.0 werkende concept.  
  
Zie voor een gedetailleerde wire-niveau AMQP 1.0-protocol handleiding, waarin wordt uitgelegd hoe Service Bus implementeert en bouwt voort op Hallo OASIS AMQP technische specificatie, Hallo [AMQP 1.0 in Azure Service Bus en Event Hubs protocol handleiding](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Concepten  
  
### <a name="entity-description"></a>De beschrijving van entiteit  

Een beschrijving van de entiteit verwijst een Service Bus tooeither [QueueDescription klasse](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription klasse](/dotnet/api/microsoft.servicebus.messaging.topicdescription), of [SubscriptionDescription klasse](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) object.  
  
### <a name="brokered-message"></a>Brokered berichten  

Hiermee geeft u een bericht in Service Bus, toegewezen tooan AMQP-bericht is. Hallo-toewijzing is gedefinieerd in Hallo [Service Bus AMQP-protocol handleiding](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Knooppunt tooentity koppelen  

Alle Hallo bewerkingen die worden beschreven in dit document een aanvraag/antwoord-patroon volgen, zijn binnen het bereik tooan entiteit en vereisen tooan entiteit knooppunt koppelen.  
  
### <a name="create-link-for-sending-requests"></a>Koppeling voor het verzenden van aanvragen maken  

Hiermee maakt u een koppeling toohello knooppunt voor het verzenden van aanvragen.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Koppeling voor het ontvangen van antwoorden maken  

Maakt een koppeling voor het ontvangen van reacties van Hallo knooppunt.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Een aanvraagbericht overdragen  

Een aanvraagbericht overgedragen.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Een antwoordbericht ontvangen  

Hallo response-bericht ontvangt van Hallo antwoord koppeling.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
Hallo-bericht van antwoord heeft Hallo formulier te volgen:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Adres van Service Bus-entiteit  

Service Bus-entiteiten moeten worden aangepakt als volgt:  
  
|Entiteitstype|Adres|Voorbeeld|  
|-----------------|-------------|-------------|  
|Wachtrij|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|Onderwerp|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|abonnement|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Berichtbewerkingen  
  
### <a name="message-renew-lock"></a>Bericht vernieuwen vergrendelen  

Breidt Hallo vergrendelen van een bericht door Hallo tijd die is opgegeven in de beschrijving van de Hallo-entiteit.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
 Hallo-bericht aanvraagtekst moet bestaan uit de sectie van een amqp-waarde met een map met de volgende vermeldingen Hallo:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|matrix van uuid|Ja|Bericht vergrendeling tokens toorenew.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt.|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit de sectie van een amqp-waarde met een map met de volgende vermeldingen Hallo:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|accountwachtwoorden|matrix van tijdstempel|Ja|Bericht vergrendeld token nieuwe verlopen bijbehorende toohello aanvragen vergrendeling van tokens.|  
  
### <a name="peek-message"></a>Bericht  

Geeft weer berichten zonder de vergrendeling.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|lang|Ja|Volgnummer uit welke peek toostart.|  
|`message-count`|int|Ja|Maximum aantal berichten toopeek.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – heeft geen berichten meer<br /><br /> 0xcc: Er is geen inhoud – geen berichten meer|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|berichten|lijst met maps|Ja|Lijst met berichten waarin elke kaart een bericht vertegenwoordigt.|  
  
Hallo-toewijzing voor een bericht moet Hallo vermeldingen volgende bevatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|Bericht|matrix van byte|Ja|AMQP 1.0 wire-bericht dat is gecodeerd.|  
  
### <a name="schedule-message"></a>Schema-bericht  

Hiermee plant u berichten.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|berichten|lijst met maps|Ja|Lijst met berichten waarin elke kaart een bericht vertegenwoordigt.|  
  
Hallo-toewijzing voor een bericht moet Hallo vermeldingen volgende bevatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bericht-id|Tekenreeks|Ja|`amqpMessage.Properties.MessageId`Als tekenreeks|  
|sessie-id|Tekenreeks|Ja|`amqpMessage.Properties.GroupId as string`|  
|Partitiesleutel|Tekenreeks|Ja|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|Bericht|matrix van byte|Ja|AMQP 1.0 wire-bericht dat is gecodeerd.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt.|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** met een map met de volgende vermeldingen Hallo sectie:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|volgnummers|matrix van lange|Ja|Het volgnummer van de geplande berichten. Volgnummer is gebruikte toocancel.|  
  
### <a name="cancel-scheduled-message"></a>Geplande bericht annuleren  

Annuleert de geplande berichten.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|volgnummers|matrix van lange|Ja|Volgnummers van geplande berichten toocancel.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt.|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** met een map met de volgende vermeldingen Hallo sectie:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|volgnummers|matrix van lange|Ja|Het volgnummer van de geplande berichten. Volgnummer is gebruikte toocancel.|  
  
## <a name="session-operations"></a>Sessie-bewerkingen  
  
### <a name="session-renew-lock"></a>Sessie vernieuwen vergrendelen  

Breidt Hallo vergrendelen van een bericht door Hallo tijd die is opgegeven in de beschrijving van de Hallo-entiteit.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|sessie-id|Tekenreeks|Ja|Sessie-ID.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – heeft geen berichten meer<br /><br /> 0xcc: Er is geen inhoud – geen berichten meer|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** met een map met de volgende vermeldingen Hallo sectie:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|vervaldatum|tijdstempel|Ja|Nieuwe verlopen.|  
  
### <a name="peek-session-message"></a>Sessie-bericht  

Geeft weer berichten voor sessie zonder de vergrendeling.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|uit de volgnummer|lang|Ja|Volgnummer uit welke peek toostart.|  
|aantal berichten|int|Ja|Maximum aantal berichten toopeek.|  
|sessie-id|Tekenreeks|Ja|Sessie-ID.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – heeft geen berichten meer<br /><br /> 0xcc: Er is geen inhoud – geen berichten meer|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** met een map met de volgende vermeldingen Hallo sectie:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|berichten|lijst met maps|Ja|Lijst met berichten waarin elke kaart een bericht vertegenwoordigt.|  
  
 Hallo-toewijzing voor een bericht moet Hallo vermeldingen volgende bevatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|Bericht|matrix van byte|Ja|AMQP 1.0 wire-bericht dat is gecodeerd.|  
  
### <a name="set-session-state"></a>Set-sessiestatus  

Sets Hallo status van een sessie.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|sessie-id|Tekenreeks|Ja|Sessie-ID.|  
|sessiestatus|bytematrix|Ja|Ondoorzichtige binaire gegevens.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
### <a name="get-session-state"></a>Get-sessiestatus  

Hallo-status van een sessie opgehaald.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|sessie-id|Tekenreeks|Ja|Sessie-ID.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|sessiestatus|bytematrix|Ja|Ondoorzichtige binaire gegevens.|  
  
### <a name="enumerate-sessions"></a>Sessies opsommen  

Sessies op een Berichtentiteit inventariseren.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|laatste-bijgewerkt-time|tijdstempel|Ja|Filter tooinclude alleen sessies bijgewerkt na een bepaald moment.|  
|Overslaan|int|Ja|Een aantal sessies overslaan.|  
|Boven|int|Ja|Maximum aantal sessies.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – heeft geen berichten meer<br /><br /> 0xcc: Er is geen inhoud – geen berichten meer|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|Overslaan|int|Ja|Aantal overgeslagen sessies als statuscode 200.|  
|sessies-id 's|Matrix van tekenreeksen|Ja|Matrix van sessie-id's als statuscode 200.|  
  
## <a name="rule-operations"></a>Bewerkingen voor regel  
  
### <a name="add-rule"></a>Regel toevoegen  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|naam van regel|Tekenreeks|Ja|Regelnaam, met uitzondering van namen abonnement en het onderwerp.|  
|Beschrijving van regel|Kaart|Ja|Regelbeschrijving zoals opgegeven in de volgende sectie.|  
  
Hallo **beschrijving van regel** kaart moet bevatten Hallo-items te volgen waarbij **sql-filter** en **correlatie-filter** sluiten elkaar wederzijds uit:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|SQL-filter|Kaart|Ja|`sql-filter`, zoals opgegeven in de volgende sectie Hallo.|  
|correlatie-filter|Kaart|Ja|`correlation-filter`, zoals opgegeven in de volgende sectie Hallo.|  
|SQL-regelactie|Kaart|Ja|`sql-rule-action`, zoals opgegeven in de volgende sectie Hallo.|  
  
Hallo sql-filter kaart moet Hallo volgende vermeldingen zijn:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|expressie|Tekenreeks|Ja|De filterexpressie SQL.|  
  
Hallo **correlatie-filter** kaart moet ten minste één van de volgende vermeldingen Hallo opnemen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|correlatie-id|Tekenreeks|Nee||  
|bericht-id|Tekenreeks|Nee||  
|tot|Tekenreeks|Nee||  
|antwoord aan|Tekenreeks|Nee||  
|Label|Tekenreeks|Nee||  
|sessie-id|Tekenreeks|Nee||  
|antwoord-naar-sessie-id|Tekenreeks|Nee||  
|type inhoud|Tekenreeks|Nee||  
|properties|Kaart|Nee|Toegewezen tooService Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Hallo **sql regelactie** kaart moet Hallo vermeldingen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|expressie|Tekenreeks|Ja|SQL-expressie in te grijpen.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
### <a name="remove-rule"></a>Regel verwijderen  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|naam van regel|Tekenreeks|Ja|Regelnaam, met uitzondering van namen abonnement en het onderwerp.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
## <a name="deferred-message-operations"></a>Uitgestelde berichtbewerkingen  
  
### <a name="receive-by-sequence-number"></a>Door volgnummer ontvangen  

Uitgestelde berichten op volgnummer ontvangt.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|volgnummers|matrix van lange|Ja|Volgnummers.|  
|ontvanger vereffenen modus|ubyte|Ja|**Ontvanger vereffenen** modus zoals opgegeven in de AMQP core v1.0.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|  
  
Hallo-bericht antwoordtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|berichten|lijst met maps|Ja|Lijst met berichten waarbij elke kaart staat voor een bericht.|  
  
Hallo-toewijzing voor een bericht moet Hallo vermeldingen volgende bevatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|LOCK-token|UUID|Ja|Vergrendeling token als `receiver-settle-mode` is 1.|  
|Bericht|matrix van byte|Ja|AMQP 1.0 wire-bericht dat is gecodeerd.|  
  
### <a name="update-disposition-status"></a>Status van de toestand bijwerken  

Hallo disposition updatestatus van uitgestelde berichten.  
  
#### <a name="request"></a>Aanvraag  

Hallo aanvraagbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|bewerking|Tekenreeks|Ja|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|Nee|Bewerking server time-out in milliseconden.|  
  
Hallo-bericht aanvraagtekst moet bestaan uit een **amqp-waarde** sectie met een **kaart** Hello vermeldingen te volgen:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|toestand-status|Tekenreeks|Ja|Voltooid<br /><br /> Afgebroken<br /><br /> Onderbroken|  
|LOCK-tokens|matrix van uuid|Ja|Status van Message vergrendeling tokens tooupdate toestand.|  
|wachtrij voor onbestelbare reden|Tekenreeks|Nee|Kan worden ingesteld als bestemming instelling te**onderbroken**.|  
|Beschrijving van de wachtrij voor onbestelbare|Tekenreeks|Nee|Kan worden ingesteld als bestemming instelling te**onderbroken**.|  
|Eigenschappen te wijzigen|Kaart|Nee|Lijst met Service Bus brokered bericht eigenschappen toomodify.|  
  
#### <a name="response"></a>Antwoord  

Hallo-antwoordbericht moet Hallo toepassingseigenschappen volgende omvatten:  
  
|Sleutel|Waardetype|Vereist|De inhoud|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Ja|HTTP-antwoordcode [RFC2616]<br /><br /> 200: OK – geslaagd, anders mislukt|  
|StatusDescription|Tekenreeks|Nee|Beschrijving van status Hallo.|

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over AMQP en Service Bus, gaat u naar Hallo koppelingen te volgen:

* [Service Bus AMQP-overzicht]
* [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd]
* [AMQP in WindowsServer-Servicebus]

[Service Bus AMQP-overzicht]: service-bus-amqp-overview.md
[AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP in WindowsServer-Servicebus]: https://msdn.microsoft.com/library/dn574799.asp