# On the Database

Currently, Veriviz uses a **PostgreSQL** database hosted on a service called [Neon](https://neon.tech/). We’re on Neon’s free tier, which includes **0.5 GB** of memory and limited read/write operations. **This is a good starting point**, but a more robust solution is definitely needed if you want to contribute or improve the project.

## Database Table

Our main table holds the following columns:

| id  | name | date | type  | json_data         | output_text        |
|-----|------|------|-------|-------------------|--------------------|
| PK  |      |      |       | JSON Graph Output | Engine Output Text |

- **id** (primary key)
- **name**: User-defined name when submitting
- **date**: Date and timestamp of the submission
- **type**: Which engine the user selected (**Sylvia** or **SEIF**)
- **json_data**: JSON data returned from the engine to display the graph
- **output_text**: Console or text output from the engine

## Accessing Neon

We have an account on [neon.tech](https://neon.tech). If you need direct access to the Neon dashboard, please contact the team for credentials.

## Deployment Integration

Our database connection string is stored in a private `.env` file. When deploying on OKD, we inject these environment variables into the container so the application can read them (e.g., via `process.env.DATABASE_URL`). This setup ensures that our DB credentials remain private, even though the rest of the code is public.

