# phabricator-rfcemail
Unofficial Allow full RFC Email registrations in Phabricator.

Some users have characters in their email addresses that are disallowed in upstream Phabricator despite being valid RFC 5322 email addresses.

For example, any Irish person with an apostrophe in their name (`O'Brien`, `O'Connor`, `D'Angelo`, etc)

## Installing

```
cd phabricator
git apply rfcemail.patch
```

## Creating

Aim to make the least changes possible. This is why we only replace the regular expression.

Checkout Phabricator. Make two copies of the `phabricator` subdir, `a` and `b`. Make your changes to `b`.

```
git patch a b > rfcemail.patch
```

Send in a PR, please make sure to include from what date onwards it is good for.

## Upstream

As of [2017-05-17](https://secure.phabricator.com/T12718) there is no interest from upstream in fixing this bug, calling them `technically-deliverable-but-bizzarely-exotic addresses`. Phacility instead recommends you maintain a patch yourself. This is that patch.

## PHP Validation

For whatever reason upstream chose not use [php builtin](http://php.net/manual/en/filter.examples.validation.php) `filter_var($email, FILTER_VALIDATE_EMAIL)` and `filter_var($email, FILTER_SANITIZE_EMAIL)`. This patch maintains that decision as to incur less code changes, but expands the regular expression.
