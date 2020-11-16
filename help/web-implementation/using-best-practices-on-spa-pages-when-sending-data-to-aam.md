---
title: Använda bästa praxis SPA sidor när data skickas till AAM
description: I det här dokumentet beskriver vi flera bästa metoder som du bör följa och vara medveten om när du skickar data från Single Page Applications (SPA) till Adobe Audience Manager (AAM). Det här dokumentet fokuserar på att använda Launch by Adobe, vilket är den rekommenderade implementeringsmetoden.
feature: implementation basics
topics: spa
audience: implementer
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
translation-type: tm+mt
source-git-commit: a108c51fdad66f4e7974eb96609b6d8f058cb6ff
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Använda bästa praxis SPA sidor när data skickas till AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

I det här dokumentet beskriver vi flera bästa metoder som du bör följa och vara medveten om när du skickar data från [!UICONTROL Single Page Applications] (SPA) till Adobe Audience Manager (AAM). Det här dokumentet fokuserar på att använda [!UICONTROL Experience Platform Launch], vilket är den rekommenderade implementeringsmetoden.

## Inledande anteckningar

* Objekten nedan förutsätter att du använder [!DNL Platform Launch] för implementering på din webbplats. Övervägandena finns fortfarande kvar om du inte använder [!DNL Platform Launch]dem, men du måste anpassa dem till din implementeringsmetod.
* Alla SPA är olika, så du kan behöva ändra några av följande saker för att bäst uppfylla dina behov, men vi ville dela några av de bästa metoderna med dig: saker som du behöver tänka på när du skickar data från SPA sidor till Audience Manager.

## Enkelt diagram över att arbeta med SPA och AAM i Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa for aam in [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Detta är som sagt en förenklad bild av hur SPA hanteras i en Adobe Audience Manager-implementering (utan Adobe Analytics) med [!DNL Platform Launch]. Som du ser är det ganska rakt fram, och det stora beslutet är hur du ska förmedla en vyändring (eller en åtgärd) till [!DNL Platform Launch].

## Startar [!DNL Launch] från SPA {#triggering-launch-from-the-spa-page}

Två av de vanligaste metoderna för att aktivera en regel i [!DNL Platform Launch] (och därmed skicka data till Audience Manager) är:

* Ställa in anpassade JavaScript-händelser (se exempel [HERE](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) med Adobe Analytics)
* Använda en [!UICONTROL Direct Call Rule]

I det här Audience Manager-exemplet kommer vi att använda en [!UICONTROL Direct Call rule] in [!DNL Launch] för att utlösa träffen i Audience Manager. Som du kommer att se i nästa avsnitt blir det här mycket användbart genom att ställa in värdet [!UICONTROL Data Layer] på ett nytt, så att det kan hämtas upp av [!UICONTROL Data Element] i [!DNL Platform Launch].

## Demo-sida {#demo-page}

Vi har skapat en liten demosida som demonstrerar hur du ändrar ett värde i [!DNL data layer] och skickar den till AAM, som du kan göra på en SPA. Den här funktionen kan utformas för mer komplicerade ändringar. Den här demosidan hittar du [här](https://aam.enablementadobe.com/SPA-Launch.html).

## Ange [!DNL data layer] {#setting-the-data-layer}

När nytt innehåll läses in på sidan eller när någon utför en åtgärd på webbplatsen måste det, som nämnts, ställas in dynamiskt i sidhuvudet BEFORE [!DNL data layer] anropas och körs [!DNL Launch] , så att de nya värdena kan hämtas från [!UICONTROL rules][!DNL Platform Launch] [!DNL data layer] och överföras till Audience Manager.

Om du går till demowebbplatsen som listas ovan och tittar på sidkällan ser du:

* Sidhuvudet [!DNL data layer] är före anropet till [!DNL Platform Launch]
* JavaScript-koden i den simulerade SPA-länken ändrar [!UICONTROL Data Layer]anropet och sedan anropet [!DNL Platform Launch] (). Om du använde anpassade JavaScript-händelser i stället för detta [!UICONTROL Direct Call Rule]är lektionen densamma. Ändra först [!DNL data layer]och ring sedan [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Additional Resources {#additional-resources}

* [SPA om Adobe forum](https://forums.adobe.com/thread/2451022)
* [Referensarkitektursajter som visar hur man implementerar SPA i Launch by Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Använda vedertagna metoder för att spåra SPA i Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Demo-webbplats som används för den här artikeln](https://aam.enablementadobe.com/SPA-Launch.html)
