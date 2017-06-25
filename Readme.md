# Scrape Social Media URLs from Group Members on meetup.com

### Installation Guide
Assuming you have Ruby 2.2.4 installed....
To install the required gem list run the following command in your terminal.

You may run into issues installing the nokogiri gem, in that case nokogiri has a troubleshooting guide available on their website.

```sh
bundle install
```

if you do not have Ruby 2.2.4 installed, and you are running a different version of ruby, make sure to go into the Gemfile and remove or comment out the line that says ruby '2.2.4'

```ruby
# comment out if you do not want to run code with your ruby version, I was using 2.2.4 on my computer.
ruby '2.2.4'
```

### Setup Configuration
Set the desired group name of your meetup.com group you would like to scrape, if the group has spaces in the name you will want to copy how its listed in the groups URL

```ruby
require 'rubygems'
require 'bundler'
require 'open-uri'
require 'csv'
require 'fileutils'

Bundler.require :default

## SET THE MEETUP.COM GROUP NAME
GROUP_NAME = 'Desired-Group-Name'
```

cd to the scrape folder root and run the scraper by typing the following in your terminal
```sh
rake scrape_meetup_users
```

terminal will output progress
```sh
$ rake scrape_meetup_users
querying member 1
adding https://twitter.com/AronLilland to tmp/twitter.csv
querying member 2
querying member 3
querying member 4
querying member 5
querying member 6
querying member 7
querying member 8
querying member 9
```
contents will be output to the ./tmp folder
