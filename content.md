# Component-Based View Templates 🧩

## Introduction
Component-Based View Templates are a design pattern that helps in maintaining a clean, consistent, and reusable codebase. This lesson will introduce you to creating reusable view components in Rails using [partials](https://edgeapi.rubyonrails.org/classes/ActionView/PartialRenderer.html), focusing on implementing a card component styled with [Bootstrap](https://getbootstrap.com/).

## Objectives
By the end of this lesson, you will be able to:

1. Understand the benefits of using view components.
2. Create a reusable partial for a [Bootstrap card](https://getbootstrap.com/docs/5.3/components/card/) component.
3. Use the partial in various views across your Rails application.

## Why Use Component-Based View Templates?
Component-Based View Templates helps keep your views DRY (Don't Repeat Yourself) and makes them easier to manage. Instead of repeating the same HTML code across multiple views, you can create a single, reusable partial. This not only saves time but also ensures consistency in the design and behavior of elements like cards, forms, and buttons across your application.

## Example: Creating a Card Component
First, ensure you have Bootstrap integrated into your Rails application. For this example, we'll assume Bootstrap is set up and ready to use.

1. Create file
Create a new file at `app/views/posts/_card.html.erb`. This will be our partial for the card component.

2. Add HTML for the Card
Inside `_card.html.erb`, write the HTML needed to display a card. Utilize Bootstrap classes to style the card properly.

```erb
<!-- app/views/posts/_card.html.erb -->
<div class="card">
  <% if post.image.present? %>
    <img class="card-img-top" src="<%= post.image.url %>" alt="Card image cap">
  <% end %>
  <div class="card-body">
    <h5 class="card-title"><%= post.title %></h5>
    <p class="card-text"><%= post.content %></p>
  </div>
</div>
```

Here, post is assumed to be a local variable that will be passed to the partial. It contains attributes like title, content, and image.

<!-- TODO: explain @ vs locals -->

3. Use the Partial
To use the partial in your views, you'll pass the post object to the partial as a local variable. In any view file, render the partial as follows.

```erb
<!-- Render the card partial for a post -->
<%= render "posts/card", post: @post %>
```

### Displaying A Collection
You can loop through an array of posts and render the card for each one.
```erb
<% @posts.each do |post| %>
  <%= render "posts/card", post: post %>
<% end %>
```

Or use the [collection](https://api.rubyonrails.org/classes/ActionView/PartialRenderer.html) shorthand.
```erb
<%= render partial: "posts/card", collection: @posts, as: :post %>
```

## Best Practices
- **Naming Conventions**: Name your partials starting with an underscore (_) to differentiate them from regular view files.
- **Local Variables**: Always pass local variables explicitly to your partials. This makes dependencies clear and avoids relying on instance variables `@`, which can make your code harder to understand.
- **Keep Partials Small**: Aim to keep your partials focused and small. If a partial grows too large, consider breaking it down into smaller components.
- **Consider Defining Accepted Locals**: [Rails 7.1 gives templates more control over the locals they receive](https://www.shakacode.com/blog/rails-7-1-allows-templates-to-define-accepted-locals/). In our example, `app/views/posts/_card.html.erb` could use a magic comment to restrict the local variable it can accept to only `post`.

```erb
<%# locals: (post:) %>
```

## Quiz

- What is the main benefit of using Component-Based View Templates in Rails?
- They improve database performance.
  - Not quite. The main benefit is reducing code duplication and improving maintainability.
- They help keep views DRY (Don't Repeat Yourself) and make them easier to manage.
  - Correct! Component-Based View Templates reduce redundancy and improve manageability.
- They enhance user authentication.
  - Not quite. Component-Based View Templates are primarily about code organization and reusability.
{: .choose_best #component_based_templates title="Benefits of Component-Based View Templates" points="1" answer="2" }

- Why should you name your partials starting with an underscore (_)?
- To differentiate them from regular view files.
  - Correct! The underscore helps distinguish partials from regular view files.
- To make them load faster.
  - Not quite. The underscore is for naming convention, not for performance.
- To enhance security.
  - Not quite. The underscore is for naming convention, not security.
{: .choose_best #naming_partials title="Naming Conventions for Partials" points="1" answer="1" }

- Why should you aim to keep your partials focused and small?
- To improve application performance.
  - Not quite. While organization is important, it doesn't directly impact performance.
- To handle user authentication.
  - Not quite. Keeping partials small is about maintainability and readability, not authentication.
- To make them easier to understand, maintain, and reuse.
  - Correct! Smaller, focused partials are easier to work with and promote reusability.
{: .choose_best #keeping_partials_small title="Keeping Partials Small" points="1" answer="3" }

## Conclusion
Using component-based view templates in Rails applications allows you to build a more maintainable and scalable front-end. By extracting repeated HTML structures into partials, you reduce redundancy, simplify updates, and achieve a more consistent user interface. This technique is powerful when combined with frameworks like Bootstrap, enabling rapid development of visually appealing features.
