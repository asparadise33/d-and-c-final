# Duke & Chord Music

A musical instrument marketplace and music education platform built as a Single Page Application (SPA). Users can browse and sell instruments, preview audio samples, enroll in music classes, and manage their accounts.

## Project Overview

Duke & Chord Music is a comprehensive full-stack web application designed as a Single Page Application (SPA). It seamlessly integrates an online musical instrument marketplace with a robust music education platform. The application offers a dynamic and interactive experience where users can:

*   **Discover and Purchase Instruments**: Browse a wide array of musical instruments available for sale, view detailed product information, and listen to audio previews before making a purchase.
*   **Sell Instruments**: Easily list their own instruments for sale through a dedicated submission process.
*   **Explore and Enroll in Music Classes**: Access a curated catalog of music classes, view class schedules, learn about instructors, and enroll to enhance their musical skills.
*   **Manage Accounts**: Securely register, log in, and manage their user profiles.

The application leverages a custom client-side routing system for dynamic content loading, a bespoke event-driven state management system for data consistency, and a component-based architecture for modular UI development. It interacts with a `json-server` mock REST API for all data persistence, supporting full CRUD operations across various data domains.

## Target Audience and Use Cases

Duke & Chord Music caters to a diverse audience within the music community:

*   **Aspiring and Professional Musicians**:
    *   **Use Case**: A guitarist looking for a specific type of vintage amplifier can browse the marketplace, filter by instrument type, and listen to sound samples.
    *   **Use Case**: A drummer wanting to sell their old drum kit can easily list it on the platform.
*   **Music Students and Learners**:
    *   **Use Case**: A beginner pianist can explore available piano classes, check instructor profiles, and enroll directly through the platform.
    *   **Use Case**: Someone interested in learning a new instrument can find an instructor and relevant classes to start their journey.
*   **Music Educators and Institutions**:
    *   **Use Case**: Instructors can list their music classes, manage schedules, and reach a broader student base.
*   **Music Enthusiasts**:
    *   **Use Case**: Individuals passionate about music can explore different instruments and learn about educational opportunities, even if they're not actively buying or selling.

This platform aims to be a central hub for musical instrument commerce and education, fostering a vibrant community around music.

## Key Features

*   **User Authentication**: Secure registration and login system, allowing users to create accounts, sign in, and access personalized features like managing their profile and listings.
*   **Instrument Marketplace**:
    *   **Browse Instruments**: Users can explore a wide range of musical instruments available for sale, with filtering options by type (percussion, string, wind) to easily find desired items.
    *   **View Detailed Information**: Each instrument listing provides comprehensive details, including descriptions, images, and crucial audio previews.
    *   **Sell Instruments**: A dedicated form allows users to easily list their own instruments for sale, facilitating a peer-to-peer marketplace.
*   **Music Classes**:
    *   **Browse Classes**: Users can browse a catalog of available music classes, discovering various instruments and skill levels.
    *   **View Class Details**: Detailed information for each class, including schedules, instructors, and curriculum, helps users make informed enrollment decisions.
*   **Employee Directory**: Provides information about the Duke & Chord team, offering transparency and a personal touch to the platform.
*   **Audio Previews**: A unique feature enabling users to listen to audio samples of instruments before making a purchase decision, enhancing the online shopping experience.

## Technology Stack

### Frontend
*   **HTML5, CSS3, JavaScript**: Core web technologies for structure, styling, and interactivity.
*   **Component-Based Architecture**: Modular UI development using self-contained JavaScript modules.
*   **Custom Client-Side Routing**: Dynamic content loading without full page refreshes, based on URL parameters.
*   **Custom Event-Driven State Management**: [`UserStateManager`](src/scripts/data/UserStateManager.js), [`InstrumentsStateManager`](src/scripts/data/InstrumentsStateManager.js), [`ClassStateManager`](src/scripts/data/ClassStateManager.js), [`ViewStateManager`](src/scripts/data/ViewStateManager.js) for data consistency and reactive UI updates.

### Backend
*   **Node.js**: Runtime environment for the custom server ([`server.js`](server.js)).
*   **json-server**: Used as a mock REST API for all data persistence and CRUD operations.

### Data Storage
*   **[`api/database.json`](api/database.json)**: JSON file serving as the mock database for `json-server`.

## Code Organization

#### Directory Structure

*   [`api/`](api/): Contains [`database.json`](api/database.json), serving as the mock data store for `json-server`.
*   [`src/`](src/): Houses all client-side application code and assets.
    *   [`src/index.html`](src/index.html): The main entry point for the Single Page Application.
    *   [`src/audio/`](src/audio/): Stores audio files for instrument previews.
    *   [`src/images/`](src/images/): Contains images used throughout the application.
    *   [`src/scripts/`](src/scripts/): Contains all JavaScript modules for the application's logic and UI.
        *   [`src/scripts/DukeChord.js`](src/scripts/DukeChord.js): The main application module responsible for overall orchestration and rendering.
        *   [`src/scripts/Home.js`](src/scripts/Home.js): Component for the home page view.
        *   [`src/scripts/main.js`](src/scripts/main.js): Initializes the application.
        *   [`src/scripts/auth/`](src/scripts/auth/): Modules related to user authentication (login, registration).
        *   [`src/scripts/classes/`](src/scripts/classes/): Modules for managing and displaying music classes.
        *   [`src/scripts/data/`](src/scripts/data/): Contains the custom state management modules (`*StateManager.js`) responsible for data persistence and application state.
        *   [`src/scripts/employees/`](src/scripts/employees/): Modules for displaying employee information.
        *   [`src/scripts/instruments/`](src/scripts/instruments/): Modules for managing and displaying musical instruments (listings, details, forms).
        *   [`src/scripts/nav/`](src/scripts/nav/): Modules for navigation components (header, navbar).
    *   [`src/styles/`](src/styles/): Contains all CSS files for styling the application.
