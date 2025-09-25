# set the base image to create the image for react app
FROM node:20-alpine

# create a user with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root
# If the app is run as root, any vulnerability in the app can be exploited to gain access to the host system
# It's a good practice to run the app as a non-root user;
#       So, the whole line is a single instruction to Docker that says: 
#       "Create a new group called app, and if that works, create a new system user called app and add them to that group.(ore per aayathan preshnama aayath !)"
RUN addgroup app && adduser -S -G app app

# set the working directory to /app
WORKDIR /app

# change ownership of the working directory to app user
RUN chown -R app:app /app

# set the user to run the app
USER app

# copy package.json and package-lock.json to the working directory
COPY --chown=app:app package*.json ./

# install dependencies
RUN npm install

# expose port 5173 to tell Docker that the container listens on the specified network ports at runtime
EXPOSE 5173

# command to run the app with host flag for Docker networking
CMD ["npm", "run", "dev", "--", "--host"]