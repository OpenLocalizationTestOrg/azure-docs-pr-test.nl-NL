Hallo taak produceert een JSON-uitvoer-bestand met metagegevens over gedetecteerde en bijgehouden. Hallo-metagegevens bevatten die wijzen op Hallo-locatie van vlakken, evenals een face ID nummer geeft Hallo bijhouden dat afzonderlijke coördinaten. Face-id-nummers zijn foutgevoelige tooreset omstandigheden wanneer Hallo voorzijde face verloren is gegaan of elkaar overlappen in Hallo-frame, waardoor bepaalde personen ophalen van meerdere id's toegewezen.

Hallo uitvoer dat JSON bevat Hallo volgende kenmerken:

| Element | Beschrijving |
| --- | --- |
| Versie |Dit verwijst toohello versie Hallo Video API. |
| Index | (Geldt alleen tooAzure Media Redactor) Hallo frame-index van de huidige gebeurtenis Hallo definieert. |
| Tijdschaal |'Maatstreepjes' per seconde van Hallo video. |
| offset |Dit is de tijdverschil Hallo voor tijdstempels. Versie 1.0 van Video-API's, zal dit altijd 0 zijn. In de toekomst scenario's die wordt ondersteund, deze waarde kan worden gewijzigd. |
| framesnelheid |Frames per seconde van Hallo video. |
| fragmenten |Hallo metagegevens is up chunked in verschillende segmenten fragmenten aangeroepen. Elke fragment bevat een start, duur, Intervalnummer en gebeurtenis(sen). |
| start |Hallo begintijd van de eerste gebeurtenis Hallo in 'maatstreepjes'. |
| Duur |Hallo-lengte van Hallo-fragment in 'maatstreepjes'. |
| interval |Hallo-interval van elke gebeurtenisvermelding binnen Hallo-fragment in 'maatstreepjes'. |
| events |Elke gebeurtenis bevat Hallo vlakken gedetecteerd en bijgehouden in die tijd. Het is een matrix van gebeurtenissen. Hallo buitenste matrix vertegenwoordigt een tijdsinterval. Hallo binnenste array bestaat uit 0 of meer gebeurtenissen die hebben plaatsgevonden op dat moment. Een leeg accolade [] betekent dat er geen vlakken zijn gedetecteerd. |
| id |Hallo-ID van Hallo gezicht dat wordt bijgehouden. Dit nummer mogelijk per ongeluk wijzigen als een gezicht niet gevonden wordt. Een bepaalde persoon moet dezelfde ID in de algemene video Hallo Hallo hebben, maar dit kan niet worden gegarandeerd vanwege toolimitations in Hallo detectie-algoritme (Occlusie, enz.) |
| x, y |Hallo linksboven X en Y-coördinaten van Hallo geconfronteerd selectiekader in een genormaliseerde schaal van 0,0 too1.0. <br/>-X en Y coördinaten zijn een relatieve toolandscape altijd, dus als u een portret video (of omlaag, in geval van iOS Hallo) hebt, u tootranspose Hallo coördinaten dienovereenkomstig hebt. |
| breedte, hoogte |Hallo breedte en hoogte van Hallo gezicht begrenzingsvak in een genormaliseerde schaal van 0,0 too1.0. |
| facesDetected |Dit is gevonden achter Hallo Hallo JSON-resultaten en bevat een overzicht van het aantal vlakken Hallo die gedetecteerd tijdens het Hallo video Hallo-algoritme. Omdat opnieuw per ongeluk Hallo id's kan worden ingesteld als een gezicht niet-gevonden wordt (bijvoorbeeld face gaat uitschakelen scherm ziet er verwijderd), Hallo true aantal vlakken in Hallo video mogelijk niet altijd gelijk aan dit nummer. |

