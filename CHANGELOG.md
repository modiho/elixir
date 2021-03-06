# Changelog for Elixir v1.1

Note: Erlang 17.1 contains a regression in its wildcard implementation that causes
tools like rebar to fail. If you have a project with rebar dependencies and is using
Erlang 17.1, remember to update to at least Erlang 17.3.

## v1.1.0-dev

### 1 Enhancements

  * [CLI] Add support for `--werl` in Windows bash-like shells
  * [Dict] Add `Dict.get_and_update/3` which behaves similar to the now deprecated Access protocol
  * [Dict] Add `Dict.get_lazy/3`, `Dict.pop_lazy/3` and `Dict.put_new_lazy/3`
  * [EEx] Add `:trim` option to EEx that automatically trims the left side of `<%` and right side `%>` if only spaces and new lines preceed/follow them
  * [Enum] Add `Enum.sample/1`, `Enum.minmax/1`, `Enum.minmax_by/2`, `Enum.reverse_slice/3`, `Enum.dedup/1`, `Enum.dedup_by/2`, `Enum.usort/1` and `Enum.usort_by/2`
  * [Enum] Inline common map usage in `Enum` functions for performance
  * [ExUnit] Add number of skipped tests to `ExUnit` output
  * [ExUnit] Make timeout configurable for the whole test suite via the `:timeout` configuration
  * [ExUnit] Allow moduledoc to be filtered/skipped in doctests
  * [File] Add `File.lstat/1` and `File.lstat/1` that works like `File.stat/1` but is able to return symlink information (i.e. it does not traverse symlinks)
  * [IEx] Add `b/1` helper that shows documentation for behaviour modules and its callback functions
  * [Integer] Add `Integer.digits/2` and `Integer.undigits/2`
  * [Inspect] Add the `:safe` option to `inspect/2` and make it safe by default, meaning failures while inspecting won't trigger other failures. Instead, it will be wrapped in an exception which is properly formatted
  * [Logger] Format and handle 17.4 onward stacktraces
  * [Kernel] No longer include `:crypto` and `:syntax_tools` as dependencies. The former is only needed if you have encrypted debug info (therefore you can add `:crypto` as a dependency manually) and the latter is no longer used
  * [Kernel] Raise when `var.Alias` syntax is used and it does not expand to an atom at compile time (previously it just warned)
  * [Kernel] `::/2` is now a special form
  * [Mix] Check Elixir version right after archive installation and provide feedback if there is a mismatch
  * [Mix] Allow rebar dependencies with `mix.exs` to be compiled with Mix
  * [Mix] Allow rebar dependencies to be specified via `:path`
  * [Record] Expand attributes and macros when extracting records
  * [Stream] Add `Stream.dedup/1`, `Stream.dedup_by/2`, `Stream.usort/1` and `Stream.usort_by/2`
  * [String] Support calculation of the jaro distance between strings (usually names) via `String.jaro_distance/2`. This is used by Mix to support "Did you mean?" feature when a task does not exist
  * [StringIO] `StringIO.flush/1` was added to flush the output of a StringIO device
  * [URI] Default ports were added for "ws" and "wss" schemas

### 2. Bug fixes

  * [Code] `:delegate_locals_to` failed to delegate to the chosen module in many situations and messed up stacktraces. This option has therefore been replaced by imports
  * [EEx] Allow EEx interpolation to also apply inside quotations `<%%= ... %>`
  * [Exception] Do not fail when calculating an exception message, even if the message is invalid
  * [ExUnit] Skipped tests now correctly count towards the total of tests in the result returned by `ExUnit.run/0`
  * [ExUnit] Fix a bug where failures when inspecting data structure or retrieving error messages could bring the whole ExUnit runner down
  * [ExUnit] Ensure the Logger is flushed when running ExUnit via Mix
  * [Kernel] Throw syntax error for undefind atom/alias syntax `:foo.Bar`
  * [Mix] Ensure automatic protocol consolidation via `:consolidate_protocols` is triggered in umbrella apps
  * [Module] Do not accept non-Elixir module names in `Module.split/1`
  * [Regex] Fix splitting of empty strings with regexes when trim is set to `true`. Now both `String.split/3` and `Regex.split/3` return an empty list when called with an empty string and trim is enabled
  * [Regex] Fix `Regex.replace/4` so it doesn't discard escape characters
  * [Version] Fix `to_string` for `Version` with numeric pre-release

### 3. Soft deprecations (no warnings emitted)

  * [Regex] Ungreedy option `r` is deprecated in favor of `U` (which is standard in regular expressions in other languages)
  * [Enum] `Enum.uniq/2` is deprecated in favor of `Enum.uniq_by/2`

### 4. Deprecations

  * [Access] The Access protocol is deprecated. The Access protocol relies on the code server in development and test mode (when protocol consolidation is not applied) and it generated a bottleneck when working with multiple processes and the Access protocol was invoked hundreds of times (which is not uncommon). In future releases the Access protocol will be removed although we will keep the `Access` module around for compatibility reasons
