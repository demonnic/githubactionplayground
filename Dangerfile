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
issue_regexp = Regexp.new(/https?:\/\/(?:www\.)?github\.com\/Mudlet\/Mudlet\/issues\/(\d+)/)
sourcefile_regexp = Regexp.new(/.*\.(cpp|c|h|lua)$/)
git.diff.each do |chunk|
  next unless chunk.path.match(sourcefile_regexp)
  message("Source file #{chunk.path}")
  additions = chunk.patch.lines.grep(/^\+/)
  message(chunk.patch)
  additions.each do |line|
    if line.include?("TODO") then
      issue_match = line.match(issue_regexp)
      failure("TODO added in #{chunk.path} without a linked github issue") unless issue_match
    end
  end
end
