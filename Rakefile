# frozen_string_literal: true

require 'rake/testtask'
require 'sassc'
require 'autoprefixer-rails'
require 'rubocop/rake_task'
require 'scss_lint/rake_task'
require 'logger'

$stdout.sync = $stderr.sync = true

# Logger
logger = Logger.new($stdout)
logger.datetime_format = '%F %T %:z'
logger.formatter = proc do |severity, datetime, _progname, msg|
  "#{datetime} | #{severity} | #{msg}\n"
end

# Tests
RuboCop::RakeTask.new
SCSSLint::RakeTask.new
Rake::TestTask.new(:test) do |t|
  t.test_files = FileList['test/test_*.rb']
  t.verbose = true
end

# Helper
class Helper
  def initialize(logger)
    @logger = logger
    Dir.mkdir('build') unless Dir.exist?('build')
  end

  def compile_scss(args = {})
    unless args.key?(:output)
      args[:output] = args[:input]
        .sub(%r{^scss/}, 'build/')
        .sub(/\.scss$/, '.css')
    end

    @logger.info(format('Processing file: %<filename>s', filename: args[:input]))
    @logger.info(format('Style: %<style>s', style: args[:style].to_s))

    File.open(args[:output], 'w') do |f|
      css = SassC::Engine.new(
        File.read(args[:input]),
        style: args[:style],
        cache: false,
        syntax: :scss,
        filename: args[:input],
        sourcemap: :none
      ).render

      f.puts AutoprefixerRails.process(
        css,
        map: false,
        cascade: false,
        from: args[:input],
        to: args[:output],
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

    @logger.info(format('Generated file: %<filename>s', filename: args[:output]))
  end

  def minify_file(args = {})
    args[:output] = minified_ext(args[:input]) unless args.key?(:output)

    # Minify file
    @logger.info(format('Processing file: %<filename>s', filename: args[:output]))
    File.open(args[:output], 'w') do |f|
      css = File.read(args[:input])

      f.puts SassC::Engine.new(
        css,
        style: :compressed,
        cache: false,
        syntax: :css,
        filename: args[:output],
        sourcemap: :none
      ).render
    end
  end

  def minified_ext(file_path)
    ext = File.extname(file_path)

    return file_path if file_path.end_with?(format('.min%<ext>s', ext: ext))

    file_path.gsub(ext, format('.min%<ext>s', ext: ext))
  end
end

namespace :build do
  files = {
    scss: Dir.glob('scss/*.scss')
  }

  helper = Helper.new(logger)

  desc 'Build CSS file'
  task :css do
    logger.info('Compiling CSS files')
    files[:scss].each do |file|
      helper.compile_scss(
        input: file,
        style: :expanded
      )
    end
    system(format(
      '%<vimcmd>s %<filelist>s',
      vimcmd: 'vim -c \'argdo setf css | execute "normal! gg=G" | update | quitall\'',
      filelist: '$(find build/ -type f -path "*.css" -a -not -path "*.min.css" | xargs)'
    ))
  end

  desc 'Minify CSS files'
  task :minify do
    logger.info('Minifying CSS files')
    Dir.chdir('build') do
      files[:css] = Dir.glob('*.css')
      files[:css].delete_if { |file| file.end_with?('.min.css') }

      files[:css].each do |file|
        helper.minify_file(input: file)
      end
    end
  end

  desc 'Build all CSS files'
  task :all do
    Rake::Task['build:css'].invoke
    Rake::Task['build:minify'].invoke
  end
end
