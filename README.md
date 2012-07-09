Bug: undefined method `refinery_user?' when use ActiveAdmin with RefineryCMS

Steps:

    rvm use --create ruby-1.9.3@refinery
    gem install bundler --pre
    gem install refinerycms
    rails new rickrockstar -m http://refinerycms.com/t/2.0.5
    # add 'activeadmin' gem to Gemfile
    bundle
    rails g active_admin:install
    rake db:migrate
    rails s
    # go to http://localhost:3000 and create an admin user
    # log out and Ctrl-C to exit server. may need to do this because otherwise refinery_user? may have been loaded
    rails s
    # open http://localhost:3000 again

Full error:

    NoMethodError in Refinery/pages#home

    Showing /Users/sandbox/.rvm/gems/ruby-1.9.3-p194@refinery/gems/refinerycms-core-2.0.5/app/views/refinery/_site_bar.html.erb where line #1 raised:

    undefined method `refinery_user?' for #<#<Class:0x00000100c70c30>:0x00000100ae7940>
    Extracted source (around line #1):

    1: <% if refinery_user? && "#{controller_name}##{action_name}" != 'pages#preview' %>
    2:   <% unless admin? # all required JS included by backend. %>
    3:     <% content_for :stylesheets, stylesheet_link_tag('refinery/site_bar') unless !!local_assigns[:exclude_css] %>
    4:     <%= yield(:stylesheets) unless local_assigns[:head] or local_assigns[:exclude_css] %>
    Trace of template inclusion: /Users/sandbox/.rvm/gems/ruby-1.9.3-p194@refinery/gems/refinerycms-core-2.0.5/app/views/layouts/application.html.erb

    Rails.root: /Users/sandbox/code/examples/rickrockstar


