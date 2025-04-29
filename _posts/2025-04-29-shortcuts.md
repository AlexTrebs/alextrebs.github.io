<h1 align="center">
  <img width="300px" src="https://github.com/AlexTrebs/shortcut/raw/refs/heads/main/docs/images/icon.png" />
</h1>
<h5 align="center">A fast, simple, browser shortcut tool.</h1>

## The problem

Daily I find myself often forgetting useful websites, remembering their use case and a name that I know them by, which conveniently is never the name of the site.

I have often used bookmarks as a solution to this, but with a deep dark nested bookmarks (with some as old as 10 years old now) this seems like a inadequate solution.

I had thought about trying to implement this to help this productivity hurdle for quite some time now. What I needed is an easy way to search by familiar terms for myself to more easily remember and access my commonly used websites.

Too many times have I searched "images" in my search bar to go from google to google images to access reverse search. There are huge draw backs to the complexity of search engines these days which I have sought to remove with this helpful app.

## The solution

I call this `Shortcut`. Currently it is designed to run as a standalone application on your PC. 

With some qiuck easy steps, you can configure a search term in your browser to shortcut to this application. This will reroute you to the website desired if there is an exact match, otherwise reroute you to Shorcut webapp to show you the closest results.

From here you have free reign over your shortcuts. You can delete them, update them, rename them, and create them. I have even add a light/dark mode!

![](https://github.com/AlexTrebs/shortcut/raw/refs/heads/main/docs/images/shortcuts_demo.gif)

## Architecture

This project is a Rust HTMX monolith application.

[HTMX](https://htmx.org) is a lightweight HTML templating structure that allows you to swap elements in the DOM through function returns.

For the templating system, we are using [Tera](https://docs.rs/tera/latest/tera/), which uses Jinga-inspired templates.

With Tera, we have chosen to use the [tera-hot-reload](https://github.com/oxidlabs/tera-hot-reload) crate. This allows for quick and easy development of the ui.
 
Roughly a page template can be described like below:

```rust
#[derive(TeraTemplate, Serialize)]
#[template(path = "template.html")]
pub struct Template {
  pub title: String
}

pub fn getTemplate(tera: Tera) {
  let context = Template { title: "template" }

  return Html(self.render(tera));
}
```

Where an example template.html can be: 

```html
{% extends "base.html" %}
 
{% block title %}{{ title }}{% endblock %}
 
{% block content %}
<main class="ml-14 pl-5 flex-1 p-4 dark:bg-neutral-800" style="justify-items: center;" >
  <div id="load-error" class="dark:text-white"></div>
  {% include "components/search/search.html" %}
  <div id="results" \>
</main>
{% endblock %}
```

With api calls, we then set the results div as the target for the output of a function. 

More examples of this can be seen in: 
- [HTMX templates directory](ui/templates)
- [Rust templates directory](src/templates)
- [Routes](src/routes/shortcut.rs)
- [Service](src/service/shortcut.rs)

The interaction between our server and our database is [sqlx](https://docs.rs/sqlx/latest/sqlx/).

In an ideal world, I would use [sqlean](https://github.com/nalgeon/sqlean), [spellfix1](https://sqlite.org/spellfix1.html) extension, or [elastic-rs](https://github.com/elastic/elasticsearch-rs?tab=readme-ov-file) to allow fuzzy searching within the database. 

But for simplicity's sake, we are currently using a [SQLite](https://sqlite.org) database without any extensions.

This means that our searches will require pulling the entire shortcut database and searching/sorting within the Rust layer. This in practice is not as bad as you think due to Rust's fast nature.

Finally, we use [tailwind](https://tailwindcss.com) for our component styling.

## If I was to re-implement it, what would it look like



## So what does this mean for the future?