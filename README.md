# Rails Models: Generating and Using the Database

Rails models represent the data and business logic of your application. They are Ruby classes that map to database tables.

## Generating a Model

To generate a model called `Article` with a `title` (string) and `body` (text), run:

```sh
bin/rails generate model Article title:string body:text
```

This creates:
- A migration file in `db/migrate/`
- A model file in `app/models/article.rb`

## Running Migrations

To apply the migration and create the `articles` table in your database:

```sh
bin/rails db:migrate
```

## Where Models Live

All model files are in the `app/models/` directory. For example:

```
app/models/article.rb
```

## Using the Rails Console

The Rails console lets you interact with your models and database directly:

```sh
bin/rails console
```

### Example Commands

```ruby
# Create a new article
article = Article.create(title: "First Post", body: "This is the body.")

# Find all articles
Article.all

# Find an article by ID
Article.find(1)

# Update an article
article.update(title: "Updated Title")

# Delete an article
article.destroy
```

### Example Output

```
> Article.create(title: "First Post", body: "This is the body.")
=> #<Article id: 1, title: "First Post", body: "This is the body.", ...>

> Article.all
=> [#<Article id: 1, title: "First Post", ...>]
```

---

This is how you generate and use models in Rails!
