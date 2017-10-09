


Dit onderwerp wordt beschreven hoe:

* Gegevens invoeren in Azure een virtuele machine (VM), wanneer deze wordt ingericht.
* Deze ophalen voor Windows- en Linux.
* Gebruik van speciale hulpprogramma's beschikbaar op sommige systemen toodetect en aangepaste gegevens automatisch afhandelen.

> [!NOTE]
> Dit artikel wordt beschreven hoe aangepaste gegevens met behulp van een virtuele machine gemaakt met hello Azure Service Management API kan worden ingevoegd. hoe toouse hello Azure Resource Management-API, Zie toosee [Hallo voorbeeldsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Injecteren van aangepaste gegevens in uw virtuele machine van Azure
Deze functie is momenteel alleen ondersteund in Hallo [Azure-opdrachtregelinterface](https://github.com/Azure/azure-xplat-cli). Hier maken we een `custom-data.txt` -bestand met onze gegevens vervolgens invoeren die in toohello VM tijdens het inrichten. Hoewel u mogelijk Hallo opties voor Hallo `azure vm create` opdracht Hallo volgende demonstreert een zeer eenvoudige benadering:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Met behulp van aangepaste gegevens in de Hallo virtuele machine
* Als uw Azure VM een VM op basis van Windows is, wordt de Hallo aangepaste gegevens te opgeslagen`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Hoewel het base64-gecodeerd tootransfer van Hallo lokale computer toohello nieuwe VM is automatisch gedecodeerd en kan worden geopend of direct gebruikt.
  
  > [!NOTE]
  > Als het Hallo-bestand aanwezig is, wordt deze overschreven. Hallo-beveiliging op Hallo directory te is ingesteld**System: volledig beheer** en **Administrators: volledig beheer**.
  > 
  > 
* Als uw Azure VM een VM op basis van Linux is en vervolgens de aangepaste gegevensbestand Hallo bevindt zich een van de volgende hello wordt geplaatst, afhankelijk van uw distro. Hallo-gegevens mogelijk base64-gecodeerd, dus u toodecode Hallo gegevens eerst moet misschien:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Cloud-init op Azure
Als uw Azure VM van een installatiekopie van een Ubuntu of virtuele CoreOS is, kunt u CustomData toosend toocloud initialisatie in een cloud-configuratie kunt gebruiken. Of als uw aangepaste gegevensbestand een script is, vervolgens cloud init kunt gewoon uitvoeren.

### <a name="ubuntu-cloud-images"></a>Ubuntu Cloud installatiekopieën
In de meeste Azure Linux-installatiekopieën, bewerkt u zou ' / etc/waagent.conf ' tooconfigure Hallo tijdelijke schijf en de wisselruimte bronbestand. Zie [gebruikershandleiding voor Azure Linux Agent](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.

Echter op Hallo Ubuntu Cloud installatiekopieën, moet u cloud-init tooconfigure Hallo resource schijf (dat wil zeggen, Hallo 'kortstondige' schijf) en de wisselruimte partitie. Hallo na pagina op Hallo Ubuntu wiki voor meer informatie Zie: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Volgende stappen: met behulp van cloud-init
Zie voor meer informatie, Hallo [cloud init-documentatie voor Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Rol van Service Management REST API-verwijzing toevoegen](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Azure-opdrachtregelinterface](https://github.com/Azure/azure-xplat-cli)

