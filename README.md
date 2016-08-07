# pry-debugger

_JRuby 9k-compatible pry debugger._

Using MRI? I strongly recommend [`pry-byebug`][pry-byebug] instead!

Adds `step`, `next`, `finish`, and `continue` commands and `breakpoints` to [Pry][pry] using [ruby-debug][ruby-debug].

To use, run JRuby with the `--debug` flag, and then invoke `pry` normally:

```ruby
def some_method
  binding.pry          # Execution will stop here.
  puts 'Hello, World!' # Run 'step' or 'next' in the console to move here.
end
```

You can also add the `--debug` flag to your `JRUBY_OPTS` environment variable, so it will be picked up by any ruby application. Do note that running `JRuby` in debug mode **does** have a noticeable impact on performance.

## Execution Commands

* `step`: Step execution into the next line or method. Takes an optional numeric argument to step multiple times.

* `next`: Step over to the next line within the same frame. Also takes an optional numeric argument to step multiple lines.

* `finish`: Execute until current stack frame returns.

* `continue`: Continue program execution and end the Pry session.

## Breakpoints

You can set and adjust breakpoints directly from a Pry session using the following commands:

* `break`: Set a new breakpoint from a line number in the current file, a file and line number, or a method. Pass an optional expression to create a conditional breakpoint. Edit existing breakpoints via various flags.

    Examples:

    ```
break SomeClass#run            Break at the start of `SomeClass#run`.
break Foo#bar if baz?          Break at `Foo#bar` only if `baz?`.
break app/models/user.rb:15    Break at line 15 in user.rb.
break 14                       Break at line 14 in the current file.

break --condition 4 x > 2      Change condition on breakpoint #4 to 'x > 2'.
break --condition 3            Remove the condition on breakpoint #3.

break --delete 5               Delete breakpoint #5.
break --disable-all            Disable all breakpoints.

break                          List all breakpoints. (Same as `breakpoints`)
break --show 2                 Show details about breakpoint #2.
    ```

    Type `break --help` from a Pry session to see all available options.

* `breakpoints`: List all defined breakpoints. Pass `-v` or `--verbose` to see the source code around each breakpoint.

## Caveats

**pry-debugger** is not yet thread-safe, so only use in single-threaded environments.

Targets JRuby 9k only. If you're using MRI, I recommend using [`pry-byebug`][pry-byebug] instead.

## Remote debugging

Support for [pry-remote][pry-remote] (>= 0.1.4) is also included. Requires explicity requiring `pry-debugger`, not just relying on pry's plugin loader.

Want to debug a Rails app running inside `foreman`? Add to your `Gemfile`:

```ruby
gem 'pry'
gem 'pry-remote'
gem 'pry-debugger'
```

Then add `binding.remote_pry` where you want to pause:

```ruby
class UsersController < ApplicationController
  def index
    binding.remote_pry
    # ...
  end
end
```

Load a page that triggers the code. Connect to the session:

```bash
$ bundle exec pry-remote
```

## Tips

Stepping through code often? Add the following shortcuts to `~/.pryrc`:

```ruby
if defined?(PryDebugger)
  Pry.commands.alias_command 'c', 'continue'
  Pry.commands.alias_command 's', 'step'
  Pry.commands.alias_command 'n', 'next'
  Pry.commands.alias_command 'f', 'finish'
end
```

## Contributors

* Gopal Patel (@nixme)
* John Mair (@banister)
* Nicolas Viennot (@nviennot)
* Benjamin R. Haskell (@benizi)
* Joshua Hou (@jshou)
* Ivo Anjo (@ivoanjo)
* ...and others who helped with [pry-nav][pry-nav]

Patches and bug reports are welcome. Just send a [pull request][pullrequests] or file an [issue][issues]. [Project changelog][changelog].

[pry]:                http://pry.github.com
[pry-remote]:         https://github.com/Mon-Ouie/pry-remote
[pry-nav]:            https://github.com/nixme/pry-nav
[pullrequests]:       https://github.com/nixme/pry-debugger/pulls
[issues]:             https://github.com/nixme/pry-debugger/issues
[changelog]:          https://github.com/nixme/pry-debugger/blob/master/CHANGELOG.md
[pry-byebug]:         https://github.com/deivid-rodriguez/pry-byebug
