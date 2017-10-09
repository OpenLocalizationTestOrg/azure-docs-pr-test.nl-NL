### <a name="tooview-local-network-gateways"></a><span data-ttu-id="d5ca7-101">de lokale netwerkgateways tooview</span><span class="sxs-lookup"><span data-stu-id="d5ca7-101">tooview local network gateways</span></span>

<span data-ttu-id="d5ca7-102">een lijst met Hallo netwerkgateways, gebruik Hallo tooview [lijst met de lokale gateway van de az netwerken](https://docs.microsoft.com/cli/azure/network/local-gateway#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d5ca7-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="d5ca7-103">tooverify hello sleutelwaarden gedeeld</span><span class="sxs-lookup"><span data-stu-id="d5ca7-103">tooverify hello shared key values</span></span>

<span data-ttu-id="d5ca7-104">Controleer of Hallo gedeeld sleutelwaarde Hallo dezelfde waarde die u voor de configuratie van uw VPN-apparaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5ca7-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="d5ca7-105">Als dit niet het geval is, Hallo verbinding opnieuw met de waarde op Hallo van Hallo apparaat worden uitgevoerd of Hallo-apparaat bijwerken Hallo waarde uit Hallo retourneren.</span><span class="sxs-lookup"><span data-stu-id="d5ca7-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="d5ca7-106">Hallo-waarden moeten overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="d5ca7-106">hello values must match.</span></span> <span data-ttu-id="d5ca7-107">Hallo tooview gedeelde sleutel, gebruik Hallo [az netwerk vpn-verbinding-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="d5ca7-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="d5ca7-108">tooview hello VPN-gateway openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="d5ca7-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="d5ca7-109">toofind hello openbare IP-adres van uw virtuele netwerkgateway, gebruik Hallo [az netwerk openbare ip-lijst](https://docs.microsoft.com/cli/azure/network/public-ip#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d5ca7-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="d5ca7-110">Hallo-uitvoer voor dit voorbeeld is gemakkelijk te lezen, opgemaakte toodisplay Hallo lijst met openbare IP-adressen in tabelindeling.</span><span class="sxs-lookup"><span data-stu-id="d5ca7-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
