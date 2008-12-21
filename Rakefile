require 'rubygems'
require 'git'
require 'net/ssh'
require 'jekyll/lib/jekyll'

namespace :publish do
  desc "Publish site content on alexgirard.com"
  task :alexgirard do
    
    puts "* Publish alexgirard.com"
  
    content = 'site-content/'
    remote = 'alexgirard.com/'
    branch = 'alexgirard.com'
  
    # Use Jekyll to generate site-content in alexgirard.com
    puts "-- Jekyll process"
    Jekyll.process(content, remote)
  
    # Get last commit message
    puts "-- fetch commit message"
    commit_message = Git.open(content).log.first.message.strip
  
    # Push alexgirard.com
    puts "-- commit and push on #{branch} branch"
    g = Git.open(remote)
    g.add
    g.commit(commit_message)
    g.push("origin", branch)
  
    # Connect to ssh and pull modifications
    puts "-- sync  on ssh server"
    Net::SSH.start("alexgirard.com", "peeloo") do |ssh|
        ssh.exec! "cd public_html; /home/peeloo/bin/git pull origin #{branch};"
    end
  end

  desc "Publish site content on alx.github.com"
  task :github do
    
    puts "* Publish alx.github.com"
  
    content = 'site-content/'
    remote = 'alx.github.com'
    branch = 'gh-page'
    
    # Switch site-content to branch gh-pages
    puts "-- checkout and merge site content on gh-page branch"
    g_content = Git.open(content)
    g_content.checkout(branch)
    g_content.merge("master")
    
    # Use Jekyll to generate site-content in alx.github.com
    puts "-- Jekyll process"
    Jekyll.process(content, remote)
    
    puts "-- fetch commit message"
    commit_message = g_content.log.first.message.strip
    
    # Push alx.github.com
    puts "-- commit and push on #{branch} branch"
    g = Git.open(remote)
    g.add
    g.commit(commit_message)
    g.push("origin", 'gh-pages')
    
    # Switch back site-content to master
    g_content.checkout("master")
  end
end

desc "Publish all content on all sites"
task :publish => ["publish:alexgirard", "publish:github"] do
  # All happen in sub-task, nthing to be done
end
