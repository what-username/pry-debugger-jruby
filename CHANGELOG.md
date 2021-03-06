## 1.1.0 (2016-12-02)

* Avoid stepping into pry code
* Add help text when running without `--debug`

## 1.0.0 (2016-12-01)

* Revamp documentation for JRuby usage
* Add workaround for using `step` in JRuby
* Fix circular require warning
* Fixed missing banner in commands causing uninitialized variable warning
* Drop support for ruby < 2.2
* Officially forked from `pry-debugger`, renaming gem to `pry-debugger-jruby` and releasing on RubyGems

## 0.2.3 (2014-07-02)

* Support [pry] 0.10

## 0.2.2 (2013-03-07)

* Relaxed [debugger][debugger] dependency.

## 0.2.1 (2012-12-26)

* Support breakpoints on methods defined in the pry console. (@banister)
* Fix support for specifying breakpoints by *file:line_number*. (@nviennot)
* Validate breakpoint conditionals are real Ruby expressions.
* Support for [debugger][debugger] ~> 1.2.0. (@jshou)
* Safer `alias_method_chain`-style patching of `Pry.start` and
  `PryRemote::Server#teardown`. (@benizi)

## 0.2.0 (2012-06-11)

* Breakpoints
* **finish** command
* Internal cleanup and bug fixes

## 0.1.0 (2012-06-07)

* First release. **step**, **next**, and **continue** commands.
  [pry-remote 0.1.4][pry-remote] support.


[pry]:         http://pryrepl.org/
[pry-remote]:  https://github.com/Mon-Ouie/pry-remote
[debugger]:    https://github.com/cldwalker/debugger
