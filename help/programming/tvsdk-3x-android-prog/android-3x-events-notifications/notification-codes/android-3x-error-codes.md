---
title: PSDK-felkoder
description: Information om olika felkoder, varningar och inbyggda felkoder.
translation-type: tm+mt
source-git-commit: eddc327087411a6214cfd8dafef66b850a603f97

---


# PSDK-felkoder {#psdk-error-codes}

Läs vidare för att få information om PSDK-felkoder, varningar och inbyggda felkoder.

## Fel

Följande tabell innehåller detaljerad information om meddelanden om ERROR-typer. De flesta fel innehåller relevanta metadata. till exempel URL för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1">
  <tr> 
   <th><b>PSDK-felnamn</b></th>
   <th><b>PSDK-felkod</b></th>
   <th><b>Beskrivning</b></th>
  </tr>
  <tr>
    <td>LYCKADES</td>
    <td>0</td>
    <td>Åtgärden som utfördes av det underliggande API:t har slutförts.</td>
  </tr>
  <tr>
    <td>INVALID_ARGUMENT</td>
    <td>1</td>
    <td>Data eller format för argument som har angetts för underliggande API är ogiltiga.</td>
  </tr>
  <tr>
    <td>NULL_POINTER</td>
    <td>2</td>
    <td>Ett av argumenten som skickades är NULL eller så initierades inte en av de interna medlemmarna.</td>
  </tr>
  <tr>
    <td>ILLEGAL_STATE</td>
    <td>3</td>
    <td>Åtgärden stöds inte i det aktuella spelarläget.</td>
  </tr>
  <tr>
    <td>INTERFACE_NOT_FOUND</td>
    <td>4</td>
    <td>Metoden interfaceCast genererar det här felet när det begärda gränssnittet inte implementeras/ärvs av det här.</td>
  </tr>
  <tr>  
    <td>CREATION_FAILED</td>
    <td>5</td>
    <td>Det gick inte att skapa en av de interna resurserna.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_OPERATION</td>
    <td>6</td>
    <td>Den begärda åtgärden stöds för närvarande inte.</td>
  </tr>
  <tr>
    <td>DATA_NOT_AVAILABLE</td>
    <td>7</td>
    <td>Begärda data är för närvarande inte tillgängliga.</td>
  </tr>
  <tr>
    <td>SEEK_ERROR</td>
    <td>8</td>
    <td>Ett fel uppstod när en sökåtgärd utfördes.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_FEATURE</td>
    <td>9</td>
    <td>Den här funktionen/funktionen stöds inte.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>10</td>
    <td>Det angivna värdet ligger utanför intervallet.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>11</td>
    <td>Den angivna strömmens ljud-/videokodek stöds inte av TVSDK eller den underliggande enheten.</td>
  </tr>
  <tr>
    <td>MEDIA_ERROR</td>
    <td>12</td>
    <td>Det angivna mediet hittades inte.</td>
  </tr>
  <tr>
    <td>NETWORK_ERROR</td>
    <td>13</td>
    <td>Ett fel uppstod vid hämtning av ett fragment eller segment (både video och ljud).</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>14</td>
    <td>Allmän felhändelse. Inte utfärdat av TVSDK. Detta är bara en markör för slutet av det numeriska kodsintervall som motsvarar TVSDK-felhändelser.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>15</td>
    <td>Den angivna söktiden är ogiltig.</td>
  </tr>
  <tr>
    <td>AUDIO_TRACK_ERROR</td>
    <td>16</td>
    <td>Ett fel relaterat till ett ljudspår uppstod (alternativt ljud)</td>
  </tr>
  <tr>
    <td>ACCESS_FROM_DIFFERENT_THREAD</td>
    <td>17</td>
    <td>PSDK API anropas från en annan tråd än den tråd i vilken PSDK initierades.</td>
  </tr>
  <tr>
    <td>ELEMENT_NOT_FOUND</td>
    <td>18</td>
    <td>Det gick inte att hitta elementet.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>19</td>
    <td>Funktionen är inte implementerad.</td>
  </tr>
  <tr>
    <td>PRE_ROLL_DISABLED</td>
    <td>20</td>
    <td>Förhandsgranskningen har inaktiverats via AdvertisingMetadata.</td>
  </tr>
  <tr>
    <td>PLAYBACK_NOT_AUTHZED</td>
    <td>57</td>
    <td>HLS-uppspelning har inte aktiverats i Flash Player. Se AuthorizedFeatures.enableMediaPlayerHLSPlayback().</td>
  </tr>
  <tr>
    <td>NETWORK_TIMEOUT</td>
    <td>58</td>
    <td>Nätverkstimeout uppstod när en resurs/anslutningsserver hämtades.</td>
  </tr>
