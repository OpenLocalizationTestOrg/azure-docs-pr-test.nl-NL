## <a name="create-a-ruby-application"></a>Een Ruby-toepassing maken
Zie voor instructies [een Ruby-toepassing maken op Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing tooUse Service Bus
Service Bus toouse downloaden en gebruiken van hello Azure Ruby, dit pakket bevat een set met gemak bibliotheken die met de REST opslagservices Hallo communiceren.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain Hallo pakket gebruiken
1. Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).
2. Typ 'gem installeren azure' hello opdracht venster tooinstall Hallo gem en afhankelijkheden.

### <a name="import-hello-package"></a>Hallo-pakket importeren
Hallo toohello bovenaan Hallo Ruby te volgen met uw favoriete teksteditor toevoegen bestand waarin u van plan toouse opslag bent:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Een Service Bus-verbinding instellen
Gebruik Hallo volgende code tooset Hallo waarden van de naam van het Hallo-naamruimte sleutel, key, ondertekenaar en host:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Hallo waarde toohello naamruimtewaarde die u hebt gemaakt in plaats van de volledige URL Hallo ingesteld. Bijvoorbeeld: **'yourexamplenamespace'**, niet 'yourexamplenamespace.servicebus.windows.net'.
