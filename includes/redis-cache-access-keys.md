<span data-ttu-id="06185-101">tooconnect tooan Azure Redis-Cache-exemplaar, cacheclients moeten Hallo hostnaam, poorten en sleutels van Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="06185-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="06185-102">Sommige clients mogelijk enigszins andere namen toothese items verwijzen.</span><span class="sxs-lookup"><span data-stu-id="06185-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="06185-103">U kunt deze informatie in hello Azure-portal of met behulp van de opdrachtregelprogramma's zoals Azure CLI kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="06185-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="06185-104">Ophalen van de hostnaam, poorten en toegangstoetsen hello Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="06185-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="06185-105">tooretrieve host name, poorten en toegangstoetsen hello Azure-Portal met [Bladeren](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in het Hallo [Azure-portal](https://portal.azure.com) en klik op **toegangssleutels** en  **Eigenschappen** in Hallo **Resource menu**.</span><span class="sxs-lookup"><span data-stu-id="06185-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Instellingen van Redis-cache](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="06185-107">Hostnaam, poorten en toegangssleutels ophalen via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="06185-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="06185-108">tooretrieve Hallo-hostnaam en poorten die met Azure CLI 2.0 kunt u bellen [az redis weergeven](https://docs.microsoft.com/cli/azure/redis#show), en u kunt aanroepen van tooretrieve Hallo sleutels [az redis lijst sleutels](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="06185-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="06185-109">Hallo volgende script roept deze twee opdrachten en het gebruik Hallo hostnaam, poorten en sleutels toohello console.</span><span class="sxs-lookup"><span data-stu-id="06185-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

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

<span data-ttu-id="06185-110">Zie voor meer informatie over dit script [Hallo hostnaam, poorten en sleutels voor Azure Redis-Cache ophalen](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="06185-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="06185-111">Zie [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Azure CLI 2.0 installeren) en [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Aan de slag met Azure CLI 2.0) voor meer informatie over Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="06185-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
