# Road Intersection Traffic Simulation (Java Edition)

## Overview

This project is a real-time traffic simulation built in **Java** using the **Java Swing** library for rendering. It visualizes a busy four-way intersection where vehicles must navigate traffic lights and traffic flow rules. The objective is to demonstrate a traffic control strategy that manages congestion and prevents collisions while allowing user interaction to spawn vehicles dynamically.

This simulation was developed to solve the "Traffic, traffic, traffic..." challenge, implementing specific rules for road layout, traffic light signaling, and vehicle behavior.

![Video](java_video_jraffic.webm)

## Features

* **Interactive Simulation**: Users can manually spawn cars from different directions using keyboard controls, or spawn them randomly.
* **Traffic Light System**: A dynamic 4-state traffic light system (North, South, East, West) that cycles automatically based on timers and lane congestion to manage flow.
* **Vehicle AI**:
    * **Routing**: Vehicles are assigned random routes (turning left, right, or going straight) indicated by their color.
    * **Collision Avoidance**: Logic to maintain safe distances between vehicles in the same lane.
    * **Traffic Compliance**: Vehicles automatically pull up to the stop line at red lights and proceed when safe.
* **Visual Rendering**: Draws a complete road intersection with lane markings, dashed lines, and dynamic colored lights using `Graphics2D`.

## Technologies Used

* **Language**: Java
* **Graphics Library**: Java Swing (`JFrame`, `JPanel`) and AWT (`Graphics2D`) for rendering the 2D environment and game loop.
* **Randomization**: `java.util.Random` for varied vehicle generation and routing.

## Installation & Running

Ensure you have the **Java Development Kit (JDK)** installed on your system.

1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/AhmedBaid/jraffic.git](https://github.com/AhmedBaid/jraffic.git)
    cd road_intersection
    ```

2.  **Compile the Java files**:
    ```bash
    javac -d build  *.java 
    ```

3.  **Run the project**:
    ```bash
    java Main
    ```

## Controls

The simulation is controlled via the keyboard. You act as the "Traffic Generator," deciding when and where cars enter the city.

| Key | Action |
| :--- | :--- |
| **UP Arrow** | Spawn a car coming from the **South** (moving Up) |
| **DOWN Arrow** | Spawn a car coming from the **North** (moving Down) |
| **LEFT Arrow** | Spawn a car coming from the **East** (moving Left) |
| **RIGHT Arrow** | Spawn a car coming from the **West** (moving Right) |
| **R** | Continuously spawn cars from **Random** directions |
| **C** or **Backspace** | Clear all cars from the screen |
| **Esc** | Exit the simulation |

> **Note:** The simulation includes safety logic that prevents you from "spamming" cars on top of each other. If a car is too close to the spawn point, a new one will not be created until there is a safe gap.

## Project Structure

The source code is modularized into object-oriented classes for clarity:

* **`Main.java`**: The entry point of the application. It sets up the `JFrame` window, handles the custom game loop (calculating delta time), manages keyboard input listeners, and orchestrates the updates for cars and traffic lights.
* **`Car.java`**: Defines the `Car` object and its behavior.
    * Handles movement and boundary clamping (`update`).
    * Determines turning paths based on assigned colors.
    * Manages speed and directional states.
* **`TrafficLight.java`**: Manages the intersection's light system.
    * Controls the timing, state switching, and congestion calculations.
    * Renders the traffic lights and diagnostic text on the screen.
* **`RoadDrawer.java`**: A utility class containing static drawing functions for the static environment, rendering the asphalt, solid gold lane dividers, and dashed yellow lines.

## Simulation Logic

### 1. The Environment
The simulation renders two crossing roads. Each road supports one lane in each direction. The center of the screen is the "conflict zone" where paths merge and diverge.

### 2. Traffic Lights
The traffic lights operate on a dynamic timer-based state machine that accounts for congestion. The system cycles through states, allowing traffic from one direction to proceed at a time while holding others:
1.  **Down** (Green for North-to-South traffic)
2.  **Left** (Green for East-to-West traffic)
3.  **Up** (Green for South-to-North traffic)
4.  **Right** (Green for West-to-East traffic)

*(Note: The system includes a brief "ALL RED" clearing state between switches to allow the intersection to empty).*

### 3. Vehicles
* **Spawning**: When a key is pressed, a vehicle is instantiated with a random color.
* **Routes**: The color of the car determines its intended path (e.g., Red cars might turn left, Yellow might turn right).
* **Movement**: Vehicles move at a fixed speed adjusted by the frame delta time (`dt`). They check the state of the traffic light and the position of the car in front of them every frame. If the light is Red or the gap to the next car is unsafe, the vehicle halts exactly at the stop line.

## Future Improvements

* Add visual assets (sprites or images) for cars instead of rectangles.
* Implement a dedicated "Yellow" light phase for smoother transitions before the "ALL RED" phase.
* Display on-screen simulation statistics (e.g., total cars passed, average wait time, current lane capacities).

---
*Project developed for the Traffic Simulation Challenge.*