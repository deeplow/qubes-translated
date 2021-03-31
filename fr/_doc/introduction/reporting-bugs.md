---
lang: fr
layout: doc
permalink: /fr/doc/reporting-bugs/
redirect_from:
- /fr/bug-reports/
- /fr/reporting-bugs/
- /fr/doc/BugReportingGuide/
- /fr/bug-report/
- /fr/wiki/BugReportingGuide/
- /fr/bugs/
- /fr/bug/
ref: 121
title: Reporting bugs and other issues
---

# Reporting bugs and other issues #
<a id="reporting-bugs-and-other-issues"></a>

All issues pertaining to the Qubes OS Project (including auxiliary infrastructure such as the [website]) are tracked in [qubes-issues], our GitHub issue tracker.
If you're looking for help, please see [Help, Support, Mailing Lists, and Forum].

## Important ##
<a id="important"></a>

- **To disclose a security issue confidentially, please see the [Security] page.**
- **In all other cases, please do not email individual developers about issues.**
- **Please note that many issues can be resolved by reading the [documentation].**
- **If you see something that should be changed in the documentation, [submit a change][Documentation Guidelines].**

## Search Tips ##
<a id="search-tips"></a>

[Search both open and closed issues.][qubes-issues-all]
For example, you may be experiencing a bug that was just fixed, in which case the report for that bug is probably closed.
In this case, it would be useful to view [all bug reports, both open and closed, with the most recently updated sorted to the top][qubes-issues-bug-up-desc].

[Search using labels.][qubes-issues-labels]
For example, you can search issues by priority ([blocker], [critical], [major], etc.) and by component ([core], [manager/widget], [Xen], etc.).

Only Qubes team members can apply labels.
Every issue must have exactly one **type** (`T: bug`, `T: enhancement`, or `T: task`), exactly one **priority** (e.g., `P: major`), and at least one **component** (e.g., `C: core`).
Issues may have additional labels, if applicable (e.g., `crypto`, `ux`).

## Issue tracker guidelines ##
<a id="issue-tracker-guidelines"></a>

### Do not submit questions ###
<a id="do-not-submit-questions"></a>

[qubes-issues] is not the place to ask questions.
This includes, but is not limited to, troubleshooting questions and questions about how to do things with Qubes.
Instead, see [Help, Support, Mailing Lists, and Forum] for appropriate place to ask questions.
By contrast, [qubes-issues] is meant for tracking more general bugs, enhancements, and tasks that affect a broad range of Qubes users.

### Every issue must be about a single, actionable thing ###
<a id="every-issue-must-be-about-a-single-actionable-thing"></a>

If your issue is not actionable, please see [Help, Support, Mailing Lists, and Forum] for the appropriate place to post it.
If your issue would be about more than one thing, file them as separate issues instead.

### New issues should not be duplicates of existing issues ###
<a id="new-issues-should-not-be-duplicates-of-existing-issues"></a>

Before you submit an issue, check to see whether it has already been reported.
Search through the existing issues -- both open and closed -- by typing your key words in the **Filters** box.
If you find an issue that seems to be similar to yours, read through it.
If you find an issue that is the same as or subsumes yours, leave a comment on the existing issue rather than filing a new one, even if the existing issue is closed.
If an issue affects more than one Qubes version, we usually keep only one issue for all versions.
The Qubes team will see your comment and reopen the issue, if appropriate.
For example, you can leave a comment with additional information to help the maintainer debug it.
Adding a comment will subscribe you to email notifications, which can be helpful in getting important updates regarding the issue.
If you don't have anything to add but still want to receive email updates, you can click the "watch" button at the bottom of the comments.

### Every issue must be of a single type ###
<a id="every-issue-must-be-of-a-single-type"></a>

Every issue must be exactly one of the following types: a bug report (`bug`), a feature or improvement request (`enhancement`), or a task (`task`).
Do not file multi-typed issues.
Instead, file multiple issues of distinct types.
The Qubes team will classify your issue according to its type.

### New issues should include all relevant information ###
<a id="new-issues-should-include-all-relevant-information"></a>

When you file a new issue, you should be sure to include the version of Qubes you're using, as well as versions of related software packages ([how to copy information out of dom0]).
If your issue is related to hardware, provide as many details as possible about the hardware.
A great way to do this is by [generating and submitting a Hardware Compatibility List (HCL) report][hcl-howto], then linking to it in your issue.
You may also need to use command-line tools such as `lspci`.
If you're reporting a bug in a package that is in a [testing] repository, please reference the appropriate issue in the [updates-status] repository.
Project maintainers really appreciate thorough explanations.
It usually helps them address the problem more quickly, so everyone wins!

