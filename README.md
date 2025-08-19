# Rails Models: Generating and Using the Database

Models are the backbone of any Rails application. They represent the data and business logic of your app, acting as the bridge between your Ruby code and the database. Understanding how to generate, use, and interact with models is essential for building dynamic, data-driven web applications.

---

## What is a Model in Rails?

A model in Rails is a Ruby class that maps to a table in your database. Each instance of the model represents a row in that table. Models handle:
- Data storage and retrieval
- Business logic and validations
- Associations (relationships) with other models

For example, an `Article` model might represent blog posts, with each article having a title and body.

---

## Generating a Model

Rails makes it easy to create new models using a generator. To generate a model called `Article` with a `title` (string) and `body` (text), run:

```sh
bin/rails generate model Article title:string body:text
```

This command creates several files for you:
- A migration file in `db/migrate/` (to create the `articles` table)
- A model file in `app/models/article.rb`
- A test file in `test/models/article_test.rb` (if using the default test framework)

**Tip:** You can add more fields by listing them after the model name, e.g. `author:string published_at:datetime`.

---

## Understanding Migrations

Migrations are Ruby files that describe changes to your database schema. When you generate a model, Rails creates a migration to add the corresponding table and columns.

To apply the migration and create the `articles` table in your database, run:

```sh
bin/rails db:migrate
```

If you ever need to change your database structure (add/remove columns, etc.), you can generate new migrations with:

```sh
bin/rails generate migration AddAuthorToArticles author:string
bin/rails db:migrate
```

---

## Where Models Live

All model files are stored in the `app/models/` directory. By convention, each model is a singular noun and the file is named in snake_case. For example:

```
app/models/article.rb
```

The model class name is always capitalized and singular (e.g., `Article`).

---

## Exploring the Model File

Open `app/models/article.rb` and you’ll see a class like this:

```ruby
class Article < ApplicationRecord
	# Add validations, associations, or methods here
end
```

By inheriting from `ApplicationRecord`, your model gets powerful features for free, like database access and validations.

---

## Using the Rails Console

The Rails console is a powerful tool for interacting with your models and database directly. It’s great for experimenting, debugging, and testing out code.

Start the console with:

```sh
bin/rails console
```

Once inside, you can run Ruby code and interact with your models:

### Example Commands

```ruby
# Create a new article (does not save to DB)
article = Article.new(title: "First Post", body: "This is the body.")

# Save the article to the database
article.save

# Or create and save in one step
Article.create(title: "Second Post", body: "Another body.")

# Find all articles
Article.all

# Find an article by ID
Article.find(1)

# Update an article
article.update(title: "Updated Title")

# Delete an article
article.destroy

# Find articles with a condition
Article.where(title: "First Post")
```

### Example Output

```
> Article.create(title: "First Post", body: "This is the body.")
=> #<Article id: 1, title: "First Post", body: "This is the body.", ...>

> Article.all
=> [#<Article id: 1, title: "First Post", ...>]

> Article.where(title: "First Post")
=> [#<Article id: 1, title: "First Post", ...>]
```

---

## Adding Validations

Models can enforce rules about your data using validations. For example, to require every article to have a title:

```ruby
# app/models/article.rb
class Article < ApplicationRecord
	validates :title, presence: true
end
```

Now, if you try to save an article without a title, it won’t work:

```ruby
Article.create(body: "Missing a title!")
# => Article not saved, title can't be blank
```

---

## Model Associations

Models can be related to each other. For example, if you have a `User` model and an `Article` model, you might set up associations like this:

```ruby
# app/models/user.rb
class User < ApplicationRecord
	has_many :articles
end

# app/models/article.rb
class Article < ApplicationRecord
	belongs_to :user
end
```

This lets you do things like:

```ruby
user = User.find(1)
user.articles # returns all articles written by this user

article = Article.first
article.user # returns the user who wrote the article
```

---

## Wrapping Up

Models are a core part of Rails, connecting your Ruby code to your database and enforcing your app’s business logic. As you build more features, you’ll use models to store data, validate input, and define relationships between different parts of your app.

**Next Steps:**
- Try adding validations or associations to your models.
- Experiment with the Rails console to create, update, and query records.
- Read more in the [Rails Active Record Basics Guide](https://guides.rubyonrails.org/active_record_basics.html).

With practice, you’ll become comfortable using models to power your Rails applications!
