---
layout: post
title:      "Using JavaScript and Rails to create and render objects"
date:       2019-04-25 13:09:18 +0000
permalink:  using_javascript_and_rails_to_create_and_render_objects
---


**ConU or Contribution University is an app** for software developers that want to track their contributions to open source projects. I built the first version of this todo-style app with Ruby on Rails (RoR) with an SQLite database and have now added the use of JavaScript (JS) and an Active Model Serializer JSON Backend to create model objects and render an index and show page without a page refresh.

**To add JavaScript to this app** I was mainly working in two view files and two JS files each being related to the Project and Issue models I defined in the initial RoR-only version. In the two JS files, projects.js and issues.js, I created prototypes for the two objects and used the same pattern to replace the Rails way of displaying newly instantiated objects in the DOM with the JavaScript way of doing so.

**Here is a summary of that pattern:**

**Step 0: Render a form** for creating a resource in the view using Rails

**Step 1: Hijack the default Rails form submission** to dynamically submit the form through JavaScript and JSON without a page refresh.

`// Hijack form submit event for all forms with id of new_issue (automatic rails id assignment)
Issue.formSubmitListener = function(){
  $('form#new_issue').on("submit", Issue.formSubmit)
}

Issue.formSubmit = function(e){
  e.preventDefault()
  // Get data needed to submit form via AJAX
  var $form = $(this);
  var action = $form.attr("action");
  var params = $form.serialize();

  // Fire post request and request json
  $.ajax({
    url: action,
    data: params,
    dataType: "json",
    method: "POST"
  })
  // Delegate behavior to prototype
  .success(Issue.success)
  .error(Issue.error)
}`

**Step 2: Translate JSON responses** from Rails into JS Model Objects the ES6 way thus instantiating a new Project or Issue object 

`function Issue(attributes){
  this.description = attributes.description;
  this.id = attributes.id;
}

// Render the li of the new issue upon successful form submission
Issue.success = function(json){
  // Create/instantiate new JS object from json of the issue that was just created
  var issue = new Issue(json);
  // Build function on prototype that when called will return equivalent of Rails partial
  var issueLi = issue.renderLI()

  // Inject li into ul
  $("ul.todo-list").append(issueLi)
  render issue
}

// Build li component using handlebars
Issue.prototype.$li = function(){
  return $("li#issue_"+this.id)
}`

**Step 3. Use Handlebars.js templates** in the Project and Issue views to inject that JSON object into the DOM thus dynamically render serialized object relationships on the page without a refresh 

`<script id="issue-template" type="text/x-handlebars-template">
  <li class="issue" id="issue_{{id}}">
    <div class="view">
      <form class="edit_issue" id="edit_issue_{{id}}" action="/projects/<%= @project.id %>/issues/{{id}}" accept-charset="UTF-8" method="post"><input name="utf8" type="hidden" value="✓">
        <input type="hidden" name="_method" value="patch">
        <%= hidden_field_tag :authenticity_token, form_authenticity_token %>
        <input name="issue[status]" type="hidden" value="0"><input class="toggle" type="checkbox" value="1" name="issue[status]" id="issue_status"></form>

      <label>{{description}}</label>

      <form class="button_to" method="post" action="/projects/<%= @project.id %>/issues/{{id}}">
        <input type="hidden" name="_method" value="delete">
        <input class="destroy" type="submit" value="x">
        <%= hidden_field_tag :authenticity_token, form_authenticity_token %>
      </form>
    </div>
  </li>
</script>`

**It was gratifying to be able to submit forms** and render newly created instances of objects in the DOM without a page refresh. By the end of this phase of the project, I had developed an appreciation for how JS and RoR can work together to deliver a high-quality user experience and also maintaining a sense of separation of concerns throughout the MVC architecture model.
