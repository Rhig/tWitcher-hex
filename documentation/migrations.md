# Migrations

This project uses <a href="https://typeorm.io/">TypeORM</a> to map MySQL tables into objects (called entities in the code). When we change an entity's definition (for example, change the name of a field), we need to change the DB's corresponding schema. This can be confusing, and cause a lot of issues as the project progresses, especially if we plan on having a production environment or sharing the code among several development and test environments.

The solution for this is <a href="https://typeorm.io/migrations#migrations">migrations</a> - code that contains the SQL commands to apply or revert changes to the DB schema.

## How to generate a migration

Generating a migration means automatically creating a migration file (a class that implements TypeORM's MigrationInterface) with the changes we've defined in the entities since the last migration was generated. We have an npm script command to do this:

```bash
# Make sure to run this from the hex-backend directory
npm run migration:generate --name=<my_migration_name>
```

This will generate the migration file under hex-backend/src/migrations/.

## How to apply a new migration

You can run migrations using the following command:

```bash
# Make sure to run this from the hex-backend directory
npm run migration:run
```

<strong>Note:</strong> This will try and find the migration files under hex-backend/dist/migrations, so you will need to run a command that builds the project (e.g. `nest build`) for it to work.

The DB has a table called 'migrations' which stores all of the applied migrations - this is how the script "knows" which migrations need to be applied, if any.
