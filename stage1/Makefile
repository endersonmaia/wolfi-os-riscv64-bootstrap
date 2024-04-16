ARCH ?= riscv64
MELANGE ?= $(shell which melange)
KEY ?= local-melange.rsa

MELANGE_OPTS ?= \
	--keyring-append ${KEY}.pub \
	--signing-key ${KEY} \
	--arch ${ARCH}

PACKAGES = \
	packages/${ARCH}/debian-stage1-${BINUTILS_VERSION}.apk

all: download ${KEY} ${PACKAGES}

packages/${ARCH}/debian-stage1-${BINUTILS_VERSION}.apk:
	${MELANGE} build debian-stage1.yaml ${MELANGE_OPTS}

${KEY}:
	${MELANGE} keygen ${KEY}

download:
	wget -q -nc -i debian-stage1/packages.list -P debian-stage1/
