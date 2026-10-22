# Control System Tuner

By Claude Opus 5.5. Gameplay designed with this 1 prompt:
"Mobile game idea: Control System Tuner.  Category: STEM games.  3 sliders: P, I, D.  Graph shows P, I, D, P+I+D, goal (input), measured (output). To pass level, meas must stay within envelope around goal and settle near goal within a time limit.  Goal can be step, ramp, s-curve, multiple steps, etc."

Resisting the temptation to improve this because I want to show how far Claude got with 1 short prompt, and then some more prompts to get it on GitHub.

A browser game about tuning PID controllers. Set P, I and D, press Run, and keep the measured response inside the spec channel until it settles.

**[Play it in your browser](https://kylesimkus.github.io/Control-System-Tuner/ControlSystemTuner.html)** (works on phones too)

## How to play

Each level is a real machine with its own physics. Move the P, I and D sliders, press Run, and watch the response draw like a chart recorder. The lower chart shows what each term of the controller is doing.

You pass when the measured trace stays out of the hatched zone and settles inside the narrow band before the deadline. Extra stars go to low tracking error, little overshoot, fast settling or a calm actuator, depending on the level. A missed run tells you what went wrong and which knob to try.

## Levels

| # | Machine | What it teaches |
|---|---|---|
| 1 | Robot arm | P alone: too little is slow, too much swings past |
| 2 | Espresso boiler | I removes the error P leaves behind |
| 3 | Quadcopter | D brakes before you arrive |
| 4 | Ship autopilot | Following a smooth S-curve turn |
| 5 | Reflow oven | Tracking a ramp profile with sensor delay |
| 6 | Cruise control | Speed steps, then a 6 % hill |
| 7 | Shower | Long dead time |
| 8 | Camera gimbal | Sensor noise and wind gusts |
| 9 | Maglev | A plant that falls without control |

## How it works

- Each machine is a small differential-equation model, stepped with fourth-order Runge–Kutta. Actuators saturate, and some move at a limited rate or act after a delay. The gimbal's sensor is noisy and the maglev is open-loop unstable.
- The controller is a parallel PID. The derivative acts on the filtered measurement, so goal steps don't kick it. Integration pauses while the actuator is saturated (anti-windup).
- The pass channel is wide while the goal moves, then narrows to a tight band by a settle deadline. Disturbances such as the hill or a gust reopen it.
- Each level's spec was set by sweeping the gain space on a log grid, so that passing needs the intended term. In those sweeps, no setting passed the espresso boiler without I, or the quadcopter and gimbal without D.

## Run it locally

Download `ControlSystemTuner.html` and open it in any modern browser. There is no build step and nothing to install. Fonts load from Google Fonts, and progress is saved in your browser.

## Credits

Concept by Kyle Simkus. Built with Claude (Anthropic).
