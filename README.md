# Event Tracker: Local Time Tracking for Birthdays & Milestones

[![Release](https://img.shields.io/github/v/release/keshavgorasiya/event-tracker)](https://github.com/keshavgorasiya/event-tracker/releases)

Direct download: https://github.com/keshavgorasiya/event-tracker/releases

A simple, fast tool to track important events and anniversaries. Add events, edit them, and see elapsed time at a glance. All data stays in your browser, so there’s no backend to manage. This project is a lightweight, single-page application built with vanilla JavaScript and CSS, designed to be easy to run anywhere and simple to customize.

Welcome to Event Tracker. This tool helps you remember dates that matter. It calculates how long since an event started, how long until the next milestone, and it updates in real time. It stores all data locally in your browser so you can trust it to stay on your device. It’s ideal for birthdays, anniversaries, project milestones, and other time-based events you want to monitor without the fuss of a server.

If you want to skip ahead to the latest release, visit the releases page. The Releases page hosts the packaged build you can download and run on your machine. This project keeps things simple by avoiding a backend, but it remains flexible enough for you to customize.

Table of contents
- Why this project exists
- Core ideas and design goals
- Features at a glance
- How it works under the hood
- Data model and local storage
- Getting started and running locally
- User guide: adding, editing, and viewing events
- Calculations and time math explained
- UI and theming details
- Accessibility and keyboard navigation
- Customization and extending
- Offline usage and privacy
- Performance considerations
- Testing and quality assurance
- Development workflow
- How to contribute
- Roadmap and future ideas
- Known limitations
- License and attribution
- Frequently asked questions

Why this project exists
Event tracking helps people stay on top of important dates without relying on external services. It matters in daily life and in work. You might want to celebrate a parent’s birthday, mark a wedding anniversary, remember the date you started a major project, or observe quarterly milestones. Keeping track of these events in a local, private way offers both peace of mind and simplicity. This project aims to deliver a clean, fast, and dependable experience that works offline and without a server.

Core ideas and design goals
- Local-first: All data lives in the browser. No back-end, no cloud storage, no account needed.
- Fast and responsive: The interface updates in real time as you add or edit events.
- Simple to use: A minimal, distraction-free UI helps you focus on the dates that matter.
- Extensible: You can customize colors, labels, and date formats to fit your preferences.
- Accessible: Keyboard friendly, screen reader support, and good contrast for readability.
- Self-contained: The app ships with its own styling and scripts, with a straightforward build path if you want to customize.

Features at a glance
- Create events with a title, date, type, and optional notes
- Edit, duplicate, and delete events
- See elapsed time since the event date
- See time remaining until the next milestone or anniversary
- Real-time calculations with years, months, days
- Local storage for data persistence across sessions
- No backend required; works offline
- Optional color tags for quick visual grouping
- Keyboard shortcuts for power users
- Lightweight and fast, with a responsive layout

How it works under the hood
Event Tracker is a single-page application built with vanilla JavaScript and CSS. It uses the browser’s localStorage API to persist user data. When you load the page, scripts read the stored events and render them in the UI. Any changes you make—adding, editing, or deleting events—are written back to localStorage, ensuring the data survives page reloads and browser restarts.

Key ideas that guide the code
- Data is plain and serializable: an array of event objects stored as JSON strings.
- Time math is performed using the built-in Date object. Timezone considerations are handled by relying on local date interpretation.
- Rendering is deterministic: the UI renders from the data model on each update to avoid drift.
- Lightweight state management: a small set of functions manage events and the UI without introducing heavy libraries.

Data model and local storage
Event objects contain:
- id: a unique string (often generated from a timestamp)
- title: string describing the event
- date: the start date of the event in ISO format (YYYY-MM-DD)
- type: category such as birthday, anniversary, milestone, or other
- notes: optional text for context
- color: optional string for a visual tag (e.g., hex color)
- createdAt: timestamp of creation
- updatedAt: timestamp of last modification

Local storage usage
- Storage key: event-tracker.events
- Data format: JSON.stringify(events)
- Read path: JSON.parse(localStorage.getItem(key) || '[]')
- Save path: localStorage.setItem(key, JSON.stringify(events))

Backup and data migration
- Manual backup: copy the JSON string from localStorage and paste it into a text file.
- Restore: paste the JSON string back into localStorage when needed.
- Migration tips: when changing the schema, write small helper functions that map old structures to new ones during startup.

Getting started and running locally
Direct download is available from the releases page. The releases page hosts the packaged build you can download and run on your machine. This project does not require a server to run locally, but you can use a simple server if you prefer. The simplest path is to open the main HTML file directly in your browser, but running from a local server helps with certain edge cases and mimics a production environment.

- Prerequisites
  - A modern web browser with JavaScript enabled
  - If you want to run a local server for testing beyond opening the file, you can use a simple static server

- Quick start (no server)
  1. Download the latest release package from the releases page.
  2. Unzip the package if needed.
  3. Locate and open index.html in your browser.
  4. Start adding events from the UI and watch the live calculations.

- Quick start (local server)
  - Python 3.x: Run python -m http.server 8000 from the project root (or the folder that contains index.html), then visit http://localhost:8000
  - Node.js with http-server (if you have it installed): npx http-server -p 8000
  - Any other static server is fine as long as it serves the index.html and assets correctly

- What you will see
  - A clean interface with a list of events
  - A form to add new events with fields for title, date, type, and notes
  - A visual tag color to color-code your events
  - A local calendar-like display or a list view depending on your layout

- Where to put your data
  - Your browser stores the data in localStorage. There is no external database or server involved. This design helps protect privacy and reduces setup complexity.

- Security and privacy considerations
  - Data stays in your browser unless you export it or copy it to another location
  - There is no network communication unless you explicitly integrate a feature to export or share data
  - If you clear your browser storage, all event data will be removed

User guide: adding, editing, and viewing events
- Adding events
  - Click the "Add Event" button
  - Enter a descriptive title (e.g., “Grandma’s Birthday”)
  - Pick a date using the date field
  - Choose a type from the predefined categories
  - Optionally add notes to capture context or reminders
  - Select a color tag for quick visual grouping
  - Save to store the event in localStorage

- Editing events
  - Each event in the list has an edit option
  - Modify any field and save changes
  - The updatedAt timestamp is refreshed, and the elapsed time is recalculated

- Deleting events
  - Remove an event if it is no longer relevant
  - Deletions are immediate and reflected in the UI and localStorage

- Viewing elapsed time
  - The app computes time since the event date
  - It also computes the time until the next anniversary or milestone, if applicable
  - Time is shown in years, months, and days where meaningful

- Sorting and filtering
  - You can sort events by date, type, or title
  - Filter by type to focus on a subset of events
  - Use search to locate a specific event quickly

Calculations and time math explained
- Time since event
  - For a given date, the app calculates the difference between today and the event date
  - The result is expressed as years, months, and days
  - The calculation accounts for varying month lengths and leap years to keep results accurate

- Time to next milestone
  - For recurring anniversaries (e.g., every year), the app determines the next occurrence
  - It then computes the time remaining to that date
  - This helps you plan celebrations or reminders well in advance

- Handling edge cases
  - If an event has a future date, the “elapsed” value shows days until the event
  - If an event has already passed, the elapsed value shows how long since the event
  - The app gracefully handles invalid dates by emitting a readable error state in the UI

UI and theming details
- Layout
  - The interface is responsive to fit both desktop and mobile screens
  - A left or top navigation area provides quick access to common actions
  - The main content area shows a list or grid of events with clear typography

- Color and theming
  - Each event can have a color tag
  - The color helps categorize events at a glance
  - You can customize color options in the settings if you choose to extend the app

- Typography and readability
  - The UI uses straightforward typography for readability
  - Font sizes adapt to screen width to preserve legibility
  - High-contrast color pairs ensure good visibility in different lighting conditions

- Visual cues
  - Badges indicate event type
  - Progress indicators show how close an upcoming event is to its milestone
  - Micro-interactions provide feedback on user actions like add, edit, and delete

Accessibility and keyboard navigation
- Focus management
  - Keyboard focus moves logically through interactive elements
  - The tab order follows a natural reading order

- ARIA and labels
  - Form fields have descriptive labels
  - Buttons have accessible names
  - Dynamic updates announce changes to assistive technology

- Color contrast
  - Contrast ratios are chosen to be accessible
  - Color tags supplement the text, not replace it

Customization and extending
- CSS and theming
  - The project ships with a clean CSS baseline
  - You can swap in your own CSS to change the look
  - If you want to adopt a utility-first approach, you can replace parts with Tailwind CSS utilities

- Adding new event types
  - Extend the set of event types in the data model
  - Add new color options for branding or personal preference
  - Ensure the UI reflects new types in filters and badges

- Localization and formatting
  - Date formatting can be adjusted to match locale preferences
  - Time-to-human formats (years, months, days) can be tuned to user expectations

- Data export and import
  - Implement export to JSON for backups
  - Import from JSON to restore from a backup
  - Ensure the import validates the data format to avoid corruption

Offline usage and privacy
- Work completely offline
  - All data remains in localStorage
  - No external calls or back-end integration is needed
  - This makes the app resilient in environments with poor connectivity

- Privacy implications
  - Your data is private to your browser
  - If you share a device, you should sign out or clear storage to protect your data

Performance considerations
- Light footprint
  - The codebase is small and efficient
  - Rendering updates are batched to avoid unnecessary reflows

- Memory usage
  - The number of events grows, but the data structure remains simple
  - LocalStorage usage remains modest unless you store a very large number of events

- Browser compatibility
  - The app relies on widely supported web APIs
  - It works in modern browsers and gracefully degrades in older environments

Testing and quality assurance
- Manual testing
  - Create a test set of events with different dates
  - Verify elapsed time calculations, filtering, and sorting
  - Test editing and deleting flows
  - Check persistence by refreshing the page

- Automated testing
  - If you add tests, you can simulate user interactions and verify localStorage writes
  - Unit tests can cover the time math helpers to ensure accuracy across edge cases

- Visual regression
  - When you modify UI, compare screenshots to ensure layout stability

Development workflow
- Repository structure overview
  - index.html: The entry point for the app
  - assets/ : Images, icons, fonts, and other static assets
  - scripts/ : JavaScript modules that manage data and UI
  - styles/ : CSS files and theme files
  - README.md: Documentation for developers and users
  - releases/ : Release bundles and packaged assets

- Build and tooling
  - The project is designed to work without a heavy build step
  - If you want to optimize assets or generate a production build, you can introduce a simple bundler
  - A minimal script can bundle JavaScript modules into a single file for faster loading

- Local development tips
  - Use a lightweight server for a more realistic environment
  - Keep your edits focused on small components to ease debugging
  - Regularly back up your localStorage to avoid data loss during development

- Versioning
  - The repository follows semantic versioning for releases
  - Every release increments the version number to reflect changes accurately
  - Users should refer to the releases page to see what changed

Contributing
- How to contribute
  - Start with a well-defined issue or feature request
  - Open a pull request with a clear description of changes
  - Include tests or demonstration snippets where applicable
  - Maintain code style consistency and add comments where helpful

- Coding standards
  - Use clear, descriptive names for functions and variables
  - Keep functions focused on a single responsibility
  - Document any non-obvious logic, especially time calculations
  - Avoid unnecessary complexity; prefer straightforward approaches

- Local setup for contributors
  - Clone the repository
  - Open index.html in a browser to see the app
  - Make changes in the JavaScript and CSS files
  - Run tests if you set up a test environment
  - Create a pull request with a summary of changes

- Review process
  - Maintainers review changes for correctness, performance, and accessibility
  - Feedback focuses on correctness of time calculations, UX clarity, and code quality
  - Expect iterative improvements before merging

Roadmap and future ideas
- Internationalization
  - Add localization for date formats and language translations
  - Provide locale-aware relative time strings

- Richer time calculations
  - Support for quarter-based or week-based milestones
  - Configurable reminder times and notification settings

- Data portability
  - Create export and import formats that work across devices
  - Enable cloud backup options with opt-in safeguards

- UI enhancements
  - Improve responsive layouts for various screen sizes
  - Add drag-and-drop reordering of events
  - Provide a calendar view alongside the list view

- Theming and branding
  - Let users save multiple themes
  - Allow custom CSS injection for advanced users

- Testing improvements
  - Add automated tests for edge cases like leap years and DST changes
  - Provide a small test runner to verify time math consistently

Known limitations
- Time calculations rely on the local system clock and timezone
- Data is stored in localStorage; users who clear storage lose data
- The app does not sync across devices unless you export/import data

License and attribution
- This project is released under the MIT License
- Attribution is simple: mention the repository name in your own project if you reuse code
- For asset usage, ensure you comply with licenses for any external images or icons you incorporate

Frequently asked questions
- Can I run this offline?
  - Yes. The app stores data locally and does not require network access after the initial load.
- Where is my data stored?
  - In your browser's localStorage. It does not leave your device unless you export it.
- How do I back up my data?
  - Export the JSON data from the localStorage and save it to a file. You can also copy the JSON string and paste it into a text file.
- How do I customize the look?
  - Modify the CSS files or swap in your own theme. If you use Tailwind CSS, you can adapt the project to use Tailwind utilities.
- How do I add a new event type?
  - Extend the data model with a new type value and update the UI to display and filter by that type.

Assets and usage notes
- Release assets
  - The releases page hosts the downloadable build you can run locally. To obtain the latest version, visit the releases page and download the package that matches your environment. The link to the releases page is provided above for convenience.
  - For quick access, you can use the badge above that links to the releases page. This badge is a visual cue that points users to the same destination: https://github.com/keshavgorasiya/event-tracker/releases

- Imagery and icons
  - The project uses simple, flat icons for clarity
  - You can replace icons with your own assets if you customize the UI
  - Any imagery you add should be small and purpose-driven to keep the app fast

- A note on branding
  - If you deploy a customized version, keep the core functionality intact
  - Respect the license of any third-party assets you incorporate

Release notes and version history
- Unreleased and past versions
  - Each release includes notes about new features, improvements, and bug fixes
  - It is useful to read the release notes to understand what changed and how to adapt your workflow

Community and support
- Community discussions
  - Join the project discussions to share ideas or report issues
  - Be respectful and constructive in your feedback

- Issue reporting
  - When you report an issue, provide steps to reproduce
  - Include screenshots or GIFs if possible
  - Mention your environment (browser, OS, version) to help diagnosis

Code of conduct
- We expect collaboration to be civil and productive
- Be kind and patient with others
- Keep feedback focused on ideas and implementations

Final housekeeping
- If you want to download again later
  - The releases page is your primary source for stable builds
  - Use the badge or the direct link to navigate there
- If you want to contribute
  - Review the contributing guidelines
  - Start with small, self-contained changes
  - Seek feedback from maintainers early

This README describes a practical, privacy-respecting solution for tracking events and anniversaries. It emphasizes local storage, offline capability, and an approachable user experience. The project aims to stay lean while offering enough customization to fit diverse needs.

Topics
- anniversary-tracker
- css3
- event-tracker
- fontend
- html5
- javascript
- local-storage
- no-backend
- productivity-tool
- single-page-application
- tailwindcss
- time-tracking
- vanilla-js
- webapp

Releases
- For the latest release package, see the releases page: https://github.com/keshavgorasiya/event-tracker/releases

Notes about usage and deployment
- This project is intended for developers and power users who want a reliable, private way to track dates
- You can customize the UI and behavior to match your preferences
- If you plan to host a copy of this app on your own site, you can repack the assets for distribution and maintain your own versioning

End-user tips and best practices
- Keep a short list of core events you care about to start
- Use color tags to group events by category
- Regularly back up your data to avoid loss
- When you need a fresh start, export the data, reset the app, and re-import if needed

A note on structure and future expansion
- The codebase is designed to be approachable
- You can split the logic into modules to improve maintainability
- As the project grows, you can introduce state management primitives or small libraries for better scalability

Thank you for exploring Event Tracker. This tool is crafted to be simple, reliable, and privacy-conscious, while still offering the flexibility you need to keep track of life’s important dates.