Ondersteuning voor twee foutopsporingsfuncties is nu beschikbaar in Azure: ondersteuning voor Console-uitvoer en Schermafbeelding voor het Azure Virtual Machines Resource Manager-implementatiemodel. 

Wanneer u uw eigen installatiekopie tooAzure of zelfs opstarten een van de installatiekopieën van het platform hello te brengen, kunnen er diverse redenen waarom een virtuele Machine in een niet-opstartbare status opgehaald. Met deze functies kunt u tooeasily diagnosticeren en op uw virtuele Machines herstellen.

Voor virtuele Linux-Machines, kunt u eenvoudig hello uitvoer van uw consolelogboek van Hallo Portal bekijken:

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Echter voor Windows en Linux virtuele Machines kunt Azure ook u een schermopname van Hallo VM van de hypervisor Hallo toosee:

![Fout](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Beide functies worden ondersteund voor virtuele Azure-machines in alle regio's. Opmerking: de schermafbeeldingen en de uitvoer kunnen duren too10 minuten tooappear in uw opslagaccount.

## <a name="common-boot-errors"></a>Veelvoorkomende opstartfouten

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Er is geen besturingssysteem gevonden](https://support.microsoft.com/help/4010142)
- [Opstartfout of OPSTARTAPPARAAT_NIET_TOEGANKELIJK](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Diagnostische gegevens op een nieuwe virtuele machine inschakelen
1. Wanneer u een nieuwe virtuele Machine maakt van Hallo Preview-Portal, selecteer Hallo **Azure Resource Manager** uit Hallo deployment model vervolgkeuzelijst:
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Hallo bewaking optie tooselect Hallo storage-account waarin u tooplace wilt dat deze diagnostische bestanden configureren.
 
    ![VM maken](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Als u met een Azure Resource Manager-sjabloon implementeert, virtuele-machinebron tooyour navigeren en Hallo diagnostische profielsectie toevoegen. Houd er rekening mee toouse Hallo '2015-06-15' API-versie-header.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. Hallo diagnostische profiel kunt u tooselect Hallo storage-account waar u tooput deze logboeken.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

een voorbeeld van een virtuele Machine met diagnostische gegevens over opstarten is ingeschakeld, het uitchecken van onze opslagplaats hier toodeploy.

## <a name="update-an-existing-virtual-machine"></a>Een bestaande virtuele machine bijwerken ##

tooenable diagnostische gegevens over opstarten via Hallo Portal, kunt u ook een bestaande virtuele Machine via de Portal Hallo bijwerken. Selecteer Hallo Boot Diagnostics optie en opslaan. Opnieuw opstarten Hallo VM tootake effect.

![Bestaande VM bijwerken](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

