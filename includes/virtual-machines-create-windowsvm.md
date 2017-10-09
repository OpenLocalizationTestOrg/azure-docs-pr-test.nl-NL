1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Beginnen in de linkerbovenhoek hello, klikt u op **Nieuw > berekenen > Windows Server 2016 Datacenter**.

    ![Navigeer toohello Azure VM-installatiekopieën in Hallo-portal](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Selecteer op de Windows Server 2016 Datacenter hello, Hallo klassieke implementatiemodel. Klik op Maken.

    ![Schermafbeelding van hello Azure VM-installatiekopieën beschikbaar zijn in de portal Hallo](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Blade Grondbeginselen

de blade grondbeginselen Hallo aanvragen beheergegevens voor Hallo virtuele machine.

1. Voer een **naam** voor Hallo virtuele machine. In voorbeeld Hallo _HeroVM_ Hallo-naam van Hallo virtuele machine is. Hallo-naam moet 1-15 tekens lang zijn en het mag geen speciale tekens bevatten.

2. Voer een **gebruikersnaam** en een sterk **wachtwoord** die gebruikte toocreate een lokaal account op Hallo VM zijn. Hallo lokale account wordt gebruikt toosign in tooand Hallo VM beheren. In voorbeeld Hallo _azureuser_ Hallo-gebruikersnaam.

 Hallo wachtwoord moet 8 123 tekens lang zijn en voldoen aan de drie buiten Hallo de volgende vier complexiteitsvereisten: één kleine letter, één hoofdletter, één cijfer en één speciaal teken. Zie meer informatie over [vereisten voor gebruikersnaam en wachtwoord](../articles/virtual-machines/windows/faq.md).

3. Hallo **abonnement** is optioneel. Een algemene instelling is 'Betalen naar gebruik'.

4. Selecteer een bestaande **resourcegroep** of Hallo typenaam voor een nieuwe resourcegroep. In voorbeeld Hallo _HeroVMRG_ Hallo-naam van de resourcegroep Hallo is.

5. Selecteer een Azure-datacenter **locatie** waar u Hallo VM toorun. In voorbeeld Hallo **VS-Oost** Hallo locatie.

6. Wanneer u klaar bent, klikt u op **volgende** toocontinue toohello volgende blade.

    ![Schermafbeelding van Hallo-instellingen op Hallo basisbeginselen blade voor het configureren van een Azure VM](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Blade Grootte

Hallo grootte blade configuratiedetails Hallo Hallo VM identificeert en een lijst met verschillende opties die OS, aantal processors, ondersteund schijftype voor opslag en Geschatte maandelijkse gebruikskosten bevatten.  

Kies een VM-grootte en klik vervolgens op **Selecteer** toocontinue. In dit voorbeeld _DS1_\__V2 standaard_ Hallo VM-grootte is.

  ![Schermafbeelding van Hallo grootte tabblad waarin hello Azure VM-grootten die u kunt selecteren](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Blade Instellingen

de blade instellingen Hallo aanvragen opties voor opslag en netwerk. U kunt Hallo standaardinstellingen accepteren. Azure maakt waar nodig de juiste vermeldingen.

Als u voor uw virtuele machine een grootte hebt geselecteerd die hierdoor wordt ondersteund, kunt u Azure Premium Storage uitproberen. Selecteer hiervoor in Schijftype de optie Premium SSD.

Wanneer u alle wijzigingen hebt aangebracht, klikt u op **OK**.

## <a name="4-summary-blade"></a>4. Blade Samenvatting

Hallo samenvatting blade bevat Hallo-instellingen die zijn opgegeven in de vorige blades Hallo. Klik op **OK** wanneer u bent klaar toomake Hallo installatiekopie.

 ![Samenvatting blade rapport geeft de opgegeven instellingen van Hallo virtuele machine](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Nadat Hallo virtuele machine is gemaakt, Hallo portal een lijst met nieuwe virtuele machine onder Hallo **alle resources**, en geeft u een tegel van Hallo virtuele machine weer op Hallo-dashboard. Hallo bijbehorende cloud service- en storage-account ook zijn gemaakt en wordt vermeld. Zowel Hallo virtuele machine en cloudservice automatisch gestart en hun status wordt vermeld als **met**.

 ![VM-Agent en Hallo eindpunten van Hallo virtuele machine configureren](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
