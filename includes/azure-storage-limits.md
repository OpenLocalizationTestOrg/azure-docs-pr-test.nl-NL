| Resource | Standaardlimiet |
| --- | --- |
| Aantal opslagaccounts per abonnement |200<sup>1</sup> |
| Maximum aantal opslagaccountcapaciteit |500 TB<sup>2</sup> |
| Maximumaantal blob-containers, blobs, bestandsshares, tabellen, wachtrijen, entiteiten of berichten per storage-account |Geen limiet |
| Maximale grootte van een enkele blob-container, een tabel of een wachtrij |Hetzelfde als de maximale opslagcapaciteit voor account |
| Maximaal aantal blokken in een blok-blob of toevoeg-blob |50,000 |
| Maximale grootte van een blok in een blok-blob |100 MB |
| Maximale grootte van een blok-blob |50.000 x 100 MB (ongeveer 4.75 TB) |
| Maximale grootte van een blok in een toevoeg-blob |4 MB |
| Maximale grootte van een toevoeg-blob |50.000 x 4 MB (ongeveer 195 GB) |
| Maximale grootte van een pagina-blob |8 TB |
| Maximale grootte van de Tabelentiteit van een |1 MB |
| Maximumaantal eigenschappen in een tabel-entiteit |252 |
| Maximale grootte van een bericht in een wachtrij |64 kB |
| Maximale grootte van een bestandsshare |5 TB |
| Maximale grootte van een bestand in een bestandsshare |1 TB |
| Maximumaantal bestanden in een bestandsshare |Alleen de limiet is Hallo 5 TB totale capaciteit van de bestandsshare Hallo |
| Maximale IOPS per share |1000 |
| Maximumaantal bestanden in een bestandsshare |Alleen de limiet is Hallo 5 TB totale capaciteit van de bestandsshare Hallo |
| Maximumaantal opgeslagen toegangsbeleid per container, bestandsshare, tabel of wachtrij |5 |
| Maximale snelheid van aanvragen voor per storage-account |BLOBs: 20.000 aanvragen per seconde<sup>2</sup> voor blobs van een geldige grootte (beperkt alleen door de limieten voor inkomend en uitgaand Hallo-account) <br />Bestanden: 1000 IOP's (8 KB groot) per bestandsshare <br />Wachtrijen: 20.000 berichten per seconde (berichtgrootte uitgaande 1 KB)<br />Tabellen: 20.000 transacties per seconde (uitgaande 1 KB entiteit grootte) |
| Doel-doorvoer voor één blob |Up too60 aanvragen MB per seconde of up too500 per seconde |
| Doel-doorvoer voor één wachtrij (1 KB berichten) |Too2000-berichten per seconde |
| Doel-doorvoer voor één tabel partitie (entiteiten 1 KB) |Up too2000 entiteiten per seconde |
| Doel-doorvoer voor één bestandsshare |Too60 MB per seconde |
| Maximale inkomende<sup>3</sup> per storage-account (ons regio's) |10 Gbps als GRS/ZRS<sup>4</sup> ingeschakeld, 20 Gbps voor LRS<sup>2</sup> |
| Maximum aantal uitgaande<sup>3</sup> per storage-account (ons regio's) |20 Gbps als RA-GRS/GRS/ZRS<sup>4</sup> ingeschakeld, 30 Gbps voor LRS<sup>2</sup> |
| Maximale inkomende<sup>3</sup> per storage-account (buiten de Verenigde Staten regio's) |5 Gbps als GRS/ZRS<sup>4</sup> ingeschakeld, 10 Gbps voor LRS<sup>2</sup> |
| Maximum aantal uitgaande<sup>3</sup> per storage-account (buiten de Verenigde Staten regio's) |10 Gbps als RA-GRS/GRS/ZRS<sup>4</sup> ingeschakeld, 15 Gbps voor LRS<sup>2</sup> |

<sup>1</sup>dit omvat zowel Standard en Premium storage-accounts. Als u meer dan 200 opslagaccounts nodig hebt, dient u een aanvraag in te dienen via de [ondersteuning van Azure](https://azure.microsoft.com/support/faq/). Hello Azure Storage-team uw bedrijfsscenario controleert en up too250 storage-accounts kan goedkeuren. 

<sup>2</sup> tooget uw standaardopslag accounts toogrow afgelopen Hallo aangekondigd limieten in de frequentie van capaciteit, inkomend en uitgaand en aanvraag, dient u een aanvraag via [ondersteuning van Azure](https://azure.microsoft.com/support/faq/). Hello Azure Storage team Hallo-aanvraag controleert en hogere limieten op basis van geval tot geval kan goedkeuren.

<sup>3</sup>*inkomend* verwijst tooall (aanvragen) verzonden gegevens tooa storage-account. *Uitgaande* verwijst tooall gegevens (antwoorden) ontvangen van een opslagaccount.  

<sup>4</sup>azure Storage-replicatieopties omvatten:
* **RA-GRS**: geografisch redundante opslag met leestoegang. Als RA-GRS is ingeschakeld, zijn uitgaande doelen voor de secundaire locatie Hallo identieke toothose voor Hallo primaire locatie.
* **GRS**: geografisch redundante opslag. 
* **ZRS**: Zone-redundante opslag. Alleen beschikbaar voor blok-blobs. 
* **LRS**: lokaal redundante opslag. 


