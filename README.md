# NAME

Test::TempDir - Temporary files support for testing.

# SYNOPSIS

	use Test::TempDir;

	my $test_tempdir = temp_root();

	my ( $fh, $file ) = tempfile();

	my $directory_scratch_obj = scratch();

# DESCRIPTION

Test::TempDir provides temporary directory creation with testing in mind.

The differences between using this and using [File::Temp](http://search.cpan.org/perldoc?File::Temp) are:

- If `t/tmp` is available (writable, creatable, etc) it's preferred over
`$ENV{TMPDIR}` etc. Otherwise a temporary directory will be used.

    This is `temp_root`

- Lock files are used on `t/tmp`, to prevent race conditions when running under a
parallel test harness.
- The `temp_root` is cleaned at the end of a test run, but not if tests failed.
- `temp_root` is emptied at the beginning of a test run unconditionally.
- The default policy is not to clean the individual `tempfiles` and `tempdirs`
within `temp_root`, in order to aid in debugging of failed tests.

# EXPORTS

- `temp_root`

    The root of the temporary stuff.

- `tempfile`
- `tempdir`

    Wrappers for the [File::Temp](http://search.cpan.org/perldoc?File::Temp) functions of the same name.

    The default options are changed to use `temp_root` for `DIR` and disable
    `CLEANUP`, but these are overridable.

- `scratch`

    Loads [Directory::Scratch](http://search.cpan.org/perldoc?Directory::Scratch) and instantiates a new one, with the same default
    options as `tempfile` and `tempdir`.

# SEE ALSO

[File::Temp](http://search.cpan.org/perldoc?File::Temp), [Directory::Scratch](http://search.cpan.org/perldoc?Directory::Scratch), [Path::Class](http://search.cpan.org/perldoc?Path::Class)

# VERSION CONTROL

This module is maintained using Git. You can get the latest version from
[git://github.com/nothingmuch/test-tempdir.git](git://github.com/nothingmuch/test-tempdir.git).

# AUTHOR

Yuval Kogman <nothingmuch@woobling.org>

# COPYRIGHT

	Copyright (c) 2008 Yuval Kogman. All rights reserved
	This program is free software; you can redistribute
	it and/or modify it under the same terms as Perl itself.
