# The Twelve-Factor App: XII. Admin Processes

Source: https://12factor.net/admin-processes

## Run admin/management tasks as one-off processes

The process formation comprises processes handling the app's regular operations, such as web requests. Developers separately need to execute one-off administrative and maintenance tasks:

- Database migrations (e.g., `manage.py migrate` in Django, `rake db:migrate` in Rails)
- Running a console or REPL shell for arbitrary code execution or inspecting app models against the live database
- Running one-time scripts from the app's repository (e.g., `php scripts/fix_bad_records.php`)

## Environment Consistency

"One-off admin processes should be run in an identical environment as the regular long-running processes of the app." They operate against the same release, using identical codebase and config. Admin code must ship with application code to prevent synchronization issues.

## Dependency Isolation

Apply the same dependency isolation techniques across all process types. For instance, if the Ruby web process uses `bundle exec thin start`, database migrations should use `bundle exec rake db:migrate`. Similarly, Python programs using Virtualenv should use the vendored `bin/python` for both the Tornado webserver and any `manage.py` admin processes.

## REPL Support

Twelve-factor favors languages providing built-in REPL shells and easy one-off script execution. In local deployments, developers invoke admin processes via direct shell commands. In production, developers use ssh or other remote execution mechanisms.
