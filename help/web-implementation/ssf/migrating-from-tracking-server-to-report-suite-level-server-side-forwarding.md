---
title: Migrera från spårningsserver till rapportservervidarebefordran på servernivå
description: I den här artikeln och videon visas hur du aktiverar vidarebefordran av analysdata på serversidan till Audience Manager på rapportsvitnivå i stället för på en spårningsservernivå.
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
source-git-commit: 4b91696f840518312ec041abdbe5217178aee405
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Migrerar från [!UICONTROL Tracking Server] till [!UICONTROL Report Suite]-nivå [!UICONTROL Server-Side Forwarding] {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

I den här artikeln och videon visas hur du aktiverar [!UICONTROL server-side forwarding] av [!DNL Analytics]-data till Audience Manager på [!UICONTROL report suite]-nivå i stället för på [!UICONTROL tracking server]-nivå.

## Introduktion {#introduction}

Om du har Adobe Audience Manager OCH Adobe Analytics kan du implementera [!UICONTROL Server-side Forwarding] av [!DNL Analytics]-data för Audience Manager. Det innebär att i stället för att din sida skickar 2 träffar (en till [!DNL Analytics] och en till Audience Manager) kan den skicka en träff till [!DNL Analytics], och [!DNL Analytics] vidarebefordrar dessa data till Audience Manager. Om du redan har detta igång och har det aktiverat/implementerat före oktober 2017 kan din [!UICONTROL server-side forwarding] vara baserad på ditt [!UICONTROL Tracking Server], som måste aktiveras av Adobe kundtjänst eller Adobe Consulting. Från och med oktober 2017 kan du nu konfigurera [!UICONTROL server-side forwarding] själv och göra det på [!UICONTROL Report Suite]-nivå (vidarebefordrar PER [!UICONTROL Report Suite]). Det finns viktiga fördelar med detta, som diskuteras nedan.

## [!UICONTROL Tracking Server] Vidarebefordra {#tracking-server-forwarding}

Din [!UICONTROL tracking server] är den plats dit du skickar dina [!DNL Analytics]-data, samt den domän där bildbegäran och cookie-filen skrivs. Den ska ställas in i DTM eller [!DNL Experience Platform Launch], eller i filen [!DNL AppMeasurement.js], och ska vanligtvis se ut så här, och din webbplats eller ditt företagsnamn ska ersätta &quot;mysite&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Om [!UICONTROL server-side forwarding] är inställt för att vidarebefordra på [!UICONTROL tracking server]-nivå vidarebefordras alla träffar som skickas till denna [!UICONTROL tracking server] (OM även Experience Cloud ID-tjänsten är aktiverad) till Audience Manager. Detta måste möjliggöras av Adobe kundtjänst eller Adobe Consulting. Det är också de som kan inaktivera det, EFTER att du har växlat över till [!UICONTROL report suite]-vidarebefordran enligt beskrivningen nedan.

Om du är osäker på om [!DNL tracking server forwarding] är aktiverat för dig kan du kontakta Adobe kundtjänst eller Adobe Consulting och de bör kunna meddela dig.

## [!UICONTROL Report Suite]-Level  [!UICONTROL Server-Side Forwarding] {#report-suite-level-server-side-forwarding}

En av de största fördelarna med att övergå till [!UICONTROL report suite]-vidarebefordran från [!UICONTROL tracking server] är att du nu kan använda &quot;Audience Analytics&quot;, vilket är möjligheten att vidarebefordra Audience Manager [!UICONTROL segments] tillbaka till Adobe Analytics för en detaljerad [!UICONTROL segment]-analys. Denna fantastiska funktion stöds INTE om du fortfarande vidarebefordrar [!UICONTROL tracking server] och inte [!UICONTROL report suite]. Mer information om Audience Analytics finns i [dokumentationen](https://marketing.adobe.com/resources/help/en_US/analytics/audiences/).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Viktigt tips {#additional-resources}

Som framgår av videon ovan bör du, när du har alla [!UICONTROL report suites] som du vill vidarebefordra till Audience Manager, kontakta Adobe kundtjänst eller Adobe Consulting och be dem inaktivera vidarebefordran av [!UICONTROL tracking server]. Du behöver inte göra detta eftersom både [!UICONTROL tracking server]-vidarebefordran och [!UICONTROL report suite]-vidarebefordran INTE leder till dubbla träffar. Det är dock bäst att endast ha [!UICONTROL report suite] vidarebefordring aktiverat. Om du låter [!UICONTROL tracking server] vidarebefordra kanske det inte bara vidarebefordrar data från [!UICONTROL report suites] som du inte vill vidarebefordra, utan när du (och alla på ditt företag) har glömt att [!UICONTROL tracking server]-vidarebefordran är aktiverad, kanske du tror att data inte vidarebefordras för en viss [!UICONTROL report suite] (eftersom den inte är aktiverad på rapportsvitnivå), men informationen vidarebefordras ändå på grund av att [!UICONTROL tracking server]. Sedan kommer du att slösa tid och pengar på att ta reda på varför det vidarebefordras och även betala för AAM serversamtal som du inte hade väntat dig. Därför är det bara en bra idé att inaktivera [!UICONTROL tracking server]-vidarebefordran så snart du har alla [!UICONTROL report suites] som är inställda att vidarebefordra och som passar ditt företags behov.
