# $FreeBSD$

PORTNAME=	readonlyrest
PORTVERSION=	1.14.1
CATEGORIES=	textproc
PKGNAMEPREFIX=	elasticsearch-plugin-

MAINTAINER=	xavi.garcia@gmail.com
COMMENT=	ElasticSearch ReadonlyREST Plugin

LICENSE=	GPLv3

USE_GITHUB=	yes
GH_ACCOUNT=	xgarcias
GH_PROJECT=	elasticsearch-plugin-readonlyrest
ES_VERSION=	5.3.0
GH_TAGNAME=	${PORTVERSION}

NO_BUILD=	yes

UNZIP_CMD=	/usr/bin/unzip

do-install:
	@${MKDIR} ${STAGEDIR}${PREFIX}/lib/elasticsearch/plugins/readonlyrest
	@${UNZIP_CMD} -j -o -d  ${STAGEDIR}${PREFIX}/lib/elasticsearch/plugins/readonlyrest ${WRKSRC}/readonlyrest-${PORTVERSION}_es${ES_VERSION}.zip

.include <bsd.port.mk>
