# Recommendation to the Head of Strategy

**Rival pit alert: do not adopt our new version; test the best existing one in the background before anyone acts on it.**

**What the alert is for.** At the end of each lap it flags rivals who may enter the pits in their next three laps, so the pit wall knows whom to watch (e.g. to react to an undercut). It is a watch list, not advice on when our car should stop.

**How we compared.** Each version learned from 2018–2021 and was compared on the first 11 races of 2022, where rivals made 370 pit stops. Each could raise at most 945 alerts (1 in 10 rival-laps). A stop is *warned* if an alert came in the three laps before it; an alert is *false* if that rival did not stop within three laps.

| Version (2022 races) | Stops warned, of 370 | Alerts | False alerts |
|---|---|---|---|
| No alert | 0 | 0 | 0 |
| Historical pit-rate rule | 94 (25%) | 931 | 681 |
| Simple decision tree | 63 (17%) | 571 | 417 |
| **More detailed tree (our change)** | **57 (15%)** | **580** | **435** |
| Best "forest" (average of 150 trees) | 140 (38%) | 945 | 605 |

**What happened with our change.** The more detailed tree did better on the older races it learned from (40% of stops warned vs 34%) but worse on 2022. Its mistakes are clustered: it was silent in both wet races (Imola, Monaco), missing all 46 stops by cars on intermediate or wet tyres, and in Baku it flagged the same cars lap after lap from lap 39 to 47 (of 51) with no stop behind any alert, a pattern learned almost entirely from the 2021 Baku race.

**Recommendation.** Do not adopt the more detailed tree, and do not rely on any version for live calls yet. The forest is the best option, but it still misses about 6 in 10 stops (230 of 370) and about 2 in 3 of its alerts are false (605 of 945). Run it in the background during races, without acting on it, and log its calls against what rivals actually do.

**Main limitation.** The same 2022 races were used to set each version's alert level and to choose between versions, so these figures are optimistic, not a final test. The data were cleaned after the races, so we have not shown that inputs like tyre age arrive on time live. Scores are not probabilities, and no positions or time gained were measured.

**Next check.** Freeze the forest and its alert level now and test it once, unchanged, on races not used so far, counting stops warned and false alerts, with a separate look at wet races and safety-car periods.
