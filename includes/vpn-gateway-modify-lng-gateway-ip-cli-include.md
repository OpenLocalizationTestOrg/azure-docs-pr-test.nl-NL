### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>toomodify hello lokale netwerkgateway 'gatewayIpAddress'

Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen. IP-adres van Hallo gateway kan worden gewijzigd zonder te verwijderen van een bestaande VPN-gatewayverbinding (indien aanwezig). toomodify hello gateway IP-adres, vervangen Hallo waarden 'Site2' en 'TestRG1' door uw eigen met hello [az netwerk lokale gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) opdracht.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Controleer of Hallo IP-adres klopt in Hallo uitvoer:

```
"gatewayIpAddress": "23.99.222.170",
```