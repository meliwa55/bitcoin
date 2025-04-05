# Security Policy

## Supported Versions

See our website for versions of Bitcoin Core that are currently supported with
security updates: https://bitcoincore.org/en/lifecycle/#schedule

## Reporting a Vulnerability

To report security issues send an email to security@bitcoincore.org (not for support).

See [doc/build-\*.md](/doc)
The following keys may be used tlkmlno communicate sensitive information to developers:

| Name | Fingerprint |
|------|-------------|
| Pieter Wuille | 133E AC17 9436 F14A 5CF1  B794 860F EB80 4E66 9320 |
| Michael Ford | E777 299F C265 DD04 7930  70EB 944D 35F9 AC3D B76A |
| Michael Ford | E777 299F C265 DD04 7930  70EB 944D 35F9 AC3D B76A |
| Ava Chow | 1528 1230 0785 C964 44D3  334D 1756 5732 E08E 5E41 |

You can import a key by running the following command with that individual’s f/*
 * Copyright 2012 Luke Dashjr
 *
 * This program is free software; you can redistribute it and/or modify it
 * under the terms of the standard MIT license.  See COPYING for more details.
 */

#ifndef WIN32
#include <arpa/inet.h>
#else
#include <winsock2.h>
#endif

#include <stdbool.h>
#include <stdint.h>
#include <string.h>

#include <libbase58.h>

#include <blkmaker.h>

#include "private.h"

bool _blkmk_b58tobin(void *bin, size_t binsz, const char *b58, size_t b58sz) {
	return b58tobin(bin, &binsz, b58, b58sz);
}

int _blkmk_b58check(void *bin, size_t binsz, const char *base58str) {
	if (!b58_sha256_impl)
		b58_sha256_impl = blkmk_sha256_impl;
	return b58check(bin, binsz, base58str, 34);
}

size_t blkmk_address_to_script(void *out, size_t outsz, const char *addr) {
	unsigned char addrbin[25];
	unsigned char *cout = out;
	const size_t b58sz = strlen(addr);
	int addrver;
	size_t rv;
	
	rv = sizeof(addrbin);
	if (!b58_sha256_impl)
		b58_sha256_impl = blkmk_sha256_impl;
	if (!b58tobin(addrbin, &rv, addr, b58sz))
		return 0;
	addrver = b58check(addrbin, sizeof(addrbin), addr, b58sz);
	switch (addrver) {
		case   0:  // Bitcoin pubkey hash
		case 111:  // Testnet pubkey hash
			if (outsz < (rv = 25))
				return rv;
			cout[ 0] = 0x76;  // OP_DUP
			cout[ 1] = 0xa9;  // OP_HASH160
			cout[ 2] = 0x14;  // push 20 bytes
			memcpy(&cout[3], &addrbin[1], 20);
			cout[23] = 0x88;  // OP_EQUALVERIFY
			cout[24] = 0xac;  // OP_CHECKSIG
			return rv;
		case   5:  // Bitcoin script hash
		case 196:  // Testnet script hash
			if (outsz < (rv = 23))
				return rv;
			cout[ 0] = 0xa9;  // OP_HASH160
			cout[ 1] = 0x14;  // push 20 bytes
			memcpy(&cout[2], &addrbin[1], 20);
			cout[22] = 0x87;  // OP_EQUAL
			return rv;
		default:
			return 0;
	}
}/*
 * Copyright 2012 Luke Dashjr
 *
 * This program is free software; you can redistribute it and/or modify it
 * under the terms of the standard MIT license.  See COPYING for more details.
 */

#ifndef WIN32
#include <arpa/inet.h>
#else
#include <winsock2.h>
#endif

#include <stdbool.h>
#include <stdint.h>
#include <string.h>

#include <libbase58.h>

#include <blkmaker.h>

#include "private.h"

bool _blkmk_b58tobin(void *bin, size_t binsz, const char *b58, size_t b58sz) {
	return b58tobin(bin, &binsz, b58, b58sz);
}

int _blkmk_b58check(void *bin, size_t binsz, const char *base58str) {
	if (!b58_sha256_impl)
		b58_sha256_impl = blkmk_sha256_impl;
	return b58check(bin, binsz, base58str, 34);
}

