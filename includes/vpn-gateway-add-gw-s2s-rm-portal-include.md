1. Klik op het Hallo-zijde van Hallo portal-pagina naar links,  **+**  en typ 'Virtuele netwerkgateway' in de zoekopdracht. Zoek in **Resultaten** naar **Virtuele netwerkgateway** en klik hierop.
2. Klik onder aan Hallo 'Virtuele netwerkgateway' blade Hallo op **maken**. Hiermee opent u Hallo **virtuele netwerkgateway aanmaken** blade.

    ![Velden van de blade Virtuele netwerkgateway maken](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Nieuwe gateway")

3. Op Hallo **virtuele netwerkgateway aanmaken** blade Hallo waarden opgeven voor uw virtuele netwerkgateway.

  - **Naam**: naam van uw gateway. Dit is niet gelijk aan de naamgeving van een gatewaysubnet Hallo. Het Hallo-naam van Hallo gateway-object maken van de.
  - **Gatewaytype**: selecteer **VPN**. VPN-gateways gebruiken type Hallo virtuele-netwerkgateway **VPN**. 
  - **VPN-type**: Selecteer Hallo VPN-type dat is opgegeven voor uw configuratie. De meeste configuraties vereisen een op route gebaseerd VPN-type.
  - **SKU**: Selecteer Hallo gateway-SKU uit Hallo vervolgkeuzelijst. Hallo-SKU's die worden vermeld in de vervolgkeuzelijst Hallo is afhankelijk van Hallo VPN-type dat u selecteert. Zie [Gateway-SKU's](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor informatie over gateway-SKU's.
  - **Locatie**: U moet mogelijk tooscroll toosee locatie. Hallo aanpassen **locatie** veld toopoint toohello locatie van het virtuele netwerk. Als Hallo locatie niet toohello regio waar uw virtuele netwerk zich bevindt verwijst, wordt Hallo virtueel netwerk niet weergegeven in de volgende stap Hallo dropdown 'Kiezen een virtueel netwerk'.
  - **Virtueel netwerk**: Kies Hallo virtueel netwerk toowhich gewenste tooadd deze gateway. Klik op **virtueel netwerk** tooopen Hallo 'Kiezen een virtueel netwerk' blade. Selecteer Hallo VNet. Als u uw VNet niet ziet, zorg er dan voor dat het veld locatie Hallo wijst toohello regio waarin het virtuele netwerk bevindt.
  - **Openbaar IP-adres**: 'Maak openbaar IP-adres' Hallo-blade een openbare IP-adres-object wordt gemaakt. Hallo openbaar IP-adres wordt dynamisch toegewezen wanneer Hallo VPN-gateway is gemaakt. VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen. Dit betekent echter niet dat dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen. de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt. Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.

    - Klik eerst **openbaar IP-adres** tooopen Hallo 'Openbare IP-adres kiezen' blade en klik vervolgens op **+ maken van nieuwe** tooopen Hallo 'Maak openbaar IP-adres' blade.
    - Voer vervolgens een **naam** voor uw openbare IP-adres, klik vervolgens op **OK** op Hallo onder aan deze blade toosave worden uw wijzigingen.

      ![Openbaar IP maken](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "PIP maken")

4. Hallo-instellingen te controleren. U kunt selecteren **pincode toodashboard** onderaan Hallo Hallo blade als u wilt dat uw gateway tooappear op Hallo-dashboard. 
5. Klik op **maken** toobegin Hallo VPN-gateway maken. Hallo-instellingen worden gevalideerd en ziet u Hallo 'Virtuele netwerkgateway implementeren' tegel op Hallo-dashboard. Maken van een gateway kan duren too45 minuten. U moet mogelijk toorefresh de status van uw portal-pagina toosee Hallo voltooid.

Nadat het Hallo-gateway is gemaakt, weergeven Hallo IP-adres dat is toegewezen tooit door te kijken Hallo virtueel netwerk in Hallo-portal. Hallo-gateway wordt weergegeven als aangesloten apparaat. U kunt klikken op Hallo verbonden apparaat (uw virtuele netwerkgateway) tooview meer informatie.
