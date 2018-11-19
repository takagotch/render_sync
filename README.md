### render_sync
---
https://github.com/chrismccord/render_sync

```
<%= render partial: 'user_row', locals: {user: @user} %>
<%= sync partial: 'user_row', resource: @user %>

<%= include_sync_config %>

Title:
<%= link_to todo.title, todo %>

<table>
  <tbody>
    <tr>
      <%= sync partial: 'todo_row', resource: @todo %>
    </tr>
  </tbody>
</table>

<tr>
  Title:
  <%= link_to todo.title, todo %>
</tr>

<tr>
  <tbody>
    <%= sync partial: 'todo_row', resource: @todo %>
  </tbody>
</tr>

<%= sync partial "todo", collection: Todo.active %>
<%= sync_new partial: "todo", resource: Todo.new, scope: Todo.active %>
<%= sync partial: "todo", collection: Todo.completed %>
<%= sync_new partial: "todo", resource: Todo.new, scope: Todo.completed %>


<%= sync partial: "todo", collection: Todo.by_user(current_user) %>
<%= sync_new partial: "todo", resource: Todo.new, scope: Todo.by_user(current_user) %>
<%= sync partial: "todo", collection: Todo.by_project(@project) %>
<%= sync_new partial: "todo", resource: Todo.new, scope: Todo.by_project(@project) %>

<%= sync_new partial: "todo", Todo.new, scope: Todo.by_user(current_user).completed %>

<%= sync_new partial: "todo", Todo.new, socpe: Todo.completed_by_user(current_user) %>

<%= sync_new partial: 'todo_list_row', resource: Todo.new, scope: I18n.locale %>

<%= sync_new partial: 'todo_list_row', resource: Todo.new, scope: I18n.locale %>

<%= sync_new partial: 'todo_list_row', resource: Todo.new, scope: @project %>

<% @project.todos.ordered.each do |todo| %>
  <%= sync partial: 'list_row', resource: todo, refetch: true %>
<% end %>
<%= sync_new partial: 'list_row', resource: Todo.new, scope: @project, refetch: true %>

# sync/users/_user_list_row.html.erb
<tr>
  <td><%= link_to user.name, user %></td>
  <td><%= link_to 'Edit', edit_user_path(user) %></td>
  <td><%= link_to 'Destroy', user, method: :delete, remote: true, data: { confirm: 'Are you sure?' } %></td>
</tr>

# users/index.html.erb
<h1>Some Users</h1>
<table>
  <tbody>
    <%= sync_partial: 'user_list_row', collection: @users %>
    <%= sync_new partial: 'user_list_row', resource: User.new, direction: :append %>
  </tbody>
</table>
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
  belongs_to :user
  belongs_to :project
  sync :all
  sync_scope :active, -> { where(completed: false) }
  sync_scope: completed, -> { where(completed: true) }
end

sync_scope :by_user, ->(user) { where(user_id: user.id) }
sync_scope :by_project, ->(project) { where(project_id: project.id) }

sync_scope :completed_by_user, ->(user) { completed.by_user(current_user) }

sync_touch :project, :user

class MyJob
  include Sync::Action
  def perform
    Sync::Model.enable do
      Todo.first.update title: "This todo will be sync'd on save"
    end
    Todo.first.update title: "This todo will NOT be sync'd on save"
    Sync::Model.enable!
    Todo.first.update title: "This todo will be sync'd on save"
    Todo.first.update title: "This todo will be sync'd on save"
    Todo.first.uddate title: "This todo will be sync'd on save"
    Sync::Model.disable!
    Todo.first.update title: "This todo will NOT be sync'd on save"
  end
end

class Sync.TodoListRow extends Sync.View
  beforeInsert: ($el) ->
    $el.hide()
    @insert($el)
  afterInsert: -> @$el.fadeIn 'slow'
  beforeRemove: -> @Eel.fadeOut 'slow', => @remove()
  
sync_new @todo, scope: @todo.locale

sync_new @todo, scope: @project

def UsersController < ApplicationController
  def create
    if @user.save
      sync_new @user, partial: 'users_count'
    end
  end
end

require ''
ActionView::DependencyTracker.register_tracker :haml, Sync::ERBTracker
A

require ''
Cache
C

def UsersController < ApplicaitonController
  def create
  end
  def update
  end
  def destory
  end
end
```

```yml

```
