# Created by: Wen Heping <wenheping@gmail.com>
# $FreeBSD: branches/2017Q2/sysutils/tmux/Makefile 434427 2017-02-20 02:57:04Z jbeich $

PORTNAME=	${TMUX_BASENAME}23
PORTVERSION=	${TMUX_VERSION}
PORTREVISION=	2
CATEGORIES=	sysutils
MASTER_SITES=	https://github.com/tmux/tmux/releases/download/${PORTVERSION}/
DISTNAME=       ${TMUX_DISTNAME}
DISTFILES=      ${TMUX_DISTNAME}.tar.gz

MAINTAINER=	mat@FreeBSD.org
COMMENT=	Terminal Multiplexer

LICENSE=	ISCL

CONFLICTS_INSTALL= tmux

TMUX_BASENAME=     tmux
TMUX_VERSION=      2.3
TMUX_DISTNAME=     ${TMUX_BASENAME}-${TMUX_VERSION}



LICENSE_FILE=	${WRKSRC}/COPYING

USES=		pkgconfig ncurses

USE_GITHUB=	nodefault
GH_TUPLE=	imomaliev:tmux-bash-completion:ef56d3e:bash

GNU_CONFIGURE=	yes
CONFIGURE_ARGS+=--sysconfdir=${PREFIX}/etc

PLIST_FILES=	bin/tmux \
		man/man1/tmux.1.gz \
		etc/bash_completion.d/tmux

PORTDOCS=	CHANGES FAQ README TODO
PORTEXAMPLES=	*

OPTIONS_DEFINE=	DOCS EXAMPLES LIBEVENT_STATIC BACKSPACE

LIBEVENT_STATIC_DESC=	Build with static libevent
BACKSPACE_DESC=	Build with tty/keys patch

BACKSPACE_EXTRA_PATCHES=	${PATCHDIR}/extra-patch-tty-keys.c

LIBEVENT_STATIC_LIB_DEPENDS_OFF=	libevent.so:devel/libevent
LIBEVENT_STATIC_BUILD_DEPENDS=	${LOCALBASE}/lib/libevent.a:devel/libevent
LIBEVENT_STATIC_VARS=	LESTATIC=${LOCALBASE}/lib/libevent.a

post-patch:
	@${REINPLACE_CMD} -e 's|/etc/tmux.conf|${PREFIX}/etc/tmux.conf|g' ${WRKSRC}/CHANGES \
		${WRKSRC}/tmux.h

post-configure-LIBEVENT_STATIC-on:
	${REINPLACE_CMD} -e '/LIBS/s|-levent[^[:blank:]]*|${LESTATIC}|' \
		${WRKSRC}/${MAKEFILE}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/tmux ${STAGEDIR}${PREFIX}/bin
	${INSTALL_MAN} ${WRKSRC}/tmux.1 ${STAGEDIR}${MANPREFIX}/man/man1
	@${MKDIR} ${STAGEDIR}${PREFIX}/etc/bash_completion.d
	${INSTALL_DATA} ${WRKSRC_bash}/completions/tmux ${STAGEDIR}${PREFIX}/etc/bash_completion.d/tmux

do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC} && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR})

do-install-EXAMPLES-on:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/example* ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
