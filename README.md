# Raid

I saw this really cool idea called `maid`, a Rake like tool that uses Markdown files to document and implement the tasks and how to do them. Go check it out at https://github.com/egoist/maid

It uses `npm` to install. Not wanting to install a bazzilion unverified dependencies I asked myself "How hard can this be?"

So here we are

## Purpose

Some of my everyday projects result in a ton of small scripts that are only related to the project but they fill up the directory and make it hard to find the real project files

By putting these all in a `Raidfile.md` I can replace all my small scripts with one file that also documents what these cryptic commands are for:

	$ raid
	raid -c         # Show configuration
	raid -s         # List all the recognised sources and shbangs
	
	raid hello      # A programming classic in Ruby
	raid df         # What free space do we have on /
	raid add        # Add some numbers in javascript
	raid echo       # Try and echo the command line arguments

## The `Raidfile.md`

The application parses the `Raidfile.md` as follows:

0. All level 2 headings, `##`, are the task names. Note there must be a space after the `##`, before the task name
0. All the quotes, `>`, after the level 2 heading are the description of the task
0. Everything between the fences, <code>```</code>, will be the script that is run. The signature is the text that is included in the opening fence
0. Everything else is ignored

See the example `Raidfile.md` for more details

## Signatures

By defaults `raid` comes with the following predefined signatures:

	Current signatures
	==================
	source          shbang                         loaded from
	--------------- ------------------------------ ---------------
	bash            #!/bin/sh                      default
	javascript      #!/usr/bin/env js              default
	js              #!/usr/bin/env js              default
	ruby            #!/usr/bin/env ruby            default
	sh              #!/bin/sh                      default

If you want to overwrite one or add a new signature you can create a `~/.raid_signatures` file such as:

	python #!/usr/bin/env python

Which will add the python signature to the list of known signatures:

	Current signatures
	==================
	source          shbang                         loaded from
	--------------- ------------------------------ ---------------
	bash            #!/bin/sh                      default
	javascript      #!/usr/bin/env js              default
	js              #!/usr/bin/env js              default
	python          #!/usr/bin/env python          ~/.raid_signatures
	ruby            #!/usr/bin/env ruby            default
	sh              #!/bin/sh                      default

# TODO

0. Document stuff
