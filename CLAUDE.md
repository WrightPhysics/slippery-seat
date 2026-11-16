# slippery-seat

Classroom animation for Richard Wright's Advanced Physics class (circular motion unit, 6.1.2 Extend your Understanding #1): Doris Locked (driver, belted, ⊗) makes a right turn beginning at A; Rex Things (passenger, not belted, ●) slides across the waxed vinyl seat until he hits Doris at B. Students (a) draw Rex's positions and B and (b) the force on Rex by Doris during the turn. Same family as bowling-ball-taps and newtons-cannon.

Live at **https://wrightphysics.org/slippery-seat/** (repo `WrightPhysics/slippery-seat`, GitHub Pages from `main`, root). The homepage card is in `WrightPhysics/wrightphysics.github.io`. Deploying = pushing to `main`; test with a cache-busting query string (`?v=2`).

## How the project works

- Everything is in **one file: `index.html`**, with inline CSS and JS and no build step. The only outside dependency is Google Fonts.
- Commit and push only when Richard asks.

## Model

- Top view, canvas 760 x 760, screen pixels with y down. The car's center drives straight up (3 dot spacings before A), turns right on a circle of radius `Rc` (Turn slider, 200 to 460 px, default 380) about C = (XA + Rc, YA), then drives straight right for 2.5 spacings. Constant speed `V`; positions are marked every `T = DS / V` (DS = 45 px of the car's travel), and A is a dot.
- Car frame: u to the car's right, w forward. Doris sits at u = -HS (outside of the turn), Rex at u = +HS (HS = 20 px); bodies have radius RB = 10.
- No seat belt: the seat is frictionless, so Rex keeps his velocity (a straight line). In the car he only slides sideways (`rexSlide`: his car-frame u from the straight line, with w held at 0). The small forward creep relative to his seat, from the inside of the turn moving slower than the car's middle, is left out on purpose because it is imperceptible over a couple of feet. His world position is drawn from that car-frame spot, which stays within a pixel or two of the straight line. `setup()` finds the moment (`tc`, 1 ms steps) when he reaches Doris (u = -HS + 2·RB); that spot is B. After B, Rex keeps his car-frame position (`L`) and moves with the car: around the circle while turning, then straight.
- Seat belt on (switch, key B): Rex stays in his seat from the start.
- Force arrows (orange `--net`, off by default because it is the answer to part b): drawn at Rex's dots and on Rex whenever he is held (after B, or belted) and the car is turning, pointing at C. Constant length (direction only). Otherwise an "F by Doris = 0" label. The checkbox label switches to "by the seat belt" when belted.
- The whole motion is a function of time, so Step jumps exactly to the next dot.
- "Inside the car" close-up (bottom-right, below C so the center marker stays visible): the car pointing up, scale 2.1, with Rex's earlier car-frame spots, so his slide toward Doris shows.
- The front seat is one bench (no gap or console), so Rex can slide straight across to Doris.
- Colors: velocity green, force orange; the car is neutral slate so it is not mistaken for a vector.

Keys: Space play/pause, S step, R reset, B seat belt, F force arrows.
