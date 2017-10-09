## <a name="set-up-azure-cli-for-azure-dns"></a>Set up Azure CLI for Azure DNS (Azure CLI instellen voor Azure DNS)

### <a name="before-you-begin"></a>Voordat u begint

Controleer of u Hallo volgende items voordat u begint met de configuratie.

* Een Azure-abonnement. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).
* Installeer de nieuwste versie Hallo van hello Azure CLI, beschikbaar voor Windows, Linux of MAC. Meer informatie vindt u op [installeren hello Azure CLI](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Meld u aan tooyour Azure-account

Open een consolevenster en doorloop de verificatie met uw referenties. Zie voor meer informatie [aanmelden tooAzure van hello Azure CLI](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Naar de CLI-modus schakelen

Azure DNS maakt gebruik van Azure Resource Manager. Zorg ervoor dat u overschakelt van CLI-modus toouse Azure Resource Manager-opdrachten.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Hallo-abonnement selecteren

Controleer de abonnementen Hallo voor Hallo-account.

```azurecli
azure account list
```

Kies welke van uw Azure-abonnementen toouse.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Azure Resource Manager vereist dat er voor alle resourcegroepen een locatie wordt opgegeven. Dit wordt gebruikt als Hallo standaardlocatie voor resources in die resourcegroep. Echter, omdat alle DNS-resources globaal en niet regionaal zijn, heeft Hallo keuze van de locatie voor resourcegroep geen invloed op Azure DNS.

U kunt deze stap overslaan als u een bestaande resourcegroep gebruikt.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Resourceprovider registreren

Hello Azure DNS-service wordt beheerd door Hallo Microsoft.Network-resourceprovider. Uw Azure-abonnement moet geregistreerde toouse deze resourceprovider voordat u Azure DNS kunt gebruiken. Dit is een eenmalige bewerking voor elk abonnement.

```azurecli
azure provider register --namespace Microsoft.Network
```

