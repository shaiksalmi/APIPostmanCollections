

# Use the official Node.js 20 image as the base image

FROM node:20

# Set the working directory in the container(linux)

WORKDIR /app

# Install Newman globally

RUN npm install -g newman

#Install Newman html report

RUN npm install -g newman-reporter-html

#Install Newman Reporter HTMLExtra

RUN npm install -g newman-reporter-htmlextra

# Copy your Postman collection and environment files to the working directory

COPY DataDrivenAPIs.json .

COPY GoRestEnv.json .

COPY myuser.csv .

# Set the command to run Newman and execute your Postman collection

CMD ["newman", "run", "DataDrivenAPIs.json", "-e", "GoRestEnv.json", "d", "myuser.csv", "-r", "cli,json,html,htmlextra"]

