#!@ENV@ make -f

#                     R E A L M S    O F    D E S P A I R  !
#   ___________________________________________________________________________
#  //            /                                                            \\
# [|_____________\   ********   *        *   ********   *        *   *******   |]
# [|   \\._.//   /  **********  **      **  **********  **      **  *********  |]
# [|   (0...0)   \  **********  ***    ***  **********  ***    ***  *********  |]
# [|    ).:.(    /  ***         ****  ****  ***    ***  ***    ***  ***        |]
# [|    {o o}    \  *********   **********  **********  ***    ***  *** ****   |]
# [|   / ' ' \   /   *********  *** ** ***  **********  ***    ***  ***  ****  |]
# [|-'- /   \ -`-\         ***  ***    ***  ***    ***  ***    ***  ***   ***  |]
# [|   .VxvxV.   /   *********  ***    ***  ***    ***  **********  *********  |]
# [|_____________\  **********  **      **  **      **  **********  *********  |]
# [|             /  *********   *        *  *        *   ********    *******   |]
#  \\____________\____________________________________________________________//
#     |                                                                     |
#     |    --{ [S]imulated [M]edieval [A]dventure Multi[U]ser [G]ame }--    |
#     |_____________________________________________________________________|
#     |                                                                     |
#     |                         -*- Makefile -*-                            |
#     |_____________________________________________________________________|
#    //                                                                     \\
#   [|  SMAUG 2.0 © 2014-2015 Antonio Cao (@burzumishi)                      |]
#   [|                                                                       |]
#   [|  AFKMud Copyright 1997-2007 by Roger Libiez (Samson),                 |]
#   [|  Levi Beckerson (Whir), Michael Ward (Tarl), Erik Wolfe (Dwip),       |]
#   [|  Cameron Carroll (Cam), Cyberfox, Karangi, Rathian, Raine,            |]
#   [|  Xorith, and Adjani.                                                  |]
#   [|  All Rights Reserved. External contributions from Remcon, Quixadhal,  |]
#   [|  Zarius and many others.                                              |]
#   [|                                                                       |]
#   [|  SMAUG 1.4 © 1994-1998 Thoric/Altrag/Blodkai/Narn/Haus/Scryn/Rennard  |]
#   [|  Swordbearer/Gorog/Grishnakh/Nivek/Tricops/Fireblade/Edmond/Conran    |]
#   [|                                                                       |]
#   [|  Merc 2.1 Diku Mud improvments © 1992-1993 Michael Chastain, Michael  |]
#   [|  Quan, and Mitchell Tse. Original Diku Mud © 1990-1991 by Sebastian   |]
#   [|  Hammer, Michael Seifert, Hans Henrik St{rfeldt, Tom Madsen, Katja    |]
#   [|  Nyboe. Win32 port Nick Gammon.                                       |]
#    \\_____________________________________________________________________//

CC = gcc
CPP = cpp
CXX = g++

ARCH = `uname -m`

localedir = $(datadir)/locale
DEFS = -DLOCALEDIR=\"$(localedir)\" @DEFS@

CLEANFILES = *~ *.o *.lo *.la *.a *.so smaug.h \
smaug$(EXEEXT) smaug-resolv$(EXEEXT) smaug-httpd$(EXEEXT) stamp-h1

# Build binaries #

# bin/smaug #
bin_PROGRAMS = smaug$(EXEEXT)

# bin/smaug-resolv #
if ENABLE_DNS_RESOLV
bin_PROGRAMS += smaug-resolv$(EXEEXT)
endif

# bin/smaug-httpd #
if HTTPD
bin_PROGRAMS += smaug-httpd$(EXEEXT)
endif

# Build Shared libraries #

# lib/libsmaug-*.la (static libs) #
noinst_LTLIBRARIES = \
libsmaug-act.la libsmaug-player.la libsmaug-mudprog.la \
libsmaug-info.la libsmaug-realm.la

# lib/libsmaug-httpd.la (static lib) #
if HTTPD
noinst_LTLIBRARIES += libsmaug-httpd.la
endif

# lib/libsmaug-dns.la (static lib) #
if ENABLE_DNS_RESOLV
noinst_LTLIBRARIES += libsmaug-dns.la
endif

# lib/libsmaug-olc.la (static lib) #
if ENABLE_OLC2
noinst_LTLIBRARIES += libsmaug-olc.la
endif

if ENABLE_OLC2
# libsmaug-olc #

libsmaug_olc_la_CXXFLAGS = -Wl,-rpath
libsmaug_olc_la_CFLAGS = -Wl,-rpath
libsmaug_olc_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_olc_la_SOURCES = \
ooedit.c oredit.c omedit.c
endif

if ENABLE_DNS_RESOLV
# libsmaug-dns #

libsmaug_dns_la_CXXFLAGS = -Wl,-rpath
libsmaug_dns_la_CFLAGS = -Wl,-rpath
libsmaug_dns_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_dns_la_SOURCES = dns.c
endif

# lib/libsmaug-act.so (shared lib) #
libsmaug_act_la_CXXFLAGS = -Wl,-rpath
libsmaug_act_la_CFLAGS = -Wl,-rpath
libsmaug_act_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_act_la_SOURCES = \
act_comm.c act_info.c act_move.c act_obj.c act_wiz.c fight.c misc.c 

# lib/libsmaug-player.so (shared lib) #
libsmaug_player_la_CXXFLAGS = -Wl,-rpath
libsmaug_player_la_CFLAGS = -Wl,-rpath
libsmaug_player_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_player_la_SOURCES = \
player.c polymorph.c update.c save.c ban.c

if ENABLE_ALIAS
libsmaug_player_la_SOURCES += alias.c
endif

