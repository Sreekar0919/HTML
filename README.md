# SmartMat: an interactive yoga and dance mat (2021)

A prototype exercise mat divided into numbered squares that coaches you through yoga poses and dance
steps. It tells you where to step or place a hand, checks that you did, and scores how quickly you
responded. This repo holds the controller script and the project website (GitHub Pages, custom
domain `www.ydmat.com`).

## How it works

```
Arduino (square sensors) ◀──serial 9600 baud──▶ arduinoConnections.py ──stdout──▶ index.js ──socket.io──▶ browser
```

- **`arduinoConnections.py`** drives a guided routine. For each move it sends the target square
  to the Arduino over serial, waits for the reply, retries up to *n* times on `incorrect`, and awards
  points by response time.
- **`index.js`** is a small Node.js server. It spawns the Python controller and streams its output to
  the web page live over socket.io.
- **Website**: `index.html` (home), `about.html` / `Info.html` (project description and demo video),
  `workout*.html` and `fullTrial.html` (routine pages), styled in `styles.css` / `workout.css`.

## Run locally

```bash
pip install pyserial          # set the serial port in arduinoConnections.py (default COM5)
npm install socket.io
node index.js
```

## Status

A 2021 prototype. The plan was a companion app that shows each move on the squares and logs workouts.
