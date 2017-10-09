Opslag wordt begrensd door schijfruimte of een vaste limiet van Hallo *maximumaantal* indexen of documenten, afhankelijk van wat zich het eerste voordoet.

| Resource | Gratis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Service Level Agreement (SLA) |Nee <sup>1</sup> |Ja |Ja |Ja |Ja |Ja |
| Opslag per partitie |50 MB |2 GB |25 GB |100 GB |200 GB |200 GB |
| Partities per service |N.v.t. |1 |12 |12 |12 |3 <sup>2</sup> |
| Partitiegrootte |N.v.t. |2 GB |25 GB |100 GB |200 GB |200 GB |
| Replica's |N.v.t. |3 |12 |12 |12 |12 |
| Maximale aantal indexen |3 |5 |50 |200 |200 |1000 per partitie of 3000 per service |
| Maximale aantal indexeerfuncties |3 |5 |50 |200 |200 |Geen ondersteuning voor indexeerfuncties |
| Maximale aantal gegevensbronnen |3 |5 |50 |200 |200 |Geen ondersteuning voor indexeerfuncties |
| Maximale aantal documenten |10.000 |1 miljoen |15 miljoen per partitie of 180 miljoen per service |60 miljoen per partitie of 720 miljoen per service |120 miljoen per partitie of 1,4 miljard per service |1 miljoen per index of 200 miljoen per partitie |
| Geschatte aantal query's per seconde (QPS) |N.v.t. |~3 per replica |~15 per replica |~60 per replica |~60 per replica |>60 per replica |

<sup>1</sup> gratis laag en de preview-functies niet bij service level agreements (Sla's) worden geleverd. Voor alle factureerbare lagen, sla's van kracht als u voldoende redundantie voor uw service inricht. Twee of meer replica's zijn vereist voor de SLA voor query (gelezen). Drie of meer replica's zijn vereist voor query's en indexering SLA (lezen / schrijven). het aantal partities Hallo is niet een SLA-overweging. 

<sup>2</sup> S3 HD heeft een vaste limiet van 3 partities die lager is dan de partities Hallo voor S3. Hallo ondergrens partitie is opgelegd omdat Hallo index aantal voor S3 HD aanzienlijk hoger is. Aangezien Servicelimieten bestaan voor beide computerbronnen (opgeslagen en verwerkt) en inhoud (indexen en documenten) Hallo inhoud limiet voor het eerst wordt bereikt.
