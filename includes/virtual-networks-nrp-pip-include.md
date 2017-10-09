## <a name="public-ip-address"></a>Openbaar IP-adres
Een openbare IP-adres resource biedt ofwel een gereserveerde of dynamische Internetgericht IP-adres. Hoewel u een openbaar IP-adres als zelfstandige object maken kunt, moet u tooassociate deze tooanother object tooactually Hallo-adres gebruiken. U kunt een openbare IP-adres tooa load balancer, toepassingsgateway of een NIC tooprovide toegang toothose internetbronnen koppelen.  

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **publicIPAllocationMethod** |Hiermee worden gedefinieerd als Hallo IP-adres *statische* of *dynamische*. |statisch, dynamische |
| **idleTimeoutInMinutes** |Hiermee definieert u Hallo niet-actieve time-out, met een standaardwaarde van vier minuten. Als er geen meer pakketten voor een bepaalde sessie binnen deze tijd wordt ontvangen, worden Hallo-sessie wordt beëindigd. |een waarde tussen 4 en 30 in |
| **IP-adres** |IP-adres toegewezen tooobject. Dit is een alleen-lezen eigenschap. |104.42.233.77 |

### <a name="dns-settings"></a>DNS-instellingen
Openbare IP-adressen hebben een onderliggend object met de naam **dnsSettings** met Hallo volgende eigenschappen:

| Eigenschap | Beschrijving | Voorbeeldwaarden |
| --- | --- | --- |
| **domainNameLabel** |Host met de naam gebruikt voor naamomzetting. |www-, ftp, vm1 |
| **FQDN-naam** |Volledig gekwalificeerde naam voor Hallo openbare IP-adres. |www.westus.cloudapp.Azure.com |
| **reverseFqdn** |FQDN-naam die wordt omgezet toohello IP-adres en is geregistreerd in DNS als een PTR-record. |www.contoso.com. |

Voorbeeld openbare IP-adres in JSON-indeling:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Aanvullende bronnen
* Vindt u meer informatie over [openbare IP-adressen](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Meer informatie over [exemplaar niveau openbare IP-adressen](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163638.aspx) voor de openbare IP-adressen.

