# saferoute-support

Support page for the SafeRoute iOS app, hosted via GitHub Pages.

Live at: https://minhajk21.github.io/saferoute-support/

This is a single-file static site. Edit `index.html` directly to update content. Changes pushed to `main` are live within a minute.

## Release-day note for branch d3b-1.4 (delete this section before merging to main)

D3b goes live on the day 1.4 reaches the App Store, after D3a (branch `d3a-1.4`) is already live on `main` with every `[RELEASE DATE]` filled in. Once D3a is published, rebase this branch onto that `main`:

```
git fetch origin
git rebase origin/main
```

This assumes D3a was merged with its own commits, not squashed. Each paragraph of `index.html` is one line, so filling in `[RELEASE DATE]` conflicts with every line this branch also changes. Expect these conflicts (tested on 20 October 2026 in a scratch copy where D3a was published with the dates filled in; the result was this branch with only the dates changed):

1. "Schools, Home values, coverage columns, Offline": the `Updated` line in the header and the "last reviewed on" line in the footer. Keep this branch's side, the one with `[1.4 RELEASE DAY]`. Its footer line also carries the sentence about school and home-value data.
2. "Support 1.4 draft (D3a): apply the build 33 fact-check": this is a cherry-pick of a D3a commit that is already on `main`, so run `git rebase --skip`. Git drops the other cherry-pick, "Support 1.4 draft (D3a): route labels without crime data, and say the row was replaced", by itself. Skip any other "Support 1.4 draft (D3a)" commit that conflicts in the same way, after checking that `main` already has its change.
3. "Support 1.4, RELEASE DAY ONLY (D3b): apply the build 33 fact-check": the 30 September correction in section 04 (share links) and the 4 October correction in section 08 (usage analytics). Keep the published D3a line, with its date, and add ` <strong>Update, [1.4 RELEASE DAY]:</strong> version 1.4 is now on the App Store.` before its closing `</p>`.

The other commits apply cleanly. Then `grep -c '\[RELEASE DATE\]' index.html` and `grep -c '\[CHECK' index.html` must both return 0, and `grep -c '\[1.4 RELEASE DAY\]' index.html` returns 4 (the `Updated` line, the two Updates in item 3, the footer). On release day, replace `[1.4 RELEASE DAY]` with the date and delete this section in the same commit.
