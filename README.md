<h1>Interactive Bézier Rope Simulation</h1>

<h2>Description</h2>

This project implements an interactive cubic Bézier curve that simulates a springy rope reacting to real time input. The curve dynamically adjusts based on mouse movement (for web) or gyroscope data (for iOS), incorporating spring damping physics for natural, rope-like behavior. Tangent vectors are visualized along the curve to illustrate its shape and motion.
The simulation is built from scratch using manual implementations of Bézier mathematics, physics integration, and no prebuilt APIs are used. It runs as a client side web app and can be adapted for iOS with Swift and CoreMotion.
This fulfills the assignment requirements: real time interactivity, Bézier math, spring physics, tangent visualization, and 60 FPS performance.

<h2>Features</h2>

Cubic Bézier Curve-Defined by 4 control points (P₀ and P₃ fixed; P₁ and P₂ dynamic).

Physics Simulation-Spring damping model for smooth, natural motion of dynamic control points.

Tangent Visualization-Normalized tangent vectors drawn at intervals along the curve.

Interactive Input-Mouse position controls displacement (web), gyroscope data can be integrated for iOS.

Rendering-Curve path, control points (as circles), and tangents on an HTML5 Canvas.

Performance-Maintains ~60 FPS using requestAnimationFrame.

<h2>How to Run</h2>

Visit the live demo at https://adityadixit1301.github.io/bezier-rope-simulation/.

Run Locally:
Clone or download the repository.
Open index.html in any modern web browser:
Move your mouse over the canvas to interact the curve will bend like a rope.
For iOS Adaptation: The logic can be ported to Swift using CoreMotion for gyroscope input. Use CADisplayLink for rendering.
No dependencies or installations required it's pure HTML5 and JavaScript.

<h2>Math and Physics Explanation</h2>

Bézier Curve Math
A cubic Bézier curve is defined by the parametric equation:

B(t) = (1−t)³P₀ + 3(1−t)²tP₁ + 3(1−t)t²P₂ + t³P₃
P₀ and P₃ are fixed endpoints.
P₁ and P₂ are dynamic control points.
The curve is sampled at small t increments (0.01) for rendering, generating points to draw as connected line segments.

Tangent Computation
Tangents are derived from the curve's derivative:

B'(t) = 3(1−t)²(P₁−P₀) + 6(1−t)t(P₂−P₁) + 3t²(P₃−P₂)
Vectors are normalized and drawn as short lines (20px length) at 5 evenly spaced t values (0.1, 0.3, 0.5, 0.7, 0.9) to visualize direction.
Physics Model
Dynamic points (P₁ and P₂) use a spring-damping system for rope-like behavior:

Acceleration: a = -k * (position - target) - damping * velocity
k = 0.1 (spring stiffness=controls how strongly points pull toward targets).
damping = 0.05 (reduces oscillation for stability).
Integration= Euler method updates position and velocity per frame (dt calculated from requestAnimationFrame).
Input Mapping= Mouse position offsets targets symmetrically (e.g., pulling the rope from the center). Velocity is clamped to prevent instability.
This creates smooth, springy motion without external libraries.

<h2>Design Choices</h2>

Platform: Web (HTML5 Canvas + JS) for portability and ease of sharing/hosting on GitHub Pages. iOS version would use Swift + CoreMotion for gyroscope input.

Rendering: Canvas for simplicity and performance. Curve sampled densely for smoothness; tangents at sparse intervals to avoid clutter.

Physics Tuning: Constants chosen for balance.Stiff enough for responsiveness but damped to avoid wild oscillations. Symmetric target updates mimic rope physics.

Code Organization: Modular functions for math, physics, input, and rendering. No globals beyond essentials.

Performance: Frame-based updates ensure 60 FPS; large dt skips prevent physics glitches.

Interactivity: Mouse input simulates "motion" for iOS, gyroscope data  could directly set targets.

Limitations: 2D only; no collision or advanced physics. Adapted for assignment constraints.

<h2>Code Structure</h2>

index.html: Main file containing HTML, CSS, and JavaScript.

Math Functions: bezierPoint() and bezierTangent() for curve and tangent calculations.

Physics: updatePhysics() for spring-damping integration.

Input: Mouse event listener sets targets.

Rendering: render() draws curve, points, and tangents.

Loop: animate() handles timing and calls updates/rendering.

File size: ~2KB (minimal and self-contained).

<h2>Screenshots</h2>
<img width="2562" height="1443" alt="image" src="https://github.com/user-attachments/assets/644f1d59-6b07-4874-8e35-ec92b294100c" />Example: A static image of the canvas showing the blue curve, red points, and green tangents.


