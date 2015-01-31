Capistrano with eZPublish 5
========================

## Required ruby gems on local machine/execution source

* bundler (1.7.12)
* capistrano (3.3.5)
* capistrano-symfony (0.4.0)
* <em>Dependencies:</em>
    * capistrano-composer (0.0.5)
    * capistrano-file-permissions (0.1.0)

You may run `gem list` to see if you already have them, if not run one or more of the following commands.<br>
<em>Note: running as sudo is not required, but highly recommended.</em>
* `sudo gem install bundler`
* `sudo gem install capistrano`
* `sudo gem install capistrano-symfony`

Installation
--------------
1. Copy ./Gemfile to `<my-project>/`
2. Update the Project-Specific variables in config/deploy.rb
3. Setup parameters.yml on your deployment destination. Default path: /var/www/<domain>/<environment>/shared/ezpublish/config/parameters.yml
4. Add `SetEnv ENVIRONMENT {prod,stage}` in your webservers virtual hosts


Usage
--------------
* Deploy to stage: `cap stage deploy`
* Deploy to prod: `cap prod deploy`


Tips
--------------
* Change sessionpath to project to prevent visitors from being logged out upon deploy <br>
`framework.session:` <br>
`    handler_id:  session.handler.native_file` <br>
`    save_path: "%kernel.root_dir%/sessions"` <br>
