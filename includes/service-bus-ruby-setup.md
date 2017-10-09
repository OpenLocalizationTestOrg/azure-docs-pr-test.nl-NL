## <a name="create-a-ruby-application"></a><span data-ttu-id="90aff-101">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="90aff-101">Create a Ruby application</span></span>
<span data-ttu-id="90aff-102">Zie voor instructies [een Ruby-toepassing maken op Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="90aff-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="90aff-103">Configureren van uw toepassing tooUse Service Bus</span><span class="sxs-lookup"><span data-stu-id="90aff-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="90aff-104">Service Bus toouse downloaden en gebruiken van hello Azure Ruby, dit pakket bevat een set met gemak bibliotheken die met de REST opslagservices Hallo communiceren.</span><span class="sxs-lookup"><span data-stu-id="90aff-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="90aff-105">RubyGems tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="90aff-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="90aff-106">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="90aff-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="90aff-107">Typ 'gem installeren azure' hello opdracht venster tooinstall Hallo gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="90aff-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="90aff-108">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="90aff-108">Import hello package</span></span>
<span data-ttu-id="90aff-109">Hallo toohello bovenaan Hallo Ruby te volgen met uw favoriete teksteditor toevoegen bestand waarin u van plan toouse opslag bent:</span><span class="sxs-lookup"><span data-stu-id="90aff-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="90aff-110">Een Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="90aff-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="90aff-111">Gebruik Hallo volgende code tooset Hallo waarden van de naam van het Hallo-naamruimte sleutel, key, ondertekenaar en host:</span><span class="sxs-lookup"><span data-stu-id="90aff-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="90aff-112">Hallo waarde toohello naamruimtewaarde die u hebt gemaakt in plaats van de volledige URL Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="90aff-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="90aff-113">Bijvoorbeeld: **'yourexamplenamespace'**, niet 'yourexamplenamespace.servicebus.windows.net'.</span><span class="sxs-lookup"><span data-stu-id="90aff-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
