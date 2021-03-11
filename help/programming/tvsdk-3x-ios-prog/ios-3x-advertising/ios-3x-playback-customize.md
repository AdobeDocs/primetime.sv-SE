---
description: När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.
title: Anpassa uppspelning med annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---


# Anpassa uppspelningen med annonser {#customize-playback-with-ads}

När uppspelningen når en annonsbrytning, skickar en annonsbrytning eller slutar i en annonsbrytning definierar TVSDK ett standardbeteende för positionen av det aktuella spelhuvudet.

>[!TIP]
>
>Du kan åsidosätta standardbeteendet genom att använda klassen `PTAdPolicySelector`.

Standardbeteendet varierar beroende på om användaren skickar annonsbrytningen under den normala uppspelningen eller söker i en video.

Du kan anpassa beteendet för annonsuppspelning på följande sätt:

* Spara positionen där användaren slutade titta på videon och återuppta uppspelningen på samma plats i en framtida session.
* Om en annonsbrytning visas för användaren visar du inga ytterligare annonser under ett antal minuter, även om användaren söker efter en ny position.
* Om innehållet inte kan spelas upp efter några minuter startar du om strömmen eller växlar om till en annan källa för samma innehåll.

   För att användaren ska kunna hoppa över annonser och återuppta den tidigare misslyckade positionen kan du inaktivera pre-roll- och/eller middle-roll-annonser under redundansuppspelningssessionen. TVSDK tillhandahåller metoder för att aktivera hoppning av annonser före och efter rullning.

## API-element för annonsuppspelning {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK innehåller klasser och metoder som du kan använda för att anpassa uppspelningsbeteendet för innehåll som innehåller reklam.
Följande API-element är användbara för att anpassa uppspelning:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>API-element</b></th> 
   <th colname="col2" class="entry"><b>Innehåll som stöder reklam</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata  </span> </td> 
   <td colname="col2"> Ange om en annonsbrytning ska markeras som bevakad av en tittare och, om ja, när den ska markeras. Ange och hämta den bevakade profilen med egenskapen <span class="codeph"> ochBreakAsWatched </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector  </span> </td> 
   <td colname="col2"> Protokoll som tillåter anpassning av TVSDK:s annonsbeteende. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> En klass som implementerar TVSDK-standardbeteendet. Programmet kan åsidosätta den här klassen för att anpassa standardbeteendena utan att implementera hela gränssnittet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer  </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime  </span>. <p>Detta är den lokala tidpunkten för uppspelningen, exklusive de monterade annonsbrytningarna. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime  </span> . <p>Här sker sökningen i förhållande till en lokal tid i strömmen. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime  </span>. <p>Den virtuella positionen på tidslinjen konverteras till den lokala positionen. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak  </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched,  </span> egenskap. Anger om tittaren har tittat på annonsen. </td> 
  </tr> 
 </tbody> 
</table>

## Konfigurera anpassad uppspelning {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Innan du kan anpassa eller åsidosätta annonsbeteenden måste du registrera annonspolicyinstansen med TVSDK.

Gör något av följande om du vill anpassa annonsbeteenden:

* Följ protokollet `PTAdPolicySelector` och implementera alla nödvändiga metoder för principval.

   Det här alternativet rekommenderas om du behöver åsidosätta **alla** standardbeteendena för annonser.

* Åsidosätt klassen `PTDefaultAdPolicySelector` och tillhandahåll implementeringar för endast de beteenden som kräver anpassning.

   Det här alternativet rekommenderas om du bara behöver åsidosätta **vissa** av standardbeteendena.

Utför följande uppgifter för båda alternativen:

1. Registrera principinstansen som ska användas av TVSDK via klientfabriken.

   >[!NOTE]
   >
   >Anpassade annonsprinciper som registreras i början av uppspelningen rensas när `PTMediaPlayer`-instansen avallokeras. Programmet måste registrera en principväljarinstans varje gång en ny uppspelningssession skapas.

   Exempel:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementera dina anpassningar.

## Hoppa över annonsbrytningar under en tidsperiod {#section_99809BE4D9BB4DEEBBF596C746CA428A}

Som standard tvingar TVSDK en annonsbrytning att spelas upp när användaren söker över en annonsbrytning. Du kan anpassa beteendet för att hoppa över en annonsbrytning om tiden som gått från en tidigare avbruten brytning är inom ett visst antal minuter.

>[!IMPORTANT]
>
>När det finns en intern sökning att hoppa över en annons kan det finnas en liten paus i uppspelningen.

Följande exempel på en anpassad annonsprincipväljare hoppar över annonser inom de kommande fem minuterna (väggklocka) efter att en användare har tittat på en annonsbrytning.

1. Registrera principinstansen som ska användas av TVSDK via klientfabriken.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementera er anpassning.

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## Spara videopositionen och återuppta den senare {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Du kan spara den aktuella uppspelningspositionen i en video och återuppta uppspelningen på samma plats i en framtida session.

Annonser som infogats dynamiskt skiljer sig mellan användarsessioner, så om du sparar positionen **med** delade annonser refererar till en annan position i en framtida session. TVSDK innehåller metoder för att hämta uppspelningspositionen samtidigt som delade annonser ignoreras.

1. När användaren avslutar en video hämtas och sparas positionen i videon.

   >[!TIP]
   >
   >Annonslängder ingår inte.

   Annonsbrytningar kan variera mellan olika sessioner på grund av annonsmönster, frekvensbegränsning och så vidare. Den aktuella tidpunkten för videon i en session kan vara annorlunda i en framtida session. När du sparar en position i videon hämtar programmet den lokala tiden. Använd egenskapen `localTime` för att läsa den här positionen, som du kan spara på enheten eller i en databas på servern.

   Om användaren till exempel är på den 20:e minuten av videon, och den här positionen innehåller fem minuters annonser, är `currentTime` 1200 sekunder, medan `localTime` vid den här positionen är 900 sekunder.

   >[!IMPORTANT]
   >
   >Lokal tid och aktuell tid är samma för live/linjära strömmar. I det här fallet har `convertToLocalTime` ingen effekt. För VOD ändras inte lokal tid medan annonser spelas upp.

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. Använd `seekToLocalTime` om du vill återuppta videon på samma plats som den som sparades från föregående session.

   >[!TIP]
   >
   >Den här metoden anropas bara med lokala tidsvärden. Om metoden anropas med aktuella tidsresultat inträffar ett felaktigt beteende.

   Använd `seekToTime` om du vill söka till aktuell tid.

1. När ditt program tar emot händelsen `PTMediaPlayerStatusReady` för statusändring söker du efter den sparade lokala tiden.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Ange annonsbrytningarna som de anges i annonsprincipgränssnittet.
1. Implementera en anpassad annonsprincipväljare genom att utöka standardväljaren för annonsprinciper.
1. Ange de annonsbrytningar som måste presenteras för användaren genom att implementera `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Den här metoden innehåller en annonsbrytning före rullning och annonsen i mitten av rullen bryts före den lokala tidspositionen. Ditt program kan bestämma sig för att spela upp en annonsbrytning i förväg och återuppta den angivna lokala tiden, spela upp en annonsbrytning i mellanrummet och återuppta den angivna lokala tiden eller spela upp inga annonsbrytningar.