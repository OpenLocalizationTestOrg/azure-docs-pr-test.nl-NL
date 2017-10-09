---
title: aaaService Bus met .NET- en AMQP 1.0 | Microsoft Docs
description: Met behulp van Azure Servicebus in .NET met AMQP
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Met behulp van Servicebus in .NET met AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Hallo Service Bus-SDK downloaden

AMQP 1.0-ondersteuning is beschikbaar in Hallo Service Bus-SDK versie 2.1 of hoger. U kunt controleren of u beschikt over de nieuwste versie Hallo Hallo Service Bus bits uit downloaden [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>.NET-toepassingen toouse AMQP 1.0 configureren

Standaard communiceert Hallo Service Bus .NET-clientbibliotheek met Hallo Service Bus-service via een toegewezen op basis van SOAP-protocol. toouse AMQP 1.0 in plaats van een standaardprotocol Hallo vereist expliciete configuratie op Hallo Service Bus-verbindingsreeks, zoals beschreven in de volgende sectie Hallo. Dan deze wijziging ongewijzigd toepassingscode blijft wanneer met behulp van AMQP 1.0.

In de huidige release hello zijn er enkele API-functies worden niet ondersteund bij gebruik van AMQP. Deze niet-ondersteunde functies later worden vermeld in de sectie Hallo [niet-ondersteunde functies, beperkingen en verschillen gebruikersgedrag](#unsupported-features-restrictions-and-behavioral-differences). Aantal Hallo geavanceerde configuratie-instellingen ook hebben een andere betekenis wanneer u AMQP.

### <a name="configuration-using-appconfig"></a>Configuratie met behulp van App.config

Het is raadzaam om voor toepassingen toouse Hallo App.config toostore instellingen voor het configuratiebestand. U kunt App.config toostore Hallo Service Bus-verbindingsreeks gebruiken voor Service Bus-toepassingen. Een voorbeeld App.config-bestand is als volgt:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

waarde van Hallo Hallo `Microsoft.ServiceBus.ConnectionString` instelling Hallo Service Bus-verbindingsreeks die wordt gebruikt tooconfigure Hallo verbinding tooService Bus is. Hallo-indeling is als volgt:

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Waar `[namespace]` en `SharedAccessKey` worden verkregen vanaf Hallo [Azure-portal] [ Azure portal] wanneer u een Service Bus-naamruimte maken. Zie voor meer informatie [maken van een Service Bus-naamruimte met behulp van hello Azure-portal][Create a Service Bus namespace using hello Azure portal].

Wanneer u AMQP, toevoeg-verbindingsreeks Hallo met `;TransportType=Amqp`. Deze notation geïnstrueerd Hallo client bibliotheek toomake de tooService verbinding met AMQP 1.0 Bus.

## <a name="message-serialization"></a>Bericht-serialisatie

Wanneer u Hallo-standaardprotocol gebruikt, Hallo standaardgedrag serialisatie van Hallo .NET-clientbibliotheek is toouse hello [DataContractSerializer] [ DataContractSerializer] tooserialize Typ een [BrokeredMessage ] [ BrokeredMessage] -exemplaar voor transport tussen Hallo-clientbibliotheek en Hallo Service Bus-service. Wanneer u Hallo AMQP-transportmodus, Hallo-clientbibliotheek systeem AMQP Hallo gebruikt voor het serialiseren van Hallo [brokered berichten] [ BrokeredMessage] in een AMQP-bericht. Deze serialisatie kunt Hallo-bericht toobe ontvangen en geïnterpreteerd door een ontvangende toepassing die mogelijk wordt uitgevoerd op een ander platform, bijvoorbeeld een Java-toepassing die gebruikmaakt van Hallo JMS API tooaccess Service Bus.

Wanneer u samenstellen een [BrokeredMessage] [ BrokeredMessage] exemplaar, kunt u een .NET-object opgeven als een parameter toohello constructor tooserve als Hallo hoofdtekst van het Hallo-bericht. Voor objecten die toegewezen tooAMQP primitieve typen worden kunnen, wordt Hallo-instantie omgezet in gegevenstypen AMQP. Als het Hallo-object kan niet rechtstreeks worden toegewezen aan een primitief type AMQP; dat wil zeggen, een aangepast type is gedefinieerd door de toepassing hello vervolgens Hallo-object is geserialiseerd met de Hallo [DataContractSerializer][DataContractSerializer], en Hallo geserialiseerd bytes worden verzonden in een bericht AMQP-gegevens.

toofacilitate interoperabiliteit met niet-.NET-clients gebruiken alleen .NET-typen die kunnen worden geserialiseerd rechtstreeks in het AMQP-typen voor Hallo hoofdtekst van het Hallo-bericht. Hallo tabel details over deze typen en Hallo bijbehorende toewijzing toohello AMQP typesysteem.

| Objecttype voor .NET-instantie | Toegewezen AMQP-Type | AMQP hoofdtekst sectietype |
| --- | --- | --- |
| BOOL |Booleaanse waarde |AMQP-waarde |
| Byte |ubyte |AMQP-waarde |
| USHORT |USHORT |AMQP-waarde |
| uint |uint |AMQP-waarde |
| ULONG |ULONG |AMQP-waarde |
| SByte |Byte |AMQP-waarde |
| korte |korte |AMQP-waarde |
| int |int |AMQP-waarde |
| lang |lang |AMQP-waarde |
| Float |Float |AMQP-waarde |
| dubbele |dubbele |AMQP-waarde |
| Decimale |decimal128 |AMQP-waarde |
| CHAR |CHAR |AMQP-waarde |
| Datum/tijd |tijdstempel |AMQP-waarde |
| GUID |UUID |AMQP-waarde |
| Byte] |Binaire |AMQP-waarde |
| Tekenreeks |Tekenreeks |AMQP-waarde |
| System.Collections.IList-implementatie |lijst |AMQP-waarde: items in het Hallo-verzameling kunnen alleen worden toepassingen die zijn gedefinieerd in deze tabel. |
| System.Array |matrix |AMQP-waarde: items in het Hallo-verzameling kunnen alleen worden toepassingen die zijn gedefinieerd in deze tabel. |
| System.Collections.IDictionary-implementatie |Kaart |AMQP-waarde: items in het Hallo-verzameling kunnen alleen worden toepassingen die zijn gedefinieerd in deze tabel. Opmerking: alleen tekenreekssleutels worden ondersteund. |
| URI |Tekenreeks beschreven (Zie de volgende tabel Hallo) |AMQP-waarde |
| DateTimeOffset |Lange beschreven (Zie de volgende tabel Hallo) |AMQP-waarde |
| TimeSpan |Lange beschreven (Zie volgende Hallo) |AMQP-waarde |
| Stroom |Binaire |AMQP-gegevens (mogelijk meerdere). Hallo gegevenssecties bevatten Hallo onbewerkte bytes lezen uit Hallo Stream-object. |
| Andere objecten |Binaire |AMQP-gegevens (mogelijk meerdere). Hallo geserialiseerd binair van Hallo-object dat gebruikmaakt van Hallo DataContractSerializer of een serialisatiefunctie opgegeven door de toepassing hello bevat. |

| .NET-type | Toegewezen AMQP beschreven Type | Opmerkingen |
| --- | --- | --- |
| URI |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| DateTimeOffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Niet-ondersteunde functies en beperkingen gebruikersgedrag verschillen

Hallo volgende kenmerken van Hallo Service Bus-.NET API worden momenteel niet ondersteund bij gebruik van AMQP:

* Transacties
* Verzenden via overdracht bestemming

Er zijn ook een aantal kleine verschillen in Hallo gedrag van Service Bus-.NET API Hallo wanneer u AMQP, vergeleken toohello standaardprotocol:

* Hallo [OperationTimeout] [ OperationTimeout] eigenschap wordt genegeerd.
* `MessageReceiver.Receive(TimeSpan.Zero)`wordt geïmplementeerd als `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Berichten voltooien door vergrendeling tokens kan alleen worden uitgevoerd door Hallo-bericht ontvangers die in eerste instantie Hallo-berichten ontvangen.

## <a name="controlling-amqp-protocol-settings"></a>AMQP-protocol-instellingen beheren

Hallo [.NET API's](/dotnet/api/) verschillende instellingen toocontrol Hallo gedrag van Hallo AMQP-protocol beschikbaar:

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: besturingselementen Hallo initiële tegoed toegepast tooa koppeling. Hallo standaardwaarde is 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: besturingselementen Hallo AMQP frame maximumgrootte aangeboden tijdens het Hallo-onderhandeling tijdens verbinding openen. Hallo standaardwaarde is 65.536 bytes.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: als overdrachten batchable, deze waarde bepaalt Hallo maximale vertraging voor het verzenden van dispositions. Overgenomen door afzenders/ontvangers standaard. Afzonderlijke afzender/ontvanger kunt Hallo standaardwaarde 20 milliseconden overschrijven.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)**: Hiermee bepaalt u of AMQP-verbindingen tot stand via een SSL-verbinding gebracht worden. Hallo standaardwaarde is **true**.

## <a name="next-steps"></a>Volgende stappen

Gereed toolearn meer? Ga naar Hallo koppelingen te volgen:

* [Service Bus AMQP-overzicht]
* [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd]
* [AMQP in WindowsServer-Servicebus]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Service Bus AMQP-overzicht]: service-bus-amqp-overview.md
[AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP in WindowsServer-Servicebus]: https://msdn.microsoft.com/library/dn574799.aspx
