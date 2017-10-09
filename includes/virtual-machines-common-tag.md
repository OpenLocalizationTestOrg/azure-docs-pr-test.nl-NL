


## <a name="tagging-a-virtual-machine-through-templates"></a>Labels van een virtuele Machine via sjablonen
Eerst gaan we kijken tagging via sjablonen. [Deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) plaatst labels op Hallo volgende resources: Compute (virtuele Machine) en opslag (Storage-Account) netwerk (openbare IP-adres, virtuele netwerk en Network Interface). Deze sjabloon is voor een virtuele machine van Windows, maar kan worden aangepast voor virtuele Linux-machines.

Klik op Hallo **implementeren tooAzure** knop van Hallo [sjabloonkoppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Dit, gaat u toohello [Azure-portal](https://portal.azure.com/) waarin u deze sjabloon kunt implementeren.

![Eenvoudige implementatie met labels](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Deze sjabloon bevat Hallo tags te volgen: *afdeling*, *toepassing*, en *gemaakt door*. U kunt toevoegen/bewerken deze tags rechtstreeks in de sjabloon Hallo indien andere tagnaam gewenst.

![Azure labels in een sjabloon](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Zoals u ziet, worden Hallo labels worden gedefinieerd als sleutel-waardeparen, gescheiden door een dubbele punt (:). Hallo-labels moeten worden gedefinieerd in deze indeling:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Hallo-sjabloonbestand opslaan als u klaar bent met het bewerken met labels Hallo van uw keuze.

Vervolgens gaat u naar Hallo **Parameters bewerken** sectie u vult Hallo waarden voor de labels.

![Labels bewerken in Azure-portal](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Klik op **maken** toodeploy deze sjabloon met de waarden van uw code.

## <a name="tagging-through-hello-portal"></a>Via de Portal Hallo-tagging
Na het maken van uw resources met labels, kunt u weergeven, toevoegen en verwijderen van labels in Hallo-portal.

Selecteer Hallo labels pictogram tooview de labels:

![Pictogram van de labels in Azure-portal](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Een nieuwe code via Hallo portal door te definiëren van uw eigen sleutel-waardepaar toevoegt en sla het.

![Nieuw label toevoegen in Azure-portal](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Uw nieuwe code wordt nu weergegeven in de lijst Hallo van codes voor uw resource.

![Nieuwe code opgeslagen in Azure-portal](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

