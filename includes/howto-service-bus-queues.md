## <a name="what-are-service-bus-queues"></a>Wat zijn Service Bus-wachtrijen?
Service Bus-wachtrijen ondersteunen een **Brokered Messaging**-communicatiemodel. Wanneer u gebruikmaakt van wachtrijen, communiceren onderdelen van een gedistribueerde toepassing niet direct met elkaar. In plaats daarvan wisselen ze berichten uit via een wachtrij die als intermediaire service (broker) fungeert. De maker van een bericht (afzender) draagt een berichtenwachtrij toohello en vervolgens blijft de verwerking ervan. Asynchroon, de gebruiker van een bericht (ontvanger) haalt het Hallo-bericht van Hallo wachtrij en verwerkt deze. Hallo producent geen toowait op een antwoord van de consumer Hallo in volgorde toocontinue tooprocess en verzenden van verdere berichten. Wachtrijen bieden **First In, eerste Out (FIFO)** message delivery tooone of meer concurrerende consumenten. Dat wil zeggen, worden berichten meestal ontvangen en verwerkt door de ontvangers Hallo in Hallo volgorde waarin ze zijn toohello wachtrij toegevoegd en elk bericht wordt ontvangen en verwerkt door slechts één berichtconsument.

![QueueConcepts](./media/howto-service-bus-queues/sb-queues-08.png)

Service Bus-wachtrijen is een technologie voor algemeen gebruik die voor een groot aantal verschillende scenario's kan worden gebruikt:

* Communicatie tussen web- en werkrollen in een meerlaagse Azure-toepassing.
* Communicatie tussen on-premises apps en in Azure gehoste apps in een hybride oplossing.
* Communicatie tussen onderdelen van een gedistribueerde toepassing die on-premises wordt uitgevoerd in verschillende organisaties of afdelingen binnen een organisatie.

Met behulp van wachtrijen kunnen tooscale u uw toepassingen eenvoudiger en meer tolerantie tooyour architectuur inschakelen.


