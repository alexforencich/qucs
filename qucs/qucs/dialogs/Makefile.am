## Process this file with automake to produce Makefile.in
# 
# qucs/dialogs/Makefile.am
#
# Automake input file.
#
# Copyright (C) 2004, 2006, 2009 Stefan Jahn <stefan@lkcc.org>
#
# This is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2, or (at your option)
# any later version.
# 
# This software is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this package; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street - Fifth Floor,
# Boston, MA 02110-1301, USA.  
#

noinst_LIBRARIES = libdialogs.a

MOCHEADERS = settingsdialog.h simmessage.h qucssettingsdialog.h      \
     labeldialog.h changedialog.h matchdialog.h digisettingsdialog.h \
     sweepdialog.h searchdialog.h librarydialog.h importdialog.h     \
     packagedialog.h savedialog.h vasettingsdialog.h                 \
     vtabbutton.h vtabbar.h vtabwidget.h vtabbeddockwidget.h

MOCFILES = $(MOCHEADERS:.h=.moc.cpp)

libdialogs_a_SOURCES = settingsdialog.cpp newprojdialog.cpp \
     simmessage.cpp qucssettingsdialog.cpp labeldialog.cpp changedialog.cpp \
     matchdialog.cpp sweepdialog.cpp digisettingsdialog.cpp searchdialog.cpp \
     librarydialog.cpp importdialog.cpp packagedialog.cpp \
     savedialog.cpp vasettingsdialog.cpp \
     vtabbutton.cpp vtabbar.cpp vtabwidget.cpp vtabbeddockwidget.cpp

nodist_libdialogs_a_SOURCES = $(MOCFILES)

noinst_HEADERS = newprojdialog.h vtabglobal.h $(MOCHEADERS)

AM_CPPFLAGS = $(X11_INCLUDES) $(QT_INCLUDES) -I$(top_srcdir)/qucs

SUFFIXES = .moc.cpp

.h.moc.cpp:
	$(MOC) -o $@ $<

CLEANFILES = *~
MAINTAINERCLEANFILES = Makefile.in *.moc.cpp
DISTCLEANFILES = *.moc.cpp