*   [`server.js`](server.js): Custom Node.js server that serves static files and proxies API requests to `json-server`.
*   [`package.json`](package.json): Defines project metadata and scripts for running the application.

#### Module Responsibilities

*   **`src/scripts/data/*StateManager.js`**: These modules are the core of the custom event-driven state management system. Each is responsible for managing a specific domain of application data (users, instruments, classes, view state), handling API interactions, and dispatching `stateChanged` events.
*   **Components (`src/scripts/*/*.js`)**: Individual JavaScript modules that encapsulate UI elements. They are responsible for generating HTML, attaching event listeners, and interacting with state managers to render dynamic content.
*   **`server.js`**: Orchestrates the backend operations, serving the frontend assets and routing API requests to the `json-server`.

### High-level architecture overview

Duke & Chord Music operates as a client-side rendered Single Page Application (SPA). Its architecture is centered around a modular, component-based design, a custom event-driven state management system, and a bespoke routing mechanism. Data persistence is handled via interactions with a `json-server` mock REST API, supporting full CRUD operations across various data domains. The application emphasizes dynamic content loading and a responsive user experience without traditional page reloads.

### Explanation of key design patterns

The application primarily utilizes the **Component Pattern** for UI development, where each logical part of the user interface is encapsulated in its own JavaScript module responsible for rendering, event handling, and state interaction. The **Observer Pattern** is central to its custom state management, allowing components to subscribe to state changes and re-render reactively. Additionally, a form of **MVC (Model-View-Controller)** or **MVVM (Model-View-ViewModel)** pattern can be observed in the separation of concerns: state managers act as models/viewmodels, components as views, and event listeners/dispatchers as controllers/viewmodels.

### State management strategy

The application employs a custom, event-driven state management system. This system is composed of several dedicated JavaScript modules, each managing a specific domain of application data:

*   [`UserStateManager`](src/scripts/data/UserStateManager.js): Manages user authentication status and profile information.
*   [`InstrumentsStateManager`](src/scripts/data/InstrumentsStateManager.js): Oversees instrument listings, filtering criteria, and related data.
*   [`ClassStateManager`](src/scripts/data/ClassStateManager.js): Handles information pertaining to music classes and enrollment.
*   [`ViewStateManager`](src/scripts/data/ViewStateManager.js): Controls the active view of the application and navigational state.

State changes within these managers dispatch custom `stateChanged` events. This allows any component subscribed to these events to detect relevant data updates and trigger a re-render, ensuring the UI remains synchronized with the application's underlying data. API calls for data fetching and modification are abstracted through these state managers, which then propagate updates.

### Routing approach

Duke & Chord Music implements a client-side routing system that enables dynamic content loading without full page refreshes. This is achieved by utilizing URL parameters (e.g., `?view=store`, `?view=classes`, `?view=instrument&id=1`) to dictate the current view and any associated data. The [`ViewStateManager`](src/scripts/data/ViewStateManager.js) is responsible for interpreting these URL parameters and updating the application's view state, which in turn prompts the main application components to render the appropriate content. This approach provides a smooth, SPA-like navigation experience.

### Component structure

The user interface is built using a component-based architecture. Each component is implemented as a self-contained JavaScript module. These modules are responsible for:

*   **HTML Generation**: Generating their specific portion of the UI as an HTML string.
*   **Event Handling**: Attaching event listeners to handle user interactions within their scope.
*   **State Interaction**: Dispatching custom events when local data is modified or when global state changes are needed, and listening for `stateChanged` events from the state managers to update their own rendering.

This modular approach promotes reusability, maintainability, and a clear separation of concerns, making the UI development more organized and scalable

## Prerequisites

- **Node.js**: Version 14.x or higher
- **npm**: Version 6.x or higher

## Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd duke_and_chord
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Install json-server Globally

The application requires json-server version 0.17.4 for API functionality:

```bash
npm i -g json-server@0.17.4
```

This global installation allows you to run json-server as a standalone service if needed.

## Running the Application

### Option 1: Using npm start (Recommended)

The simplest way to run the application is using the npm start script, which launches the custom server:

```bash
npm start
```

This will start the server on port 5002 (or the port specified in the PORT environment variable). The server handles both:
- Static file serving for the front-end application
- API routing through json-server

Access the application at: `http://localhost:5002`

### Option 2: Using json-server Directly

Alternatively, you can run json-server directly with the database file:

```bash
json-server --watch api/database.json --port 5002
```

Note: This method only provides API functionality. You'll need a separate static file server for the front-end.
