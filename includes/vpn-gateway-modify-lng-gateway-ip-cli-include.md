### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="d9e95-101">toomodify hello lokale netwerkgateway 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="d9e95-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="d9e95-102">Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d9e95-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="d9e95-103">IP-adres van Hallo gateway kan worden gewijzigd zonder te verwijderen van een bestaande VPN-gatewayverbinding (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="d9e95-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="d9e95-104">toomodify hello gateway IP-adres, vervangen Hallo waarden 'Site2' en 'TestRG1' door uw eigen met hello [az netwerk lokale gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="d9e95-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="d9e95-105">Controleer of Hallo IP-adres klopt in Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="d9e95-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```