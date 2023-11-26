# `!bmakelib.timed`

Times the execution of a given target and report the duration with milliseconds precision.

The following variables will be populated:
  * `stdlib.vars.timed.begin-ts.TARGET_NAME` (nanos)`
  * `stdlib.vars.timed.end-ts.TARGET_NAME` (nanos)`
  * `stdlib.vars.timed.duration.TARGET_NAME` (millis)`

### Example 1

Makefile:

```Makefile
my-target :
	@sleep 2
	@echo 😴 I slept for 2 seconds.
```

Shell:

```text
$ make my-target!bmakelib.timed
Using default value 'yes' for variable 'stdlib.conf.timed.SILENT'
😴 I slept for 2 seconds.
Target 'my-target' took 2009ms to complete.
```

### Example 2

Makefile:

```Makefile
some-target :
	@sleep 2

my-target : stdlib.conf.timed.SILENT = yes
my-target : some-target!bmakelib.timed
	@echo ✅ Made some-target in $(stdlib.vars.timed.duration.some-target)ms 🙌
```

Shell:

```text
$ make my-target
✅ Made some-target in 2008ms 🙌
```

### Notes

See `!timed` below for a shorter name.

---

# `bmakelib.conf.timed.convenience-target`

Whether to define the convenience target `!timed`.
Set to 'no' *before* including bmakelib to disable.

---

# `!timed`

Convenice target with a shorter and more intuitive name.  It's a drop-in replacement for
`!bmakelib.timed`.

Lets you write

```Makefile
some-target : other-target!timed
```

or

```text
$ make my-target!timed
```

See also `bmakelib.conf.timed.convenience-target`.

---

 # `bmakelib.conf.timed.SILENT`

 If set to yes, causes `!bmakelib.timed` to emit an info containing the duration of the target.

---


