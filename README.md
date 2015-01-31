Capistrano with eZPublish 5
========================

## Required ruby gems on local machine/execution source

Run `gem list` to see if you meet the requirements

* bundler (1.7.12)
* capistrano (3.3.5)
* capistrano-symfony (0.4.0)
* <em>Dependencies:</em>
    * capistrano-composer (0.0.5)
    * capistrano-file-permissions (0.1.0)

<em>Note: running as sudo is not required, but highly recommended.</em>

* `sudo gem install bundler`
* `sudo gem install capistrano`
* `sudo gem install capistrano-symfony`

Installation
--------------
1. Copy deploymentfiles: `cp -R <capistrano-ezpublish dir>/*  <my-project>/`
2. Test your ruby/rake/gem dependecies with cd `<my-project> && bundle exec cap install STAGES=prod,stage`. <br>
You should get some `... already exists`-output and the last output should be `Capified`.
3. Update the Project-Specific variables in config/deploy.rb
4. Setup parameters.yml on your deployment destination. <br>
   Default path: `/var/www/<domain>/<environment>/shared/ezpublish/config/parameters.yml` <br>
   E.g: SSH to server and run: `mkdir -p /var/www/htollefsen.com/stage/shared/ezpublish/config && cd $_ && touch parameters.yml && cd -`

Optional
--------------
* Override the sessionpath to your project to prevent visitors from being logged out on deploy: <br>
`framework.session.handler_id: session.handler.native_file` <br>
`framework.session.save_path: "%kernel.root_dir%/sessions"` <br>
* If you are running Enterprise Edition, remember to apply an `auth.json` in your home-dir on the servers, or in your projects root dir to access `updates.ez.no`

Usage
--------------
* Deploy to stage: `cap stage deploy`
* Deploy to prod: `cap prod deploy`

Adding stage environment
--------------
1. Add `SetEnv ENVIRONMENT stage` in your webservers virtual hosts
2. Add symfony config_stage.yml to your config folder at `ezpublish/config/config_stage.yml`
3. Add a `config/deploy/stage.rb`-file (or use the default), and update :branch, :symfony_env and the roles if needed


