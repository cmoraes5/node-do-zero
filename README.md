 ## Video API

This API allows you to manage videos. You can create, list, update, and delete videos.

### Prerequisites

- Node.js 16 or later
- PostgreSQL database

### Installation

1. Clone this repository.
2. Run `npm install`.
3. Create a `.env` file and add your PostgreSQL database connection string to it.
4. Run `npm start`.

### Usage

The API is available at the following endpoints:

- `/videos`: List all videos.
- `/videos/:id`: Get a specific video.
- `/videos`: Create a new video.
- `/videos/:id`: Update a video.
- `/videos/:id`: Delete a video.

### Code Explanation

The code is divided into the following files:

- `create-table.js`: Creates the `videos` table in the PostgreSQL database.
- `database-postgres.js`: Contains the `DatabasePostgres` class, which implements the methods for interacting with the PostgreSQL database.
- `db.js`: Imports the `postgres` library and creates a connection to the PostgreSQL database.
- `server.js`: Starts the Fastify server and defines the routes for the API.

The following code snippets explain the key parts of the code:

```js
// create-table.js

sql`
  CREATE TABLE videos (
    id          TEXT PRIMARY KEY,
    title       TEXT,
    description TEXT,
    duration    INTEGER
  )
`.then(() => {
  console.log('Tabela criada!') // This will give me feedback when the table is finished being created.
})
```

This code creates the `videos` table in the PostgreSQL database. The `id` column is the primary key, and the `title`, `description`, and `duration` columns are text, text, and integer, respectively.

```js
// database-postgres.js

export class DatabasePostgres {

  async list(search) {
    let videos

    if (search) {
      videos = await sql`select * from videos where title ilike ${'%' +search + '%'}`
    } else {
      videos = await sql`select * from videos`
    }

    return videos
  }

  async create(video) {
    const videoId = randomUUID()

    const { title, description, duration } = video

    await sql`insert into videos (id, title, description, duration)
  }
}
    
