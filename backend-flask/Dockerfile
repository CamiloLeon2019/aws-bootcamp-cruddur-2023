FROM python:3.10-slim-buster

# Inside container
# Make a new folder inside the container
WORKDIR /backend-flask

# Outside container -> Inside container
# This contains the python libraries we require to run the app
COPY requirements.txt requirements.txt

# Copy the script into the container
COPY script-flask.sh /

#Inside Container
#This actually installs the libraries used for the app
RUN pip3 install -r requirements.txt

# Make the script executable
RUN chmod +x /script-flask.sh

# Outside container -> Inside Container
# . means everything on the current directory 
# first . /backend-flask outside the container
# second . /backend-flask inside the container
COPY . .

# Set Environment Variables (Env Vars)
# Inside Container  will set the variable on the container once is run 
ENV FLASK_ENV=development

EXPOSE ${PORT}

# Command used to run flask
CMD [ "/script-flask.sh"]