# lib/libsmaug-mudprog.so (shared lib) #
libsmaug_mudprog_la_CXXFLAGS = -Wl,-rpath
libsmaug_mudprog_la_CFLAGS = -Wl,-rpath
libsmaug_mudprog_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_mudprog_la_SOURCES = \
mud_comm.c mud_prog.c

# lib/libsmaug-info.so (shared lib) #
libsmaug_info_la_CXXFLAGS = -Wl,-rpath
libsmaug_info_la_CFLAGS = -Wl,-rpath
libsmaug_info_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_info_la_SOURCES = \
boards.c comments.c hint.c news.c requests.c 

if ENABLE_MSSP
libsmaug_info_la_SOURCES += mssp.c
endif

# lib/libsmaug-realm.so (shared lib) #
libsmaug_realm_la_CXXFLAGS = -Wl,-rpath
libsmaug_realm_la_CFLAGS = -Wl,-rpath
libsmaug_realm_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_realm_la_SOURCES = \
adminlist.c build.c clans.c deity.c grub.c house.c \
ibuild.c liquids.c magic.c makeobjs.c mapout.c mpxset.c planes.c \
renumber.c reset.c shops.c skills.c special.c stances.c starmap.c \
stat_obj.c tables.c track.c variables.c

if ENABLE_COLOR
libsmaug_realm_la_SOURCES += color.c
else
libsmaug_realm_la_SOURCES += colorize.c
endif

if OVERLANDCODE
libsmaug_realm_la_SOURCES += overland.c
endif

if ENABLE_MAPPER
libsmaug_realm_la_SOURCES += mapper.c
endif

if ENABLE_TIMEZONE
libsmaug_realm_la_SOURCES += timezone.c
endif

if ENABLE_HOLIDAYS
libsmaug_realm_la_SOURCES += holidays.c
endif

if ENABLE_WEATHER
libsmaug_realm_la_SOURCES += weather.c
endif

if BANK_INSTALLED
libsmaug_realm_la_SOURCES += bank.c 
endif

if ENABLE_UNDERTAKER
libsmaug_realm_la_SOURCES += undertaker.c
endif

if ENABLE_ARCHERY
libsmaug_realm_la_SOURCES += archery.c
endif

if ENABLE_ARENA
libsmaug_realm_la_SOURCES += arena.c
endif

if ENABLE_QUEST
libsmaug_realm_la_SOURCES += quest.c
endif

if MARRIAGE
libsmaug_realm_la_SOURCES += marry.c
endif

if ENABLE_DICE
libsmaug_realm_la_SOURCES += dice.c
endif

# bin/smaug #

smaug_CXXFLAGS = -Wl,-rpath
smaug_CFLAGS = -Wl,-rpath
smaug_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

smaug_SOURCES = smaug.c \
i18n.c const.c db.c handler.c hashstr.c \
ident.c imm_host.c interp.c win32srv.c sha256.c

if ENABLE_HOTBOOT
smaug_SOURCES += hotboot.c
endif

smaug_LDADD = \
libsmaug-act.la libsmaug-player.la \
libsmaug-mudprog.la libsmaug-info.la libsmaug-realm.la

if ENABLE_DNS_RESOLV
smaug_LDADD += libsmaug-dns.la 
endif

if ENABLE_OLC2
smaug_LDADD += libsmaug-olc.la 
endif

if HTTPD
# libsmaug-httpd #

libsmaug_httpd_la_CXXFLAGS = -Wl,-rpath
libsmaug_httpd_la_CFLAGS = -Wl,-rpath
libsmaug_httpd_la_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

libsmaug_httpd_la_SOURCES = mongoose.c

# bin/smaug-httpd #

smaug_httpd_CXXFLAGS = -g -O0 -Wl,-rpath -I../.. -pthread -DMONGOOSE_ENABLE_THREADS -DNS_ENABLE_SSL -lssl
smaug_httpd_CFLAGS = -g -O0 -Wl,-rpath -I../.. -pthread -DMONGOOSE_ENABLE_THREADS -DNS_ENABLE_SSL -lssl
smaug_httpd_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

smaug_httpd_SOURCES = httpd.c

smaug_httpd_LDADD = libsmaug-httpd.la
endif

if ENABLE_DNS_RESOLV
# bin/smaug-resolv #

smaug_resolv_CXXFLAGS = -Wl,-rpath
smaug_resolv_CFLAGS = -Wl,-rpath
smaug_resolv_LDFLAGS = -Wl,-rpath $(LTLIBINTL)

smaug_resolv_SOURCES = resolv.c
endif

# Source Code Headers #

include_HEADERS = \
smaug.h mud.h bet.h hint.h i18n.h house.h \
liquids.h news.h sha256.h gettext.h 

if HTTPD
include_HEADERS += mongoose.h
endif

if ENABLE_HOTBOOT
include_HEADERS += hotboot.h
endif

if ENABLE_COLOR
include_HEADERS += color.h
endif

if ENABLE_MAPPER
include_HEADERS += mapper.h
endif

if ENABLE_MSSP
include_HEADERS += mssp.h
endif

if ENABLE_TIMEZONE
include_HEADERS += timezone.h
endif

if ENABLE_HOLIDAYS
include_HEADERS += holidays.h
endif

if ENABLE_QUEST
include_HEADERS += quest.h
endif

if ENABLE_WEATHER
include_HEADERS += weather.h
endif

if ENABLE_DNS_RESOLV
include_HEADERS += dns.h
endif

if ENABLE_OLC2
include_HEADERS += olc.h
endif

if OVERLANDCODE
include_HEADERS += overland.h
endif

if ENABLE_ALIAS
include_HEADERS += alias.h
endif
