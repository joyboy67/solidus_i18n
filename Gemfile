# frozen_string_literal: true

source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

branch = ENV.fetch('SOLIDUS_BRANCH', 'master')
solidus_git, solidus_frontend_git = if (branch == 'master') || (branch >= 'v3.2')
                                      %w[solidusio/solidus solidusio/solidus_frontend]
                                    else
                                      %w[solidusio/solidus] * 2
                                    end
gem 'solidus', github: solidus_git, branch: branch
gem 'solidus_frontend', github: solidus_frontend_git, branch: branch

# Needed to help Bundler figure out how to resolve dependencies,
# otherwise it takes forever to resolve them.
# See https://github.com/bundler/bundler/issues/6677
gem 'rails', '>0.a'

case ENV['DB']
when 'mysql'
  gem 'mysql2'
when 'postgresql'
  gem 'pg'
else
  gem 'sqlite3'
end

group :development, :test do
  gem 'i18n-tasks', '~> 0.9' if branch == 'master'
end

gemspec

# Use a local Gemfile to include development dependencies that might not be
# relevant for the project or for other contributors, e.g.: `gem 'pry-debug'`.
eval_gemfile 'Gemfile-local' if File.exist? 'Gemfile-local'
