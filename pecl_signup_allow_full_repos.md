# Allow easier pecl signup

Currently it is reasonably tricky to signup for a pecl account. We have are acting as 'gate-keepers' to the project and have a slow response to people wanting to create an account.


## Allow a new signup method

Allow people who want a PECL account to submit a link to github repo
(or alternative VCS provider) that contains a 'ready-to-ship' PHP
extension repo.

We (or probably, I) will provide a tool that allows people to check
that their repo is ready to be submitted to PECL, including all the
appropriate things like buildconf works, the name of the project is
set in the appropriate place.

On signup, when someone submits a 'ready-to-ship' extension we will
have code that checks the extension for conformance, and if the
extension looks ready to go, their application is listed on a page
where anyone with PECL karma can approve or reject the application.

This would remove the bottleneck of only a few people being able to
approve the PECL accounts, while still blocking most inappropriate
signup attempts.
