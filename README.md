# HR-TIL

![til](https://raw.githubusercontent.com/hashrocket/hr-til/master/app/assets/images/banner.png)

[![Circle CI](https://circleci.com/gh/hashrocket/hr-til.svg?style=svg)](https://circleci.com/gh/hashrocket/hr-til) [![Code Climate](https://codeclimate.com/github/hashrocket/hr-til/badges/gpa.svg)](https://codeclimate.com/github/hashrocket/hr-til) [![Issue Count](https://codeclimate.com/github/hashrocket/hr-til/badges/issue_count.svg)](https://codeclimate.com/github/hashrocket/hr-til)

> TIL is an open-source project by the team at
> [Hashrocket](https://hashrocket.com/) that catalogues the sharing &
> accumulation of knowledge as it happens day-to-day. Posts have a 200-word
> limit, and posting is open to any Rocketeer as well as select friends of the
> team. We hope you enjoy learning along with us.

This site was open-sourced as a window into our development process, as well as
to allow people to experiment with the site on their own and contribute to the
project.

### Pivotal Boston Fork

This fork of TIL serves the Pivotal Boston office.

To add a new channel, first modify `db/seeds.rb`. Next, you can log into the database and insert a new channel like so:

```
$ RAILS_ENV=production DATABASE_URL=the_database_url rails c
$ Channel.find_or_create_by!(name: 'my-new-channel')
```

### Install

If you are creating your own version of the site,
[fork](https://help.github.com/articles/fork-a-repo/) the repository.

Then, follow these setup steps:

```sh
$ git clone https://github.com/hashrocket/hr-til
$ cd hr-til
$ gem install bundler
$ bundle install
$ cp config/application.yml{.example,}
$ rake db:create db:migrate db:seed
$ rails s
```

In development, `db:seed` will load sample data for channels, developers, and
posts. Omit this command to opt-out of this step, or create your own sample
data in `db/seeds/development.rb`.

Authentication is managed by Omniauth and Google. See the
[omniauth-google-oauth2
README](https://github.com/zquestz/omniauth-google-oauth2/blob/master/README.md)
and [Google Oauth 2
docs](https://developers.google.com/identity/protocols/OAuth2WebServer) for
setup instructions. To allow users from a domain, multiple domains, or a
specific email to log in, set those configurations in your environmental
variables:

```yml
# config/application.yml

permitted_domains: 'hashrocket.com|hshrckt.com'
permitted_emails: 'friend@whitelist.com'
```
Ensure you have set the google client id and google client secret via Oauth instructions.

Once set, visit '/admin' and log in with a permitted email address or domain.

### Testing

Run all tests with:

```
$ rake
```

Or, run all the test in parallel with [flatware](https://github.com/briandunn/flatware):

```
$ flatware fan rake db:test:prepare
$ flatware rspec && flatware cucumber
```

### Dependencies

- The gem `selenium-webdriver` depends on the Firefox browser.
- The gems `flatware-rspec` and `flatware-cucumber` require ZeroMQ. Learn more
[here](https://github.com/briandunn/flatware).

### Hosting

Staging and production instances are located here:

* https://hr-til-staging.herokuapp.com
* https://hr-til-production.herokuapp.com

### Environmental Variables

`basic_auth_credentials` both toggles and defines basic authentication:

```yml
# config/application.yml

basic_auth_credentials: username:password
```

`slack_post_endpoint` allows the app to post to [Slack](https://slack.com/):

```yml
# config/application.yml

slack_post_endpoint: /services/some/hashes
```

### Contributing

1. [Fork](https://help.github.com/articles/fork-a-repo/) it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

Bug reports and pull requests are welcome on GitHub at
https://github.com/hashrocket/hr-til. This project is intended to be a safe,
welcoming space for collaboration, and contributors are expected to adhere to
the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

### Usage

We love seeing forks of Today I Learned in production! Please consult our
[usage guide](/USAGE.md) for guidelines on appropriate styling and attribution.

### License

TIL is released under the [MIT License](http://www.opensource.org/licenses/MIT).

---

### About

[![Hashrocket logo](https://hashrocket.com/hashrocket_logo.svg)](https://hashrocket.com)

TIL is supported by the team at [Hashrocket, a
multidisciplinary design and development consultancy](https://hashrocket.com). If you'd like to [work with
us](https://hashrocket.com/contact-us/hire-us) or [join our
team](https://hashrocket.com/contact-us/jobs), don't hesitate to get in touch.
