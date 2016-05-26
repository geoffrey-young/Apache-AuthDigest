# NAME

Apache::AuthDigest - reimplementation of mod\_digest.c in Perl

# SYNOPSIS

    PerlModule Apache::AuthDigest

    <Location /protected>
      PerlAuthenHandler Apache::AuthDigest
      Require valid-user
      AuthType Digest
      AuthName "cookbook"
      AuthDigestFile .htdigest
    </Location>

# DESCRIPTION

Apache::AuthDigest is a reimplementation of mod\_digest,
the standard Apache module that implements Digest authentication.
For more information on Digest authentication, see RFC 2617:
  ftp://ftp.isi.edu/in-notes/rfc2617.txt

To do this, Apache::AuthDigest uses an API provided by
Apache::AuthDigest::API, which is included in this distribution.
see the Apache::AuthDigest::API manpage if you want to implement
a Digest authentication scheme that uses something other than
a flat file.

# EXAMPLE

The configuration for Apache::AuthDigest is relatively simple:

    PerlModule Apache::AuthDigest

    <Location /protected>
      PerlAuthenHandler Apache::AuthDigest
      Require valid-user
      AuthType Digest
      AuthName "cookbook"
      AuthDigestFile .htdigest
    </Location>

please note that Apache::AuthDigest does not configure a handler
for the authorization phase, which is a bit different than mod\_digest.
if you want to use something other than Require valid-user, you will
need to use Apache::AuthzDigest:

    PerlModule Apache::AuthDigest
    PerlModule Apache::AuthzDigest

    <Location /protected>
      PerlAuthenHandler Apache::AuthDigest
      PerlAuthzHandler Apache::AuthzDigest
      Require user foo
      AuthType Digest
      AuthName "cookbook"
      AuthDigestFile .htdigest
    </Location>

see the Apache::AuthzDigest manpage for more information.

# NOTES

this module essentially mimics the Digest implementation provided
by mod\_digest.c that ships with Apache.  there is another
implementation, classified as "experimental" that also ships with
Apache, mod\_auth\_digest.c, which is more complete wrt RFC 2617.
of particular interest is that the mod\_digest implementation does
not work with MSIE (so neither does this implemenation).  at some
point, Apache::AuthDigest::API::Full will implement a completely
compliant API - this will have to do for now.

Apache::AuthDigest will decline to process the transaction
if mod\_digest.c is detected, allowing the faster mod\_digest
implementation to control the fate of the request.

# FEATURES/BUGS

none that I know of yet, but consider this alphaware.

# SEE ALSO

perl(1), mod\_perl(1), Apache(3), Apache::AuthDigest(3)

# AUTHORS

Geoffrey Young <geoff@modperlcookbook.org>

Paul Lindner <paul@modperlcookbook.org>

Randy Kobes <randy@modperlcookbook.org>

# COPYRIGHT

Copyright (c) 2002, Geoffrey Young, Paul Lindner, Randy Kobes.  

All rights reserved.

This module is free software.  It may be used, redistributed
and/or modified under the same terms as Perl itself.

# HISTORY

This code is derived from the _Cookbook::DigestAPI_ module,
available as part of "The mod\_perl Developer's Cookbook".

For more information, visit http://www.modperlcookbook.org/
