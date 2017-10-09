Hallo volgende tabel bevat quota's en specifieke tooAzure Event Hubs wordt beperkt. Zie voor meer informatie over prijzen van Event Hubs [prijzen van Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

| Limiet | Bereik | Type | Gedrag wanneer overschreden | Waarde |
| --- | --- | --- | --- | --- |
| Het aantal van Event Hubs per naamruimte |naamruimte |Statisch |De volgende aanvragen voor het maken van een nieuwe naamruimte worden geweigerd. |10 |
| Aantal partities per Event Hub |Entiteit |Statisch |- |32 |
| Aantal consumergroepen per Event Hub |Entiteit |Statisch |- |20 |
| Aantal AMQP-verbindingen per naamruimte |naamruimte |Statisch |De volgende aanvragen voor aanvullende verbindingen wordt geweigerd en een uitzondering is ontvangen door Hallo code aanroepen. |5,000 |
| Maximale grootte van Event Hubs-gebeurtenis|Systeeminstellingen |Statisch |- |256 kB |
| Maximale grootte van de naam van een Event Hub |Entiteit |Statisch |- |50 tekens |
| Het aantal niet-epoche ontvangers per klantengroep |Entiteit |Statisch |- |5 |
| Maximale bewaarperiode van gebeurtenisgegevens |Entiteit |Statisch |- |1-7 dagen |
| Maximum aantal Throughput Units |naamruimte |Statisch |Meer dan Hallo doorvoer eenheid limiet zorgt ervoor dat uw gegevens toobe beperkt en genereert een  **[ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)**. U kunt een groter aantal doorvoereenheden voor een standaard aanvragen laag met indiening een [ondersteuningsaanvraag](/azure/azure-supportability/how-to-create-azure-support-request). [Aanvullende doorvoereenheden](../articles/event-hubs/event-hubs-auto-inflate.md) zijn beschikbaar in blokken van 20 op basis van de vastgelegde aankoop. |20 |