</table>

## Varningar

Följande tabell innehåller detaljerad information om WARN-typmeddelanden.
De flesta varningar innehåller relevanta metadata. URL:en till den resurs som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Felnamn</b></th>
    <th><b>Code</b></th>
    <th><b>Beskrivning</b></th>
  </tr>
  <tr>
    <td>PLAYBACK_OPERATION_FAILED</td>
    <td>200</td>
    <td>Ett fel uppstod under uppspelningen. En uppspelningsrelaterad åtgärd misslyckades</td>
  </tr>
  <tr>  
    <td>NATIVE_WARNING</td>
    <td>201</td>
    <td>Ett fel uppstod i AVE-biblioteket på låg nivå.</td>
  </tr>
  <tr>
    <td>AD_RESOLVER_FAILED</td>
    <td>202</td>
    <td>Det gick inte att matcha annonser med plugin-programmet för annonser.</td>
  </tr>
  <tr>
    <td>AD_MANIFEST_LOAD_FAILED</td>
    <td>203</td>
    <td>Det gick inte att läsa in Ad-manifestet.</td>
  </tr>
  <tr>
    <td>AD_RESOLUTION_IN_PROGRESS</td>
    <td>204</td>
    <td>Åtgärd för att lösa annonser pågår.</td>
  </tr>
  </table>

## Info

<table frame="all" colsep="1" rowsep="1">
  <tr> 
    <th><b>Felnamn</b></th>
    <th><b>Code</b></th>
    <th><b>Beskrivning</b></th>
  </tr>
  <tr>
    <td>REVENUE_OPTIMIZATION_REPORTING</td>
    <td>300</td>
    <td>TVSDK-detaljerade meddelanden för ytterligare rapportering och analys.</td>
  </tr>
 </table>

## Inbyggda felkoder

Video Encoder-gränssnittet i AVE returnerar dessa videouppspelningsmeddelanden i NATIVE_ERROR-metadataobjektet.

