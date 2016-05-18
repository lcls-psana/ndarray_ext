#------------------------------------------------------------------------
# File and Version Information:
#  $Id$
#
# Description:
#  SConscript file for package ndarray_ext
#------------------------------------------------------------------------

# Do not delete following line, it must be present in 
# SConscript file for any SIT project
Import('*')

import os
from os.path import join as pjoin
from SConsTools.buildExternalPackage import buildExternalPackage
from SConsTools.buildExternalPackage import prefixForBuildExternal
from SConsTools.standardExternalPackage import standardExternalPackage

#
# For the standard external packages which contain includes, libraries, 
# and applications it is usually sufficient to call standardExternalPackage()
# giving few keyword arguments. Here is a complete list of arguments:
#
#    PREFIX   - top directory of the external package
#    INCDIR   - include directory, absolute or relative to PREFIX
#    INCLUDES - include files to copy (space-separated list of patterns)
#    PYDIR    - Python src directory, absolute or relative to PREFIX
#    LINKPY   - Python files to link (patterns), or all files if not present
#    PYDIRSEP - if present and evaluates to True installs python code to a 
#               separate directory arch/$SIT_ARCH/python/<package>
#    LIBDIR   - libraries directory, absolute or relative to PREFIX
#    COPYLIBS - library names to copy
#    LINKLIBS - library names to link, or all libs if LINKLIBS and COPYLIBS are empty
#    BINDIR   - binaries directory, absolute or relative to PREFIX
#    LINKBINS - binary names to link, or all binaries if not present
#    PKGLIBS  - names of libraries that have to be linked for this package
#    DEPS     - names of other packages that we depend upon
#    PKGINFO  - package information, such as RPM package name

pkg = 'ndarray'
PREFIX = prefixForBuildExternal(pkg)

buildcmds = [ 
  "DESTDIR=%s make" % PREFIX,
  "DESTDIR=%s make install" % PREFIX
]

buildExternalPackage(pkg=pkg, buildcmds=buildcmds, PREFIX=PREFIX)

INCDIR = "ndarray"
DOCGEN = {'doxy-all': pjoin('arch', '$SIT_ARCH', 'geninc', pkg)}
DEPS = ['boost']
standardExternalPackage ( pkg, **locals() )
