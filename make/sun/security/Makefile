#
# Copyright (c) 1996, 2011, Oracle and/or its affiliates. All rights reserved.
# DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
#
# This code is free software; you can redistribute it and/or modify it
# under the terms of the GNU General Public License version 2 only, as
# published by the Free Software Foundation.  Oracle designates this
# particular file as subject to the "Classpath" exception as provided
# by Oracle in the LICENSE file that accompanied this code.
#
# This code is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
# FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
# version 2 for more details (a copy is included in the LICENSE file that
# accompanied this code).
#
# You should have received a copy of the GNU General Public License version
# 2 along with this work; if not, write to the Free Software Foundation,
# Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
#
# Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
# or visit www.oracle.com if you need additional information or have any
# questions.
#

#
# Build classes for security tools:
#
#		* keytool
#		* jarsigner
#		* policytool
#
# Also install wrappers for all of these.
#

BUILDDIR = ../..
include $(BUILDDIR)/common/Defs.gmk

# build sun/security/jgss/wrapper on non-windows platform
JGSS_WRAPPER =
ifneq ($(PLATFORM), windows)
    JGSS_WRAPPER = jgss/wrapper
endif

# Build PKCS#11 on all platforms except 64-bit Windows.
# We exclude windows-amd64 because we don't have any
# 64-bit PKCS#11 implementations to test with on that platform.
PKCS11 = pkcs11
ifeq ($(ARCH_DATA_MODEL), 64)
  ifeq ($(PLATFORM), windows)
    PKCS11 =
  endif
endif

# Build Microsoft CryptoAPI provider only on Windows platform.
MSCAPI =
ifeq ($(PLATFORM), windows)
  MSCAPI = mscapi
endif

# Build in-tree elliptic curve crypto provider only when
# DISABLE_INTREE_EC is not set
INTREE_EC = ec
ifdef DISABLE_INTREE_EC
  INTREE_EC =
endif

SUBDIRS       = $(INTREE_EC) other action util krb5
SUBDIRS_misc  = jgss $(PKCS11) $(JGSS_WRAPPER) $(MSCAPI) smartcardio
SUBDIRS_tools = tools
include $(BUILDDIR)/common/Subdirs.gmk

all build clean clobber::
	$(SUBDIRS-loop)

clean::
	$(RM) -r $(CLASSBINDIR)/sun/security
