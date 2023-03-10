#[===[ * libpng version 1.6.21, January 15, 2016
 *
 * Copyright (c) 1998-2002,2004,2006-2016 Glenn Randers-Pehrson
 * (Version 0.96 Copyright (c) 1996, 1997 Andreas Dilger)
 * (Version 0.88 Copyright (c) 1995, 1996 Guy Eric Schalnat, Group 42, Inc.)
 *
 * This code is released under the libpng license (See LICENSE, below)
 *
 * Authors and maintainers:
 *   libpng versions 0.71, May 1995, through 0.88, January 1996: Guy Schalnat
 *   libpng versions 0.89, June 1996, through 0.96, May 1997: Andreas Dilger
 *   libpng versions 0.97, January 1998, through 1.6.21, January 15, 2016:
 *     Glenn Randers-Pehrson.
 *   See also "Contributing Authors", below. 
 *
 * COPYRIGHT NOTICE, DISCLAIMER, and LICENSE:
 *
 * If you modify libpng you may insert additional notices immediately following
 * this sentence.
 *
 * This code is released under the libpng license.
 *
 * libpng versions 1.0.7, July 1, 2000, through 1.6.21, January 15, 2016, are
 * Copyright (c) 2000-2002, 2004, 2006-2016 Glenn Randers-Pehrson, are
 * derived from libpng-1.0.6, and are distributed according to the same
 * disclaimer and license as libpng-1.0.6 with the following individuals
 * added to the list of Contributing Authors:
 *
 *    Simon-Pierre Cadieux
 *    Eric S. Raymond
 *    Mans Rullgard
 *    Cosmin Truta
 *    Gilles Vollant
 *    James Yu
 *
 * and with the following additions to the disclaimer:
 *
 *    There is no warranty against interference with your enjoyment of the
 *    library or against infringement.  There is no warranty that our
 *    efforts or the library will fulfill any of your particular purposes
 *    or needs.  This library is provided with all faults, and the entire
 *    risk of satisfactory quality, performance, accuracy, and effort is with
 *    the user.
 *
 * libpng versions 0.97, January 1998, through 1.0.6, March 20, 2000, are
 * Copyright (c) 1998-2000 Glenn Randers-Pehrson, are derived from
 * libpng-0.96, and are distributed according to the same disclaimer and
 * license as libpng-0.96, with the following individuals added to the list
 * of Contributing Authors:
 *
 *    Tom Lane
 *    Glenn Randers-Pehrson
 *    Willem van Schaik
 *
 * libpng versions 0.89, June 1996, through 0.96, May 1997, are
 * Copyright (c) 1996-1997 Andreas Dilger, are derived from libpng-0.88,
 * and are distributed according to the same disclaimer and license as
 * libpng-0.88, with the following individuals added to the list of
 * Contributing Authors:
 *
 *    John Bowler
 *    Kevin Bracey
 *    Sam Bushell
 *    Magnus Holmgren
 *    Greg Roelofs
 *    Tom Tanner
 *
 * libpng versions 0.5, May 1995, through 0.88, January 1996, are
 * Copyright (c) 1995-1996 Guy Eric Schalnat, Group 42, Inc.
 *
 * For the purposes of this copyright and license, "Contributing Authors"
 * is defined as the following set of individuals:
 *
 *    Andreas Dilger
 *    Dave Martindale
 *    Guy Eric Schalnat
 *    Paul Schmidt
 *    Tim Wegner
 *
 * The PNG Reference Library is supplied "AS IS".  The Contributing Authors
 * and Group 42, Inc. disclaim all warranties, expressed or implied,
 * including, without limitation, the warranties of merchantability and of
 * fitness for any purpose.  The Contributing Authors and Group 42, Inc.
 * assume no liability for direct, indirect, incidental, special, exemplary,
 * or consequential damages, which may result from the use of the PNG
 * Reference Library, even if advised of the possibility of such damage.
 *
 * Permission is hereby granted to use, copy, modify, and distribute this
 * source code, or portions hereof, for any purpose, without fee, subject
 * to the following restrictions:
 *
 *   1. The origin of this source code must not be misrepresented.
 *
 *   2. Altered versions must be plainly marked as such and must not
 *      be misrepresented as being the original source.
 *
 *   3. This Copyright notice may not be removed or altered from any
 *      source or altered source distribution.
 *
 * The Contributing Authors and Group 42, Inc. specifically permit, without
 * fee, and encourage the use of this source code as a component to
 * supporting the PNG file format in commercial products.  If you use this
 * source code in a product, acknowledgment is not required but would be
 * appreciated.
 *
 * END OF COPYRIGHT NOTICE, DISCLAIMER, and LICENSE.
 ]===]

cmake_minimum_required (VERSION 3.0.0)
# name of the library
project(LibPng)
 

find_package(ZLIB REQUIRED)
include_directories(${ZLIB_INCLUDE_DIR})

set(SOURCES
    png.c
     pngerror.c
     pngget.c
     pngmem.c
     pngpread.c
     pngread.c
     pngrio.c
     pngtrans.c
     pngrutil.c
     pngset.c
     pngrtran.c
     pngwio.c
     pngwrite.c
     pngwtran.c
     pngwutil.c
     pngdebug.h
     pnginfo.h
     pngpriv.h
     pngstruct.h
    )
 
set(PUBLICHEADERS
        png.h
        pngconf.h
        pnglibconf.h
	    )
        

# if static library
add_library(LibPng STATIC ${SOURCES} ${PUBLICHEADERS})
 
# we need consistent naming windows and unix
set_target_properties(LibPng PROPERTIES PREFIX "")
 
set_target_properties(LibPng PROPERTIES OUTPUT_NAME "libpng")


# import for static library
set_property(TARGET LibPng PROPERTY POSITION_INDEPENDENT_CODE ON)
 
# wo definded PROJECT_VERSION, cMake would not work
set(PROJECT_VERSION "1.0")

set_target_properties(LibPng PROPERTIES
    VERSION ${PROJECT_VERSION}
    PUBLIC_HEADER ${PUBLICHEADERS})


# specify content of install directory
install(TARGETS LibPng DESTINATION lib)
install(FILES ${PUBLICHEADERS} DESTINATION include)