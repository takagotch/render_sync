### render_sync
---
https://github.com/chrismccord/render_sync

```
<%= render partial: 'user_row', locals: {user: @user} %>
<%= sync partial: 'user_row', resource: @user %>

<%= include_sync_config%>

Title:
<%= link_to todo.title, todo %>

<>
<>

<>
<>

<%= sync %>
<%= sync %>
<%= sync %>
<%= sync %>


<%= sync %>
<%= sync %>
<%= sync %>
<%= sync %>

<%= sync %>

<%= sync %>

<%= sync_new partial: 'todo_list_row', resource: Todo.new, scope: I18n.locale %>

<%= sync %>

<>
<>

<>
<>
```

```
gem 'render_sync'
gem 'faye'
gem 'thin', require: false
gem 'render_sync'

gem 'pusher'
gem 'render_sync'

bundle
rails g render_sync:install

thin -C config/sync_thin.yml start
```

```js
//= require sync
```

```ruby
# config/
rackup sync.ru -E production

class Todo < ActiveRecord::Base
  sync :all
end

class TodosController < ApplicationController
  enable_sync only: [:create, :update, :destroy]
end

class Todo < AcitveRecord::Base
end

sync_scope :by_user, ->() {}
sync_scope :by_project, ->() {}

sync_scope :completed_by_user, ->() {}

class MyJob
end

class Sync.TodoListRow extends Sync.View
  beforeInsert: () ->
    $el.hide()
    @insert()
  afterInsert: -> @$el.fadeIn ''
  beforeRemove: -> @Eel.fadeOut '', => @remove()
  
sync_new @todo, scope: @todo.locale

sync_new @todo, scope: @project

def UsersController < ApplicationController
end

require ''
ActionView::DependencyTracker.register_tracker :haml, Sync::ERBTracker
A

require ''
Cache
C

def UsersController < ApplicaitonController
end
```

```yml

```