### Use the provided issue template ###
<a id="use-the-provided-issue-template"></a>

Please use the provided issue template.
Do not delete it or remove parts of it.
The issue template is carefully designed to elicit important information.
Without this information, the issue is likely to be incomplete.

It is also important to note the placement and content of the HTML comments in the issue template.
These help us to have issues with a consistent format.

### There are no guarantees that your issue will be addressed ###
<a id="there-are-no-guarantees-that-your-issue-will-be-addressed"></a>

Keep in mind that `qubes-issues` is an issue tracker, not a support system.
Creating a new issue is simply a way for you to submit an item for the Qubes team's consideration.
It is up to the Qubes team to decide whether or how to address your issue, which may include closing the issue without taking any action on it.
Even if your issue is kept open, however, you should not expect it to be addressed within any particular time frame, or at all.
At the time of this writing, there are well over one thousand open issues in `qubes-issues`.
The Qubes team has its own roadmap and priorities, which will govern the manner and order in which open issues are addressed.

## Following up afterward ##
<a id="following-up-afterward"></a>

If the Qubes developers make a code change that resolves your issue, then your GitHub issue will typically be closed from the relevant patch message.
After that, the package containing the fix will move to the appropriate [testing] repository, then to the appropriate stable repository.
If you so choose, you can test the fix while it's in the [testing] repository, or you can wait for it to land in the stable repository.
If, after testing the fix, you find that it does not really fix your bug, please leave a comment on your issue explaining the situation.
When you do, we will receive a notification and respond on your issue or reopen it (or both).
Please **do not** create a duplicate issue or attempt to contact the developers individually about your problem.

In other cases, your issue may be closed with a specific resolution, such as `R: invalid`, `R: duplicate`, or `R: won't fix`.
Each of these labels has a description that explains the label.
We'll also leave a comment explaining why we're closing the issue with one of these specific resolutions.
If the issue is closed without one of these specific resolutions, then it means, by default, that your reported bug was fixed or your requested enhancement was implemented.

## See also ##
<a id="see-also"></a>

- [Help, Support, Mailing Lists, and Forum]
- [Testing New Releases and Updates][testing]
- [How to Contribute]
- [Contributing Code]
- [Package Contributions]
- [Documentation Guidelines]

[qubes-issues-all]: https://github.com/QubesOS/qubes-issues/issues?utf8=%E2%9C%93&q=is%3Aissue
[qubes-issues-bug-up-desc]: https://github.com/QubesOS/qubes-issues/issues?q=label%3Abug+sort%3Aupdated-desc
[qubes-issues-labels]: https://github.com/QubesOS/qubes-issues/labels
[blocker]: https://github.com/QubesOS/qubes-issues/labels/P%3A%20blocker
[critical]: https://github.com/QubesOS/qubes-issues/labels/P%3A%20critical
[core]: https://github.com/QubesOS/qubes-issues/issues?q=is%3Aopen+is%3Aissue+label%3A%22C%3A+core%22
[manager/widget]: https://github.com/QubesOS/qubes-issues/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3A%22C%3A+manager%2Fwidget%22+
[Xen]: https://github.com/QubesOS/qubes-issues/issues?q=is%3Aopen+is%3Aissue+label%3A%22C%3A+Xen%22
[major]: https://github.com/QubesOS/qubes-issues/labels/P%3A%20major
[Security]: /fr/security/
[documentation]: /fr/doc/
[website]: /fr/
[qubes-issues]: https://github.com/QubesOS/qubes-issues/issues
[Help, Support, Mailing Lists, and Forum]: /fr/support/
[updates-status]: https://github.com/QubesOS/updates-status/issues
[how to copy information out of dom0]: /fr/doc/copy-from-dom0/
[testing]: /fr/doc/testing/
[How to Contribute]: /fr/doc/contributing/
[Contributing Code]: /fr/doc/contributing/#contributing-code
[Package Contributions]: /fr/doc/package-contributions/
[Documentation Guidelines]: /fr/doc/doc-guidelines/
[hcl-howto]: /fr/doc/hcl/#generating-and-submitting-new-reports