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


# here is an example setting up a fictional package

assert env.get('CONDA',False), "not conda build"

pkg = "ndarray"
cdir = os.path.abspath(os.curdir)
reldir = os.path.split(cdir)[0]
extpkgs_dir = pjoin(reldir, 'extpkgs')
assert os.path.exists(extpkgs_dir), "No extpkgs dir in release."
srcpkgdir = pjoin(extpkgs_dir, pkg)
assert os.path.exists(srcpkgdir), \
    "The source package: %s for this proxy package is not in the release" % pkg
PREFIX = pjoin(cdir, env['SIT_ARCH'], 'include')
if not os.path.exists(PREFIX): os.mkdir(PREFIX)

build_cmds_and_error_messages = [
    ("DESTDIR=%s make" % PREFIX, "make failed"),
    ("DESTDIR=%s make install" % PREFIX, "make install failed")
]

os.chdir(srcpkgdir)
for cmd, err in build_cmds_and_error_messages:
    print cmd
    assert 0 == os.system(cmd), "%s: %s" % (msg, cmd)
os.chdir(cdir)

INCDIR = "ndarray"
DOCGEN = {'doxy-all': pjoin('arch', '$SIT_ARCH', 'geninc', pkg)}
DEPS = ['boost']
standardExternalPackage ( pkg, **locals() )
