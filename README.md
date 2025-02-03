# LabelStudioDataAnnotator

A wrapper around the [Label Studio](https://labelstud.io/) data annotation tool, including the labeling UI and an ML backend. The backend model provides predictions that the user can either accept or modify to streamline the annotation process. This tool runs both services in a Docker container with images **labelstudio** and **ml-backend**. 

## Startup:

1. Install ```Docker Desktop``` for [Mac](https://docs.docker.com/desktop/setup/install/mac-install/), [Windows](https://docs.docker.com/desktop/setup/install/windows-install/), or [Linux](https://docs.docker.com/desktop/setup/install/linux/).

2. Clone this repository: ```git clone https://github.com/yourusername/LabelStudioDataAnnotator.git```.

3. ```cd REPOSITORY_PATH/LabelStudioDataAnnotator```.

4. If you want to add your own model to the ML backend, see **Updating backend model** below.

5. Start the Docker container: ```docker-compose up --build```. This will serve the Label Studio UI on local port 8080 and the ML backend on local port 9090.

6. Navigate to (http://localhost:8080) and sign up for an account.

7. Create a project: click the blue ```Create``` button in the top left. Specify a name, import data via upload, and select the desired ```Labeling Setup```.

    a. This repository is configured for the ```Named Entity Recognition``` labeling task. Add labels ```DEPARTMENT``` and ```INSITUTION``` and delete the preset labels. 

8. Connect the ML backend: click on the tile for your project and navigate to ```Settings -> Model -> Connect Model```. Give the model a name and enter the backend URL (http://host.docker.internal:9090). No authentication is necessary.

9. Begin labeling: click on the project name in the top sidebar or the tile from the ```Projects``` view and then click ```Label All Tasks```. After labeling, export the annotations by clicking ```Export``` from the project menu. 

## Updating backend model

This repository comes with a Named Entity Recognition (NER) model in the ML backend by default. If you wish to change the model for a different annotation task, at minimum you must:

1. Update the ```setup()``` and ```predict()``` methods of the ```NewModel``` class in ```model.py``` to initialize and run inference with your desired model. Include any model dependencies in ```requirements.txt```.