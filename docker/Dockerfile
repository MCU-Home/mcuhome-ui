# SPDX-FileCopyrightText: 2026 The MCUHome Contributors
# SPDX-License-Identifier: Apache-2.0
#
# The Home Assistant App image: nginx serving the front end's static
# distribution, and nothing else. There is no back end yet, so what this
# image shows is the front end running on its in-memory mock data.
#
# Nothing is built here. The distribution is produced outside Docker —
# `./gradlew :web:wasmJsBrowserDistribution` in `frontend/`, run locally
# or by the release workflow — and this file only copies the result, so
# the image needs no JDK, no Node and no toolchain of any kind. The
# consequence is that the build context must already contain a built
# `frontend/web/build/dist/wasmJs/productionExecutable/`; without it the
# COPY below fails.
#
# The context is the repository root, because the image needs two paths
# from it — the distribution and the server configuration beside this
# file. The repository with its build directories is several hundred
# megabytes, so `.dockerignore` excludes everything and adds those two
# paths back.
#
# Build from the repository root:
#   docker build -f docker/Dockerfile -t mcuhome-ui .

FROM nginx:1.30.4-alpine

# The port Home Assistant's ingress connects to (ingress_port in the app
# repository's config.yaml). Stated for readers; nginx listens because
# the configuration below says so, not because of this line.
EXPOSE 8099

COPY docker/default.conf /etc/nginx/conf.d/default.conf
COPY frontend/web/build/dist/wasmJs/productionExecutable/ /usr/share/nginx/html/
