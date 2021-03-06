A brief overview of versioning, branches, and releases

Facade will follow a three decimal release notation, e.g. v1.0.0

The first decimal is the major number, and it denotes database compatibility. If
for any reason a database changes (e.g. adding or removing tables or columns, or
changing the way the database is accessed), the major number will be
incremented. A migration path must be provided from the previous database schema
to the new one in setup.py under the "update" function.

The second decimal is the feature number, and it denotes a release which adds
new features but where the database structure is unchanged.  Examples include
changes to the web UI, performance improvements, and refactoring existing
functions. These releases must be self contained, meaning that a user has to do
no more than pull the new code. Any new feature that requires user intervention
before Facade works properly should be done in a major release.

The last decimal is for bug fix releases, which can happen at any time and
must apply transparently.

In general, users will run Facade from master. Master should always be stable,
with work happening in development branches. At release time, the relevant
development branch will be merged into master, and the tagged.

When a new major release happens, a branch will be created just prior to merging
any patches which break backwards compatibility (e.g. v1-compat, v2-compat,
etc). When checked out, this branch must be sufficient to continue running
Facade as usual on the prior version of the database. This provides a safety net
for users who may be unaware that pulling a new copy of the code could break
backwards compatibility and their ability to export config files. In this
situation, the user can check out the branch which corresponds with their
current major version, export their config files for safekeeping, check out
master, and do a migration or start fresh by importing their config files.

Since Facade is intended to run unattended until you need stats, the goal is to
make it easy to recover when unavoidable changes roll through.

