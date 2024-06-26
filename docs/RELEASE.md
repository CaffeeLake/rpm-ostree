---
parent: Contributing
nav_order: 3
---

# Releasing rpm-ostree

1. Increment the `year_version` and `release_version` macros in `configure.ac`.
2. Increment the `Version` field in `rpm-ostree.spec`.
3. Verify the libdnf deps in `rpm-ostree.spec` are up to date by copy/pasting
   the relevant bits from the spec in the git submodule (`libdnf/libdnf.spec`).
4. Submit as a PR and wait until reviewed *and* CI is green.
5. Once merged, do `git pull $upstream && git reset --hard $upstream/main` on
   your local `main` branch to make sure you're on the right commit.
6. Draft release notes by seeding a HackMD.io with `git shortlog $last_tag..`
   and ideally collaborating with others. Filter out the commits from
   `dependabot`. See previous releases for format.
7. Use [`git-evtag`](https://github.com/cgwalters/git-evtag) to create a signed
   tag with the release notes as its content. Make the first line be the name of
   the tag itself.
8. Push the tag using `git push $upstream v202X.XX`.
9. Create the xz tarball: `make -C packaging -f Makefile.dist-packaging dist-snapshot`
10. Create a GitHub release for the new release tag using its contents and
    attach the tarball.
