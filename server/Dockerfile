FROM node:18-alpine

ARG NODE_ENV=production
ARG user=node
ARG project_dir=/opt/node_app
ENV NODE_ENV $NODE_ENV

ARG PORT=3000
ENV PORT $PORT
EXPOSE $PORT 3000

RUN corepack enable

# prepare working dir
RUN mkdir $project_dir && chown $user:$user $project_dir
WORKDIR /opt/node_app

USER $user

WORKDIR $project_dir

COPY --chown=$user .yarn .yarn
COPY --chown=$user .yarnrc.yml .
COPY --chown=$user yarn.lock* .

COPY server/package.json .

# RUN yarn install
RUN yarn install --immutable

WORKDIR $project_dir/app

# COPY server .
# COPY app/src/locales ./src/locales

CMD ["node", "-r", "dotenv/config", "-r", "./src/tracing.js", "./src/index.js"]
