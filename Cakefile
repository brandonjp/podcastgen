fs = require 'fs'
{spawn, exec} = require 'child_process'
CSON = require 'cson-safe'

# ANSI Terminal Colors.
bold = red = green = reset = ''
unless process.env.NODE_DISABLE_COLORS
  bold  = '\x1B[0;1m'
  red   = '\x1B[0;31m'
  green = '\x1B[0;32m'
  reset = '\x1B[0m'
  
# Log a message with a color.
log = (message, color, explanation) ->
  console.log color + message + reset + ' ' + (explanation or '')

# Build transformer from source.
build = (cb) ->
  run 'mkdir', ['-p','bin', 'lib'], ->
    compile ['podcastgen','command'], 'src/', 'lib/', cb

compile = (srcFiles, srcDir, destDir, cb) ->
  srcFilePaths = srcFiles.map (filename) -> "#{srcDir}/#{filename}.coffee"
  args = ['--bare', '-o', destDir, '--compile'].concat srcFilePaths
  coffee args, cb

# Run CoffeeScript command
coffee = (args, cb) -> run 'coffee', args, cb

run = (executable, args = [], cb) ->
  proc =         spawn executable, args
  proc.stdout.on 'data', (buffer) -> log buffer.toString(), green
  proc.stderr.on 'data', (buffer) -> log buffer.toString(), red
  proc.on        'exit', (status) ->
		cb() if typeof cb is 'function'

task 'build', 'build podcastgen from source', build
