FROM node:18-alpine

ARG NODE_ENV=production
ARG user=node
ARG project_dir=/opt/node_app
ENV NODE_ENV $NODE_ENV

ARG PORT=5173
ENV PORT $PORT
EXPOSE $PORT

RUN corepack enable

# prepare working dir
RUN mkdir $project_dir && chown $user:$user $project_dir

USER $user

WORKDIR $project_dir

COPY --chown=$user .yarn .yarn
COPY --chown=$user .yarnrc.yml  .
COPY --chown=$user yarn.lock* .

COPY front/package.json .

RUN yarn install --immutable

# COPY --chown=$user app app

CMD ["yarn", "dev"]
