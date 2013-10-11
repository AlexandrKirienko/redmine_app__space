# Redmine Application Space

Tested with redmine 2.3.2, compatible with 2.x

Enhance Redmine application menu (the one that is displayed when browsing outside of projects) with dynamic configurability options.
* Administrators can select the set of applications available
* Users can select the applications they will see listed in the application menu

Both full controllers and partials (e.g. the my/blocks views) can be made an application.

## Installation

Follow standard Redmine procedure, including database migrations

## Usage

As an administrator, enter the plugin configuration page and flag the applications you want to let the users use.

As an user, you can find a new 'Applications' entry in the top-left menu, which allows to select applications wanted into the application menu.

Plugins that add entries into the application menu in the standard Redmine way keep a fixed, non configurable entry

## How to create a new managed app

* name your plugin 'redmine_app_<appname>'. Note that this plugin has a double underscore between 'app' and 'space', so your plugin will be always loaded after this, which is mandatory.
* this plugin creates two new routing verbs, 'application' for apps with a controller, and 'block' for simple partials to display as apps.
  These verbs create routes from 'apps/<name>' that must be loaded _before_ this plugin load 'apps/:tab' in order not to be ignored.
  Therefore, you must declare your app routing within init.rb into a section like the following:
     RedmineApp::Application.routes.prepend do
        application 'name_of_app', :to => 'controller#method', :via => get
        block 'name_of_app', 'partial_path'
     end
  The syntax is similar to that of the 'match' verb, with some simplifications. Blocks restrict to the get method as default if :via is not specified.
* create translations:
** label_<name> is the text listed in the applications menu
** label_<name>_description is the help text displayed in the app selection pages

