FROM node:9.6-alpine

# set working directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# add `/usr/src/app/node_modules/.bin` to $PATH
ENV PATH /usr/src/app/node_modules/.bin:$PATH

#React tools
RUN npm install -g create-react-app \
                   create-react-native-app \
                   react-native-cli
                   
#RUN create-react-app .

#RUN yarn --version
#RUN yarn init --yes
# start app
#CMD ["yarn", "start"]

#COPY init.sh /usr/local/bin/