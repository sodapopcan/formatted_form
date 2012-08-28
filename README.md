# Bootstrap Builder

A Rails form builder that generates [Twitter Bootstrap](http://twitter.github.com/bootstrap) markup and helps keep your code clean.

* Includes Twiter Bootstrap 2.0.4 CSS and Javascript files
* Uses existing Rails helpers
* Auto-generates labels
* Generates horizontal, vertical and inline forms
* Groups of checkboxes
* Groups of radio buttons
* Prevents double clicking on submit buttons

## Installation

Add gem definition to your Gemfile and run `bundle install`:
    
``` ruby
gem 'bootstrap_builder'
```

Require it in your CSS and JS manifest files:

``` css
//= require bootstrap_builder
```

## Configuration

You can change the default configuration of this gem by adding the following code to you initializers:

``` ruby
BootstrapBuilder.configure do |conf|
  conf.default_form_class = 'form-vertical' # Set the form class. Default is 'form-horizontal'
end
```

## Usage (with haml)

Use `bootstrap_form_for` when you want to render a form with Bootstrap markup.

### A sample user form

``` ruby
= bootstrap_form_for @user, :url => [:admin, @user] do |f|
  = f.text_field :name
  = f.number_field :age, nil, :in => 1...100
  = f.email_field :email, :prepend => '@'
  = f.phone_field :phone
  = f.password_field :password
  = f.password_field :password_confirmation
  = f.select :role, User::ROLES
  = f.time_zone_select :time_zone
  = f.check_box :reminder, :label => 'Send Daily Reminder?'
  = f.submit 'Save'
```

### A login form

Add a class to the form or any field to change the way it is rendered.

``` ruby
= bootstrap_form_for @session_user, :url => login_path, :class => 'form-horizontal' do |f|
  = f.text_field :email
  = f.password_field :password
  = f.check_box :remember_me, :label => 'Remember me when I come back'
  = f.submit 'Log In'
```

### A search form

Hide the label by passing `:label => ''` on any field. (Useful for inline search forms)


``` ruby
= bootstrap_form_for @search, :url => [:admin, :users], :html => {:method => :get, :class => 'form-search'} do |f|
  = f.text_field :name_equals, :label => 'Find by', :placeholder => 'Name'
  = f.select :role_equals, User::ROLES, :label => ''
  = f.submit 'Search', :class => 'btn-default'
```

*(Example using [MetaSearch](https://github.com/ernie/meta_search) helpers)*

### Checkboxes

A single checkbox:

``` ruby
= f.check_box :send_reminder
```

A group of checkboxes:
  
``` ruby
= f.check_box :colours, :values => [['Red', 1], ['Green', 2], ['Blue', 3]]
```

Use the :help_block option to show the label on the right side:

``` ruby
= f.check_box :approved, :help_block => 'Label on the Right'
```


### Radio buttons

A single radio button:

``` ruby
= f.check_box :role, 'admin'
```

A group of radio buttons:

``` ruby
= f.radio_button :role, [['Admin', 1], ['Manager', 2], ['Editor', 3]]
```

### More examples

Override the autogenerated label by using the `:label` option on any element.

``` ruby
= f.text_field :name, :label => 'Full name'
```

Use `:append` and `:prepend` on any field:

``` ruby
= f.text_field :price, :append => '.00'
= f.email_field :email, :prepend => '@'
```

Use `:help_block` to provide extra description to a fields:

``` ruby
= f.email_field :email, :help_block => 'Please enter your emails address'
```

## Extra functionality

### Prevent double clicking on submit buttons

If you add 'bootstrap_builder' to your Javascript manifest you'll be able to add an extra `:change_to_text` option to submit buttons.
  
``` css
//= require bootstrap_builder
```

This will allow you to prevent double clicking by replacing the submit button with a string after the button is clicked:

``` ruby
= f.submit 'Log In', :change_to_text => 'Saving ...'
```

---

Copyright 2012 Jack Neto, [The Working Group, Inc](http://www.theworkinggroup.ca)

