# Circle of Doom

A visualization that shows a Formula 1 race on a single circle. Drivers are placed by their **time gap** to the leader, not by distance.

The project is one `index.html` file: HTML, CSS and JavaScript. It needs no installation and no libraries.

## How to run

Open `index.html` in a browser.

If the OpenF1 modes show a network or CORS error, start a local server in the project folder:

```bash
python -m http.server
```

Then open `http://localhost:8000` in your browser.

## How to read the circle

- The full circle is one lap time (the "Reference lap" in the center).
- The checkered flag at the top marks the leader.
- The further a driver is behind the leader, the further they sit counter-clockwise. For example, with a 90-second lap, a driver 9 seconds behind sits 36° around the circle.
- Select a driver and every label shows the gap relative to that driver.
- The purple arc shows where the selected driver would rejoin if they pitted now.

## Features

- Safety Car, pit stops, OUT and "+1L" (lapped) states
- Pit prediction ("if he pitted now: P3 → P16")
- Speed control (1× to 200×) and a race time slider
- Light and dark theme, works on phones

## Data sources

| Mode | Description |
|---|---|
| Simulation | A made-up race. No internet needed. |
| OpenF1 replay | Loads a past race from the [OpenF1](https://openf1.org) API and plays it back. |
| OpenF1 live | Fetches the latest gaps every 7 seconds. OpenF1 may require a token during a session. |

The pace and strategy values in the simulation are invented and do not reflect real performance.

## Code structure

All logic lives in `index.html`. The top of the file has a map and each section is commented:

1. Constants
2. Helper functions
3. Simulator (`simulateRace`)
4. OpenF1 API
5. Frame calculator (`computeFrame`)
6. Pit prediction (`pitPrediction`)
7. Rendering (SVG)
8. Controls

Data flow: source → `RACE` object → `computeFrame(race, T)` → `draw(frame)` → screen.

## Inspiration

The idea comes from the "Circle of Doom" feature in MultiViewer. This project is independent of it and is not an official product.
