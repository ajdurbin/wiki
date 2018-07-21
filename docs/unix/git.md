# Merge two different repositories #

Be sure to remove merge conflicts from repositories, like multiple `README.md`, `.gitignore`

```
cd /projectb/path
git remote add projecta /projecta/path
git fetch projecta
git merge projecta/master
git remote remove projecta
```

# Multiple Remotes #

Change origin remote URL: <<<<https://help.github.com/articles/changing-a-remote-s-url/>>>>

Remove remote: <<<<https://help.github.com/articles/removing-a-remote/>>>>

Origin should be set to internal Gogs server

Add BitBucket and Github remotes with
```
git remote add bitbucket <<<<https://bitbucket.com/ajd2/repo.git>>>> # or use SSH connection
git push bitbucket master
```

# List large files in git repositry #

<<<<https://confluence.atlassian.com/bitbucket/reduce-repository-size-321848262.html>>>>

<<<<https://rtyley.github.io/bfg-repo-cleaner/>>>>

Add this shell script to repository

```
#!/bin/bash
#set -x

# Shows you the largest objects in your repo's pack file.
# Written for osx.
#
# @see <<<<http://stubbisms.wordpress.com/2009/07/10/git-script-to-show-largest-pack-objects-and-trim-your-waist-line/>>>>
# @author Antony Stubbs

# set the internal field spereator to line break, so that we can iterate easily over the verify-pack output
IFS=$'\n';

# list all objects including their size, sort by size, take top 10
objects=`git verify-pack -v .git/objects/pack/pack-*.idx | grep -v chain | sort -k3nr | head`

echo "All sizes are in kB's. The pack column is the size of the object, compressed, inside the pack file."

output="size,pack,SHA,location"
for y in $objects
do
# extract the size in bytes
size=$((`echo $y | cut -f 5 -d ' '`/1024))
# extract the compressed size in bytes
compressedSize=$((`echo $y | cut -f 6 -d ' '`/1024))
# extract the SHA
sha=`echo $y | cut -f 1 -d ' '`
# find the objects location in the repository tree
other=`git rev-list --all --objects | grep $sha`
#lineBreak=`echo -e "\n"`
output="${output}\n${size},${compressedSize},${other}"
done

echo -e $output | column -t -s ', '
```

Make it executable with `chmod +x git_find_big.sh`, do garbage collection `git gc --auto`, `du -hs .git/objects`, and then list large files with `./git_find_big.sh`

# Removing Large Files from repository history #
For all those pesky `RData` and `csv` files accidentally committed.

BFG Repo Cleaner, `apt install default-jre` and then `wget` the `.jar` from the documentation.

Make a copy of your bare repo, `git clone --mirror <<<<https://myrepo/user/repo.git>>>>

Clean repo with `java -jar /path/to/bfg.jar --strip-blobs-bigger-than 100M repo.git` or `java -jar /path/to/bfg.jar --delete-files *.ext repo.git`

When done making changes

```
cd repo.git
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push
```