<table frame="all" colsep="1" rowsep="1">
  <tr>
    <th><b>Felnamn</b></th>
    <th><b>Code</b></th>
    <th><b>Beskrivning</b></th>
  </tr>
  <tr>  
    <td>END_OF_PERIOD</td>
    <td>-1</td>
    <td>Periodens slut.</td>
  </tr>
  <tr>
    <td>LYCKADES</td>
    <td>0</td>
    <td>Åtgärden lyckades.</td>
  </tr>
  <tr>
    <td>ASYNC_OPERATION_IN_PROGRESS</td>
    <td>1</td>
    <td>Asynkron åtgärd. Åtgärden har begärts. Information om lyckade/misslyckade åtgärder kommer att vara tillgänglig senare.</td>
  </tr>
  <tr>
    <td>EOF</td>
    <td>2</td>
    <td>Åtgärden är inte möjlig på grund av ett filslutsvillkor (EOF).</td>
  </tr>
  <tr>
    <td>DECODER_FAILED</td>
    <td>3</td>
    <td>Avkodaren misslyckades vid körning.</td>
  </tr>
  <tr>
    <td>DEVICE_OPEN_ERROR</td>
    <td>4</td>
    <td>Det gick inte att öppna maskinvaruavkodaren.</td>
  </tr>
  <tr>
    <td>FILE_NOT_FOUND</td>
    <td>5</td>
    <td>Resursen kan inte hittas.</td>
  </tr>
  <tr>
    <td>GENERIC_ERROR</td>
    <td>6</td>
    <td>Allmänt fel.</td>
  </tr>
  <tr>
    <td>IRRECOVERABLE_ERROR</td>
    <td>7</td>
    <td>Ett feltillstånd som videomotorn inte kan återställas från.</td>
  </tr>
  <tr>
    <td>LOST_CONNECTION_RECOVERABLE</td>
    <td>8</td>
    <td>Nätverksfel, försöker återställa.</td>
  </tr>
  <tr> 
    <td>NO_FIXED_SIZE</td>
    <td>9</td>
    <td>Resursens storlek kan inte bestämmas.</td>
  </tr>
  <tr>
    <td>NOT_IMPLEMENTED</td>
    <td>10</td>
    <td>Funktionen är inte implementerad.</td>
  </tr>
  <tr>
    <td>OUT_OF_MEMORY</td>
    <td>11</td>
    <td>Slut på minne.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR</td>
    <td>12</td>
    <td>Ett fel uppstod när mediefilen parsades.</td>
  </tr>
  <tr>  
    <td>SIZE_UNKNOWN</td>
    <td>13</td>
    <td>Resursen har en storlek, men är okänd.</td>
  </tr>
  <tr>  
    <td>UNDER_FLOW</td>
    <td>14</td>
    <td>Underflödesvillkor.</td>
  </tr>
  <tr> 
    <td>UNSUPPORTED_CONFIG</td>
    <td>15</td>
    <td>Konfigurationen stöds inte.</td>
  </tr>
  <tr>  
    <td>UNSUPPORTED_OPERATION</td>
    <td>16</td>
    <td>Åtgärden stöds inte.</td>
  </tr>
  <tr>
    <td>WAITING_FOR_INIT</td>
    <td>17</td>
    <td>Har inte initierats än.</td>
  </tr>
  <tr>  
    <td>INVALID_PARAMETER</td>
    <td>18</td>
    <td>Ogiltig parameter.</td>
  </tr>
  <tr>
    <td>INVALID_OPERATION</td>
    <td>19</td>
    <td>Åtgärden tillåts inte.</td>
  </tr>
  <tr>
    <td>OP_ONLY_ALLOWED_IN_PAUSED_STATE</td>
    <td>20</td>
    <td>Åtgärden tillåts endast när den pausas.</td>
  </tr>
  <tr> 
    <td>OP_INVALID_WITH_AUDIO_ONLY_FILE</td>
    <td>21</td>
    <td>Åtgärden kan inte användas på filer med enbart ljud.</td>
  </tr>
  <tr>
    <td>PREVIOUS_STEP_SEEK_IN_PROGRESS</td>
    <td>22</td>
    <td>Tidigare sökåtgärd pågår fortfarande.</td>
  </tr>
  <tr> 
    <td>SOURCE_NOT_SPECIFIED</td>
    <td>23</td>
    <td>Resursen har inte angetts.</td>
  </tr>
  <tr>
    <td>RANGE_ERROR</td>
    <td>24</td>
    <td>Det angivna värdet ligger utanför intervallet.</td>
  </tr>
  <tr>
    <td>INVALID_SEEK_TIME</td>
    <td>25</td>
    <td>Ogiltig söktid.</td>
  </tr>
  <tr>
    <td>FILE_STRUCTURE_INVALID</td>
    <td>26</td>
    <td>Den angivna filen överensstämmer inte med den förväntade syntaxen.</td>
  </tr>
  <tr>
    <td>COMPONENT_CREATION_FAILURE</td>
    <td>27</td>
    <td>Det gick inte att skapa en nödvändig komponent.</td>
  </tr>
  <tr>
    <td>DRM_INIT_ERROR</td>
    <td>28</td>
    <td>Det gick inte att skapa DRM-kontext.</td>
  </tr>
  <tr>
    <td>CONTAINER_NOT_SUPPORTED</td>
    <td>29</td>
    <td>Behållartypen stöds inte.</td>
  </tr>
  <tr>
    <td>SEEK_FAILED</td>
    <td>30</td>
    <td>Sökningen misslyckades.</td>
  </tr>
  <tr>
    <td>CODEC_NOT_SUPPORTED</td>
    <td>31</td>
    <td>Kodeken stöds inte.</td>
  </tr>
  <tr>
    <td>NETWORK_UNAVAILABLE</td>
    <td>32</td>
    <td>Nätverket är inte tillgängligt.</td>
  </tr>
  <tr>  
    <td>NETWORK_ERROR</td>
    <td>33</td>
    <td>Det gick inte att hämta data från nätverket.</td>
  </tr>
  <tr>
    <td>ÖVERFLÖDE</td>
    <td>34</td>
    <td>Spill.</td>
  </tr>
  <tr>  
    <td>VIDEO_PROFILE_NOT_SUPPORTED</td>
    <td>35</td>
    <td>Videoprofilen stöds inte.</td>
  </tr>
  <tr>
    <td>PERIOD_NOT_LOADED</td>
    <td>36</td>
    <td>Ett försök att utföra en åtgärd gjordes på en HOLD-period eller en period som ännu inte har lästs in.</td>
  </tr>
  <tr> 
    <td>INVALID_REPLACE_DURATION</td>
    <td>37</td>
    <td>Den angivna tidslängden för ersättning är ogiltig eller sträcker sig utanför strömmens slut.</td>
  </tr>
  <tr>
    <td>CALLED_FROM_WRONG_THREAD</td>
    <td>38</td>
    <td>API kan inte anropas från fel tråd. För det mesta för API-element som endast ska anropas från huvudtråden.</td>
  </tr>
  <tr>
    <td>FRAGMENT_READ_ERROR</td>
    <td>39</td>
    <td>Fragmentläsningsfel. Det finns ingen redundans. Motorn kommer att försöka läsa nästa fragment.</td>
  </tr>
  <tr>
    <td>AVBRUTEN</td>
    <td>40</td>
    <td>Åtgärden avbröts av ett explicit anrop om att avbryta eller förstöra.</td>
  </tr>
  <tr>
    <td>UNSUPPORTED_HLS_VERSION</td>
    <td>41</td>
    <td>Det går inte att spela upp den här versionen av HLS-media.</td>
  </tr>
  <tr>
    <td>CANNOT_FAIL_OVER</td>
    <td>42</td>
    <td>Det går inte att redundansväxla.</td>
  </tr>
  <tr> 
    <td>HTTP_TIME_OUT</td>
    <td>43</td>
    <td>Tidsgränsen för HTTP-hämtning har uppnåtts.</td>
  </tr>
  <tr>
    <td>NETWORK_DOWN</td>
    <td>44</td>
    <td>Användarens nätverksanslutning är inte tillgänglig. Uppspelningen kan avbrytas när som helst och återupptas när anslutningen är tillgänglig.</td>
  </tr>
  <tr>
    <td>NO_USABLE_BITRATE_PROFILE</td>
    <td>45</td>
    <td>Ingen användbar bithastighetsprofil hittades i strömmen.</td>
  </tr>
  <tr>
    <td>BAD_MANIFEST_SIGNATURE</td>
    <td>46</td>
    <td>Manifestet har en felaktig signatur. Det misslyckades med signeringstestet av manifestet.</td>
  </tr>
  <tr>
    <td>CANNOT_LOAD_PLAYLIST</td>
    <td>47</td>
    <td>Det går inte att läsa in en spelningslista.</td>
  </tr>
  <tr>
    <td>REPLACEMENT_FAILED</td>
    <td>48</td>
    <td>Det gick inte att ersätta den som angetts i ett Infoga-API. Det innebär att infogningen lyckades, men inte ersättningen. Ersättningen kan misslyckas om manifestet som ska ersättas har tagits bort från tidslinjen.</td>
  </tr>
  <tr>
    <td>SWITCH_TO_ASYMMETRIC_PROFILE</td>
    <td>49</td>
    <td>DRM växlar till en asymmetrisk profil. Alla profiler förväntas vara justerade i längd. Annars kommer den här varningen att kastas och uppspelningen kan innehålla hopp.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_BACKWARD</td>
    <td>50</td>
    <td>Live-fönstret förväntas bara flyttas framåt. Om inte kommer den här varningen att kastas och fönstret kommer inte att läsas. Därför kan det finnas hopp (eller stopp/lång paus) i uppspelningen.</td>
  </tr>
  <tr>
    <td>CURRENT_PERIOD_EXPIRED</td>
    <td>51</td>
    <td>Live-fönstret har flyttats utanför den aktuella perioden.</td>
  </tr>
  <tr>
    <td>CONTENT_LENGTH_MISMATCH</td>
    <td>52</td>
    <td>Den innehållslängd som rapporterades av HTTP-servern matchade inte den faktiska mediestorleken.</td>
  </tr>
  <tr>
    <td>PERIOD_HOLD</td>
    <td>53</td>
    <td>Medieläsaren kan inte läsa vidare eftersom den har nått den tid som anges av setHoldAt API.</td>
  </tr>
  <tr>  
    <td>LIVE_HOLD</td>
    <td>54</td>
    <td>Medieläsaren kan inte läsa in segment eftersom den har nått slutet av det aktiva fönstret. Inläsning av segment återupptas när servern annonserar nya media till det aktiva fönstret. Det här läget nås vanligtvis om:<ul><li>bufferTime är för hög (lika med eller högre än livefönstrets varaktighet).</li><li>En kombination av ett eller flera API:er för att infoga/radera har ersatt fler media än de lade till.</li><li>Nästa period är en aktiv period med en väntande medieersättning (på grund av InsertBy API-anrop)</li></ul></td>
  </tr>
  <tr>
    <td>BAD_MEDIA_INTERLEAVING</td>
    <td>55</td>
    <td>Ljud- och videointerfolieringen i mediet är inte korrekt gjord. Detta är ett paketeringsfel. Varningen skickas när skillnaden överstiger två sekunder.</td>
  </tr>
  <tr>
    <td>DRM_NOT_AVAILABLE</td>
    <td>56</td>
    <td></td>
  </tr>
  <tr>  
    <td>PLAYBACK_NOT_AUTHZED</td>
    <td>57</td>
    <td>HLS-uppspelning har inte aktiverats i Flash Player. Se AuthorizedFeatures.enableHLSPlayback.</td>
  </tr>
  <tr>
    <td>BAD_MEDIA_SAMPLE_FOUND</td>
    <td>58</td>
    <td>Avkodaren tog emot ett felaktigt prov som inte kan avkodas. Det här är vanligtvis inget allvarligt fel, men det indikerar att det kan finnas fel i ljud/video. För många instanser av det här felet indikerar felaktig kodning eller felaktig fil.</td>
  </tr>
  <tr>
    <td>RANGE_SPANS_READ_HEAD</td>
    <td>59</td>
    <td>När uppspelningen har startat får inte intervallet Infoga/Ersätt innehålla läshuvudet.</td>
  </tr>
  <tr> 
    <td>POSTROLL_WITH_LIVE_NOT_ALLOWED</td>
    <td>60</td>
    <td>Infogningar efter rullning är inte tillåtna på direktmedia. De tillåts dock efter att servern har markerat mediet som fullständigt.</td>
  </tr>
  <tr>
    <td>INTERNAL_ERROR</td>
    <td>61</td>
    <td>Ett mycket sällsynt problem som aldrig skulle inträffa.</td>
  </tr>
  <tr>  
    <td>SPS_PPS_FOUND_OUTSIDE_AVCC</td>
    <td>62</td>
    <td>Strömmen följer inte paketeringsrekommendationen att alltid placera H264 SPS/PPS i en AVCC. Problem med sökning/uppspelning kan eventuellt visas.</td>
  </tr>
  <tr>  
    <td>PARTIAL_REPLACEMENT</td>
    <td>63</td>
    <td>Ersättningen som anges i ett Infoga API har bara delvis utförts. Detta inträffar när replaceDuration sträcker sig över tidslinjens varaktighet.</td>
  </tr>
  <tr>
    <td>RENDITION_M3U8_ERROR</td>
    <td>64</td>
    <td>Det uppstod ett fel när återgivningsspellistan lästes in. Detta gäller endast AVE, inte FlashPlayer.</td>
  </tr>
  <tr>
    <td>NULL_OPERATION</td>
    <td>65</td>
    <td>Åtgärden gör ingenting.</td>
  </tr>
  <tr>
    <td>SEGMENT_SKIPPED_ON_FAILURE</td>
    <td>66</td>
    <td>Segmentet kan inte spelas upp och hoppas över vid fel.</td>
  </tr>
  <tr>
    <td>INCOMPATIBLE_RENDER_MODE</td>
    <td>67</td>
    <td>Inkompatibelt renderingsläge.</td>
  </tr>
  <tr>
    <td>PROTOCOL_NOT_SUPPORTED</td>
    <td>68</td>
    <td>Webbprotokollet som används i URL:en stöds inte.</td>
  </tr>
  <tr>
    <td>PARSE_ERROR_INCOMPATIBLE_VERSION</td>
    <td>69</td>
    <td>Fel vid parsning av mediefil.</td>
  </tr>
  <tr>  
    <td>MANIFEST_FILE_UNEXPECTEDLY_CHANGED</td>
    <td>70</td>
    <td>Manifestfilen ändrades på ett oväntat sätt.</td>
  </tr>
  <tr>
    <td>CANNOT_SPLIT_TIMELINE</td>
    <td>71</td>
    <td>Det går inte att utföra en delad åtgärd på en tidslinje.</td>
  </tr>
  <tr>
    <td>CANNOT_ERASE_TIMELINE</td>
    <td>72</td>
    <td>Det går inte att utföra en raderingsåtgärd på en tidslinje.</td>
  </tr>
  <tr>
    <td>DID_NOT_GET_NEXT_FRAGMENT</td>
    <td>73</td>
    <td>Hämtade inte nästa fragment.</td>
  </tr>
  <tr>
    <td>NO_TIMELINE</td>
    <td>74</td>
    <td>Det finns ingen tidslinje i en intern datastruktur.</td>
  </tr>
  <tr>
    <td>LISTENER_NOT_FOUND</td>
    <td>75</td>
    <td>Ingen avlyssnare hittades i en intern datastruktur.</td>
  </tr>
  <tr>
    <td>AUDIO_START_ERROR</td>
    <td>76</td>
    <td>Det gick inte att starta ljudet.</td>
  </tr>
  <tr>
    <td>NO_AUDIO_SINK</td>
    <td>77</td>
    <td>Det finns ingen ljudmottagare i en intern datastruktur.</td>
  </tr>
  <tr>  
    <td>FILE_OPEN_ERROR</td>
    <td>78</td>
    <td>Det gick inte att öppna filen.</td>
  </tr>
  <tr>
    <td>FILE_WRITE_ERROR</td>
    <td>79</td>
    <td>Det går inte att skriva till en fil.</td>
  </tr>
  <tr>
    <td>FILE_READ_ERROR</td>
    <td>80</td>
    <td>Det går inte att läsa från en fil.</td>
  </tr>
  <tr>
    <td>ID3PARSE_ERROR</td>
    <td>81</td>
    <td>Det uppstod ett fel vid analys av ID3-data.</td>
  </tr>
  <tr>
    <td>SECURITY_ERROR</td>
    <td>82</td>
    <td>Det gick inte att läsa in innehållet på grund av säkerhetsbegränsningar.</td>
  </tr>
  <tr>
    <td>TIMELINE_TOO_SHORT</td>
    <td>83</td>
    <td>Tidslinjens varaktighet är för kort. Om det här är en direktström kan det hända att buffring sker ofta.</td>
  </tr>
  <tr>
    <td>AUDIO_ONLY_STREAM_START</td>
    <td>84</td>
    <td>Strömmen har växlats till en ström med enbart ljud.</td>
  </tr>
  <tr>  
    <td>AUDIO_ONLY_STREAM_END</td>
    <td>85</td>
    <td>Strömmen har växlats från enbart ljud till en ström med video.</td>
  </tr>
  <tr>
    <td>KEY_NOT_FOUND</td>
    <td>87</td>
    <td>Det går inte att hitta nyckeln.</td>
  </tr>
  <tr>
    <td>INVALID_KEY</td>
    <td>88</td>
    <td>Nyckeln är ogiltig.</td>
  </tr>
  <tr>
    <td>KEY_SERVER_NOT_FOUND</td>
    <td>89</td>
    <td>Nyckelservern returnerar ingen nyckel.</td>
  </tr>
  <tr>
    <td>MAIN_MANIFEST_UPDATE_TO_BE_HANDLED</td>
    <td>90</td>
    <td>Det går inte att hantera uppdateringen av huvudmanifestet.</td>
  </tr>
  <tr>
    <td>UNREPORTED_TIME_DISCONTINUITY_FOUND</td>
    <td>91</td>
    <td>Orapporterad tid (PTS) - avbrott hittades.</td>
  </tr>
  <tr>
    <td>UNMATCHED_AV_DISCONTINUITY_FOUND</td>
    <td>92</td>
    <td>Omatchat ljud- och videoavbrott hittades.</td>
  </tr>
  <tr>
    <td>TRICKPLAY_ENDED_DUE_TO_ERROR</td>
    <td>93</td>
    <td>Det uppstod ett fel när media spelades upp i trickläge. Trick-uppspelningsläget avslutas och flödet pausas. Anropa Play() för att spela upp media i normalt läge.</td>
  </tr>
  <tr>
    <td>LIVE_WINDOW_MOVED_AHEAD</td>
    <td>95</td>
    <td>Spelaren är utanför det aktiva fönstret och måste söka framåt för att komma ifatt.</td>
  </tr>
</table>
