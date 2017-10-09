Wanneer u gegevens schijven tooa Linux VM toevoegt, kan er fouten optreden als een schijf niet op LUN 0 bestaat. Als u een schijf handmatig met Hallo toevoegt `azure vm disk attach-new` opdracht en geeft u een LUN (`--lun`) in plaats van Hallo zodat Azure-platform toodetermine Hallo juiste LUN, behandelen die een schijf al bestaat / wordt aangelegd op LUN 0. 

Overweeg het volgende voorbeeld met een fragment van uitvoer van Hallo Hallo `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

Hallo twee gegevensschijven bestaat op LUN 0 en 1 LUN (de eerste kolom Hallo in Hallo `lsscsi` uitvoer details `[host:channel:target:lun]`). Beide schijven moeten accessbile uit binnen Hallo VM. Als u handmatig Hallo eerste schijf toobe toegevoegd LUN 1 en de tweede schijf Hallo op LUN 2 had opgegeven, ziet u mogelijk niet Hallo schijven correct van binnen uw virtuele machine.

> [!NOTE]
> Hello Azure `host` waarde 5 in deze voorbeelden, maar dit kan variëren afhankelijk van Hallo type opslag dat u selecteert.
> 
> 

Dit gedrag van de schijf is niet een probleem met de Azure, maar Hallo manier in welke Hallo Linux volgt kernel Hallo SCSI-specificaties. Als de Hallo Linux kernel scant Hallo SCSI-bus op gekoppelde apparaten, kan een apparaat moet worden gevonden op LUN 0 om Hallo system toocontinue scannen voor extra apparaten. Als zodanig:

* Controleer de uitvoer Hallo van `lsscsi` na het toevoegen van een data schijf tooverify dat er een schijf voor LUN 0.
* Als de schijf niet correct binnen uw virtuele machine weergegeven wordt, controleert u of dat een schijf op LUN 0 bestaat.

