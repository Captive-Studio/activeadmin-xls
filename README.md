# Active Admin Xls

ℹ️ This is a fork of the [official repository](https://github.com/thambley/activeadmin-xls) who isn't maintained anymore

Excel Spreadsheet Export for [Active Admin]

[![Version][rubygems_badge]][rubygems]
[![Travis CI][travis_badge]][travis]
[![Quality][codeclimate_badge]][codeclimate]
[![Coverage][codecov_badge]][codecov]
[![Inch CI][inch_badge]][inch]

## Synopsis

This gem provides xls downloads for Active Admin resources.

This gem borrows heavily from [activeadmin-axlsx] and [to_xls].

## Usage

Add the following to your Gemfile. All resource index views will now include a link for download directly to xls.

```ruby
gem "activeadmin-xls", git: "https://github.com/Captive-Studio/activeadmin-xls"
```

For Active Admin 1.0 and above, you will also have to update config/initializers/active_admin.rb.  Update the download\_links setting to include xls:

```ruby
config.download_links = %i[csv xml json xls]
```

## Dependencies

This gem depends on [spreadsheet] to generate xls files.

## Examples

Here are a few quick examples of things you can easily tweak.

### Localize column headers

```ruby
# app/admin/posts.rb
ActiveAdmin.register Post do
  config.xls_builder.i18n_scope = [:active_record, :models, :posts]
end
```

### Use blocks for adding computed fields

```ruby
# app/admin/posts.rb
ActiveAdmin.register Post do
  config.xls_builder.column('author_name') do |resource|
    resource.author.name
  end
end
```

### Change the column header format

```ruby
# app/admin/posts.rb
ActiveAdmin.register Post do
  config.xls_builder.header_format = { weight: :bold,
                                       color: :blue }
end
```

### Remove columns

```ruby
# app/admin/posts.rb
ActiveAdmin.register Post do
  config.xls_builder.delete_columns :id, :created_at, :updated_at
end
```

### Restrict columns to a list

```ruby
# app/admin/posts.rb
ActiveAdmin.register Post do
  config.xls_builder.only_columns :title, :author
end
```

## Using the DSL

Everything that you do with the config's default builder can be done via
the resource DSL.

Below is an example of the DSL

```ruby
ActiveAdmin.register Post do

  # i18n_scope and header style are set via options
  xls(i18n_scope: [:active_admin, :xls, :post],
      header_format: { weight: :bold, color: :blue }) do

    # Specify that you want to white list column output.
    # whitelist

    # Do not serialize the header, only output data.
    # skip_header

    # restrict columns to a list without customization
    # only_columns :title, :author

    # deleting columns from the report
    delete_columns :id, :created_at, :updated_at

    # adding a column to the report with customization
    column(:author) { |post| "#{post.author.first_name} #{post.author.last_name}" }

    # inserting additional data with after_filter
    after_filter do |sheet|
      # todo
    end

    # inserting data with before_filter
    before_filter do |sheet|
      # todo
    end
  end
end
```

## Testing

Running specs for this gem requires that you construct a rails application.

To execute the specs, navigate to the gem directory, run bundle install and run these to rake tasks:

### Rails 4.2

```text
bundle install --gemfile=gemfiles/rails_42.gemfile
```

```text
BUNDLE_GEMFILE=gemfiles/rails_42.gemfile bundle exec rake setup
```

```text
BUNDLE_GEMFILE=gemfiles/rails_42.gemfile bundle exec rake
```

### Rails 5.2

```text
bundle install --gemfile=gemfiles/rails_52.gemfile
```

```text
BUNDLE_GEMFILE=gemfiles/rails_52.gemfile bundle exec rake setup
```

```text
BUNDLE_GEMFILE=gemfiles/rails_52.gemfile bundle exec rake
```

### Rails 6.0

```text
bundle install --gemfile=gemfiles/rails_60.gemfile
```

```text
BUNDLE_GEMFILE=gemfiles/rails_60.gemfile bundle exec rake setup
```

```text
BUNDLE_GEMFILE=gemfiles/rails_60.gemfile bundle exec rake
```

About Captive
-------------

![captive](https://raw.githubusercontent.com/Captive-Studio/assets/main/logo_captive_blue_avec_fond.webp)

This repo is maintained by Captive.
The names and logos for captive are trademarks of captive-studio.

We love open source software!
See [our other projects][community] or
[hire us][hire] to design, develop, and grow your product.

[community]: https://github.com/Captive-Studio
[hire]: https://www.captive.fr/contact?utm_source=github

[Active Admin]:https://www.activeadmin.info/
[activeadmin-axlsx]:https://github.com/randym/activeadmin-axlsx
[to_xls]:https://github.com/splendeo/to_xls
[spreadsheet]:https://github.com/zdavatz/spreadsheet

[rubygems_badge]: https://img.shields.io/gem/v/activeadmin-xls.svg
[rubygems]: https://rubygems.org/gems/activeadmin-xls
[travis_badge]: https://img.shields.io/travis/thambley/activeadmin-xls/master.svg
[travis]: https://travis-ci.org/thambley/activeadmin-xls
[codeclimate_badge]: https://api.codeclimate.com/v1/badges/e294712bac54d4520182/maintainability
[codeclimate]: https://codeclimate.com/github/thambley/activeadmin-xls/maintainability
[codecov_badge]: https://codecov.io/gh/thambley/activeadmin-xls/branch/master/graph/badge.svg
[codecov]: https://codecov.io/gh/thambley/activeadmin-xls
[inch_badge]: http://inch-ci.org/github/thambley/activeadmin-xls.svg?branch=master
[inch]: http://inch-ci.org/github/thambley/activeadmin-xls