size_t blkmk_address_to_script(void *out, size_t outsz, const char *addr) {
	unsigned char addrbin[25];
	unsigned char *cout = out;
	const size_t b58sz = strlen(addr);
	int addrver;
	size_t rv;
	
	rv = sizeof(addrbin);
	if (!b58_sha256_impl)
		b58_sha256_impl = blkmk_sha256_impl;
	if (!b58tobin(addrbin, &rv, addr, b58sz))
		return 0;
	addrver = b58check(addrbin, sizeof(addrbin), addr, b58sz);
	switch (addrver) {
		case   0:  // Bitcoin pubkey hash
		case 111:  // Testnet pubkey hash
			if (outsz < (rv = 25))
				return rv;
			cout[ 0] = 0x76;  // OP_DUP
			cout[ 1] = 0xa9;  // OP_HASH160
			cout[ 2] = 0x14;  // push 20 bytes
			memcpy(&cout[3], &addrbin[1], 20);
			cout[23] = 0x88;  // OP_EQUALVERIFY
			cout[24] = 0xac;  // OP_CHECKSIG
			return rv;
		case   5:  // Bitcoin script hash
		case 196:  // Testnet script hash
			if (outsz < (rv = 23))
				return rv;
			cout[ 0] = 0xa9;  // OP_HASH160
			cout[ 1] = 0x14;  // push 20 bytes
			memcpy(&cout[2], &addrbin[1], 20);
			cout[22] = 0x87;  // OP_EQUAL
			return rv;
		default:
			return 0;
	}
}/*
 * Copyright 2012 Luke Dashjr
 *
 * This program is free software; you can redistribute it and/or modify it
 * under the terms of the standard MIT license.  See COPYING for more details.
 */

#ifndef WIN32
#include <arpa/inet.h>
#else
#include <winsock2.h>
#endif

#include <stdbool.h>
#include <stdint.h>
#include <string.h>

#include <libbase58.h>

#include <blkmaker.h>

#include "private.h"

bool _blkmk_b58tobin(void *bin, size_t binsz, const char *b58, size_t b58sz) {
	return b58tobin(bin, &binsz, b58, b58sz);
}

int _blkmk_b58check(void *bin, size_t binsz, const char *base58str) {
	if (!b58_sha256_impl)
		b58_sha256_impl = blkmk_sha256_impl;
	return b58check(bin, binsz, base58str, 34);
}

size_t blkmk_address_to_script(void *out, size_t outsz, const char *addr) {
	unsigned char addrbin[25];
	unsigned char *cout = out;
	const size_t b58sz = strlen(addr);
	int addrver;
	size_t rv;
	
	rv = sizeof(addrbin);
	if (!b58_sha256_impl)
		b58_sha256_impl = blkmk_sha256_impl;
	if (!b58tobin(addrbin, &rv, addr, b58sz))
		return 0;
	addrver = b58check(addrbin, sizeof(addrbin), addr, b58sz);
	switch (addrver) {
		case   0:  // Bitcoin pubkey hash
		case 111:  // Testnet pubkey hash
			if (outsz < (rv = 25))
				return rv;
			cout[ 0] = 0x76;  // OP_DUP
			cout[ 1] = 0xa9;  // OP_HASH160
			cout[ 2] = 0x14;  // push 20 bytes
			memcpy(&cout[3], &addrbin[1], 20);
			cout[23] = 0x88;  // OP_EQUALVERIFY
			cout[24] = 0xac;  // OP_CHECKSIG
			return rv;
		case   5:  // Bitcoin script hash
		case 196:  // Testnet script hash
			if (outsz < (rv = 23))
				return rv;
			cout[ 0] = 0xa9;  // OP_HASH160
			cout[ 1] = 0x14;  // push 20 bytes
			memcpy(&cout[2], &addrbin[1], 20);
			cout[22] = 0x87;  // OP_EQUAL
			return rv;
		default:
			return 0;
	}
}ingerprint: `gpg --keyserver hkps://keys.openpgp.org --recv-keys "<fingerprint>"` Ensure that you put quotes around fingerprints containing spaces.
