Edit Articles - Text directions and code
Section 4, Lecture 85
Route for editing articles takes the form ->

/articles/:id/edit

Edit action in the articles controller:

def edit

@article = Article.find(params[:id])

end

Update action in the articles controller:

def update

@article = Article.find(params[:id])

if @article.update(article_params)

flash[:notice] = "Article was successfully updated"

redirect_to article_path(@article)

else

render 'edit'

end

end

To create edit template, create a file named edit.html.erb under the app/views/articles folder and fill in the following code:

<h1>Edit existing article</h1>

<% if @article.errors.any? %>

<h2>The following errors prevented the article from getting created</h2>

<ul>

<% @article.errors.full_messages.each do |msg| %>

<li><%= msg %></li>

<% end %>

</ul>

<% end %>

<%= form_for @article do |f| %>

<p>

<%= f.label :title %><br/>

<%= f.text_field :title %>

</p>

<p>

<%= f.label :description %><br/>

<%= f.text_area :description %>

</p>

<p>

<%= f.submit %>

</p>

<% end %>

##########

Complete New and Show Actions - Text directions and code
Section 4, Lecture 83
Completed create action in articles controller:

def create
    @article = Article.new(article_params)
    if @article.save
        flash[:notice] = "Article was successfully created"
        redirect_to article_path(@article)
    else
        render 'new'
    end
end

Flash message code added to application.html.erb under app/views/layouts folder (right under <body> and above <%= yield %>:

<% flash.each do |name, msg| %>

<ul>

<li><%= msg %></li>

</ul>

<% end %>

Code added to display errors in the new.html.erb template under app/views/articles folder:

<% if @article.errors.any? %>

<h2>The following errors prevented the article from getting created</h2>

<ul>

<% @article.errors.full_messages.each do |msg| %>

<li><%= msg %></li>

<% end %>

</ul>

<% end %>
###
To create the show action, add the following show method to articles_controller.rb file:

def show

@article = Article.find(params[:id])

end
###

To create the show view, add a show.html.erb file under the app/views/articles folder and fill in the code:

<h1>Showing selected article</h1>

<p>

Title: <%= @article.title %>

</p>

<p>

Description: <%= @article.description %>

</p>

