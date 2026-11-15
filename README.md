# Lunar Quest

**Run a Moon base. Every choice costs something.**

Lunar Quest is a browser game for ages 7 to 12 where players split limited power between air, radiation shielding, food and science. Real NASA space weather decides how stormy their mission gets.

A browser game for ages 7–12 about running a Moon base for 14 days. Built for the 2026 NASA Space Apps Challenge: *Build a Junior Astronaut Mission Trainer*.

No install, no account. Open `index.html` in a browser, or use the GitHub Pages link.

## The trade-off

Each day you have a small amount of power. You split it between jobs:

| Job | What it does | What it costs you |
|---|---|---|
| **Air** | Makes oxygen. The crew breathes 3 a day. Tank holds 20, starts at 12. | Power not spent elsewhere. |
| **Shield** | Piles moon dirt (regolith) to block radiation. Each level cuts daily dose by 9%. Highest level is 8. One level slumps away each night. | Power not spent elsewhere. |
| **Science** | Earns points toward the 35 point goal. | Power not spent elsewhere. |
| **Greenhouse** (Explorer mode) | Grows food. The crew eats 2 a day. Tank holds 20, starts at 14. | Power not spent elsewhere. |

Unused power goes to a battery that holds 6. A **storm shelter** cuts a storm's extra radiation by 70% but means no science that day, and does nothing on a quiet day.

The mission ends early if the air runs out, the food runs out (Explorer mode), or the crew's radiation dose reaches **36**. Otherwise you win by collecting 35 science points in 14 days.

### Two landing sites

| | Sunlit Ridge | Icy Crater Floor |
|---|---|---|
| Power per day | 10 | 6 |
| Air per power | 1 | 1.5 (water ice) |
| Food per power | 1 | 1.25 (water for plants) |
| Science per power | 1 | 1.5 (ice samples) |
| Radiation | Full sky | 10% less (walls block some sky) |

### Replayability

Each run draws solar storms at random and one dust day that cuts solar power by 3. A flare gives a one-day warning before its particles arrive.

## Real data used

| Source | How it is used |
|---|---|
| [NASA DONKI](https://ccmc.gsfc.nasa.gov/tools/DONKI/) flares (`/DONKI/FLR`) | Storm strength. On load the game requests M and X class flares from the recent months (60 to 180 days) and draws storms from them. M-class becomes strength 2.5. X-class scales up with its number, capped at 7. |
| NASA DONKI past 7 days (`FLR`, `CME`, `GST`, `SEP`) | **Today's real Sun** panel on the start screen. It counts medium and big flares, clouds of gas (CMEs), the highest Kp index and particle events. A quiet, active or stormy week sets how many storms you face (2, 3 or 4). |
| [OSDR RadLab](https://visualization.osdr.nasa.gov/radlab/gui/data-api/) (`/radlab/api`) | A real ISS absorbed dose rate (micrograys per hour) shown on the start and end screens. The game asks for one hour of ISS data from 1 April 2022, so this is an archive reading, not live. |
| [NASA OSDR](https://osdr.nasa.gov/bio/repo/) | Background on how spaceflight affects the body. |
| [CSA food production toolkit](https://www.asc-csa.gc.ca/eng/youth-educators/toolkits/food-production/) | The inspiration for the greenhouse job and its end-screen fact, plus learning links in the game. |
| [CSA space resources for STEM and youth](https://www.asc-csa.gc.ca/eng/youth-educators/resources-stem-and-youth-organizations.asp) | Learning links in the game. |
| Chang'e-4 lander dosimeter (published research) | The Moon-versus-Earth radiation comparison on the end screen (about 1.4 mSv per day, roughly 200 times Earth's surface). Rounded; verify before citing. |

The start screen shows whether flare data is **live** or **archived**. If a request fails, the game falls back to a small hand-picked set of real flares (M-class, X5.8 on 11 May 2024, X9.0 on 3 Oct 2024, X9.3 on 6 Sep 2017, estimated X28 on 4 Nov 2003) and random storm counts. The archive is never presented as live.

### What is simplified

- Power, air, food, shield and science numbers are scaled game values, not mission data.
- The radiation limit of 36 is a game number, not a real dose limit.
- Storm particles arrive one day after the flare. In reality fast particles can arrive within hours and slower gas clouds in one to three days.

## Run it

Open `index.html` directly, or serve the folder:

```
python3 -m http.server 8000
```

Then visit http://localhost:8000. Live NASA data needs internet access.

## Host on GitHub Pages

1. Put `index.html`, `README.md` and `LICENSE` in a repository.
2. Open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then save.
4. After a minute the game is live at `https://<your-username>.github.io/<repo-name>/`.

### NASA API key

`index.html` contains a free personal NASA API key in the `NASA_KEY` constant near the top of the script. On a public site everyone can see it. If it is misused, request a new one at https://api.nasa.gov and replace the value. If the key is rejected or rate limited, the game retries with NASA's shared `DEMO_KEY`.

## Ideas for next steps

- Choose the RadLab time window from the latest available data instead of a fixed archive hour.
- Show a real OSDR study after each run.
- Add Mars as a second destination using Mars Trek terrain and a longer communication delay.
- A teacher mode that shows the debrief for a whole class.

## Credits

Space weather data from NASA DONKI and radiation data from NASA OSDR RadLab. Food and STEM learning resources from the Canadian Space Agency. NASA does not endorse this project. Fonts: Chakra Petch and Lexend from Google Fonts.
