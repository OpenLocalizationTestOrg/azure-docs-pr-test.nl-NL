<span data-ttu-id="4282b-101">Voor het maken van een verbinding met een exemplaar van Azure Redis Cache, hebben de cache-clients de hostnaam, poorten en sleutels van de cache nodig.</span><span class="sxs-lookup"><span data-stu-id="4282b-101">To connect to an Azure Redis Cache instance, cache clients need the host name, ports, and keys of the cache.</span></span> <span data-ttu-id="4282b-102">Sommige clients gebruiken enigszins andere namen om naar deze items te verwijzen.</span><span class="sxs-lookup"><span data-stu-id="4282b-102">Some clients may refer to these items by slightly different names.</span></span> <span data-ttu-id="4282b-103">U kunt deze informatie ophalen in Azure Portal of met behulp van opdrachtregelprogramma's zoals Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4282b-103">You can retrieve this information in the Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-the-azure-portal"></a><span data-ttu-id="4282b-104">Hostnaam, poorten en toegangssleutels ophalen via Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4282b-104">Retrieve host name, ports, and access keys using the Azure Portal</span></span>
<span data-ttu-id="4282b-105">Als u de hostnaam, poorten en toegangssleutels wilt ophalen via Azure Portal, [bladert](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) u naar de cache in [Azure Portal](https://portal.azure.com) en klikt u op **Toegangssleutels** en **Eigenschappen** in het **menu Resource**.</span><span class="sxs-lookup"><span data-stu-id="4282b-105">To retrieve host name, ports, and access keys using the Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) to your cache in the [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in the **Resource menu**.</span></span> 

![Instellingen van Redis-cache](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="4282b-107">Hostnaam, poorten en toegangssleutels ophalen via Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4282b-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="4282b-108">Als u de hostnaam en poorten met Azure CLI 2.0 wilt ophalen, kunt u [az redis show](https://docs.microsoft.com/cli/azure/redis#show) oproepen. Als u de sleutels wilt ophalen, kunt u [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys) oproepen.</span><span class="sxs-lookup"><span data-stu-id="4282b-108">To retrieve the host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and to retrieve the keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="4282b-109">Het volgende script roept deze twee opdrachten aan en echoot de hostnaam, poorten en sleutels naar de console.</span><span class="sxs-lookup"><span data-stu-id="4282b-109">The following script calls these two commands and echos the hostname, ports, and keys to the console.</span></span>

```azurecli
#/bin/bash

# Retrieve the hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve the hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve the keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display the retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="4282b-110">Zie [Get the hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md) (De hostnaam, poorten en sleutels voor Azure Redis Cache ophalen) voor meer informatie over dit script.</span><span class="sxs-lookup"><span data-stu-id="4282b-110">For more information about this script, see [Get the hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="4282b-111">Zie [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Azure CLI 2.0 installeren) en [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Aan de slag met Azure CLI 2.0) voor meer informatie over Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4282b-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
