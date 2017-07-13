## randomized directory walk

This is a drop-in replacement for `path/filepath.Walk()` that goes
through the directory in a randomized order rather than
lexigraphically sorted.

## Why?

I have some projects that involve directory trees with hundreds of
thousands or millions of files that I want to go through and do
checksums on periodically ("active anti-entropy"). It easily takes
hours to weeks to make it through the whole thing. That's fine; this
is a background process. However, it's problematic if the process is
restarted more often than that. Since it always starts at the
beginning, the files early on the list get checked quickly each time
it starts up, but the ones at the end of the list may never get
checked. This implementation goes in a random order, so it avoids a
"hot spot" at the beginning.
