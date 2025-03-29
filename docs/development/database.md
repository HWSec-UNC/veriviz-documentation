# On the Database

The database is something that could use an upgrade. Right now, it is very simple and uses PostgreSQL and a service know as neontech, check out [here](https://neon.tech/). We are using the free tier of neon tech whcih has a limited amount of memory(0.5 GB) and read/writes. What is store in the database is:
| id | name | date | type | json_data | output_text |
| -- | ---- | ---- | ---- | --------- | ----------- |
Where
- **id** is the primary key
- **name** is the name the user gives when submitting
- **Date** is the date and timestamp of the submission
- **Type** is the engine the user selects(Sylvia or SEIF)
- **json_data** is the json data returned from the engine to display the graph view
- **output_text** is the outputted text file from the engine

For access to the neon tech databse website, contact us. How it works in deployment is the databse acess is store din a private `.env` file that we have to OKD when first deploying.