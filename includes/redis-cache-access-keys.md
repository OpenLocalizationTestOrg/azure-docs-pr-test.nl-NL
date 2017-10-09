tooconnect tooan Azure Redis-Cache-exemplaar, cacheclients moeten Hallo hostnaam, poorten en sleutels van Hallo-cache. Sommige clients mogelijk enigszins andere namen toothese items verwijzen. U kunt deze informatie in hello Azure-portal of met behulp van de opdrachtregelprogramma's zoals Azure CLI kunt ophalen.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Ophalen van de hostnaam, poorten en toegangstoetsen hello Azure Portal gebruiken
tooretrieve host name, poorten en toegangstoetsen hello Azure-Portal met [Bladeren](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in het Hallo [Azure-portal](https://portal.azure.com) en klik op **toegangssleutels** en  **Eigenschappen** in Hallo **Resource menu**. 

![Instellingen van Redis-cache](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Hostnaam, poorten en toegangssleutels ophalen via Azure CLI
tooretrieve Hallo-hostnaam en poorten die met Azure CLI 2.0 kunt u bellen [az redis weergeven](https://docs.microsoft.com/cli/azure/redis#show), en u kunt aanroepen van tooretrieve Hallo sleutels [az redis lijst sleutels](https://docs.microsoft.com/cli/azure/redis#list-keys). Hallo volgende script roept deze twee opdrachten en het gebruik Hallo hostnaam, poorten en sleutels toohello console.

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

Zie voor meer informatie over dit script [Hallo hostnaam, poorten en sleutels voor Azure Redis-Cache ophalen](../articles/redis-cache/scripts/cache-keys-ports.md). Zie [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Azure CLI 2.0 installeren) en [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Aan de slag met Azure CLI 2.0) voor meer informatie over Azure CLI 2.0.
