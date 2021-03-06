# InterviewScheduler
This project consists in a interview calendar API.
Its purpose is to specify time slots available for candidates and interviewers in order to
get matches between them.
![Figure 1](https://github.com/bioslikk/InterviewScheduler/blob/master/service_ui.png?raw=true)

## Project Structure
```
InterviewScheduler/
    interview_scheduler_service/- Package containing all the code necessary to run the python application (application.py)
        business/               - Business logic code here 
            controllers/        - Since this application is a REST service, every endpoint is mapped to a function in this dir
            utils/              - Collection of functions used by diferent controllers and functions
        crud/                   - Has all the functions needed to access the mongo database
    test/                       - Has unit tests. Run them using *pytest*
    application.py              - Entrypoint for the application
    docker-compose.yaml         - Docker-compose file that runs the back-end and mongo-database
    Dockerfile                  - Dockerfile used to create an image used in the docker-compose.yaml
    init_mongo.py               - Populates the database with sample data
    README.md                   - This is the document you are reading
    requirements.txt            - File that specifies dependencies to be installed using pip
    swagger.yaml                - Document that specifies the REST interface following the openApi 2.0 specification standards
```

To analyse the code, I suggest going to `localhost:4001/v1/ui` to see all the endpoints
 and then going to the `interview_scheduler/business/controllers/` directory to see each endpoint function.
## Run this project
### Using docker-compose
```bash
# Runs the interview scheduler service and the mongo database 
docker-compose up -d
# Populates the database with users and interview slots described in the "Populate database" section
./init_database.sh
```
You can now go to `localhost:4001/v1/ui` to experiment with the endpoints.
### Do it yourself
You can also run this service without docker
#### Interview Scheduler Service
To install the dependencies you could activate a `virtualenv` and do
```bash
pip install -r requirements.txt
```
To run the service in dev mode you can do
```bash
python application.py
```
or using a WSGI
```bash
uwsgi --http :4001 -w application:application -p 16
```

#### Mongo database
You could run a mongo database by doing
```bash
docker run --name some-mongo --net=host -d mongo
```
If you don't, you need to have the mongoDB running in your machine and available on port 27017
## Populate database
After running the application, you could add a few users with many random overlapping time slots 
to observe its behaviour.

If you ran the project using docker-compose, do:
```bash
./init_database.sh
```
else
```bash
python init_mongo.py
```
You can now go to the `/slots/matches` endpoint and see the matches between these candidates and interviewers,
or you could use the API to create more accounts, authenticate and create more interview slots.


 
