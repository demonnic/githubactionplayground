# Automates some of the checks for PRs

## Checks title formatting. This formatting is used for changelog and release note generation.
title_regex = Regexp.new(/^\[?(fix|improvement|addition)\]?:/i)
if github.pr_title.match(/^\[?WIP\]?\:/)
  failure("PR is still a WIP, do not merge") 
elsif not github.pr_title.match(title_regex)
  failure("PR title must start with `Fix:`, `Improvement:`, or `Addition:` in order to be merged")
else
  pr_type = github.pr_title[title_regex,1]
  message("PR title is proper, PR is of type `#{pr_type}`")
end

## Checks that any TODOs on changed lines have a link to a github issue
git.diff.each do |chunk|
  message chunk.patch
end
