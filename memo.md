# Recommendation to the Head of Strategy

**Rival pit alert: do not adopt our new version; trial the best existing one in the background first.**

**What the alert is for.** At the end of each lap it flags rivals who may enter the pits in their next three laps, so the pit wall knows whom to watch (e.g. to react to an undercut). It is a watch list, not advice on when our car should stop.

**How we compared.** Each version learned from 2018–2021 and was compared on the first 11 races of 2022 (370 rival pit stops), with at most 945 alerts each (1 in 10 rival-laps). A stop is *warned* if an alert came in the three laps before it; an alert is *false* if no stop followed within three laps.

| Version (2022 races) | Stops warned, of 370 | Alerts | False alerts |
|---|---|---|---|
| Historical pit-rate rule | 94 (25%) | 931 | 681 |
| Simple decision tree | 63 (17%) | 571 | 417 |
| **More detailed tree (ours)** | **57 (15%)** | **580** | **435** |
| Best "forest" (150 trees) | 140 (38%) | 945 | 605 |

**Our change.** The more detailed tree did better on the 2018–2021 races it learned from (40% of stops warned vs 34%) but worse on 2022. Its mistakes cluster: it was silent in both wet races (Imola, Monaco), missing all 46 stops on intermediate or wet tyres, and at Baku it kept flagging the same cars lap after lap from lap 39 to 47 (of 51), all false alarms.

**Recommendation.** Do not rely on any version for live calls yet. The forest is the best option, but it still misses 230 of 370 stops, and 605 of its 945 alerts are false. Run it silently during races and log its calls against what rivals do.

**Main limitation.** The same 2022 races set each version's alert level and chose between versions, so these figures are optimistic, not a final test. The data were cleaned after the races, and live tyre-age data may arrive late. No positions or time gained were measured.

**Next check.** Freeze the forest and its alert level, then test it once, unchanged, on races not used so far, looking separately at wet races and safety-car periods.
