---
name: commit
description: Git commit message convention
disable-model-invocation: false
---
# convention
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```
appends a ! after the type/scope, introduces a breaking API change

# types
- fix
- feat
- build
- chore
- ci
- docs
- style
- refactor
- perf
- test

# examples
- feat: allow provided config object to extend other configs
- feat(lang): add Polish language
- feat(api)!: send an email to the customer when a product is shipped

# workflow
1. Check `git status` to see untracked and modified files
2. Run `git add` to stage all relevant files before committing
3. Create commit with conventional commit message format
4. Verify commit with `git status`

