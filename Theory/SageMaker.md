## AWS - SageMaker
ML infrastructure as a service.
SageMaker is a fully managed service that enables data scientists and ML engineers to build, train, deploy, and monitor machine learning models at scale without managing infrastructure.

#### problem it solves
Without SageMaker, you must:
- Provision EC2s / GPUs
- Install CUDA, drivers
- Handle distributed training
- Build custom inference servers
- Scale endpoints
- Monitor drift and latency
SageMaker abstracts all of that.

#### Training Jobs
What a training job is: A managed ML training run that:
- Spins up compute (CPU/GPU)
- Trains your model
- Saves model artifacts to S3
- Terminates infrastructure automatically

Inputs:
- Training code (script or container)
- Training data (from S3)
- Instance type (CPU/GPU)
- Hyperparameters

Outputs:
- Model artifacts (model.tar.gz) in S3
- Logs in CloudWatch

#### Processing jobs (data prep before ML)
What they are: Serverless jobs used for:
- Data cleaning
- Feature engineering
- Validation
- Train/test split
SageMaker Processing is used for data preprocessing and feature generation before training.

#### Model Artifacts
After training SageMaker produces output file like model.tar.gz
This contains:
- model weights
- serialized model
- inference code (sometimes)
which is stored in S3 (not SageMaker)

#### Endpoints (Inference & Deployment)
What is an endpoint? A fully managed, real-time inference service.

- Auto-scales
- Exposes HTTPS endpoint
- Supports A/B testing
- Supports rolling updates

Typical flow:
Client → SageMaker Endpoint → Model → Prediction

Built-in algorithms: XGBoost, Linear, K-means

#### Questions
Q1: SageMaker vs EC2 for ML?
EC2 gives control but requires setup. SageMaker abstracts infrastructure, scaling, and deployment, making it faster and safer for production ML.

Q2: SageMaker vs ECS for inference?
SageMaker endpoints are optimized for ML inference, while ECS gives more flexibility and cost control for custom inference services.

Q3: Does SageMaker store data?
No. Data and models are stored in S3. SageMaker manages compute.

Q4: When would you NOT use SageMaker?
For very simple models or lightweight inference where Lambda or ECS is cheaper.

SageMaker in ONE MINUTE 
Store raw data in S3, preprocess it using Glue or SageMaker Processing jobs, train models using SageMaker training jobs, and store the model artifacts back in S3. For deployment, Either use SageMaker endpoints for real-time inference or Batch Transform for offline predictions. SageMaker handles infrastructure, scaling, and monitoring, allowing to focus on model performance.