[![CPAN version](https://badge.fury.io/pl/Encode-Base58-GMP.svg)](https://badge.fury.io/pl/Encode-Base58-GMP)
[![Build Status](https://travis-ci.org/grokify/base58-gmp-perl.svg?branch=master)](https://travis-ci.org/grokify/base58-gmp-perl)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/grokify/encode-base58-gmp/master/LICENSE)

Encode::Base58::GMP
===================

High speed Base58 encoding using GMP with BigInt and MD5 support

For version 1.0 upgrades, please read the INCOMPATIBLE CHANGES section below.

## Synopsis

```perl
use Encode::Base58::GMP;

# Encode Int as Base58
encode_base58(12345);                        # => 4ER string
encode_base58('0x3039');                     # => 4ER string
encode_base58(Math::GMPz->new('0x3039'));    # => 4ER string

# Encode Int as Base58 using GMP alphabet
encode_base58(12345,'bitcoin');              # => 4fr string
encode_base58(12345,'gmp');                  # => 3cn string

# Decode Base58 as Math::GMPz Int
decode_base58('4ER');                        # => 12345 Math::GMPz object
int decode_base58('4ER');                    # => 12345 integer

# Decode Base58 as Math::GMPz Int using GMP alphabet
decode_base58('4fr','bitcoin');              # => 12345 Math::GMPz object
decode_base58('3cn','gmp');                  # => 12345 Math::GMPz object

# MD5 Base58 Digest
md5_base58('foo@bar.com');                   # => w6fdCRXnUXyz7EtDn5TgN9

# Convert between alphabets for Bitcoin, Flickr and GMP
base58_from_to('123456789abcdefghijk','flickr','gmp') # => 0123456789ABCDEFGHIJ
base58_from_to('0123456789ABCDEFGHIJ','gmp','flickr') # => 123456789abcdefghijk

# Convert between Flickr and GMP - Deprecated
base58_flickr_to_gmp('123456789abcdefghijk') # => 0123456789ABCDEFGHIJ
base58_gmp_to_flickr('0123456789ABCDEFGHIJ') # => 123456789abcdefghijk
```

## Description

Encode::Base58::GMP is a Base58 encoder/decoder implementation using the GNU
Multiple Precision Arithmetic Library (GMP) with transcoding between
Flickr, Bitcoin and GMP Base58 implementations. The Flickr alphabet is the
default and used when no alphabet is provided.

Flickr Alphabet: [0-9a-zA-Z] excluding [0OIl] to improve human readability

Bitcoin Alphabet: [0-9A-Za-z] excluding [0OIl] to improve human readability

GMP Alphabet: [0-9A-Za-v]

The encode_base58, decode_base58 and md5_base58 methods support an alphabet
parameter which can be set to the supported alphabets ['bitcoin', 'flickr',
'gmp'] to indicate the value to be encoded or decoded.

## Requirements

This module requires GMP 4.2.0 and above. Prior versions are limited to Base36.

Perl 5.8.9 or above is required to ensure proper bigint handling. If you are not
using bigint numbers, it may be possible to skip the bigint tests and do a force
install; however, lower Perl versions are not supported.

## Functions

### encode_base58 ( $number [, $alphabet ] )

This routine encodes a $number in Base58. $number can be a Math::GMPz object
or a binary, octal, decimal or hexidecimal number. Binary, octal and hexidecimal
string literals must be prefixed with 0[Bb]/0/0[Xx] respectively. The Flickr
alphabet is used unless $alphabet is set to 'gmp'.

### decode_base58 ( $base58 [, $alphabet ] )

This routine decodes a Base58 value and returns a Math::GMPz object. Use int
on the return value to convert the Math::GMPz object to an integer.
The Flickr alphabet is used unless $alphabet is set to 'gmp'.

### base58_from_to( $base58, $from_alphabet, $to_alphabet )

This routine encodes a Base58 string from one encoding to another encoding.
This routing is not exported by default.

### base58_flickr_to_gmp( $base58_as_flickr )

This routine converts a Flickr Base58 string to a GMP Base58 string. This
routine is not exported by default.

### base58_gmp_to_flickr( $base58_as_gmp )

This routine converts a GMP Base58 string to a Flickr Base58 string. This
routine is not exported by default.

### md5_base58( $data [, $alphabet ] )

This routine returns a MD5 digest in Base58. This routine is not exported
by default.

## Changes

* 1.00 April 30, 2013
  * Add Bitcoin alphabet support.
  * Add zero-padding for md5_base58. This is an incompatible change from version 0.09.

### Incompatible Changes

* 1.00 April 30, 2013
  * md5_base58 is now zero-padded to provide a fixed-length Base58 string. Prior versions were not padding with leading zero values.

## See Also

1. [Encode::Base58](https://metacpan.org/pod/Encode::Base58), [Encode::Base58::BigInt](https://metacpan.org/pod/Encode::Base58::BigInt), [Math::GMPz](https://metacpan.org/pod/Math::GMPz), [Digest::MD5](https://metacpan.org/pod/Digest::MD5)
1. [Flickr](http://www.flickr.com/groups/api/discuss/72157616713786392/)
1. [Ruby version](https://rubygems.org/gems/base58_gmp)
1. [PHP Base64 example](http://marcus.bointon.com/archives/92-PHP-Base-62-encoding.html)

## Contributions

Any reports of problems, comments or suggestions are most welcome.

Please report these on [Github](https://github.com/grokify/base58-gmp-perl)

## License

Encode::Base58::GMP is available under an MIT-style license. See [LICENSE.txt](LICENSE.txt) for details.

Encode::Base58::GMP &copy; 2011-2015 by John Wang