Sauna
=====
##### Filter your social streams. Find the fresh links. Share with your readers.

Sauna is a social news aggregator and curation tool.
This is the open-source version of [Sauna.io](http://sauna.io).

It scans your Twitter stream and RSS feeds looking for links.
And it automatically extracts the important text and images from each link.
Over time, Sauna learns what types of links you like, and hides the ones you don't.

Sauna also allows you to curate the links you like with your friends, fans,
or readers. Create a customized linkstream site (like [bruno.sauna.io](http://bruno.sauna.io)). Built-in social sharing on Twitter and Facebook, with scheduled posting.

Sauna was created by Bruno Bornsztein for [Curbly](http://www.curbly.com).


Installation
------------

*Note: I'm still trying to smooth out the install process. Please help
me out by going through the steps and telling me what doesn't work!*

Sauna runs on Ruby 1.9.x with Rails 3.2.

Prior to installing, you'll need [mongodb](http://www.mongodb.org/) and [Redis](http://redis.io/) installed on your machine.

1. Clone the repository: `git clone https://github.com/bborn/opensauna.git`
2. Copy `sample.env` to `.env`. Don't add `.env` to the git repo.
3. Fill in the required values in your `.env` file.

    `SECRET_TOKEN`  - use `rake secret` to generate a token

    `BASE_HOST_NAME` - for Heroku, this will be `yourappname.herokuapp.com`, unless you add a custom domain, in which case it'll be `customdomain.com` (without `www`)

4. `bundle install`
5. `rake db:migrate`
6. `bundle exec foreman start -f Procfile.local`. (The app should now be
running on `localhost:5000`)


Deploying to Heroku
-------------------

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)


To Deploy Manually to heroku:

1. Create a new Heroku app
2. Set the required variables from your local `.env` file on Heroku
(using `heroku config:set`). You can also use the
[heroku-config](https://github.com/ddollar/heroku-config) plugin to sync local and remote config vars.
3. Provision the required addons:

  - [rediscloud](https://addons.heroku.com/rediscloud)
  - [mongohq](https://addons.heroku.com/mongohq)
  - [memcachier](https://addons.heroku.com/memcachier)
  - [sendgrid](https://addons.heroku.com/sendgrid)

4. Push your app to Heroku (`git push heroku`) and migrate (`heroku run rake
db:migrate`)

Running Workers on Heroku
-------------------------

Look in the `Procfile` to see which processes are defined. You can leave
workers running for each of these, but a better approach is to use
autoscaling. Try [Hirefire](http://hirefire.io/),
[AdeptScale](https://addons.heroku.com/adept-scale) or the
[Autoscaler](https://github.com/JustinLove/autoscaler) gem.

Admin User
----------
Set the boolean `admin` attribute to `true` on a user to give him access to the
admin backend (`/admin`) and Sidekiq UI (`/sidekiq`). On Heroku, you can
use `heroku run console` to do this.


