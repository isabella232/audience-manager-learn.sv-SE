---
title: Migrera från spårningsserver till vidarebefordran på servernivå på rapportnivå
description: Lär dig hur du aktiverar vidarebefordran av Adobe Analytics-data på serversidan till Audience Manager på en rapportsvitnivå i stället för på en spårningsservernivå.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Migrera från spårningsserver till vidarebefordran på servernivå på rapportnivå {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

I den här artikeln och videon visas hur du aktiverar vidarebefordran på serversidan av [!DNL Analytics] Data till Audience Manager vid [!UICONTROL report suite] i stället för på en [!UICONTROL tracking server] nivå.

## Introduktion {#introduction}

Om du har Adobe Audience Manager OCH Adobe Analytics kan du implementera vidarebefordran på serversidan av [!DNL Analytics] data till Audience Manager. Det innebär att i stället för att sidan skickar två träffar (ett till [!DNL Analytics] och en till Audience Manager) kan den skicka en träff till [!DNL Analytics]och [!DNL Analytics] kommer att vidarebefordra dessa data till Audience Manager.

Om du redan har detta igång och har det aktiverat/implementerat före oktober 2017 kan vidarebefordran på serversidan vara baserad på din [!UICONTROL Tracking Server]som måste aktiveras av Adobe kundtjänst eller Adobe Consulting. Från och med oktober 2017 kan du nu konfigurera vidarebefordran på serversidan själv och göra det på rapportsvitnivå (vidarebefordran per rapportserie). Det finns viktiga fördelar med detta, som diskuteras nedan.

## [!UICONTROL Tracking server] vidarebefordran {#tracking-server-forwarding}

Dina [!UICONTROL tracking server] är platsen dit du skickar din [!DNL Analytics] data, och även den domän där bildbegäran och cookie-filen skrivs. Den ska ställas in i DTM eller [!DNL Experience Platform Launch]eller i [!DNL AppMeasurement.js] och ser ut så här, då din webbplats eller ditt företagsnamn ersätter &quot;minwebbplats&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Om vidarebefordran på serversidan är konfigurerad att vidarebefordras på [!UICONTROL tracking server] nivå, alla träffar som skickas till den här [!UICONTROL tracking server] (OM även Experience Cloud ID-tjänsten är aktiverad) kommer att vidarebefordras till Audience Manager. Detta måste möjliggöras av Adobe kundtjänst eller Adobe Consulting. Det är också de som kan inaktivera det, EFTER att du har växlat till [!UICONTROL report suite] vidarebefordran enligt beskrivningen nedan.

Om du är osäker [!DNL tracking server forwarding] är aktiverat för dig, kontakta Adobe kundtjänst eller Adobe Consulting och de bör kunna tala om det för dig.

## [!UICONTROL Report-suite]-Nivå vidarebefordring på serversidan {#report-suite-level-server-side-forwarding}

En av de största fördelarna med att gå över till [!UICONTROL report suite] vidarebefordra från [!UICONTROL tracking server] vidarebefordran är att du nu kommer att kunna använda &quot;Audience Analytics&quot;, vilket är möjligheten att vidarebefordra Audience Manager [!UICONTROL segments] tillbaka till Adobe Analytics för detaljerad segmentanalys. Den här suveräna funktionen stöds INTE om du fortfarande är på [!UICONTROL tracking server] vidarebefordra och inte [!UICONTROL report suite] vidarebefordran. Mer information om Audience Analytics finns i [dokumentation](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Viktigt tips {#additional-resources}

Så som anges i videon ovan har du alla [!UICONTROL report suites] Vill du vidarebefordra till Audience Manager ska du kontakta Adobe kundtjänst eller Adobe Consulting och inaktivera [!UICONTROL tracking server] vidarebefordran. Det är inte akut för dig att göra detta, för att ha båda [!UICONTROL tracking server] vidarebefordran och [!UICONTROL report suite] vidarebefordran resulterar inte i dubbla träffar. Det är dock bäst att endast ha [!UICONTROL report suite] vidare.

Om du går [!UICONTROL tracking server] vidarebefordra vidare, kan inte bara vidarebefordra data från [!UICONTROL report suites] att du inte vill vidarebefordras, men i framtiden, efter att du (och alla på ditt företag) har glömt att [!UICONTROL tracking server] vidarebefordran är aktiverat, du kanske tror att data inte vidarebefordras för en viss [!UICONTROL report suite]. Detta beror på att den inte är aktiverad på rapportsvitnivå, men data vidarebefordras ändå på grund av [!UICONTROL tracking server]. Sedan kommer du att slösa tid och pengar på att ta reda på varför det vidarebefordras och även betala för AAM serversamtal som du inte hade väntat dig. Därför är det en bra idé att inaktivera [!UICONTROL tracking server] vidarebefordran så snart du har alla [!UICONTROL report suites] är redo att utveckla som passar era affärsbehov.
