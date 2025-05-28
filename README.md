# openfoodfacts-build-cache

A repo to store some build caches of the Open Food Facts taxonomies (when GitHub cache is not the right option) for [product opener (aka open food facts server)](https://github.com/openfoodfacts/openfoodfacts-server/).

The mechanism is [explained here](https://openfoodfacts.github.io/openfoodfacts-server/dev/explain-taxonomy-build-cache/).

# Cleaning up old history

To do this I used `git rebase` to get rid of old history. The overall process was as follows:

Checkout the repository locally and run:

```
git rebase -i --root
```

You can then interactively edit the rebase file, changing `pick` to `drop` for all of the older `put_to_cache ...` commits. I kept the commits to the LICENCE and README.md.

You may get an issue if not all README.md commits are included, like this:

```
CONFLICT (modify/delete): README.md deleted in HEAD and modified in 2bdb4533 (doc: Add repo doc (#2)).  Version 2bdb4533 (doc: Add repo doc (#2)) of README.md left in tree.
error: could not apply 2bdb4533... doc: Add repo doc (#2)
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
```

I resolved this by checking the content of README.md and after verifying it was all OK I ran:

```
git add README.md
git rebase --continue
```

Finally push the revised commit history back to the origin with:

```
git push -f
```
