# -*- coding: utf-8 -*-
#-------------------------------------------------------------------------#
#   Copyright (C) 2017 by Christoph Thelen                                #
#   doc_bacardi@users.sourceforge.net                                     #
#                                                                         #
#   This program is free software; you can redistribute it and/or modify  #
#   it under the terms of the GNU General Public License as published by  #
#   the Free Software Foundation; either version 2 of the License, or     #
#   (at your option) any later version.                                   #
#                                                                         #
#   This program is distributed in the hope that it will be useful,       #
#   but WITHOUT ANY WARRANTY; without even the implied warranty of        #
#   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         #
#   GNU General Public License for more details.                          #
#                                                                         #
#   You should have received a copy of the GNU General Public License     #
#   along with this program; if not, write to the                         #
#   Free Software Foundation, Inc.,                                       #
#   59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.             #
#-------------------------------------------------------------------------#


#----------------------------------------------------------------------------
#
# Set up the Muhkuh Build System.
#

SConscript('mbs/SConscript')
Import('atEnv')

import os.path
import tarfile


#----------------------------------------------------------------------------
#
# Depack the source archive.
#
tSrcArchive = tarfile.open('vstruct-2.0.1.tar.gz', 'r')
tSrcArchive.extractall('targets/depack')
tSrcArchive.close()
strDepackPath = 'targets/depack/vstruct-2.0.1/'

#----------------------------------------------------------------------------
#
# Build the artifacts.
#

strGroup = 'com.github.toxicfrog'
strModule = 'vstruct'

# Split the group by dots.
aGroup = strGroup.split('.')
# Build the path for all artifacts.
strModulePath = 'targets/jonchki/repository/%s/%s/%s' % ('/'.join(aGroup), strModule, PROJECT_VERSION)

strArtifact = 'vstruct'

tArcList = atEnv.DEFAULT.ArchiveList('zip')

tArcList.AddFiles('',
                  'installer/install.lua')

tArcList.AddFiles('lua/vstruct',
                  os.path.join(strDepackPath, 'api.lua'),
                  os.path.join(strDepackPath, 'ast.lua'),
                  os.path.join(strDepackPath, 'compat1x.lua'),
                  os.path.join(strDepackPath, 'cursor.lua'),
                  os.path.join(strDepackPath, 'init.lua'),
                  os.path.join(strDepackPath, 'io.lua'),
                  os.path.join(strDepackPath, 'lexer.lua'))
tArcList.AddFiles('lua/vstruct/ast',
                  os.path.join(strDepackPath, 'ast/Bitpack.lua'),
                  os.path.join(strDepackPath, 'ast/IO.lua'),
                  os.path.join(strDepackPath, 'ast/List.lua'),
                  os.path.join(strDepackPath, 'ast/Name.lua'),
                  os.path.join(strDepackPath, 'ast/Node.lua'),
                  os.path.join(strDepackPath, 'ast/Repeat.lua'),
                  os.path.join(strDepackPath, 'ast/Root.lua'),
                  os.path.join(strDepackPath, 'ast/Table.lua'))
tArcList.AddFiles('lua/vstruct/io',
                  os.path.join(strDepackPath, 'io/a.lua'),
                  os.path.join(strDepackPath, 'io/b.lua'),
                  os.path.join(strDepackPath, 'io/bigendian.lua'),
                  os.path.join(strDepackPath, 'io/c.lua'),
                  os.path.join(strDepackPath, 'io/defaults.lua'),
                  os.path.join(strDepackPath, 'io/endianness.lua'),
                  os.path.join(strDepackPath, 'io/f.lua'),
                  os.path.join(strDepackPath, 'io/hostendian.lua'),
                  os.path.join(strDepackPath, 'io/i.lua'),
                  os.path.join(strDepackPath, 'io/littleendian.lua'),
                  os.path.join(strDepackPath, 'io/m.lua'),
                  os.path.join(strDepackPath, 'io/p.lua'),
                  os.path.join(strDepackPath, 'io/s.lua'),
                  os.path.join(strDepackPath, 'io/seekb.lua'),
                  os.path.join(strDepackPath, 'io/seekf.lua'),
                  os.path.join(strDepackPath, 'io/seekto.lua'),
                  os.path.join(strDepackPath, 'io/u.lua'),
                  os.path.join(strDepackPath, 'io/x.lua'),
                  os.path.join(strDepackPath, 'io/z.lua'))

tArtifact = atEnv.DEFAULT.Archive(os.path.join(strModulePath, '%s-%s.zip' % (strArtifact, PROJECT_VERSION)), None, ARCHIVE_CONTENTS = tArcList)
tArtifactHash = atEnv.DEFAULT.Hash('%s.hash' % tArtifact[0].get_path(), tArtifact[0].get_path(), HASH_ALGORITHM='md5,sha1,sha224,sha256,sha384,sha512', HASH_TEMPLATE='${ID_UC}:${HASH}\n')
tConfiguration = atEnv.DEFAULT.Version(os.path.join(strModulePath, '%s-%s.xml' % (strArtifact, PROJECT_VERSION)), 'installer/%s.xml' % strModule)
tConfigurationHash = atEnv.DEFAULT.Hash('%s.hash' % tConfiguration[0].get_path(), tConfiguration[0].get_path(), HASH_ALGORITHM='md5,sha1,sha224,sha256,sha384,sha512', HASH_TEMPLATE='${ID_UC}:${HASH}\n')
tArtifactPom = atEnv.DEFAULT.ArtifactVersion(os.path.join(strModulePath, '%s-%s.pom' % (strArtifact, PROJECT_VERSION)), 'installer/pom.xml')
