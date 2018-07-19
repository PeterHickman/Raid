# Raid

I saw this really cool idea called `maid`, a Rake like tool that uses Markdown files to document and implement the tasks and how to do them. Go check it out at https://github.com/egoist/maid

It uses `npm` to install. Not wanting to install a bazzilion unverified dependencies I asked myself "How hard can this be?"

And here we are

## Purpose

Some of my everyday projects result in a ton of small scripts that are only related to the project but they fill up the directory and make it hard to find the real project files

By putting these all in a `Raidfile.md` I can replace all my small scripts with one file that also documents what these cryptic commands are for:

	$ raid
	raid -c         # Show configuration
	raid -s         # List all the recognised sources and shbangs
	
	raid add        # Add some numbers in javascript
	raid df         # What free space do we have on /
	raid echo       # Try and echo the command line arguments
	raid hello      # A programming classic in Ruby

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

# NAQ - Never asked questions

### About the name `raid`

Well the inspiration was called `maid` and I wrote this in Ruby so it got called `raid`. It was easier than thinking of a new name, I'm lazy like that

### No I mean `raid` is already a computer term

Yeah I know but surprisingly `raid` isn't a CLI command. I did at least check that out. Neither my Mac nor the various Ubuntu servers I manage have this as a command and since I am writing this for my own convenience thats good enough for me

### It's not that much like `maid` though

`maid` does a lot more. It has some really interesting features but the one that struck me was the use of Markdown as the file format to document the various tasks. That alone was a stroke of genius. Also being a Ruby programmer I saw it as a more flexible tool than Rake which us Ruby people use quite a lot. `maid` inspired a solution for the problems I faced with lots of one line scripts that I need. Once the problem was solved I moved on

But I recommend you check out `maid` at https://github.com/egoist/maid for yourself. It might be just what you need

### Not the fastest thing is it

Well we have a Ruby script parse a markdown file to create a temporary file that it then shells out to execute. So no, it's not built for speed. But it is convenient enough for me

It's my itch and this is how I scratch it :)
