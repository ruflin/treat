# All commands are prefixed with "treat:".
namespace :treat do
  
  # Sandbox a script, for development.
  # Syntax: rake treat:sandbox
  task :sandbox do
    require './lib/treat'
    require './spec/sandbox'
  end
  
  # Prints the current version of Treat.
  # Syntax: rake treat:version
  task :version do
    # Parse out the version number from file.
    path = '../lib/treat/version.rb'
    file = File.expand_path(path, __FILE__)
    contents = File.read(file)
    puts contents[/VERSION = "([^"]+)"/, 1]
  end

  # Installs a language pack (default to english).
  # A language pack is a set of gems, binaries and
  # model files that support the various workers 
  # that are available for that particular language.
  # Syntax: rake treat:install (installs english)
  # - OR -  rake treast:install[some_language]
  task :install, [:language] do |t, args|
    require './lib/treat'
    Treat.install(args.language || 'english')
  end
  
  # Runs 1) the core library specs and 2) the 
  # worker specs for a) all languages (default) 
  # or b) a specific language (if specified).
  # Also outputs the coverage for the whole 
  # library to treat/coverage (using SimpleCov).
  # N.B. the worker specs are dynamically defined
  # following the examples found in spec/workers.
  # (see /spec/language/workers for more info)
  # Syntax: rake treat:spec (core + all langs)
  # - OR -  rake treat:spec[some_language]
  task :spec, [:language] do |t, args|
    require_relative 'spec/helper'
    Treat::Specs::Helper.start_coverage
    Treat::Specs::Helper.run_core_specs
    Treat::Specs::Helper.run_examples_as(
    :specs, args.language)
  end
  
  # Runs worker benchmarks for all languages (by 
  # default), or for a specific language (if supplied).
  # Also outputs an HTML table 
  # Syntax: rake treat:benchmark (all languages)
  # - OR -  rake treat:benchmark[language]
  task :benchmark, [:language] do |t, args|
    require_relative 'spec/helper'
    Treat::Specs::Helper.run_examples_as(
    :benchmarks, args.language)
  end

end
