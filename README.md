batchgit
========

A shell script for maintaining git repositories system wide

##Configuration
When the script is first run it looks for a dot file called `~/.batchgitrc`. If this doesn't exist, as it won't the first time you run this script, it will search for all of the git repos on the disk and ask if you want to add them to the file or not. Repos added will be monitored, others will not be. This is useful if you used git clone to get a program or script but don't want to monitor it every time.

##How to run

###Initial run

The configuration file won't exist so the script will search for git repos across the disk. It will list each one it finds and ask if you want to track it. You can add them using Y/y, or ignore them using N/n.

###Multiple choice

        $ batchgit

This will offer a multiple choice for different options which can be selected using the numbers.

###Resetting configuration file

        $ batchgit -f
        $ batchgit -find

Either of these will search for git repos across the whole disk, just like the inital run.

###Adding single directores manually

        $ batchgit -a ~/path/to/repo
        $ batchgit -add ~/path/to/repo
        $ batchgit -a ./

The use of the `-a` flag will append the directory to the configuration file. This option will make the configuration file if it doesn't already exist, allowing you to manually `cd` around and add dirs rather than go through the setup. 

Using `./` for either of the add flags will add the current directory to the configuration file. If you use some shell magic, you can probably add directories recursively from your current location. Maybe I'll add that as a todo.

It will also check to see if the folders in the configuration file still exist, if not it will remove them to avoid issues. 

###Removing single directores manually

        $ batchgit -d ~/path/to/repo
        $ batchgit -del ~/path/to/repo
        $ batchgit -d ./

This flag works exactly the opposite to the previous one. Instead of adding single directories it will remove them. 

###git status

        $ batchgit -status
        $ batchgit -s

The script will pull the list of git repos it's tracking from the configuration file and will list any modified or untracked files in red.

###git pull

        $ batchgit -pull
        $ batchgit -d

Script will loop through git repositories and pull from remote source.

###git push

        $ batchgit -push
        $ batchgit -u

Script will loop through git repositories, pull first to avoid conflicts and then push to remote source.

        $ batchgit -pushonly
        $ batchgit -po
        
Script will only push rather than pull then push

##Issues

###Why are some of my repos not being found?
By default, it only looks for git repos from the home folder recursively. This means that if your repo lives in `\var` or something then it won't be found. If this is an issue I can add this to the todo list. Just raise an issue!

##TODO
1. Bootstrap new computer using `~/.batchgitrc` to git clone.
2. Tidy up output.
3. Add generic commit message.
4. Open new shells in places where changes have happened.
5. Strip out # you sometimes see in git
6. Only show pwd if repo has something to push, similar to how status works
7. Add a secondary, larger list for less frequent monitoring or maybe just pulling
8. Add a `-d` flag for removing directory
9. Add folders recursively from current location to configuration file.
10. ~~Handle directories that have been deleted since config file wrote~~
11. Add option for rebasing
