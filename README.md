# LAB-Video-Game-Library-API

In this lab, you'll build a basic Express API to serve a collection of video game data. The data is provided as two JSON files:

- `games.js` — an array of video game objects.
- `platforms.js` — an array of platform objects.

## Setup

1. Install dependencies: Setup your project using `npm init -y` and install dependencies for `express`, `morgan`, and `uuid`
2. Load the data from the provided `.js` files and export your Express app.

3. The required routes are defined below.  Use Postman to test your routes as you write them.

4. Your app should filter and sort utilizing query parameters

5. Errors should be handled with `try-catch` blocks.  Appropriate error messages should be sent back to the user. 

---

## Routes

Your API should have a router for Games and a separate route for Platforms.  The following routes are required to implement

### `/api/games`

- `GET /api/games`

  - Returns a list of all games.

- `GET /api/games/:id`

  - Returns a single game by its UUID.

- `POST /api/games`

  - Adds a new game to the collection.
  - Expects a request body like this:
    ```json
    {
      "title": "Game Title",
      "releaseYear": 2025,
      "genres": ["Action", "Adventure"],
      "platforms": ["Switch", "PC"]
    }
    ```

- `PATCH /api/games/:id`

  - Updates an existing game.
  - Accepts any subset of fields from the POST format.

- `DELETE /api/games/:id`

  - Deletes the game with the given ID.

### `/api/platforms`

- `GET /api/platforms`

  - Returns a list of all platforms.

- `GET /api/platforms/:id`

  - Returns a single platform by its ID.

---

## Filtering and Sorting

Your application should support filtering and sorting of game and platform data through query parameters on the API endpoints.

## Games Endpoint: `GET /api/games`

This endpoint returns a list of games. It accepts the following **optional** query parameters to filter and sort the results:

- **`platform`**  
  Filters games by the platform name. Only games available on the specified platform will be returned.  
  *Example:* `?platform=Nintendo Switch` returns games released for the Nintendo Switch.

- **`genre`**  
  Filters games by genre. Only games that belong to the specified genre will be included.  
  *Example:* `?genre=RPG` returns games categorized as role-playing games.

- **`year`**  
  Filters games by release year. Only games released in the specified year will be returned.  
  *Example:* `?year=2025` returns games released in the year 2025.

- **`sortBy`**  
  Specifies the field to sort the results by. Supported fields are:  
  - `title` — Sorts games alphabetically by their title.  
  - `releaseYear` — Sorts games by their release year.

- **`order`**  
  Specifies the sort direction. Must be used together with the `sortBy` parameter.  
  - `asc` — Sorts in ascending order (A-Z or oldest to newest).  
  - `desc` — Sorts in descending order (Z-A or newest to oldest).

**Default sorting:** If no `sortBy` parameter is provided, games should be sorted alphabetically by `title` in ascending order.

**Example requests:**

- `GET /api/games?platform=PC&sortBy=releaseYear&order=desc`  
  Returns PC games sorted by release year from newest to oldest.

- `GET /api/games?genre=RPG`  
  Returns all RPG games sorted alphabetically by title.

---

## Platforms Endpoint: `GET /api/platforms`

This endpoint returns a list of available platforms. It accepts the following optional query parameter:

- **`sortBy`**  
  Specifies the field to sort platforms by. Supported fields are:  
  - `title` — Sorts platforms alphabetically by their name.  
  - `releaseYear` — Sorts platforms by their release year.

**Example requests:**

- `GET /api/platforms?sortBy=title`  
  Returns platforms sorted alphabetically.

- `GET /api/platforms?sortBy=releaseYear`  
  Returns platforms sorted by release year from oldest to newest.

  **Default sorting:** If no `sortBy` parameter is provided, games should be sorted alphabetically by `title` in ascending order.

## Bonus Goals

1. **Add Pagination**  
   Implement pagination for the `/api/games` endpoint using query parameters like `page` and `limit` to return a subset of results per request.

2. **Case-Insensitive Filtering and Sorting**  
   Make all filtering and sorting on games and platforms case-insensitive for a better user experience.
