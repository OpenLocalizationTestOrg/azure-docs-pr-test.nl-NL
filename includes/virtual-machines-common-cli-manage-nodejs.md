Voordat u kunt Azure CLI Hallo met Resource Manager-opdrachten en sjablonen toodeploy Azure-resources en werkbelastingen resourcegroepen gebruiken, moet u een account met Azure. Als u geen account hebt, kunt u [hier een gratis proefversie starten](https://azure.microsoft.com/pricing/free-trial/).

Als u nog niet hebt geïnstalleerd hello Azure CLI en verbonden tooyour abonnement, Zie [installeren hello Azure CLI](../articles/cli-install-nodejs.md) Hallo-modus te instellen`arm` met `azure config mode arm`, en maak verbinding tooAzure Hello `azure login` opdracht.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- Azure CLI 10 – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Basisopdrachten van Azure Resource Manager in Azure CLI
In dit artikel bevat informatie over basic opdrachten die u wilt dat toouse met Azure CLI toomanage en communiceren met uw resources (voornamelijk VM's) in uw Azure-abonnement.  Voor meer hulp bij specifieke opdrachtregelopties en opties, kunt u opties en Hallo opdracht online help door te typen `azure <command> <subcommand> --help` of `azure help <command> <subcommand>`.

> [!NOTE]
> Deze voorbeelden bevatten geen sjabloonbewerkingen die over het algemeen worden aanbevolen voor VM-implementaties in Resource Manager. Zie voor informatie [gebruik hello Azure CLI met Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) en [implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en Azure CLI Hallo](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Taak | Resource Manager |
| --- | --- | --- |
| Maak Hallo meest eenvoudige VM |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Hallo verkrijgen `image-urn` van Hallo `azure vm image list` opdracht. Zie [dit artikel](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor voorbeelden.) |
| Een Linux-VM maken |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Een Windows-VM maken |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Lijst met VM's opvragen |`azure  vm list [options]` |
| Informatie over een VM ophalen |`azure  vm show [options] <resource_group> <name>` |
| Een VM starten |`azure vm start [options] <resource_group> <name>` |
| Een VM stoppen |`azure vm stop [options] <resource_group> <name>` |
| De toewijzing van een VM ongedaan maken |`azure vm deallocate [options] <resource-group> <name>` |
| Een VM opnieuw opstarten |`azure vm restart [options] <resource_group> <name>` |
| Een VM verwijderen |`azure vm delete [options] <resource_group> <name>` |
| Een virtuele machine vastleggen |`azure vm capture [options] <resource_group> <name>` |
| Een VM maken van een gebruikersinstallatiekopie |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Een VM maken van een gespecialiseerde schijf |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Toevoegen van een data schijf tooa VM |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Een gegevensschijf verwijderen van een VM |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Toevoegen van een generieke uitbreiding tooa VM |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Toegang van de VM-extensie tooa VM toevoegen |`azure vm reset-access [options] <resource-group> <name>` |
| Docker-extensie tooa VM toevoegen |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Een VM-extensie verwijderen |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Verbruik van VM-resources opvragen |`azure vm list-usage [options] <location>` |
| Alle beschikbare VM-grootten opvragen |`azure vm sizes [options]` |

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer voorbeelden van Hallo CLI-opdrachten overschrijden basic VM management [Using hello Azure CLI met Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).
