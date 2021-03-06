# encoding: utf-8

require 'rubygems'
require 'bundler'
begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end
require 'rake'

require 'jeweler'
Jeweler::Tasks.new do |gem|
  # gem is a Gem::Specification... see http://docs.rubygems.org/read/chapter/20 for more options
  gem.name = "malm"
  gem.homepage = "http://github.com/madlep/malm"
  gem.license = "MIT"
  gem.summary = %Q{Easy SMTP server for local development}
  gem.description = %Q{SMTP server with web interface for easy local development. Sets up a little mail server that you can send messages to, and provides a web front end to let you see what your app did.}
  gem.email = "julian.doherty.ml@gmail.com"
  gem.authors = ["madlep"]
  # dependencies defined in Gemfile
end
Jeweler::RubygemsDotOrgTasks.new

require 'rspec/core'
require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = FileList['spec/**/*_spec.rb']
end

RSpec::Core::RakeTask.new(:rcov) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
  spec.rcov = true
end

task :default => [:coffee, :spec]

task :release => ["coffee", "gemspec:release","git:release","gemcutter:release"]

desc "Clean out yucky dev stuff"
task :clean => "coffee:clean"

desc "compile coffeescript"
task :coffee  => "coffee:compile"

namespace :coffee do
  
  coffee_src_dir = File.join(File.dirname(__FILE__), "web", "src", "coffee")
  coffee_out_dir = File.join(File.dirname(__FILE__), "web", "public", "js")
  
  task :compile do
    `coffee -o #{coffee_out_dir} #{coffee_src_dir}/*.coffee`
  end
  
  task :clean do
    `rm #{coffee_out_dir}/*.js`
  end
end