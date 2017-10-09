<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall een update van hello Azure-portal

1. Selecteer op de pagina StorSimple hello, uw apparaat. Navigeer te**apparaten** > **onderhoud**.
2. Klik onder aan de pagina Hallo Hallo op **Updates zoeken**. Een taak gemaakt tooscan naar beschikbare updates. U wordt gewaarschuwd wanneer het Hallo-taak is voltooid.
3. In Hallo **Software-Updates** sectie op Hallo dezelfde pagina Hallo nieuwe software-updates beschikbaar zijn. U wordt aangeraden de releaseopmerkingen Hallo te controleren voordat u een update op uw apparaat toepassen.
4. Klik onder aan de pagina Hallo Hallo op **Updates installeren**, en vervolgens **OK**.
5. In Hallo **updates installeren** in het dialoogvenster Zorg ervoor dat u Hallo aanbevelingen hebt gevolgd en selecteer vervolgens **ik Hallo hierboven vereiste begrijpen en gereed tooupgrade ben mijn apparaat** en op Hallo controleren de knop.
   
    ![Bevestigingsbericht](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Er wordt een reeks vereiste controles gestart. Deze controles zijn onder andere:
   
   * **Controller statuscontroles** tooverify dat beide apparaatcontrollers Hallo in orde en online zijn.
   * **Hardware-onderdeel statuscontroles** tooverify dat alle hardware-onderdelen op uw StorSimple-apparaat Hallo zijn in orde.
   * **DATA 0 controleert** tooverify dat DATA 0 is ingeschakeld op uw apparaat. Als deze interface niet is ingeschakeld, schakelt u deze in en probeert u het vervolgens opnieuw.
   * **DATA 2 en DATA 3 controles** tooverify DATA 2 en DATA 3-netwerkinterfaces zijn niet ingeschakeld. Als deze interfaces zijn ingeschakeld, moet u deze functies uitschakelen en probeer tooupdate uw apparaat. Deze controle wordt alleen uitgevoerd als u een update uitvoert vanaf een apparaat met GA-software. Voor apparaten met versies 0.1, 0.2 of 0.3 is deze controle niet nodig.
   * **Controle van de gateway** op elk apparaat waarop een eerdere tooUpdate van versie 1 wordt uitgevoerd. Deze controle wordt uitgevoerd op alle Hallo apparaat vóór update 1 software die wordt uitgevoerd, maar niet op Hallo-apparaten met een gateway is geconfigureerd voor een netwerkinterface dan DATA 0.
     
     Hallo-update wordt toegepast als alle controles zijn voltooid. U wordt gewaarschuwd wanneer Hallo controles uitgevoerd worden.
     
     ![Melding voor controles](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Hallo Hier volgt een voorbeeld waarin Hallo controles is mislukt. U moet controleren of beide apparaatcontrollers Hallo in orde en online zijn. U moet ook toocheck Hallo status van Hallo hardware-onderdelen. In dit voorbeeld vereisen de onderdelen Controller 0 en Controller 1 aandacht. Mogelijk moet u toocontact Microsoft Support als u deze problemen door u zelf kan niet oplossen.
     
       ![Controles zijn mislukt](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Nadat het Hallo-controles zijn voltooid, wordt een updatetaak gemaakt. U wordt gewaarschuwd wanneer de bijwerktaak Hallo is gemaakt.
   
    ![Maken van bijwerktaak](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    Hallo-update wordt vervolgens toegepast op uw apparaat.
    
8. toomonitor hello voortgang van de bijwerktaak hello, klikt u op **taak weergeven**. Op Hallo **taken** pagina ziet u Hallo voortgang bijwerken.
9. Hallo update duurt enkele uren toocomplete. Hallo updatetaak te selecteren en klik op **Details** tooview Hallo details van de taak Hallo op elk gewenst moment.
10. Nadat het Hallo-taak is voltooid, gaat u toohello **onderhoud** pagina en schuif naar beneden te**Software-Updates**.

