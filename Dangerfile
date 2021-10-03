if github.pr_title.match(/^\[?WIP\]?\:/)
  failure("PR is still a WIP, do not merge") 
elsif github.pr_title.match(/^\[(fix|improvement|addition)\]:/i)
  failure("PR title must start with `Fix:`, `Improvement:`, or `Addition:` in order to be merged")
else
  pr_type = github.pr_title[/^\[(fix|improvement|addition)\]:/i,1]
  message("PR title is proper, PR is of type `#{pr_type}`")
end
