1. In de portal Hallo van **alle resources**, klikt u op **+ toevoegen**. In Hallo **Alles** blade zoekvak, type **lokale netwerkgateway**, klikt u vervolgens op tooreturn een lijst met bronnen. Klik op **lokale netwerkgateway** tooopen Hallo blade en klik vervolgens op **maken** tooopen hello **de lokale netwerkgateway maken** blade.
   
    ![maak een lokale netwerkgateway](./media/vpn-gateway-add-lng-rm-portal-include/lng.png)

2. Op Hallo **blade lokale netwerkgateway maken**, Geef een **naam** voor uw lokale netwerkgateway-object. Gebruik indien mogelijk iets intuïtieve zoals **ClassicVNetLocal** of **TestVNet1Local**. Dit vergemakkelijkt het voor u tooidentify Hallo lokale netwerkgateway in Hallo-portal.
3. Geef een geldige openbare **IP-adres** voor Hallo VPN-apparaat of virtueel netwerk gateway toowhich gewenste tooconnect.<br>**Als deze lokaal netwerk een on-premises-locatie vertegenwoordigt:** Hallo openbare IP-adres van Hallo VPN-apparaat dat u wilt dat tooconnect naar opgeven. Het mag zich niet achter NAT en toobe die door Azure bereikbaar is.<br>**Als u deze lokaal netwerk vertegenwoordigt een andere VNet:** Hallo openbare IP-adres dat de virtuele netwerkgateway toohello is toegewezen voor dit VNet opgeven.<br>**Als u nog geen Hallo IP-adres hebt:** u kunt een geldige tijdelijke aanduiding voor IP-adres, gezamenlijk en keert u terug en wijzig deze instelling voordat u verbinding maakt.
4. **Adresruimte** verwijst toohello-adresbereiken voor Hallo-netwerk dat dit lokaal netwerk vertegenwoordigt. U kunt meerdere adresruimtebereiken toevoegen. Zorg ervoor dat Hallo bereiken die u hier opgeeft niet overlappen met adresbereiken van andere netwerken toowhich die u verbinding maakt.
5. Voor **abonnement**, Controleer of deze Hallo juiste abonnement wordt weergegeven.
6. Voor **resourcegroep**, selecteer Hallo resourcegroep die u toouse wilt. U kunt een nieuwe resourcegroep maken of een resourcegroep selecteren die u al hebt gemaakt.
7. Voor **locatie**, selecteer Hallo locatie waarin deze bron wordt gemaakt. U kunt tooselect Hallo dezelfde locatie die zich in uw VNet bevindt, maar u bent geen vereiste toodo dus.
8. Klik op **maken** toocreate Hallo lokale netwerkgateway.

