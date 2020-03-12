---
description: Du kan välja att använda standardbeteenden för annonser.
seo-description: Du kan välja att använda standardbeteenden för annonser.
seo-title: Använd standardbeteendet för uppspelning
title: Använd standardbeteendet för uppspelning
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Använd standardbeteendet för uppspelning{#use-the-default-playback-behavior}

Du kan välja att använda standardbeteenden för annonser.

Så här använder du standardbeteenden:

    * Om du implementerar en egen ContentFactory-klass returnerar du en ny instans av DefaultAdPolicySelector i din implementering av doRetrieveAdPolicySelector.
    
    &quot;
    public class CustomContentFactory extends ContentFactory {
    
    //...
    // din egen kod för annonsklasser
    //...
    
    /**
    * @inheritDoc
    */
    override protected
    functionRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector {
    return new DefaultAdPolicySelector(item);
    }
    &quot;
    
    
    * Om du inte har en anpassad implementering för klassen&quot;ContentFactory&quot;, TVSDK K använder &quot;DefaultAdPolicySelector&quot;.