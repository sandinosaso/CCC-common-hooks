Contributing
================

Coding rules
------------
To ensure consistency throughout the source code, keep these rules in mind as you are working:

* All features or bug fixes must be tested by one or more specs (unit-tests).
* All public API methods must be documented. (Details TBC).
* PHP code **must** follow Yii2 framwork [Code Conventions](https://github.com/yiisoft/yii2/blob/master/docs/internals/core-code-style.md)

**Note:** Legacy projects will continue using their own conventions. Old code will remain as is.

Commit Message Guidelines
-------------------------
(Source: [Angular contributing guidelines](https://github.com/angular/angular/blob/master/CONTRIBUTING.md))

We have very precise rules over how our git commit messages can be formatted.  This leads to **more
readable messages** that are easy to follow when looking through the **project history**.  But also,
we use the git commit messages to **generate the Angular change log**.

### Commit Message Format
Each commit message consists of a **header**, a **body** and a **footer**.  The header has a special
format that includes a **type**, a **scope** and a **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

The **header** is mandatory and the **scope** of the header is optional.

Any line of the commit message cannot be longer 100 characters! This allows the message to be easier
to read on GitHub as well as in various git tools.

### Revert
If the commit reverts a previous commit, it should begin with `revert: `, followed by the header of the reverted commit. In the body it should say: `This reverts commit <hash>.`, where the hash is the SHA of the commit being reverted.

### Type
Must be one of the following:

* **feat**: A new feature
* **fix**: A bug fix
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing
  semi-colons, etc)
* **refactor**: A code change that neither fixes a bug nor adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing tests
* **chore**: Changes to the build process or auxiliary tools and libraries such as documentation
  generation

### Scope
The scope could be anything specifying place of the commit change. For example
`SettingHelper`, `User`, etc.

### Subject
The subject contains succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

### Body
Just as in the **subject**, use the imperative, present tense: "change" not "changed" nor "changes".
The body should include the motivation for the change and contrast this with previous behavior.

### Footer
The footer should contain any information about **Breaking Changes** and is also the place to
reference GitHub issues that this commit **Closes**.

**Breaking Changes** should start with the word `BREAKING CHANGE:` with a space or two newlines. The rest of the commit message is then used for this

###Automatically checking message format
----------------------------------------

You can use a Git Hook to automatically check the format whenever you make a git commit.
This way you ensure your commits are correct before doing them. All this is done automatically
by an script that is called when you do git commit -m "YOUR MESSAGE"

You can use this file https://gist.github.com/sandinosaso/76ce4f2323e2cacd469d
save it to PROJECT_HOME_FOLDER/.git/hooks/prepare-commit-msg

and give it run permissions:
```chmod +x prepare-commit-msg```

Example usage:

**Wrong commit message get refused automatically:**

```
sandino@envy:~/github/CCCAPI/api$ git commit -m "Fix some bug error."
> Wrong commit message aborting commit: prepare-commit-msg.
> Expecting `git commit -m "<type>(<scope>): <subject><BLANK LINE><body><BLANK LINE>(<footer>)"`
```

**Good commit message:**

```
sandino@envy:~/github/CCCAPI/api$ git commit -m "fix(UserController.php): Fixes problem when obtaining licensee

After blank line this is the body of the commit messages
it can have several lines longs"
> Commit message OK: prepare-commit-msg
[CA-21 0c48cb0] [CA-21] fix(UserController.php): Fixes problem when obtaining licensee
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```

In the commit that was ok, the branch name is prepended to your commit message
automatically, so the text becomes:

```
"[CA-21] fix(UserController.php): Fixes problem..."
```

This way your commit automatically get tracked by JIRA issue an you can see it easily.
Moreover when your branch get merged to master it easy and clear to see where those commits
came from just looking at the list because they start with the JIRA issue ID.

You can use this hook to help you but if you find it is more restrictive or just not 
usefull you can change the code and share it with other if you make any improvment.
The code is in php so it easy to understand the hardest part may be the regular expression
that is used to check the commit message format, you can use this online tool to test
the expression that is currently being used: https://regex101.com/r/hP0bO5/ and test your changes.

This hook is already integrated to vagrant-dev-legacy machine so all apps will use it when 
they are started first time.

If you already have a vagrant created you can do this manually:

```
git clone git@github.com:sandinosaso/CCC-common-hooks.git
rm -fR .git/hooks/
cd apps
rm -fR ccc-customer-admin/.git/hooks/
rm -fR ccc-lh/.git/hooks/
rm -fR ccc-sipps-admin/.git/hooks/
rm -fR DSCAdmin/.git/hooks/
rm -fR DSCAuth/.git/hooks/
rm -fR DSCBWAssessments/.git/hooks/
rm -fR DSCCommon/.git/hooks/
rm -fR DSCDeploy/.git/hooks/
rm -fR DSCLanguage/.git/hooks/
rm -fR DSCPortal/.git/hooks/
rm -fR DSCRedirect/.git/hooks/
rm -fR IWBA/.git/hooks/
rm -fR SIPPSAssessment/.git/hooks/
```

```
ln -s CCC-common-hooks/hooks ccc-customer-admin/.git/hooks
ln -s CCC-common-hooks/hooks ccc-lh/.git/hooks
ln -s CCC-common-hooks/hooks ccc-sipps-admin/.git/hooks
ln -s CCC-common-hooks/hooks DSCAdmin/.git/hooks
ln -s CCC-common-hooks/hooks DSCAuth/.git/hooks
ln -s CCC-common-hooks/hooks DSCBWAssessments/.git/hooks
ln -s CCC-common-hooks/hooks DSCCommon/.git/hooks
ln -s CCC-common-hooks/hooks DSCDeploy/.git/hooks
ln -s CCC-common-hooks/hooks DSCLanguage/.git/hooks
ln -s CCC-common-hooks/hooks DSCPortal/.git/hooks
ln -s CCC-common-hooks/hooks DSCRedirect/.git/hooks
ln -s CCC-common-hooks/hooks IWBA/.git/hooks
ln -s CCC-common-hooks/hooks SIPPSAssessment/.git/hooks
```


The workflow: Jira and GitHub
-----------------------------



Further reading: [Processing JIRA issues with commit messages
](https://confluence.atlassian.com/jiracloud/jira-user-s-guide/working-with-an-issue/processing-jira-issues-with-commit-messages)

