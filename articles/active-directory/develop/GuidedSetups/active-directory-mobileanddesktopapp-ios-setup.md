---
title: Azure AD v2 iOS Getting Started - instellingen | Microsoft Docs
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
ms.openlocfilehash: d25353a61b2a60bff28aa0679d38110e77d19e64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="61dff-103">Uw iOS-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="61dff-103">Setting up your iOS application</span></span>

<span data-ttu-id="61dff-104">Deze sectie bevat stapsgewijze instructies voor het maken van een nieuw project te laten zien hoe een toepassing voor iOS (Swift) worden geïntegreerd met *aanmelden met Microsoft* zodat Web-API's waarvoor een token op te vragen.</span><span class="sxs-lookup"><span data-stu-id="61dff-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="61dff-105">Voorkeur voor het downloaden van dit voorbeeld XCode-project in plaats daarvan?</span><span class="sxs-lookup"><span data-stu-id="61dff-105">Prefer to download this sample's XCode project instead?</span></span> <span data-ttu-id="61dff-106">[Downloaden van een project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) en doorgaan met de [configuratiestap](#create-an-application-express) voor het configureren van het codevoorbeeld voordat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61dff-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


## <a name="install-carthage-to-download-and-build-msal"></a><span data-ttu-id="61dff-107">Carthage te downloaden en te bouwen MSAL installeren</span><span class="sxs-lookup"><span data-stu-id="61dff-107">Install Carthage to download and build MSAL</span></span>
<span data-ttu-id="61dff-108">Carthage package manager wordt gebruikt tijdens de evaluatieperiode van MSAL – het behoud van de mogelijkheden van Microsoft wijzigingen aanbrengen in de bibliotheek is geïntegreerd met XCode.</span><span class="sxs-lookup"><span data-stu-id="61dff-108">Carthage package manager is used during the preview period of MSAL – it integrates with XCode while maintaining the ability for Microsoft to make changes to the library.</span></span>

- <span data-ttu-id="61dff-109">Download en installeer de nieuwste versie van Carthage [hier](https://github.com/Carthage/Carthage/releases "Carthage download-URL")</span><span class="sxs-lookup"><span data-stu-id="61dff-109">Download and install the latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="61dff-110">Maken van de toepassing</span><span class="sxs-lookup"><span data-stu-id="61dff-110">Creating your application</span></span>

1.  <span data-ttu-id="61dff-111">Open Xcode en selecteer`Create a new Xcode project`</span><span class="sxs-lookup"><span data-stu-id="61dff-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="61dff-112">Selecteer `iOS`  >  `Single view Application` en klik op *volgende*</span><span class="sxs-lookup"><span data-stu-id="61dff-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="61dff-113">Geef een productnaam en klik op *volgende*</span><span class="sxs-lookup"><span data-stu-id="61dff-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="61dff-114">Selecteer een map voor het maken van uw app en klik op *maken*</span><span class="sxs-lookup"><span data-stu-id="61dff-114">Select a folder to create your app and click *Create*</span></span>

## <a name="build-the-msal-framework"></a><span data-ttu-id="61dff-115">Het Framework MSAL bouwen</span><span class="sxs-lookup"><span data-stu-id="61dff-115">Build the MSAL Framework</span></span>

<span data-ttu-id="61dff-116">Volg de instructies hieronder om te halen en vervolgens de nieuwste versie van Carthage MSAL bibliotheken maken:</span><span class="sxs-lookup"><span data-stu-id="61dff-116">Follow the instructions below to pull and then build the latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="61dff-117">Open de terminal bash en Ga naar de hoofdmap van de App</span><span class="sxs-lookup"><span data-stu-id="61dff-117">Open the bash terminal and go to the App’s root folder</span></span>
2.  <span data-ttu-id="61dff-118">Kopieer de hieronder en plak in de terminal bash een 'Cartfile'-bestand te maken:</span><span class="sxs-lookup"><span data-stu-id="61dff-118">Copy the below and paste in the bash terminal to create a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="61dff-119">Kopieer en plak de onderstaande.</span><span class="sxs-lookup"><span data-stu-id="61dff-119">Copy and paste the below.</span></span> <span data-ttu-id="61dff-120">Met deze opdracht haalt afhankelijkheden in een map Carthage/opdrachten om uitchecken en vervolgens maakt de MSAL-bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="61dff-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds the MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="61dff-121">Het proces dat hierboven wordt gebruikt om te downloaden en bouwen van de Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="61dff-121">The process above is used to download and build the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="61dff-122">MSAL verwerkt ophalen, opslaan in cache en vernieuwen van gebruikerstokens gebruikt voor toegang tot API's die zijn beveiligd door de Azure Active Directory-v2.</span><span class="sxs-lookup"><span data-stu-id="61dff-122">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by the Azure Active Directory v2.</span></span>

## <a name="add-the-msal-framework-to-your-application"></a><span data-ttu-id="61dff-123">Het framework MSAL aan uw toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="61dff-123">Add the MSAL framework to your application</span></span>
1.  <span data-ttu-id="61dff-124">Open in Xcode, de `General` tabblad</span><span class="sxs-lookup"><span data-stu-id="61dff-124">In Xcode, open the `General` tab</span></span>
2.  <span data-ttu-id="61dff-125">Ga naar de `Linked Frameworks and Libraries` sectie en klikt u op`+`</span><span class="sxs-lookup"><span data-stu-id="61dff-125">Go to the `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="61dff-126">Selecteer `Add other…`</span><span class="sxs-lookup"><span data-stu-id="61dff-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="61dff-127">Selecteer: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` en klik op *Open*.</span><span class="sxs-lookup"><span data-stu-id="61dff-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="61dff-128">U ziet `MSAL.framework` toegevoegd aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="61dff-128">You should see `MSAL.framework` added to the list.</span></span>
5.  <span data-ttu-id="61dff-129">Ga naar `Build Phases` tabblad en klik op `+` pictogram kiezen`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="61dff-129">Go to `Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="61dff-130">Voeg de volgende inhoud naar de *gebied script*:</span><span class="sxs-lookup"><span data-stu-id="61dff-130">Add the following contents to the *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="61dff-131">Het volgende toevoegen aan <code>Input Files</code> door te klikken op <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="61dff-131">Add the following to <code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="61dff-132">Maken van de gebruikersinterface van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="61dff-132">Creating your application’s UI</span></span>
<span data-ttu-id="61dff-133">Een bestand Main.storyboard moet automatisch worden gemaakt als onderdeel van uw project-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="61dff-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="61dff-134">Volg de onderstaande instructies voor het maken van de gebruikersinterface van de app:</span><span class="sxs-lookup"><span data-stu-id="61dff-134">Follow the instructions below to create the app UI:</span></span>

1.  <span data-ttu-id="61dff-135">Control + klik `Main.storyboard` online zetten van het contextafhankelijke menu en klik vervolgens op:`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="61dff-135">Control+click `Main.storyboard` to bring up the contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="61dff-136">Vervang de `<scenes>` knooppunt met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="61dff-136">Replace the `<scenes>` node with the code below:</span></span>

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
