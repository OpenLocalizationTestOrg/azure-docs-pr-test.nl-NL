een VNet in het Resource Manager-implementatiemodel Hallo met behulp van Azure-portal Hallo toocreate Hallo volgende stappen. Gebruik Hallo [voorbeeldwaarden](#values) als u deze stappen uit als een zelfstudie. Als u deze stappen niet als een zelfstudie doet, moet u ervoor tooreplace Hallo waarden door uw eigen. Zie voor meer informatie over het werken met virtuele netwerken Hallo [Virtual Network-overzicht](../articles/virtual-network/virtual-networks-overview.md).

1. Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en meld u aan met uw Azure-account.
2. Klik op **Nieuw**. In Hallo **zoeken Hallo marketplace** veld, typt u 'Virtueel netwerk'. Zoek **virtueel netwerk** Hallo geretourneerde lijst en klik op tooopen hello **virtueel netwerk** blade.
3. Aan de onderkant Hallo van Hallo virtueel netwerk blade van Hallo **een implementatiemodel selecteren** Selecteer **Resource Manager**, en klik vervolgens op **maken**. Hiermee opent u Hallo 'Virtueel netwerk maken' blade.

    ![Blade Virtueel netwerk maken](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Blade Virtueel netwerk maken")
4. Op Hallo **virtueel netwerk maken** blade Hallo VNet-instellingen configureren. Bij het invullen van Hallo velden wordt hello rood uitroepteken een groen vinkje wanneer Hallo-tekens worden ingevoerd in Hallo veld geldig zijn.

  - **Naam**: Voer Hallo-naam voor het virtuele netwerk. In dit voorbeeld wordt de naam TestVNet1 gebruikt.
  - **Adresruimte**: Voer Hallo-adresruimte. Als u meerdere adres spaties tooadd hebt, kunt u uw eerste adresruimte toevoegen. U kunt later extra adresruimten toevoegen na het maken van Hallo VNet. Zorg ervoor dat Hallo-adresruimte die u opgeeft dat niet overlapt met adresruimte Hallo voor uw on-premises locatie.
  - **De subnetnaam van het**: Hallo eerste subnet naam en het subnet-adresbereik toevoegen. U kunt extra subnetten en gatewaysubnet hello later toevoegen na het maken van dit VNet. 
  - **Abonnement**: Controleer of dat weergegeven Hallo abonnement correct is Hallo. U kunt abonnementen wijzigen met behulp van Hallo vervolgkeuzelijst.
  - **Resourcegroep**: selecteer een bestaande resourcegroep of maak een nieuwe door een naam te typen voor uw nieuwe resourcegroep. Als u een nieuwe groep maakt, naam resourcegroep voor Hallo tooyour volgens de geplande configuratiewaarden. Zie [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.
  - **Locatie**: Selecteer Hallo locatie voor uw VNet. Hallo locatie bepaalt waar Hallo-resources die u toothis VNet implementeert blijven staan.

5. Selecteer **pincode toodashboard** als u kunnen toofind toobe uw VNet gemakkelijk op Hallo dashboard wilt en klik vervolgens op **maken**. Wanneer u op **maken**, ziet u een tegel op uw dashboard die nieuwe Hallo voortgang van uw VNet. Hallo tegel wijzigingen als Hallo VNet wordt gemaakt.
