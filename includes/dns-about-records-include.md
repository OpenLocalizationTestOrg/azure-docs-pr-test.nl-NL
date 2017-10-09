### <a name="record-names"></a>Recordnamen

In Azure DNS worden records opgegeven met behulp van relatieve namen. Een *volledig gekwalificeerd* domeinnaam (FQDN) bevat Hallo zonenaam, terwijl een *relatieve* heeft geen naam. Bijvoorbeeld, biedt Hallo relatieve record naam 'www' hello zone 'contoso.com' hello volledig gekwalificeerde naam 'www.contoso.com'.

Een *apex* record is een DNS-record in de hoofdmap van de hello (of *apex*) van een DNS-zone. Bijvoorbeeld in Hallo DNS-zone 'contoso.com' een record apex heeft ook Hallo volledig gekwalificeerde naam 'contoso.com' (dit is wel een *Open* domein).  Volgens de conventies Hallo relatieve naam ' @' gebruikte toorepresent apex records is.

### <a name="record-types"></a>Recordtypen

Elke DNS-record heeft een naam en een type. Records zijn ingedeeld in verschillende typen volgens toohello gegevens die ze bevatten. Hallo meest voorkomende type is een 'A'-record, waarmee een naam tooan IPv4-adres wordt toegewezen. Een andere voorkomende type is een 'MX'-record, waarmee een naam tooa e-mailserver wordt toegewezen.

Azure DNS ondersteunt alle algemene DNS-recordtypen: A, AAAA, CNAME MX, NS, PTR, SOA, SRV en TXT. Houd er rekening mee dat [SPF-records worden gerepresenteerd door TXT-records](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>Recordsets

Soms moet u toocreate meer dan één DNS-record met een bepaalde naam en type. Stel bijvoorbeeld dat Hallo 'www.contoso.com'-website wordt gehost op twee verschillende IP-adressen. Hallo website vereist twee verschillende A-records, één voor elk IP-adres. Dit is een voorbeeld van een recordset:

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

Azure DNS beheert alle DNS-records met *recordsets*. Een recordset (ook wel bekend als een *resource* Recordset) is een verzameling van DNS-records in een zone waarvoor Hallo dezelfde naam en van het Hallo Hallo hetzelfde type. De meeste recordsets bevatten één record. Voorbeelden zoals Hallo hierboven, wordt echter in die een recordset bevat meer dan een record, zijn niet ongewoon.

Bijvoorbeeld, Stel dat u een A-record 'www' al hebt gemaakt in de zone Hallo 'contoso.com', '134.170.185.46' (Hallo eerste record hierboven) wijzen toohello IP adres.  toocreate Hallo tweede record u wilt toevoegen die record toohello bestaande record ingesteld plaats van een extra recordset maken.

Hallo SOA- en CNAME-recordtypen zijn uitzonderingen. Hallo DNS-standaarden niet toe dat meerdere records met dezelfde naam voor deze typen hello, deze recordsets kunnen daarom alleen bevatten één record.
