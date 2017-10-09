1. In de portal Hallo van **alle resources**, klikt u op **+ toevoegen**. 
2. In Hallo **Alles** blade zoekvak, type **lokale netwerkgateway**, klikt u vervolgens op toosearch. Er wordt dan een lijst geretourneerd. Klik op **lokale netwerkgateway** tooopen Hallo blade en klik vervolgens op **maken** tooopen hello **de lokale netwerkgateway maken** blade.

  ![maak een lokale netwerkgateway](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. Op Hallo **blade lokale netwerkgateway maken**, Hallo waarden opgeven voor uw lokale netwerkgateway.

  - **Naam:** geef een naam op voor uw lokale netwerkgateway.
  - **IP-adres:** dit openbare IP-adres van Hallo VPN-apparaat dat u wilt dat Azure tooconnect naar Hallo is. Geef een geldig openbaar IP-adres op. Hallo IP-adres mag zich niet achter NAT en toobe die door Azure bereikbaar is. Als u geen nu Hallo IP-adres hebt, kunt u Hallo waarden in de schermopname hello, maar u moet toogo terug en de IP-adres van de tijdelijke aanduiding vervangt door Hallo openbare IP-adres van uw VPN-apparaat. Azure zich anders niet kunnen tooconnect.
  - **Adresruimte** verwijst toohello-adresbereiken voor Hallo-netwerk dat dit lokaal netwerk vertegenwoordigt. U kunt meerdere adresruimtebereiken toevoegen. Zorg ervoor dat Hallo bereiken die u hier opgeeft niet overlappen met adresbereiken van andere netwerken die u wilt dat tooconnect aan. Azure routeert Hallo-adresbereik dat u toohello lokale VPN-apparaat IP-adres opgeeft. *Uw eigen waarden hier gebruiken, geen waarden weergegeven in de schermafbeelding Hallo Hallo*.
  - **Abonnement:** controleren die Hallo juiste abonnement wordt weergegeven.
  - **Resourcegroep:** Selecteer Hallo resourcegroep die u toouse wilt. U kunt een nieuwe resourcegroep maken of een resourcegroep selecteren die u al hebt gemaakt.
  - **Locatie:** Hallo locatie die dit object wordt gemaakt in selecteren. U kunt tooselect Hallo dezelfde locatie die zich in uw VNet bevindt, maar u bent geen vereiste toodo dus.

4. Wanneer u klaar bent met het Hallo-waarden opgeven, klikt u op **maken** onderaan Hallo Hallo blade toocreate Hallo lokale netwerkgateway.
