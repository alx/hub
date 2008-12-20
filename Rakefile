require 'rubygems'
require 'git'
require 'jekyll/lib/jekyll'

desc "Publish site content on alexgirard.com"
task :publish_alexgirard do
  # Use Jekyll to generate site-content in alexgirard.com
  Jekyll.process 'site-content/', 'alexgirard.com/'
  # Push alexgirard.com
  
  # Connect to ssh adn pull modifications
end

desc "Publish site content on alx.github.com"
task :publish_github do
  # Switch site-content to branch gh-pages
  # Merge changes from master
  # Use Jekyll to generate site-content in alx.github.com
  # Push alx.github.com
  # Switch back site-content to master
end
