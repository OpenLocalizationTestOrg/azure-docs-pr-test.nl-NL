## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Een virtuele machine maken

Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht. 

Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* en SSH-sleutels gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel. toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. Let op Hallo `publicIpAddress`. Dit adres is gebruikte tooaccess Hallo VM.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>Poort 80 openen voor webverkeer 

Standaard worden alleen SSH-verbindingen zijn toegestaan in Linux VM's geïmplementeerd in Azure. Omdat deze virtuele machine toobe een webserver gaat, moet u tooopen poort 80 van Hallo internet. Gebruik Hallo [az vm open poort](/cli/azure/vm#open-port) opdracht tooopen Hallo gewenst poort.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>SSH in uw virtuele machine


Als u niet al weet Hallo openbare IP-adres van uw virtuele machine, Voer Hallo [az netwerk openbare ip-lijst](/cli/azure/network/public-ip#list) opdracht:


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine. Vervang Hallo juiste openbare IP-adres van uw virtuele machine. In dit voorbeeld Hallo IP-adres is *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

