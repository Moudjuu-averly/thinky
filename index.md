---
layout: default
hl: index
---


[![](/images/thinky-header.png)](/)

<header>
<div class="description">
    <h2>Thinky</h2>
    A light Node.js ORM for RethinkDB
</div>

<hr/>

<h3>Batteries included:</h3>
<ul>
<li>Schemas</li>
<li>All standard relations</li>
<li>Automatic creation of tables/indexes</li>
<li>And more!</li>
</ul>



</header>

### Quickstart

<p>Install via <code>npm</code>.</p>

<div class="highlight"><pre><code class="bash language-bash" data-lang="bash">npm install thinky
</code></pre></div>


Create models with schemas.

```javascript
var thinky = require('thinky')();
var type = thinky.type;

// Create a model - the table is automatically created
var Post = thinky.createModel("Post", {
    id: type.string(),
    title: type.string(),
    content: type.string(),
    idAuthor: type.string()
}); 

var Author = thinky.createModel("Author", {
    id: type.string(),
    name: type.string()
});

// Join the models
Post.belongsTo(Author, "author", "idAuthor", "id");
```

Save a new post with its author.

```js
// Create a new post
var post = new Post({
    title: "Hello World!",
    content: "This is an example."
});

// Create a new author
var author = new Author({
    name: "Michel"
});

// Join the documents
post.author = author;


post.saveAll().then(function(result) {
    /*
    post = result = {
        id: "0e4a6f6f-cc0c-4aa5-951a-fcfc480dd05a",
        title: "Hello World!",
        content: "This is an example.",
        idAuthor: "3851d8b4-5358-43f2-ba23-f4d481358901",
        author: {
            id: "3851d8b4-5358-43f2-ba23-f4d481358901",
            name: "Michel"
        }
    }
    */
});
```

And there is lot more! Here is a non exhaustive list:

- Enforce schemas.
- Multiple relations: `hasOne`, `belongsTo`, `hasMany` and `hasAndBelongsToMany`.
- Automatically create tables and indexes.
- Automatically remove relations when a document is deleted.

You can learn more about thinky with these links:

- The [quickstart](/thinky/documentation/)
- The [examples on GitHub](https://github.com/neumino/thinky/tree/master/examples)
- The [API documentation](/thinky/documentation/api/thinky/)
