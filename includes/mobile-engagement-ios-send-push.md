### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Verleen toegang tooyour Pushcertificaat tooMobile Engagement
tooallow Mobile Engagement toosend Pushmeldingen namens u, moet u deze toegang hebben tot tooyour certificaat toogrant. Dit wordt gedaan door te configureren en uw certificaat voeren in Hallo Mobile Engagement-portal. Zorg dat u uw .p12-certificaat verkrijgt zoals uitgelegd in de [Apple-documentatie](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Navigeer tooyour Mobile Engagement-portal. Zorg ervoor dat u in de juiste Hallo bent en klik vervolgens op Hallo **Engage** knop Hallo onderaan:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Klik op Hallo **instellingen** pagina in de Engagement-Portal. Klik op Hallo **Native Pushbericht** sectie tooupload uw p12-certificaat:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Selecteer uw p12, upload het en typ uw wachtwoord:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Een melding tooyour app verzenden
We gaan nu een eenvoudige pushmeldingcampagne die een push-tooour-app stuurt maken:

1. Navigeer toohello **bereiken** tabblad in uw Mobile Engagement-portal.
2. Klik op **nieuwe aankondiging** toocreate uw pushcampagne
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Hallo eerste velden van uw campagne instellen:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Geef uw campagne een **naam**. 
   * Selecteer Hallo **leveringstijd** als **alleen buiten app**: dit is Hallo eenvoudig Apple-pushmeldingentype met een beetje tekst.
   * Typ in de berichttekst hello, eerste Hallo **titel** die de eerste regel Hallo in Hallo push worden.
   * Typ vervolgens uw **bericht** die de tweede regel Hallo zijn
4. Schuif naar beneden en selecteer in de Hallo sectie inhoud **alleen melding**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Instelling Hallo meest elementaire campagne is voltooid. Nu Schuif naar beneden en klik op **maken** knop toosave uw pushmeldingcampagne. 
6. Klik ten slotte op **activeren** toosend push-melding. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. U ontvangt Hallo melding op uw iOS-apparaat in het meldingencentrum Hallo Hallo volgende:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Als u een Apple Watch gekoppeld aan dit iOS-apparaat hebt vervolgens ziet u Hallo melding op uw Apple Watch:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

