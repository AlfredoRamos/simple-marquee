require 'rake/testtask'
require 'sass'
require 'autoprefixer-rails'
require 'scss_lint/rake_task'

$stdout.sync = $stderr.sync = true

# Tests
Rake::TestTask.new(:test) do |t|
  t.test_files = FileList['test/test_*.rb']
  t.verbose = true
end

# SCSS Lint
SCSSLint::RakeTask.new

namespace :build do
  files = {
    input: 'scss/main.scss',
    output: ['build/marquee.css', 'build/marquee.min.css']
  }

  desc 'Build setup'
  task :setup do
    Dir.mkdir('build') unless Dir.exist?('build')
  end

  desc 'Base build'
  task :base, [:opts] => [:setup] do |_t, args|
    File.open(args[:opts][:output], 'w') do |f|
      css = Sass::Engine.new(
        File.read(args[:opts][:input]),
        style: args[:opts][:style],
        cache: false,
        syntax: :scss,
        filename: args[:opts][:input],
        sourcemap: :none
      ).render

      f.puts AutoprefixerRails.process(
        css,
        map: false,
        cascade: false,
        from: args[:opts][:input],
        to: args[:opts][:output],
        browsers: [
          '>= 1%',
          'last 1 major version',
          'not dead',
          'Chrome >= 45',
          'Firefox >= 38',
          'Edge >= 12',
          'Explorer >= 10',
          'iOS >= 9',
          'Safari >= 9',
          'Android >= 4.4',
          'Opera >= 30'
        ]
      ).css
    end
  end

  desc 'Build CSS file'
  task :css do
    Rake::Task['build:base'].reenable
    Rake::Task['build:base'].invoke(
      input: files[:input],
      output: files[:output].first,
      style: :expanded
    )
  end

  desc 'Build minified CSS file'
  task :minified do
    Rake::Task['build:base'].reenable
    Rake::Task['build:base'].invoke(
      input: files[:input],
      output: files[:output].last,
      style: :compressed
    )
  end

  desc 'Build all CSS files'
  task :all do
    Rake::Task['build:css'].invoke
    Rake::Task['build:minified'].invoke
  end
end
