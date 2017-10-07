---
title: aaaAzure virtuele-machineschaalsets Veelgestelde vragen | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over virtuele-machineschaalsets ophalen.
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Azure virtuele-machineschaalsets Veelgestelde vragen

Vind antwoorden op veelgestelde vragen over virtuele-machineschaalset toofrequently Hiermee stelt u in Azure.

## <a name="autoscale"></a>Automatisch schalen

### <a name="what-are-best-practices-for-azure-autoscale"></a>Wat zijn de aanbevolen procedures voor het Azure-automatisch schalen?

Zie voor aanbevolen procedures voor automatisch schalen [aanbevolen procedures voor automatisch schalen virtuele machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Waar vind ik metrische namen voor automatisch schalen die gebruikmaakt van de host gebaseerde metrische gegevens

Zie voor namen van meetwaarde voor automatisch schalen die gebruikmaakt van de host gebaseerde metrische gegevens [ondersteund met een Azure-Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Zijn er geen voorbeelden van automatisch schalen op basis van een Azure Service Bus-onderwerp en wachtrij-lengte?

Ja. Zie voor voorbeelden van automatisch schalen op basis van een Azure Service Bus-onderwerp en wachtrij-lengte [Azure Monitor automatisch schalen algemene metrische gegevens](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Gebruik voor een Service Bus-wachtrij Hallo JSON te volgen:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Gebruik voor een opslagwachtrij Hallo JSON te volgen:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Van de voorbeeldwaarden vervangt door uw resource Uniform Resource-id's (URI).


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Moet ik automatisch schalen met behulp van metrische gegevens op de host of een extensie voor diagnostische gegevens?

Op een VM toouse hostniveau metrische gegevens of Gast OS gebaseerde metrische gegevens kunt u een instelling voor automatisch schalen.

Zie voor een lijst van ondersteunde metrische gegevens [Azure Monitor automatisch schalen algemene metrische gegevens](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Zie voor een volledige voorbeeld voor virtuele-machineschaalsets [geavanceerde automatisch schalen configureren met behulp van Resource Manager-sjablonen voor virtuele-machineschaalsets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

Hallo-voorbeeld gebruikt Hallo hostniveau CPU metriek en een aantal bericht metriek.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Hoe stel waarschuwingsregels op een virtuele-machineschaalset?

U kunt waarschuwingen maken op de metrische gegevens voor de virtuele-machineschaalsets via PowerShell of Azure CLI. Zie voor meer informatie [Azure Monitor PowerShell snel starten voorbeelden](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) en [Azure Monitor platformoverschrijdende CLI snel starten voorbeelden](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Hallo TargetResourceId van Hallo virtuele-machineschaalset ziet er als volgt: 

/Subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.COMPUTE/virtualMachineScaleSets/yourvmssname

Kunt u een VM-prestatiemeteritem als Hallo metrische tooset een waarschuwing voor. Zie voor meer informatie [Gastbesturingssysteem metrische gegevens voor VM's van Windows Resource Manager gebaseerde](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) en [Gastbesturingssysteem metrische gegevens voor virtuele Linux-machines](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in Hallo [Azure Monitor automatisch schalen algemene metrische gegevens](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artikel.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Hoe stel ik automatisch schalen op een virtuele-machineschaalset ingesteld met behulp van PowerShell

tooset up automatisch schalen op een virtuele-machineschaalset ingesteld met behulp van PowerShell, Zie Hallo blogbericht [hoe tooadd automatisch schalen tooan schaal van de virtuele machine van Azure instelt](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificaten

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Hoe ik een certificaat toohello VM veilig verzenden? Hoe ik inrichten met een virtuele machine scale set toorun een website waar hello SSL voor Hallo website wordt verzonden veilig vanuit de configuratie van een certificaat? (Hallo algemene rotatie certificaatbewerking zou worden bijna Hallo hetzelfde als de bewerking configuratie bijwerken.) Hebt u een voorbeeld van hoe toodo dit? 

toosecurely een certificaat toohello VM verzenden, kunt u een klant-certificaat installeren rechtstreeks in een Windows-certificaatarchief van de sleutelkluis van de klant Hallo.

Hallo JSON volgende gebruiken:

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

Hallo code biedt ondersteuning voor Windows en Linux.

Zie voor meer informatie [maken of bijwerken een virtuele-machineschaalset](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Voorbeeld van een zelfondertekend certificaat

1.  Een zelfondertekend certificaat maken in een sleutelkluis.

    Hallo volgende PowerShell-opdrachten gebruiken:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Deze opdracht kunt u Hallo invoer voor hello Azure Resource Manager-sjabloon.

    Voor een voorbeeld van hoe toocreate een zelfondertekend certificaat in een sleutelkluis zien [scenario's voor beveiliging van Service Fabric-cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Hallo Resource Manager-sjabloon wijzigen.

    Deze eigenschap te toevoegen**virtualMachineProfile**, als onderdeel van Hallo stelt de virtuele-machineschaalset resource:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Kan ik een SSH-sleutelpaar toouse voor SSH-verificatie opgeven met een Linux-virtuele machine schaal van Resource Manager-sjabloon instellen?  

Ja. Hallo REST-API voor **osProfile** is vergelijkbaar toohello standard VM REST-API. 

Omvatten **osProfile** in uw sjabloon:

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
Dit blok JSON wordt gebruikt in [Hallo 101-vm-SSH-sleutelbestand GitHub snel starten sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Hallo besturingssysteemprofiel wordt ook gebruikt bij [hello grelayhost.json GitHub quick start sjabloon](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Zie voor meer informatie [maken of bijwerken een virtuele-machineschaalset](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Hoe kan ik afgeschaft certificaten verwijderen? 

tooremove afgeschaft verwijderen Hallo Oud certificaat van de lijst van certificaten kluis Hallo-certificaten. Alle Hallo certificaten dat u op uw computer in de lijst Hallo tooremain wilt laten. Hallo-certificaat wordt niet verwijderd uit alle virtuele machines. Deze ook voegt geen Hallo certificaat toonew virtuele machines die zijn gemaakt in Hallo virtuele-machineschaalset. 

tooremove hello certificaat van de bestaande virtuele machines, een aangepast script schrijven extensie toomanually verwijderen Hallo certificaten uit het certificaatarchief.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Hoe ik een bestaande openbare SSH-sleutel invoeren in Hallo virtuele machine scale set SSH-laag tijdens het inrichten? Ik toostore Hallo SSH openbare sleutelwaarden in Azure Sleutelkluis wilt en deze vervolgens in mijn Resource Manager-sjabloon gebruiken.

Als u virtuele machines Hallo alleen met een openbare SSH-sleutel biedt, hoeft u geen tooput Hallo openbare sleutels in de Sleutelkluis. Openbare sleutels zijn niet geheim.
 
Wanneer u een Linux-VM maakt, kunt u openbare SSH-sleutels als tekst zonder opmaak bieden:

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
linuxConfiguration elementnaam | Vereist | Type | Beschrijving
--- | --- | --- | --- |  ---
SSH | Nee | Verzameling | Hiermee geeft u op Hallo SSH-sleutel configuratie voor een Linux-besturingssysteem
Pad | Ja | Tekenreeks | Hiermee geeft u Hallo Linux-bestandspad waar Hallo SSH-sleutels of het certificaat moet zich bevinden
keyData | Ja | Tekenreeks | Hiermee geeft u een base64-gecodeerd openbare SSH-sleutel

Zie voor een voorbeeld [Hallo 101-vm-SSH-sleutelbestand GitHub snel starten sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Wanneer ik uitvoeren `Update-AzureRmVmss` na het toevoegen van meer dan één certificaat uit Hallo sleutel kluis, zie ik Hallo volgende weergegeven:
 
>Update-AzureRmVmss: Lijst geheim bevat herhaalde exemplaren van /subscriptions/ < Mijn-abonnement-id > / resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev die niet is toegestaan.
 
Dit kan gebeuren als u toore probeert-Hallo dezelfde kluis in plaats van een nieuw certificaat voor de kluis voor bestaande bronkluis Hallo toevoegen. Hallo `Add-AzureRmVmssSecret` opdracht werkt niet goed als u extra geheimen toevoegt.
 
tooadd meer geheimen van Hallo dezelfde sleutelkluis, update Hallo $vmss.properties.osProfile.secrets[0].vaultCertificates lijst.
 
Zie voor Hallo invoerstructuur verwacht, [maken of bijwerken wordt ingesteld door een virtuele machine](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Hallo-geheim niet vinden in Hallo virtuele machine scale set object dat zich in de sleutelkluis Hallo. Vervolgens voegt u uw verwijzing (Hallo-URL en de naam van de geheime store Hallo) toohello lijst met certificaten die zijn gekoppeld aan het Hallo-kluis.

> [!NOTE] 
> U verwijderen niet op dit moment certificaten uit de virtuele machines met behulp van Hallo virtuele machine scale set API.
>

Nieuwe virtuele machines geen Hallo oude certificaat. Virtuele machines die Hallo certificaat hebben en die al zijn geïmplementeerd hebben echter Hallo oude certificaat.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Kan ik push certificaten toohello virtuele-machineschaalset instellen zonder Hallo-wachtwoord als Hallo certificaat in Hallo geheime store?

U hoeft niet toohard code wachtwoorden in scripts. U kunt dynamisch ophalen van wachtwoorden met Hallo machtigingen u toorun Hallo-implementatiescript gebruiken. Als u een script dat een certificaat van Hallo geheime store sleutelkluis verplaatst hebt, Hallo geheime store `get certificate` opdracht levert ook wachtwoord op Hallo van Hallo pfx-bestand.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Hoe Hallo geheimen eigenschap van virtualMachineProfile.osProfile voor een virtuele-machineschaalset werk instellen? Waarom moet ik Hallo sourceVault waarde wanneer ik heb toospecify absolute URI voor een certificaat met behulp van Hallo certificateUrl eigenschap Hallo? 

Een verwijzing van Windows Remote Management (WinRM)-certificaat moet aanwezig zijn in Hallo geheimen-eigenschap van het Hallo-besturingssysteemprofiel. 

Hallo doel Hallo bronkluis aangegeven is tooenforce toegangsbeheerlijst (ACL) toegangscontrolebeleid die aanwezig zijn in Azure Cloud Service-model van een gebruiker. Als Hallo bronkluis is niet opgegeven, worden gebruikers die u geen machtigingen voor toegang tot of toodeploy geheimen tooa sleutelkluis hebt kunnen toothrough Compute Resource Provider (CRP). ACL's bestaan zelfs voor bronnen die niet bestaan.

Als u een onjuiste bron kluis-ID, maar een geldige sleutelkluis-URL opgeeft, wordt er een fout gerapporteerd bij het pollen van Hallo-bewerking.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Als ik geheimen tooan bestaande virtuele-machineschaalset toevoegt, worden geheimen Hallo ingevoegd in de bestaande virtuele machines, of alleen nieuwe? 

Certificaten worden toegevoegd tooall uw virtuele machines, zelfs al bestaande elementen zijn. Als u uw virtuele-machineschaalset upgradePolicy eigenschap ingesteld te**handmatige**, Hallo certificaat toohello VM wordt toegevoegd wanneer u een handmatige update op Hallo VM uitvoeren.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Waar ik certificaten plaatsen voor virtuele Linux-machines?

hoe toodeploy certificaten voor Linux VM's, Zie toolearn [tooVMs certificaten van een door de klant beheerd sleutelkluis implementeren](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Hoe kan ik een nieuwe kluis certificaat tooa nieuw certificaatobject toevoegen

tooadd een kluis certificaat tooan bestaande geheim, Zie Hallo PowerShell-voorbeeld te volgen. Gebruik slechts één geheime object.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Wat gebeurt er toocertificates als installatiekopie van een virtuele machine?

Als u een virtuele machine installatiekopie, worden certificaten verwijderd. Verwijderingen Hallo gehele besturingssysteemschijf teruggezet. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Wat gebeurt er als u een certificaat uit de sleutelkluis Hallo verwijderen?

Als Hallo geheim wordt verwijderd uit de sleutelkluis hello en u voert `stop deallocate` voor alle VM's en start deze opnieuw, wordt er een fout optreedt. Hallo-fout treedt op omdat Hallo CRP tooretrieve Hallo geheimen van de sleutelkluis hello heeft, maar niet kunnen worden. In dit scenario kunt u certificaten Hallo verwijderen uit Hallo virtuele machine scale set model. 

Hallo CRP onderdeel geheimen van de klant niet bewaard is gebleven. Als u `stop deallocate` voor alle virtuele machines in Hallo virtuele-machineschaalset, Hallo-cache wordt verwijderd. In dit scenario worden geheimen opgehaald uit de sleutelkluis Hallo.

U kunt dit probleem niet tegenkomen wanneer uitbreiden, omdat er een cachekopie van Hallo geheim in Azure Service Fabric (in Hallo één fabric tenant model).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Waarom hebt toospecify Hallo exacte locatie voor Hallo certificaat-URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), zoals aangegeven in [scenario's voor beveiliging van Service Fabric-cluster](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Hello Azure Key Vault documentatie wordt aangegeven dat Hallo die geheim REST-API ophalen Hallo meest recente versie van Hallo geheim retourneren moet als Hallo-versie is niet opgegeven.
 
Methode | URL
--- | ---
TOEVOEGEN | https://mykeyvault.Vault.Azure.NET/secrets/ {geheim name} / {geheim versie}? api-version = {api-versie}

Vervang {*geheim naam*} met de naam van de Hallo en vervangen {*geheim versie*} met Hallo-versie van Hallo geheim gewenste tooretrieve. Hallo geheime versie kan worden uitgesloten. In dat geval wordt wordt de huidige versie hello opgehaald.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Waarom heb ik toospecify Hallo certificaatversie bij het gebruik van Sleutelkluis?

Hallo-doel van Hallo Sleutelkluis vereiste toospecify Hallo certificaatversie is toomake het toohello gebruiker wissen welk certificaat wordt geïmplementeerd op hun virtuele machines.

Als u een virtuele machine maken en werk vervolgens het geheim in de sleutelkluis hello, wordt Hallo nieuwe certificaat is niet gedownload tooyour virtuele machines. Maar uw virtuele machines worden weergegeven en nieuwe virtuele machines ophalen van het nieuwe geheim Hallo tooreference. tooavoid, bent u vereiste tooreference een geheime versie.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Mijn team werkt met verschillende certificaten die worden gedistribueerd toous als cer openbare sleutels. Wat is de aanbevolen aanpak voor het implementeren van deze certificaten tooa virtuele-machineschaalset Hallo?

toodeploy .cer openbare sleutels tooa virtuele-machineschaalset, kunt u een .pfx-bestand met CER-bestanden genereren. toodo dit, gebruik `X509ContentType = Pfx`. Bijvoorbeeld Hallo cer-bestand laden als een object x509Certificate2 in C# of PowerShell en vervolgens Hallo-methode aanroepen. 

Zie voor meer informatie [X509Certificate.Export methode (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Ik zie een optie om gebruikers toopass in certificaten niet als base64-tekenreeksen. De meeste andere resourceproviders hebt deze optie.

tooemulate doorgeven in een certificaat als een base64-tekenreeks kan u Hallo laatste samengestelde URL in het Resource Manager-sjabloon extraheren. Hallo JSON-eigenschap in de Resource Manager-sjabloon volgende omvatten:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>Heb ik toowrap certificaten in JSON-objecten in sleutelkluizen?

In de virtuele-machineschaalsets en virtuele machines moeten certificaten worden verpakt in JSON-objecten. 

We bieden ook ondersteuning Hallo inhoudstype application/x-pkcs12. Zie voor instructies over het gebruik van de x-toepassing-pkcs12 [PFX-certificaten in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
We ondersteunen momenteel geen cer-bestanden. toouse .cer-bestanden, exporteert u ze in pfx-containers.



## <a name="compliance"></a>Naleving

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Zijn de virtuele-machineschaalsets PCI-compatibel?

Virtuele-machineschaalsets zijn een thin API-laag bovenop Hallo CRP. Beide onderdelen maken deel uit van Hallo compute-platform in hello Azure service-structuur.

Virtuele-machineschaalsets zijn vanuit het oogpunt van naleving van een fundamenteel onderdeel van hello Azure compute-platform. Ze delen een team, hulpprogramma's, processen, implementatiemethode, beveiligingsmechanismen, just in time (Just in time) compilatie, bewaking, waarschuwingen, enzovoort, met Hallo CRP zelf. Virtuele-machineschaalsets zijn Payment Card Industry (PCI)-compatibele omdat Hallo CRP deel uitmaakt van het huidige PCI Data Security Standard (DSS) attestation Hallo.

Zie voor meer informatie [Microsoft Trust Center Hallo](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Extensies

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Hoe verwijder ik een virtuele machine uitbreiding van de schaal

een virtuele-machineschaalset toodelete instellen-uitbreiding, gebruik Hallo volgende PowerShell-voorbeeld:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
U vindt Hallo Extensienaam waarde in `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Er is dat een virtuele-machineschaalset voorbeeldsjabloon die met Operations Management Suite integreert?

Zie voor een virtuele-machineschaalset ingesteld voorbeeld van de sjabloon die in combinatie met Operations Management Suite, Hallo tweede voorbeeld in [een Azure Service Fabric-cluster implementeren en schakel de bewaking met behulp van logboekanalyse](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Extensies lijken toorun parallel op virtuele-machineschaalsets. Dit zorgt ervoor dat mijn toofail aangepast script-extensie. Wat kan ik doen toofix dit?

toolearn over sequentiëren uitbreiding in virtuele-machineschaalsets, Zie [sequentiëren uitbreiding in virtuele Azure-machine-schaalsets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Hoe stel ik Hallo wachtwoord voor virtuele machines in mijn virtuele-machineschaalset

tooreset hello wachtwoord voor virtuele machines in uw virtuele-machineschaalset instellen, gebruikt u uitbreidingen voor toegang tot VM. 

Gebruik Hallo PowerShell-voorbeeld te volgen:

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Hoe kan ik een extensie tooall VM's in mijn virtuele-machineschaalset toevoegen

Als updatebeleid te is ingesteld**automatische**, Hallo-sjabloon opnieuw te implementeren met eigenschappen van nieuwe extensie Hallo updates alle virtuele machines.

Als updatebeleid te is ingesteld**handmatige**werk eerst Hallo-extensie en alle exemplaren in uw virtuele machines vervolgens handmatig bijwerken.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Als het Hallo-extensies die zijn gekoppeld aan een bestaande virtuele-machineschaalset zijn bijgewerkt, zijn de bestaande virtuele machines die van invloed op een? (Dat wil zeggen, virtuele machines wordt Hallo *niet* overeen Hallo virtuele machine scale set model?) Of worden ze genegeerd? Wanneer een bestaande virtuele machine is service moeten worden hersteld of worden hersteld met een installatiekopie, Hallo-scripts die momenteel zijn geconfigureerd op Hallo virtuele-machineschaalset uitgevoerd, of worden Hallo-scripts die zijn geconfigureerd als Hallo die VM voor het eerst werd gemaakt gebruikt?

Als Hallo uitbreidingsdefinitie in het virtuele-machineschaalset Hallo ingesteld model wordt bijgewerkt en Hallo upgradePolicy eigenschap is ingesteld op te**automatische**, Hallo VM's worden bijgewerkt. Als Hallo upgradePolicy eigenschap is ingesteld, te**handmatige**, extensies zijn gemarkeerd als niet overeenkomt met Hallo-model. 

Als een bestaande VM-service moeten worden hersteld, wordt deze weergegeven als een herstart en Hallo-extensies worden niet opnieuw uitgevoerd. Als deze wordt teruggezet, is het zoals Hallo OS station vervangen door de broninstallatiekopie Hallo. Alle specialisatie uit de meest recente model hello, zoals-extensies worden uitgevoerd.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Hoe ik deelnemen aan een virtuele machine scale set tooan Azure AD-domein?

toojoin een virtuele machine scale set tooan Azure Active Directory (Azure AD)-domein, kunt u een uitbreiding definiëren. 

een uitbreiding toodefine gebruikt Hallo JsonADDomainExtension eigenschap:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>De extensie scale set van mijn virtuele machine probeert tooinstall iets dat moet worden opgestart. Bijvoorbeeld 'commandToExecute': ' powershell.exe - ExecutionPolicy Unrestricted Install-WindowsFeature – naam FS-Resource-Manager – IncludeManagementTools '

Als uw scale set-extensie van virtuele machine tooinstall iets dat moet worden opgestart probeert, kunt u hello Azure Automation Desired State Configuration (DSC Automation)-extensie. Als Hallo besturingssysteem Windows Server 2012 R2, wordt Azure ophaalt in Hallo Windows Management Framework (WMF) 5.0 setup opnieuw is opgestart, en vervolgens verder met de Hallo-configuratie. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Hoe kan ik antimalware inschakelen in mijn virtuele-machineschaalset?

tooturn op anti-malware op uw virtuele-machineschaalset instellen, gebruikt u Hallo PowerShell-voorbeeld te volgen:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Ik heb nodig tooexecute een aangepast script dat wordt gehost in een persoonlijke storage-account. Hallo-script met succes wordt uitgevoerd wanneer Hallo opslag openbaar is, maar wanneer ik probeer toouse Shared Access Signature (SAS), is mislukt. Dit bericht wordt weergegeven: 'Verplichte parameters ontbreekt voor geldige Shared Access Signature'. Koppeling + SAS werkt prima vanuit Mijn lokale browser.

een aangepast script dat wordt gehost in een persoonlijke opslagaccount tooexecute beveiligde instellingen met de Hallo opslagaccountsleutel en de naam instellen. Zie voor meer informatie [aangepast Script uitbreiding voor Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Netwerken
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>Is het mogelijk tooassign een Netwerkbeveiligingsgroep (NSG) tooa schaal instellen, zodat de tooall Hallo VM NIC's in de verzameling hello wordt toegepast?

Ja. Een Netwerkbeveiligingsgroep kunnen direct tooa schaalset door ernaar wordt verwezen in Hallo networkInterfaceConfigurations sectie Hallo netwerkprofiel worden aangebracht. Voorbeeld:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Hoe kan ik dat doen geen VIP's wisselen voor virtuele-machineschaalsets in Hallo dezelfde abonnement en dezelfde regio?

Als er twee virtuele-machineschaalsets met de front-ends van Azure Load Balancer en ze zich in hetzelfde abonnement en dezelfde regio Hallo, kan u Hallo openbare IP-adressen van elkaar ongedaan en toohello andere toewijzen. Zie [VIP's wisselen: blauw groen implementatie in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) bijvoorbeeld. Dit betekent dat er een vertraging al als Hallo resources worden weergegeven ongedaan/toegewezen op Hallo niveau. Een optie voor snellere is toouse Azure Application Gateway met twee back-endpools en een regel voor doorsturen. U kunt ook u uw toepassing met kan host [-Azure App service](https://azure.microsoft.com/en-us/services/app-service/) die ondersteuning biedt voor het snel overschakelen tussen sites omwisselen fasering en productie.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Hoe geef ik een bereik van particuliere IP-adressen toouse voor statische privé IP-adrestoewijzing

IP-adressen zijn geselecteerd uit een subnet op dat u opgeeft. 

Hallo toewijzingsmethode van virtuele machine scale set IP-adressen is altijd 'dynamische' hoeft niet, maar dat dat deze IP-adressen kunnen wijzigen. In dit geval betekent 'dynamische' alleen dat u geen Hallo IP-adres in een PUT-aanvraag opgeven. Hallo statische instellen via het Hallo-subnet opgeven. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Hoe implementeer ik een virtuele machine scale set tooan bestaande Azure-netwerk 

een virtuele-machineschaalset toodeploy tooan bestaande virtuele Azure-netwerk, raadpleegt u [implementeren van een virtuele machine scale set tooan bestaande virtuele netwerk](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Hoe toevoegen Hallo IP-adres van Hallo eerste virtuele machine in een virtuele-machineschaalset toohello uitvoer van een sjabloon ingesteld?

tooadd hello IP-adres van Hallo eerste virtuele machine in een virtuele machine scale set toohello uitvoer van een sjabloon, Zie [ARM: ophalen VMSS van privé IP-adressen](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Kan ik schaalsets met versnelde toegang gebruiken?

Ja. toouse versnelde netwerken, instellingen voor enableAcceleratedNetworking tootrue in uw scale set van networkInterfaceConfigurations. Bijvoorbeeld
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Hoe kan ik Hallo DNS-servers die worden gebruikt door een schaalset configureren?

toocreate een VM-schaalset met een aangepaste DNS-configuratie, voeg dat een dnsSettings JSON pakket toohello schaalset networkInterfaceConfigurations-sectie. Voorbeeld:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Hoe kan ik een scale set tooassign een openbare IP-adres tooeach VM configureren?

een VM-die schaalset toocreate wijst een openbare IP-adres tooeach VM, zorg ervoor dat Hallo API-versie van Hallo Microsoft.Compute/virtualMAchineScaleSets resource 2017-03-30 en toevoegen een _publicipaddressconfiguration_ JSON-pakket toohello schaalset ipConfigurations-sectie. Voorbeeld:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Kan ik een scale set toowork met meerdere Toepassingsgateways configureren?

Ja. U kunt Hallo resource-id's voor meerdere pools toohello van de toepassingsgateway back-end-adres toevoegen _applicationGatewayBackendAddressPools_ lijst in Hallo _ipConfigurations_ gedeelte van uw schaalset netwerkprofiel.

## <a name="scale"></a>Schalen

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>In welk geval zou ik een virtuele-machineschaalset ingesteld met minder dan twee virtuele machines maken?

Een reden toocreate een virtuele machine schaalset met minder dan twee virtuele machines wordt toouse Hallo elastische eigenschappen van een virtuele-machineschaalset ingesteld. Bijvoorbeeld, kan u een virtuele-machineschaalset weergeven met nul toodefine VMs uw infrastructuur implementeren zonder VM gebruikskosten betaalt. Wanneer u klaar toodeploy virtuele machines bent, verhogen vervolgens capaciteit' Hallo' van Hallo aantal virtuele machines scale set toohello productie-exemplaar.

Een andere reden dat u een virtuele-machineschaalset ingesteld met minder dan twee virtuele machines kunt maken, is als u zich zorgen over minder dan de beschikbaarheid in met behulp van een beschikbaarheidsset met discrete virtuele machines. Virtuele-machineschaalsets bieden u een toowork manier met niet gedifferentieerde compute-eenheden die vervangbare zijn. Deze uniformiteit is een belangrijke onderscheid voor virtuele-machineschaalsets versus beschikbaarheidssets. Veel staatloze werkbelastingen volgen afzonderlijke eenheden niet. Als de werkbelasting Hallo komt, kunt u terugschroeven tooone compute-eenheid en opschalen toomany wanneer Hallo werkbelasting toeneemt.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Hoe wijzig ik Hallo aantal VM's in een virtuele-machineschaalset

Zie toochange Hallo aantal VM's in een virtuele-machineschaalset [wijzigen Hallo-exemplaren van een virtuele-machineschaalset](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Hoe ik aangepaste waarschuwingen voor als bepaalde drempelwaarden zijn bereikt definiëren?

Hebt u enige flexibiliteit in hoe u waarschuwingen voor de opgegeven drempelwaarden verwerken. U kunt bijvoorbeeld aangepaste webhooks definiëren. Hallo na webhook voorbeeld is van een Resource Manager-sjabloon:

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

In dit voorbeeld wordt een waarschuwing tooPagerduty.com wanneer een drempelwaarde is bereikt.



## <a name="patching-and-operations"></a>Patching en bewerkingen

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Hoe maak ik een schaal instellen in een bestaande resourcegroep

Schaalsets maken in een bestaande resource groep is nog niet mogelijk hello Azure-portal, maar u kunt een bestaande resourcegroep opgeven bij het implementeren van een schaal van een Azure Resource Manager-sjabloon instellen. U kunt ook een bestaande resourcegroep opgeven bij het maken van een schaal ingesteld met Azure PowerShell of CLI.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Kan verplaatsen we dat een schaalset tooanother resourcegroep?

Ja, kunt u scale set resources tooa nieuw abonnement of resourcegroep verplaatsen.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Hoe tooI bijwerken mijn virtuele-machineschaalset tooa nieuwe installatiekopie? Hoe u beheer patchen?

tooupdate instellen voor uw virtuele-machineschaalset tooa nieuwe installatiekopie en toomanage patchen, Zie [upgraden van een virtuele-machineschaalset](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Kan ik Hallo terugzetten van de installatiekopie bewerking tooreset een virtuele machine gebruiken zonder Hallo afbeelding te wijzigen? (Dat wil zeggen, ik wil opnieuw een VM toofactory-instellingen in plaats van de nieuwe installatiekopie tooa.)

Ja, kunt u Hallo terugzetten van de installatiekopie bewerking tooreset een virtuele machine zonder Hallo afbeelding te wijzigen. Echter, als uw virtuele-machineschaalset verwijst naar een platforminstallatiekopie met `version = latest`, uw virtuele machine kunt bijwerken tooa hoger OS-installatiekopie bij het aanroepen van `reimage`.

Zie voor meer informatie [beheren van alle VM's in een virtuele-machineschaalset](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Problemen oplossen

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Hoe schakel ik op diagnostische gegevens over opstarten?

tooturn op diagnostische gegevens over opstarten, maak eerst een opslagaccount. Zet dit JSON-blok in uw virtuele-machineschaalset **virtualMachineProfile**, en Hallo virtuele-machineschaalset bijwerken:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Wanneer een nieuwe virtuele machine wordt gemaakt, ziet u Hallo InstanceView eigenschap Hallo VM Hallo details voor Hallo schermafbeelding, enzovoort. Hier volgt een voorbeeld:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Eigenschappen van virtuele machine

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Hoe krijg eigenschapsinformatie voor elke virtuele machine zonder dat meerdere aanroepen? Bijvoorbeeld, hoe ik krijgt Hallo foutdomein voor elk Hallo 100 virtuele machines in mijn virtuele-machineschaalset?

tooget eigenschapsinformatie voor elke virtuele machine zonder dat meerdere aanroepen, u kunt aanroepen `ListVMInstanceViews` als volgt een REST-API `GET` op Hallo resource-URI te volgen:

/Subscriptions/ < subscription_id > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtuele machines? $expand = instanceView & $select = instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Kan ik andere uitbreiding argumenten doorgeven toodifferent virtuele machines in een virtuele-machineschaalset?

Nee, u kunt niet doorgeven andere uitbreiding argumenten toodifferent virtuele machines in een virtuele-machineschaalset. Extensies kunnen echter op basis van unieke eigenschappen Hallo Hallo VM ze worden uitgevoerd, bijvoorbeeld als u op de naam van de machine Hallo fungeren. Extensies ook kunnen een query metagegevens van het exemplaar op http://169.254.169.254 tooget meer informatie over Hallo VM.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Waarom zijn er onderbrekingen tussen mijn namen voor machines van virtuele machine scale set VM en VM-id's? Bijvoorbeeld: 0, 1, 3...

Er onderbrekingen tussen de namen voor machines van virtuele machine scale set VM en VM-id's zijn omdat uw virtuele-machineschaalset **overprovision** eigenschap is ingesteld toohello standaardwaarde **true**. Als te overmatige inrichting is ingesteld**true**, meer virtuele machines dan aangevraagd worden gemaakt. Extra virtuele machines vervolgens verwijderd. In dit geval u krijgen hogere implementatie betrouwbaarheid, maar regels op Hallo kosten van aaneengesloten naming en aaneengesloten Network Address Translation (NAT). 

U kunt deze eigenschap instellen te**false**. Voor kleine virtuele machine-schaalsets beïnvloeden niet dit betrouwbaarheid van de implementatie aanzienlijk.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Wat is Hallo verschil tussen een virtuele machine in een virtuele-machineschaalset verwijderen en toewijzing Hallo VM? Wanneer moet ik een via andere Hallo kiezen?

Hallo belangrijkste verschil tussen een virtuele machine in een virtuele-machineschaalset verwijderen en toewijzing Hallo VM is dat `deallocate` Hallo virtuele harde schijven (VHD's) niet verwijderen. Er zijn kosten voor opslag die is gekoppeld aan die wordt uitgevoerd `stop deallocate`. U mogelijk een of andere voor een van de volgende redenen Hallo Hallo:

- U wilt toostop compute-kosten te betalen, maar u wilt dat de status van tookeep Hallo schijf Hallo virtuele machines.
- Wilt u sneller dan u een virtuele-machineschaalset kan uitbreiden toostart een set van virtuele machines.
  - Verwante toothis scenario wordt u mogelijk hebt gemaakt uw eigen engine voor het automatisch schalen en wilt dat een snellere end-to-end-schaal.
- U hebt een virtuele-machineschaalset die ongelijkmatig verdeeld is over domeinen met fouten of update-domeinen. Dit wordt mogelijk omdat u selectief virtuele machines verwijderd, of omdat de virtuele machines zijn verwijderd na overmatige inrichting. Met `stop deallocate` gevolgd door `start` op Hallo virtuele machine schaal instelt gelijkmatig Hallo VMs verdeelt over domeinen met fouten of update-domeinen.

