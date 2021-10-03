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
sourcefiles = (git.modified_files + git.added_files).uniq.select { |file| file.match(sourcefile_regexp) }
sourcefiles.each do |filename|
  additions = git.diff_for_file(filename).patch.lines.grep(/^\+/)
  additions.each do |line|
    next unless line.include?("TODO")
    failure("TODO included in additions to file #{filename} without an issue link") unless line.match(issue_regexp)
  end
end