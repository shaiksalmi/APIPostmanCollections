

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

#Ensure the results directory exists
RUN mkdir -p /app/results

# Copy your Postman collection and environment files to the working directory

COPY GoRestAPIWorkflowColl.json /app/
COPY GoRestEnv.json /app/


# Set the command to run Newman and execute your Postman collection

CMD ["newman", "run", "/app/GoRestAPIWorkflowColl.json", "-e", "/app/GoRestEnv.json", "-r", "cli,json,html,htmlextra", "--reporter-htmlextra-export", "/app/results/myrest.html"]

