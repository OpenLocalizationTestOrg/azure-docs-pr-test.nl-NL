## <a name="sample-scenario"></a>Voorbeeldscenario
toobetter laten zien hoe toomanage nsg's, in dit artikel gebruikt Hallo scenario hieronder.

![VNet-scenario](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

In dit scenario maakt u een NSG voor elk subnet in Hallo **TestVNet** virtueel netwerk, zoals hieronder beschreven: 

* **NSG-FrontEnd**. Hallo-front-end NSG worden toegepaste toohello *FrontEnd* subnet, en bevatten twee regels:    
  * **RDP-regel**. Deze regel kan de RDP-verkeer toohello *FrontEnd* subnet.
  * **Web-regel**. Deze regel kunnen HTTP-verkeer toohello *FrontEnd* subnet.
* **NSG-back-end**. Hallo back-end NSG wordt toegepast toohello worden *back-end* subnet, en bevatten twee regels:    
  * **SQL-regel**. Met deze regel kunnen SQL verkeer alleen via Hallo *FrontEnd* subnet.
  * **Web-regel**. Deze regel niet alle verkeer van Hallo gebonden *back-end* subnet.

Hallo combinatie van deze regels een DMZ-achtige scenario maken, waarbij Hallo back-end-subnet kan alleen inkomend verkeer voor SQL-verkeer ontvangen van Hallo front-end-subnet, en heeft geen toohello toegang tot Internet, terwijl de front-end-subnet Hallo met de Hallo communiceren kan Internet, en alleen binnenkomende HTTP-aanvragen ontvangen.

toodeploy hello scenario hierboven beschreven, volg [deze koppeling](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), klikt u op **tooAzure implementeren**, vervang Hallo standaardparameterwaarden indien nodig en volg de instructies Hallo in Hallo-portal. Is in instructies voor het voorbeeld hieronder Hallo sjabloon Hallo gebruikte toodeploy een resource groepsnamen **RG NSG**. 

