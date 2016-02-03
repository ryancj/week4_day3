#Week 3 Day 3
Combine Day 1 and Day 2. Interact and display the interaction between user
input with databases, models and controllers.

Simple pluralize Method
```ruby
"question".pluralize
```

####Questions
- Routes
```ruby
get "/questions/new" => "questions#new", as: :new_question
post "/questions" => "questions#create", as: :questions
```
```ruby
class QuestionsController < ApplicationController
  def new
    @question = Question.new
  end
end
```
- Controllers
```ruby
class QuestionsController < ApplicationController
  def new
    @question = Question.new
  end

  def create
    # params => {"question" =>{"title"=>"hello world", "body"=>"something here"}}
    # question = Question.new
    # question.title = params[:question][:title]
    # question.body = params[:question][:body]

    # using params.require ensures a key called 'question'
    # in my params. the 'permit' method will only allow parameters
    # that you explicitly list, in this case: title and body
    question_params = params.require(:question).permit([:title, :body])
    question = Question.new question_params
    question.save
    render text: params
  end
end
```
- form_for
```ruby
# form_for takes in an ActiveRecord object as a first argument. Then it looks
# at the object. If the object  is not persisted (not yet saved to the database.
# The  form will automatically use POST for its 'method'. It will also
# automatically use 'questions_path' as its actions (convention is that the
# 'questions_path' will submit to 'create'action)
form_for @question do |f|

end
```
```ruby
<h1>New Question</h1>
<%# we call 'f' the form object %>
<%= form_for @question do |f| %>
  <%# we call 'f' the form object %>
  <div>
    <%= f.label :title %>
    <%= f.text_field :title %>
  </div>
  <div class="">
    <%= f.label :body %>
    <%= f.text_area :body %>
  </div>
  <div>
    <%= f.submit %>
  </div>
<% end %>
```
