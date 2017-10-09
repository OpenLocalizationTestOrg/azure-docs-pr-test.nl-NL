### <a name="tooview-local-network-gateways"></a>de lokale netwerkgateways tooview

een lijst met Hallo netwerkgateways, gebruik Hallo tooview [lijst met de lokale gateway van de az netwerken](https://docs.microsoft.com/cli/azure/network/local-gateway#list) opdracht.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>tooverify hello sleutelwaarden gedeeld

Controleer of Hallo gedeeld sleutelwaarde Hallo dezelfde waarde die u voor de configuratie van uw VPN-apparaat gebruikt. Als dit niet het geval is, Hallo verbinding opnieuw met de waarde op Hallo van Hallo apparaat worden uitgevoerd of Hallo-apparaat bijwerken Hallo waarde uit Hallo retourneren. Hallo-waarden moeten overeenkomen. Hallo tooview gedeelde sleutel, gebruik Hallo [az netwerk vpn-verbinding-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>tooview hello VPN-gateway openbare IP-adres

toofind hello openbare IP-adres van uw virtuele netwerkgateway, gebruik Hallo [az netwerk openbare ip-lijst](https://docs.microsoft.com/cli/azure/network/public-ip#list) opdracht. Hallo-uitvoer voor dit voorbeeld is gemakkelijk te lezen, opgemaakte toodisplay Hallo lijst met openbare IP-adressen in tabelindeling.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
