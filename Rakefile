desc "Build"
task :build do
  Rake::Task["import"].invoke unless File.directory?("blog/_posts")

  sh "bundle exec jekyll build --config _config.yml --trace"
end

task default: :build

desc "Clean generated code"
task :clean do
  system "rm -rf _site .jekyll-cache"
end

desc "Local server"
task :server do
  sh "bundle exec jekyll serve --trace --watch"
end

namespace :lint do
  desc "Lint Ruby"
  task :ruby do
    sh "bundle exec standardrb"
  end

  desc "Lint YAML"
  task :yaml do
    if `which yamllint`.chomp.empty?
      abort "yamllint is not installed. Install it with `pip3 install yamllint`."
    end

    sh "yamllint -c .yamllint.yml ."
  end
end

desc "Run all linters"
task lint: %i[lint:ruby lint:yaml]
