
* Hallo conversie vereist Hallo VM opnieuw wordt opgestart, dus Hallo migratie van uw virtuele machines tijdens een onderhoudsvenster vooraf bestaande plannen. 

* Hallo-conversie is niet omkeerbaar. 

* Worden ervoor tootest Hallo conversie. Een virtuele machine migreren voordat u Hallo migratie in de productieomgeving uitvoert.

* Tijdens de conversie Hallo toewijzing ongedaan Hallo VM. Hallo VM ontvangt een nieuw IP-adres wanneer deze wordt opgestart na de conversie van Hallo. Indien nodig, kunt u [een statisch IP-adres toewijzen](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello VM.

* Hallo oorspronkelijke VHD's en Hallo storage-account die wordt gebruikt door Hallo VM vóór de conversie niet verwijderd. Ze blijven tooincur kosten. tooavoid wordt gefactureerd voor deze artefacten verwijderen Hallo oorspronkelijke VHD-blobs nadat u hebt gecontroleerd dat Hallo conversie is voltooid.
