---
title: aaaAzure AD v2 iOS Getting Started - instellingen | Microsoft Docs
description: Hoe iOS (Swift)-toepassingen met een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="eeb81-103">Uw iOS-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="eeb81-103">Setting up your iOS application</span></span>

<span data-ttu-id="eeb81-104">Deze sectie bevat stapsgewijze instructies voor het toocreate een nieuw project toodemonstrate hoe een toepassing voor iOS (Swift) toointegrate met *aanmelden met Microsoft* zodat Web-API's waarvoor een token op te vragen.</span><span class="sxs-lookup"><span data-stu-id="eeb81-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="eeb81-105">Voorkeur toodownload dit voorbeeld XCode-project in plaats daarvan?</span><span class="sxs-lookup"><span data-stu-id="eeb81-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="eeb81-106">[Downloaden van een project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="eeb81-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="eeb81-107">Installeer Carthage toodownload en MSAL bouwen</span><span class="sxs-lookup"><span data-stu-id="eeb81-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="eeb81-108">Carthage package manager wordt gebruikt tijdens de evaluatieperiode Hallo van MSAL – het is geïntegreerd met XCode behoud Hallo mogelijkheid voor toohello-bibliotheek van Microsoft toomake wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="eeb81-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="eeb81-109">Download en installeer de nieuwste versie Hallo van Carthage [hier](https://github.com/Carthage/Carthage/releases "Carthage download-URL")</span><span class="sxs-lookup"><span data-stu-id="eeb81-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="eeb81-110">Maken van de toepassing</span><span class="sxs-lookup"><span data-stu-id="eeb81-110">Creating your application</span></span>

1.  <span data-ttu-id="eeb81-111">Open Xcode en selecteer`Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="eeb81-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="eeb81-112">Selecteer `iOS`  >  `Single view Application` en klik op *volgende*</span><span class="sxs-lookup"><span data-stu-id="eeb81-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="eeb81-113">Geef een productnaam en klik op *volgende*</span><span class="sxs-lookup"><span data-stu-id="eeb81-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="eeb81-114">Selecteer een map toocreate uw app en klik op *maken*</span><span class="sxs-lookup"><span data-stu-id="eeb81-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="eeb81-115">Hallo MSAL Framework bouwen</span><span class="sxs-lookup"><span data-stu-id="eeb81-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="eeb81-116">Volg onderstaande toopull Hallo-instructies en vervolgens samenstellen Hallo meest recente versie van Carthage MSAL bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="eeb81-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="eeb81-117">Open de Hallo bash terminal en gaat u de hoofdmap van de App toohello</span><span class="sxs-lookup"><span data-stu-id="eeb81-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="eeb81-118">Hallo onderstaande bestand kopiëren en plakken in Hallo bash terminal toocreate een 'Cartfile':</span><span class="sxs-lookup"><span data-stu-id="eeb81-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="eeb81-119">Kopieer en plak de onderstaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="eeb81-119">Copy and paste hello below.</span></span> <span data-ttu-id="eeb81-120">Met deze opdracht haalt afhankelijkheden in een map Carthage/opdrachten om uitchecken vervolgens builds Hallo MSAL bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="eeb81-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="eeb81-121">Hallo proces hierboven is gebruikte toodownload en build Hallo Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="eeb81-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="eeb81-122">MSAL verwerkt aanschaf, opslaan in cache en gebruiker tokens die worden gebruikt tooaccess API's die zijn beveiligd door Azure Active Directory-v2 hello te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="eeb81-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="eeb81-123">Hallo MSAL framework tooyour toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="eeb81-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="eeb81-124">Open in Xcode hello `General` tabblad</span><span class="sxs-lookup"><span data-stu-id="eeb81-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="eeb81-125">Ga toohello `Linked Frameworks and Libraries` sectie en klikt u op`+`</span><span class="sxs-lookup"><span data-stu-id="eeb81-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="eeb81-126">Selecteer `Add other…`</span><span class="sxs-lookup"><span data-stu-id="eeb81-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="eeb81-127">Selecteer: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` en klik op *Open*.</span><span class="sxs-lookup"><span data-stu-id="eeb81-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="eeb81-128">U ziet `MSAL.framework` toohello lijst toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="eeb81-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="eeb81-129">Ga te`Build Phases` tabblad en klik op `+` pictogram kiezen`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="eeb81-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="eeb81-130">Hallo inhoud toohello na toevoegen *gebied script*:</span><span class="sxs-lookup"><span data-stu-id="eeb81-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="eeb81-131">Hallo te volgende toevoegen<code>Input Files</code> door te klikken op <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="eeb81-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="eeb81-132">Maken van de gebruikersinterface van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="eeb81-132">Creating your application’s UI</span></span>
<span data-ttu-id="eeb81-133">Een bestand Main.storyboard moet automatisch worden gemaakt als onderdeel van uw project-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="eeb81-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="eeb81-134">Volg onderstaande toocreate Hallo app UI Hallo instructies:</span><span class="sxs-lookup"><span data-stu-id="eeb81-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="eeb81-135">Control + klik `Main.storyboard` toobring Hallo contextafhankelijke menu omhoog en klik vervolgens op:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="eeb81-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="eeb81-136">Vervang Hallo `<scenes>` knooppunt met Hallo-code hieronder:</span><span class="sxs-lookup"><span data-stu-id="eeb81-136">Replace hello `<scenes>` node with hello code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
