omniauth-venmo
==============

Venmo OAuth2 Strategy for OmniAuth 1.x and supports the OAuth 2.0 server-side flow.

*Venmo API docs are currently in the works and will be released upon completion.*

## Installation

Add to your `Gemfile`:

```ruby
gem 'omniauth-venmo'
```

Then `bundle install`.


## Usage

`OmniAuth::Strategies::Venmo` is simply a Rack middleware. Read the OmniAuth 1.0 docs for detailed instructions: https://github.com/intridea/omniauth.

Here's a quick example, adding the middleware to a Rails app in `config/initializers/omniauth.rb`:

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :venmo, ENV['VENMO_CLIENT_ID'], ENV['VENMO_CLIENT_SECRET']
end
```

## Configuration

Currently, there is only one configuration option that needs to be set:

* `scope`: A comma-separated list of permissions you want to request from the user. The available permissions are as follows: `access_feed`, `access_profile`, `access_friends`, and `make_payments`.  Default: `access_profile`

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :venmo, ENV['VENMO_CLIENT_ID'], ENV['VENMO_CLIENT_SECRET'], :scope => 'access_profile,make_payments'
end
```

## Auth Hash

Here's an example *Auth Hash* available in `request.env['omniauth.auth']`:

```ruby
{
  :provider => 'venmo',
  :uid => '1234567',
  :info => {
    :username => 'tmilewski',
    :email => 'foo@bar.com',
    :phone => '16105553287',
    :name => 'Tom Milewski',
    :first_name => 'Tom',
    :last_name => 'Milewski',
    :image => 'https://venmopics.appspot.com/u/v1/s/caa2d1a7-192d-4516-bfef-4ef8a1cd9dbe',
    :balance => 0.0,
    :urls => { :profile => 'https://venmo.com/tmilewski' },
  },
  :credentials => {
    :token => 'ABCDEF...',
    :expires => false
  },
  :extra => {
    :raw_info => {
      :id => '1234567',
      :username => 'tmilewski',
      :email => 'foo@bar.com',
      :phone => '16105553287',
      :name => 'Tom Milewski',
      :firstname => 'Tom',
      :lastname => 'Milewski',
      :picture => 'https://venmopics.appspot.com/u/v1/s/caa2d1a7-192d-4516-bfef-4ef8a1cd9dbe',
      :balance => 0.0,
      :urls => { :profile => 'https://venmo.com/tmilewski' },
    }
  }
}
```

## License

Copyright (c) 2013 by Tom Milewski

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
