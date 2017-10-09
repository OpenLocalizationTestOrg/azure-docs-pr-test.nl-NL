### <a name="noconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - er is geen gatewayverbinding

Als u geen gatewayverbinding hebt en u wilt dat tooadd of IP-adresvoorvoegsels verwijderen, gebruikt u Hallo dezelfde opdracht dat u toocreate Hallo lokale netwerkgateway, [az local-netwerkgateway maken](https://docs.microsoft.com/cli/azure/network/local-gateway#create). U kunt deze opdracht tooupdate Hallo gateway IP-adres ook gebruiken voor Hallo VPN-apparaat. huidige instellingen voor toooverwrite hello, gebruik Hallo bestaande naam van uw lokale netwerkgateway. Als u een andere naam gebruikt, kunt u een nieuwe lokale netwerkgateway maken, in plaats van het overschrijven van Hallo bestaande.

Telkens wanneer u een wijziging, Hallo volledige lijst met voorvoegsels moet worden opgegeven, niet alleen Hallo-prefixes die u wilt toochange. Geef alleen Hallo voorvoegsels die u tookeep wilt. In dit geval 10.0.0.0/24 en 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - gatewayverbinding bestaande

Als u een gatewayverbinding hebt en tooadd wilt of IP-adresvoorvoegsels verwijdert, kunt u Hallo voorvoegsels met bijwerken [az netwerk lokale gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Dit veroorzaakt enige downtime in uw VPN-verbinding. Wanneer Hallo IP-adres wijzigen-prefixes, hoeft u geen toodelete Hallo VPN-gateway.

Telkens wanneer u een wijziging, Hallo volledige lijst met voorvoegsels moet worden opgegeven, niet alleen Hallo-prefixes die u wilt toochange. In dit voorbeeld zijn 10.0.0.0/24 en 20.0.0.0/24 al aanwezig. We Hallo voorvoegsels 30.0.0.0/24 en 40.0.0.0/24 toevoegen en alle 4 van Hallo voorvoegsels opgeven bij het bijwerken.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```