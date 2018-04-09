require 'puppetlabs_spec_helper/rake_tasks'

exclude_paths = [
  'modules/**/*',
  'pkg/**/*',
  'spec/**/*',
  'vendor/**/*'
]

# Puppet-Lint >= 1.1.0
Rake::Task[:lint].clear
PuppetLint::RakeTask.new :lint do |config|
  config.ignore_paths = exclude_paths
  config.disable_checks = %w[class_inherits_from_params_class 140chars]
  config.fail_on_warnings = true
end
PuppetLint.configuration.relative = true
PuppetSyntax.exclude_paths = exclude_paths

Rake::Task[:default].prerequisites.clear
task :default => :all

desc 'Clean up modules / pkg'
task :clean do
  sh 'rm -rf modules pkg spec/fixtures'
end

task :success do
  puts "\n\e[32mAll tests passing...\e[0m"
end

desc 'Run all'
task :all => %i[
  clean
  test
  success
]

desc 'Run rubocop, syntax, lint, and spec tests'
task :test => %i[
  rubocop
  syntax
  lint
  metadata_lint
  spec
]
