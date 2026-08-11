# Temple of Echoes --- Git Workflow

## Branches

``` text
main
└── develop
    └── feature/<feature-name>
```

### Branch purpose

#### `main`

Stable project baseline.

Do not develop experimental features directly on `main`.

#### `develop`

Integration branch for completed features.

#### `feature/*`

Used for one meaningful feature.

Current branch:

``` text
feature/health-system
```

## Basic workflow

Check branch:

``` powershell
git branch
```

Check status:

``` powershell
git status
```

Create a feature branch:

``` powershell
git checkout -b feature/<feature-name>
```

Stage changes:

``` powershell
git add .
```

Review staged changes:

``` powershell
git status
```

Commit:

``` powershell
git commit -m "Describe the change"
```

Push:

``` powershell
git push -u origin feature/<feature-name>
```

For an existing tracking branch:

``` powershell
git push
```

## Unreal + Git rules

Before committing:

1.  Close Unreal Engine when practical.
2.  Save the project.
3.  Check `git status`.
4.  Make sure generated folders are ignored.
5.  Review the changed files.
6.  Commit only the intended work.

## Important ignored Unreal folders

These should normally remain ignored:

``` text
Binaries/
DerivedDataCache/
Intermediate/
Saved/
.vs/
Build/
```

## Git LFS

Unreal binary assets should use Git LFS.

Current `.gitattributes` rules:

``` text
*.uasset filter=lfs diff=lfs merge=lfs -text
*.umap filter=lfs diff=lfs merge=lfs -text
```

Check whether a file is configured for LFS:

``` powershell
git check-attr filter -- "Content/Path/To/File.uasset"
```

Expected result:

``` text
filter: lfs
```

List LFS objects:

``` powershell
git lfs ls-files
```

## Recovery rule

Before a major system change, create a clean commit.

That gives the team a known restore point.

Recommended:

``` text
Working feature
      ↓
Compile
      ↓
Play-test
      ↓
Fix
      ↓
Clean working tree
      ↓
Commit
      ↓
Push
```

## Commit message examples

Good:

``` text
Add universal health integration
Fix enemy attack damage
Add player health HUD
Integrate combat damage
Fix enemy navigation
Add HP potion pickup
```

Avoid vague messages such as:

``` text
update
changes
test
new
fix
```

## Do not rewrite history casually

Avoid:

``` powershell
git push --force
```

Use normal pushes whenever possible.

If history rewriting is genuinely required, stop and verify the branch
and remote state first.
