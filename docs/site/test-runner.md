---
title: Test Runner
description: Calva provides commands and facilities that make running your Clojure tests easier 
---

# Test Runner

Calva provides commands that make running your Clojure tests easier.

!!! Note
    Since the test commands utilize cider-nrepl, they only work with Clojure, not ClojureScript. See [this issue](https://github.com/clojure-emacs/cider-nrepl/issues/555) for more details.

## Test Commands

Command | Shortcut | Description
--------|----------|------------
Run All Tests | `ctrl+alt+c shift+t` | Runs all tests
Run Failing Tests | `ctrl+alt+c ctrl+t` | Runs the tests that failed
Run Tests for Current Namespace | `ctrl+alt+c t` | Runs the tests for the current namespace. If not a `-test` namespace, tests for the current namespace plus its corresponding `<current-namespace>-test` namespace will be run.
Run Current Test | `ctrl+alt+c ctrl+alt+t` | Runs the test at the cursor. This includes a `defn` with a `:test` in its metadata, a `defn` defined in a `with-test`, and a `deftest`.
Toggle between implementation and test | - | Switches the file between implementation and test, prompts to create a new file if not found.

## Test on Save

You can enable the Calva setting "Test on Save" to have tests for the current namespace run on file save.

## Troubleshooting

### Tests Are Not Found

If you have tests in a test directory separate from your source directory, and those tests are not being found by the test runner, make sure the test directory is included in your paths. This will not be the case by default with a tools.deps (deps.edn) project. If your project is a tools.deps project, you can create an alias in your deps.edn file with `:extra-paths` that includes `"test"` (or the name of your test directory).

```clojure
{:aliases {:dev {:extra-paths ["test"]}}}
```

Having added the above to your deps.edn, when you jack-in, choose the `:dev` alias and the `test` directory will be added to your paths, which will allow tests located in the directory to be found by the test runner.

### Toggle between implementation and test command not working as intended

This feature mostly works with projects that has leiningen style folder structure and makes some assumption about your folder structure and test file names.
- It assumes that the test files ends with `_test` prefix.
- It assumes that your implementation files are in `src` folder and the test files are in `test` folder.

If you are using any non leiningen style folder structure, you may have to add source paths inside `.lsp/config.edn`.