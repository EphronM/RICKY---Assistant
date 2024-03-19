
# RICKY Assistant


Introducing Ricky 🚀

Your personal assistant infused with the wit and wisdom of **Rick Sanchez** from the hit TV show Rick and Morty. Unlike typical AI bots, Ricky doesn't just provide answers—it embodies the unpredictable personality of Rick himself.

![Rick_Sanchez](https://github.com/EphronM/RICKY---Assistant/assets/94764266/e4d7dabc-f6a0-4c21-af18-44d15bd919d2)


With its ability to break the fourth wall and deliver sarcastic humour, Ricky brings a unique charm to your interactions. Whether you're seeking philosophical insights or simply looking for a laugh, Ricky is your go-to companion for interdimensional adventures.

Experience the genius of Rick Sanchez in a whole new way with Ricky — your ultimate interdimensional companion. 🌌

# Technical details
###  Technology Stack:


* Ricky is powered by Mistral 7B Instruct v0.2, utilizing LLM (Large Language Model) capabilities.
* Utilizes a RAG (Retriever-Reader-Generator) based approach to understand user queries and respond in a sarcastic manner.
* The chat agent is converted into a user-friendly UI using Gradio.


### Customization:

* Ricky's functionality can be easily customized for other characters or personas by modifying the information data while reusing existing code.
### Deployment:

* Deployed using best MLOps practices, ensuring reliability and scalability.
* Hosted on AWS EC2 instances, specifically using a t2.micro instance.
* Packaged as a Docker image for efficient deployment and management.
* Automated deployment pipeline set up using GitHub Actions for seamless integration and continuous delivery.

### Production Deployment:
* Detailed information on how the deployment pipeline is structured and executed is provided in the "PRODUCTION DEPLOYMENT" section of the README.


Source model (LLM)           |  Customization
:-------------------------:|:-------------------------:
![A_Mistral_AI_logo](https://github.com/EphronM/RICKY---Assistant/assets/94764266/8ab65aac-6236-4cc2-bd8b-681eaef4ed16)  |  ![pngegg](https://github.com/EphronM/RICKY---Assistant/assets/94764266/4e2b7e07-cc43-4fe2-a4df-67f0c3a8d954)



# Now lets talk to Ricky Locally



#### Mode 1: 
Using a Local LLM Instance for Question Answering
* **Download Required Models**: The application utilizes a Mistral 7B Instruct from Hugging Face for inference. All related source code can be found in src/local_llm/.

* **Set Up Environment**: Ensure you have a GPU with 16GB VRAM. If so, proceed to login to COMET-ML, create a project, and obtain an API key for logging prompts and responses.

* **Configure Environment Variables**: Set the following environment variables:
```
COMET_WORKSPACE: < Your COMET username > 
COMET_PROJECT_NAME: < Name of your COMET project >
COMET_API_KEY: < API key obtained from COMET-ML >

```
* **Install Dependencies**: Run pip install -r src/local_llm/requirements.txt to install necessary requirements, preferably in a new virtual environment to avoid conflicts.

* **Run the Application**: Execute ./run_local_llm_app.sh to start the application. It will build a pipeline using Langchain to convert user queries into prompts, infer responses using the Mistral LLM, and stream them in real-time. The prompts and responses are logged onto the COMET-ML dashboard for tracking.

#### Mode 2: 

Using Mistral API for Question Answering
* Accessing Mistral API: The application employs Mistral API services for question answering. All relevant source code is available in src/llm_api/.

* **Prepare Environment**: Login to COMET-ML, create a project, and obtain an API key for logging. Additionally, log in to the Mistral.ai console and create an API key. Note that you will be charged based on API usage; however, the pricing with the open-sourced Instruct 7B version is relatively low ($0.25 / 1 Million tokens).

* **Set Up Environment Variables**: Set the following environment variables:
```
MISTRAL_API_KEY: < API key obtained from Mistral.ai >
COMET_WORKSPACE, COMET_PROJECT_NAME, COMET_API_KEY: < COMET-ML credentials for logging prompts and responses >
```
* **Install Dependencies**: Run pip install -r src/llm_api/requirements.txt to install necessary requirements, preferably in a new virtual environment to avoid conflicts.

* **Launch the Application**: Execute ./run_llm_api_app.sh to run the application. It will convert user queries into prompts, infer responses using the Mistral API, and stream them in real-time to the front-end UI built with Gradio.

# Production Deployment
For production deployment, Mistral API is utilized for question answering, as it doesn't require a device with 16GB GPU RAM like the other mode.

### Workflow
* **GitHub Actions**: The entire deployment workflow is defined in .github/workflows/cd_llm_api_app.yaml. It's triggered automatically upon a push to the deploy branch.

* **Environment Variables**: Necessary environment variables such as Mistral API key, COMET ML logger, and AWS credentials are securely set in GitHub Action secrets. These variables are utilized by the GitHub runner during deployment.

### Deployment Process
* **Code Validation**: Upon a push to the deploy branch, the runner checks the code.

* **Docker Image Build**: The runner builds the Docker image.

* **AWS Authentication**: Using the keys provided in secrets, the runner logs onto AWS.

* **ECR Push**: The built Docker image is pushed to AWS Elastic Container Registry (ECR).

* **EC2 Deployment**: A second job is triggered inside an EC2 instance. It pulls the latest Docker image from ECR and starts the container.




# Acknowledgements
* Special thanks to the creators of Rick and Morty for inspiring this project.
* Thanks to the open-source community for their contributions and support.


Fin.

Let's hope ricky doesn't team up with Morty to escape from my digital prison 

![wallpaperflare com_wallpaper](https://github.com/EphronM/RICKY---Assistant/assets/94764266/9b48303b-d144-4a13-a9ad-525ac4c8f623)
