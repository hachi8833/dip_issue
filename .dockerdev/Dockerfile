ARG NODE_MAJOR
ARG HOST
ARG NUXT_HOST
# === Base image ===
FROM node:${NODE_MAJOR}-bullseye-slim as base

# Dependencies
COPY ./.dockerdev/Aptfile /tmp/Aptfile
RUN apt-get update -qq \
  && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    $(grep -Ev '^\s*#' /tmp/Aptfile | xargs) \
  && apt-get clean \
  && rm -rf /var/cache/apt/archives/* \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && truncate -s 0 /var/log/*log

RUN mkdir /app

WORKDIR /app
# ENV HOST 0.0.0.0
# EXPOSE 3000


# === Development image ===
FROM base as development
ENV NODE_ENV=development
# EXPOSE 9229
CMD ["/usr/bin/bash"]


# === Production image ===
FROM base as production
ENV NODE_ENV=production

RUN chown -R node:node /app
USER node

COPY --chown=node:node package.json yarn.lock ./
RUN yarn install

COPY --chown=node:node . .

CMD ["yarn", "start"]
