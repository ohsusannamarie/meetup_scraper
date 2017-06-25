require 'rubygems'
require 'bundler'
require 'open-uri'
require 'csv'
require 'fileutils'

Bundler.require :default

## SET THE MEETUP.COM GROUP NAME
GROUP_NAME = 'ReactJS-OC'

def add_to_file(url: nil, type: nil)
  puts "adding #{url} to tmp/#{type}.csv"
  case type
  when 'twitter'
    CSV.open('./tmp/twitter.csv', 'ab') do |csv|
      csv << [url]
    end
  when 'linkedin'
    CSV.open('./tmp/linkedin.csv', 'ab') do |csv|
      csv << [url]
    end
  when 'facebook'
    CSV.open('./tmp/facebook.csv', 'ab') do |csv|
      csv << [url]
    end
  when 'flickr'
    CSV.open('./tmp/flickr.csv', 'ab') do |csv|
      csv << [url]
    end
  when 'tumblr'
    CSV.open('./tmp/tumblr.csv', 'ab') do |csv|
      csv << [url]
    end
  end
end

def parse_member(page_url)
  page = Nokogiri::HTML(open(page_url))
  social_links = page.css('ul.inlineList li a')
  social_links.each do |social|
    if social['href'].include?('twitter')
      add_to_file(url: social['href'], type: 'twitter')
    elsif social['href'].include?('linkedin')
      add_to_file(url: social['href'], type: 'linkedin')
    elsif social['href'].include?('facebook')
      add_to_file(url: social['href'], type: 'facebook')
    elsif social['href'].include?('flickr')
      add_to_file(url: social['href'], type: 'flickr')
    elsif social['href'].include?('tumblr')
      add_to_file(url: social['href'], type: 'tumblr')
    end
  end
end

task :scrape_meetup_users do
  # delete directory
  FileUtils.rm_rf('./tmp')
  # make directory
  FileUtils.mkdir('./tmp')

  start_num = 0
  last_page = false
  ct = 0
  while last_page == false do
    page_url = "https://www.meetup.com/#{GROUP_NAME}/members/?offset=#{start_num}&sort=last_visited&desc=1"
    page = Nokogiri::HTML(open(page_url))
    member_list = page.css('ul#memberList li div a')
    tmp = nil
    member_list.each do |member_link|
      next if member_link['href'] == tmp
      ct += 1
      puts "querying member #{ct}"
      parse_member(member_link['href'])
      tmp = member_link['href']
    end
    if member_list.count < 40
      last_page = true
    end
    start_num += 40
  end
  puts '.........'
  puts 'complete!'
end
