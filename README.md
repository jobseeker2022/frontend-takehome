# Telegraph Frontend Take-home

This repo has everything you need to complete the take-home assignment. Know that we are excited about you as a candidate, and can't wait to see what you build!

Applicant Note:

for Mapbox API, place your API token in a .env file locally at the root of this projec, using the variable name found in env.example

## Requirements

- Node v14 or above
- Yarn `$ npm install --global yarn`

## Getting Started

### Installation and setup

1. Fork and clone this repo onto your own computer
2. Install the dependencies via Yarn `$ yarn install`

### Recommended IDE Setup

- [VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar)

### Running the dev server

- From your repo, run `$ yarn run dev` to start the Vite dev server.
- Navigate to `localhost:3000` to see your application running in a browser.

## Expectations

- Fetch API data in your top-level component i.e. `App.vue` and feed down into child components
- Install and configure a CSS framework like Bulma or Material (Bulma preferred!). [Bulma docs](https://bulma.io)
- Use dayjs, date-fns or another similar library for parsing and formatting dates.
- Display information in a map using [MapboxGL](https://docs.mapbox.com/mapbox-gl-js/example/simple-map/)
  - The MapboxGL library is included as an npm dependency
  - You will need to create a Mapbox account and use the associated access token
- Use Vue 3 to create your components. [Composition API](https://v3.vuejs.org/guide/composition-api-introduction.html#introduction) is preffered, but not required.
- Break your app down into smaller components wherever it seems practical. Your `App.vue` should only handle fetching data and rendering child components.
- Complete the assignment according to the below "user stories" and the linked mockup(s)
- Don't overdo it! Spend 3-4 hours working, commit, and push up to a feature branch in your forked repo.

## User Stories

### 1. Header Information

As a user, I expect to see a header with "Waybill Details" present at the top of the application.
Beneath the header, I expect to see a table view with an overview of the waybill data. This table should include the following:

- Waybill equipment ID
- Waybill created date in MM/DD/YYYY format
- Waybill origin
- Waybill destination
- Waybill asset status
- Waybill ETA in MM/DD/YYYY format
  - **BONUS**: Add conditional logic to render waybill ETA with red text if ETA is in the past and waybill asset status is not "Complete"

### 2. Map Markers

As a user, I expect to see a map displaying key waybill locations as map markers.

- The map should be centered between the waybill origin and destination long/lat pairs.
- Markers should be added to the map for each milestone in the waybill `milestones` property.
- Use the first available long/lat pair from each milestone's `events` array to create the markers.
- There should be 1 marker for each milestone, provided the `milestone.events` array contains at least 1 event with a valid long/lat.

### 3. BONUS: Full Event List

**Note**: This user store is optional, and on an "if-you-have-time" basis.

As a user, I expect to be able to view the full list of waybill events.

- The event list should be populated from the `waybill.events` property.
- The list should **not** be displayed by default.
- I should see a link or button with the text, "View events"
- When I click the "View events" link, I should be presented with the full events list
- The events list can either be a modal which appears, or a panel that expands/collapses

## Fetching data

- Your project should make an async request for JSON data when the root component mounts to the DOM.
- Make sure you have default and/or "loading" UI elements to render while the request is in-progress.
- Sample data is available from the following API endpoint: https://mocki.io/v1/de8e9ad3-bd34-445e-87b3-c44e6e3efbe9
- Use a library like Axios, or the built-in [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) to fetch data.

## Mockup

- Follow [this Figma mockup](https://www.figma.com/file/ejrZ0CzAEJ4zLtlXyvB8Po/FE-take-home?node-id=0%3A1) for the general layout of your project
- Feel free to select colors, fonts etc. but don't feel pressured to do so.
