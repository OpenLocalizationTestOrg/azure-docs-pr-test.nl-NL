Hallo volgende tabel worden beschreven Hallo belangrijke quota, limieten, standaardwaarden en vertragingen in Azure Scheduler.

| Resource | Beschrijving van de limiet |
| --- | --- |
| **De grootte van de taak** |Maximale grootte is 16 kB. Als een plaatsen of een PATCH in een taak die groter is dan deze limiet resulteert, wordt een 400 Ongeldige aanvraag statuscode geretourneerd. |
| **De grootte van de aanvraag-URL** |Maximale grootte van de aanvraag-URL Hallo is 2048 tekens. |
| **Cumulatieve header-grootte** |Maximale cumulatieve header-grootte is 4096 tekens. |
| **Header-telling** |Maximale header aantal is 50 headers. |
| **Grootte van standaardberichthoofdtekst** |Maximale grootte is 8192 tekens. |
| **Terugkeerpatroon in beslag neemt** |Maximale terugkeerpatroon span is 18 maanden. |
| **Tijd toostart tijd** |Maximaal 'tijd toostart keer' is 18 maanden. |
| **Jobgeschiedenis** |Maximale antwoordtekst die zijn opgeslagen in de taakgeschiedenis is 2048 bytes. |
| **Frequentie** |Hallo standaard maximale frequentie quotum is 1 uur in een gratis taakverzameling en 1 minuut in een standaard taakverzameling. de maximale frequentie Hallo kan worden geconfigureerd op een lager is dan de maximale Hallo taak verzameling toobe. Alle taken in de taakverzameling Hallo zijn beperkt Hallo-waarde ingesteld op Hallo taakverzameling. Als u een taak met een hogere frequentie dan de maximale frequentie voor de taakverzameling Hallo Hallo toocreate probeert vervolgens mislukt aanvraag met statuscode 409 Conflict. |
| **Taken** |Hallo max taken standaardquotum is 5 taken in een gratis taakverzameling en 50 taken in een standaard taakverzameling. maximum aantal taken Hallo kan worden geconfigureerd op een taakverzameling. Alle taken in de taakverzameling Hallo zijn beperkt Hallo-waarde ingesteld op Hallo taakverzameling. Als u probeert toocreate meer taken dan Hallo maximale taken quota, wordt het Hallo-aanvraag is mislukt met statuscode 409 Conflict. |
| **Taakverzamelingen** |Maximum aantal taakverzameling per abonnement is 200.000. |
| **Geschiedenis vasthouden** |Taakgeschiedenis up too2 maanden bewaard of up toohello laatste 1000 uitvoeringen. |
| **Voltooide en mislukte taak bewaren** |Voltooide en mislukte jobs worden bewaard gedurende 60 dagen. |
| **Time-out** |Er is een statische (niet-configureerbare) aanvraag time-out van 60 seconden voor HTTP-acties. Volg voor actieve bewerkingen langer, asynchrone HTTP-protocollen. bijvoorbeeld, een 202 onmiddellijk geretourneerd, maar blijven werken op de achtergrond Hallo. |

