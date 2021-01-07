# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
# directories %w(app lib config test spec features) \
#  .select{|d| Dir.exist?(d) ? d : UI.warning("Directory #{d} does not exist")}

## Note: if you are using the `directories` clause above and you are not
## watching the project directory ('.'), then you will want to move
## the Guardfile to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you'll have to watch "config/Guardfile" instead of "Guardfile"

guard :brakeman, run_on_start: true do
  watch(%r{^app/.+\.(erb|haml|rhtml|rb)$})
  watch(%r{^config/.+\.rb$})
  watch(%r{^lib/.+\.rb$})
  watch('Gemfile')
end

guard :bundler do
  require 'guard/bundler'
  require 'guard/bundler/verify'
  helper = Guard::Bundler::Verify.new

  files = ['Gemfile']
  files += Dir['*.gemspec'] if files.any? { |f| helper.uses_gemspec?(f) }

  # Assume files are symlinked from somewhere
  files.each { |file| watch(helper.real_path(file)) }
end

# Usage:
#     guard :foreman, <options hash>
#
# Possible options:
# * :concurreny - how many of each type of process you would like to run (default is, sensibly, one of each)
# * :env - one or more .env files to load
# * :procfile - an alternate Procfile to use (default is Procfile)
# * :port - an alternate port to use (default is 5000)
# * :root - an alternate application root
guard :foreman do
  # Rails example - Watch controllers, models, helpers, lib, and config files
  watch( /^app\/(controllers|models|helpers)\/.+\.rb$/ )
  watch( /^lib\/.+\.rb$/ )
  watch( /^config\/*/ )
end
