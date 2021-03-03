---
title: Använda bästa praxis SPA sidor när data skickas till AAM
description: I det här dokumentet beskriver vi flera bästa metoder som du bör följa och vara medveten om när du skickar data från Single Page Applications (SPA) till Adobe Audience Manager (AAM). Det här dokumentet fokuserar på att använda Launch by Adobe, vilket är den rekommenderade implementeringsmetoden.
feature: Implementeringsgrunder
topics: spa
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1390
topic: SPA
role: '"Utvecklare, datatekniker"'
level: Erfaren
translation-type: tm+mt
source-git-commit: a7dc335e75697a7b1720eccdadbb9605fdeda798
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# Använda bästa praxis på SPA sidor när data skickas till AAM {#using-best-practices-on-spa-pages-when-sending-data-to-aam}

I det här dokumentet beskriver vi flera metodtips som du bör följa och vara medveten om när du skickar data från [!UICONTROL Single Page Applications] (SPA) till Adobe Audience Manager (AAM). Det här dokumentet fokuserar på att använda [!UICONTROL Experience Platform Launch], vilket är den rekommenderade implementeringsmetoden.

## Inledande anteckningar

* Objekten nedan förutsätter att du använder [!DNL Platform Launch] för att implementera på din webbplats. Tänk på detta om du inte använder [!DNL Platform Launch], men du måste anpassa dem till din implementeringsmetod.
* Alla SPA är olika, så du kan behöva justera några av följande saker för att bäst uppfylla dina behov, men vi ville dela några av de bästa metoderna med dig: saker som du behöver tänka på när du skickar data från SPA sidor till Audience Manager.

## Enkelt diagram över att arbeta med SPA och AAM i Experience Platform Launch {#simple-diagram-of-working-with-spas-and-aam-in-experience-platform-launch}

![spa for aam in  [!DNL launch]](assets/spa_for_aam_in_launch.png)

>[!NOTE]
>Detta är som sagt ett förenklat diagram över hur SPA sidor hanteras i en Adobe Audience Manager-implementering (utan Adobe Analytics) med [!DNL Platform Launch]. Som du ser är det ganska rakt framåt, och det stora beslutet är hur du ska kommunicera en vyändring (eller en åtgärd) till [!DNL Platform Launch].

## Startar [!DNL Launch] från SPA {#triggering-launch-from-the-spa-page}

Två av de vanligaste metoderna för att aktivera en regel i [!DNL Platform Launch] (och därmed skicka data till Audience Manager) är:

* Ställa in anpassade JavaScript-händelser (se exempel [HERE](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html) med Adobe Analytics)
* Använda en [!UICONTROL Direct Call Rule]

I det här Audience Manager-exemplet ska vi använda en [!UICONTROL Direct Call rule] i [!DNL Launch] för att utlösa träffen som går in i Audience Manager. Som du kommer att se i nästa avsnitt blir detta verkligen användbart genom att ställa in [!UICONTROL Data Layer] på ett nytt värde, så att det kan hämtas av [!UICONTROL Data Element] i [!DNL Platform Launch].

## Demonstrationssida {#demo-page}

Vi har skapat en liten demosida som visar hur du ändrar ett värde i [!DNL data layer] och skickar den till AAM, som du kan göra på en SPA. Den här funktionen kan utformas för mer komplicerade ändringar. Du hittar den här demosidan [HÄR](https://aam.enablementadobe.com/SPA-Launch.html).

## Ange [!DNL data layer] {#setting-the-data-layer}

När nytt innehåll läses in på sidan eller när någon utför en åtgärd på webbplatsen måste [!DNL data layer] ställas in dynamiskt i sidhuvudet INNAN [!DNL Launch] anropas och kör [!UICONTROL rules], så att [!DNL Platform Launch] kan hämta de nya värdena från [!DNL data layer] och överföra dem till Audience Manager.

Om du går till demowebbplatsen som listas ovan och tittar på sidkällan ser du:

* [!DNL data layer] är i sidhuvudet, före anropet till [!DNL Platform Launch]
* JavaScript i den simulerade SPA-länken ändrar [!UICONTROL Data Layer] och anropar SEDAN [!DNL Platform Launch] (anropet _satellit.track()). Om du använde anpassade JavaScript-händelser i stället för [!UICONTROL Direct Call Rule] är lektionen densamma. Ändra först [!DNL data layer] och ring sedan [!DNL Launch].

>[!VIDEO](https://video.tv.adobe.com/v/23322/?quality=12)

## Ytterligare resurser {#additional-resources}

* [SPA om Adobe forum](https://forums.adobe.com/thread/2451022)
* [Referensarkitektursajter som visar hur man implementerar SPA i Launch by Adobe](https://helpx.adobe.com/experience-manager/kt/integration/using/launch-reference-architecture-SPA-tutorial-implement.html)
* [Använda vedertagna metoder för att spåra SPA i Adobe Analytics](https://helpx.adobe.com/analytics/kt/using/spa-analytics-best-practices-feature-video-use.html)
* [Demo-webbplats som används för den här artikeln](https://aam.enablementadobe.com/SPA-Launch.html)
