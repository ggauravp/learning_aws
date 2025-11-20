# Trigger the lamda function to add data uploaded in s3 directly into postgres database  
1. first create a bucket 
2. create a lamda function
3. Add a trigger to lamda, which can be done from both lamda or s3.

- Above mentioned 3 steps are the basic step for triggering lamda through s3 
- But to place the data uploaded in s3 directly into postgres we need to use  **psycopg2 library**
- And to use psycopg library we need to add layer to lamda.
- A layer is basically a way to package common libraries or dependencies separately from your      Lambda function code. Not every Lambda needs a layer. The Lambda Python runtime doesn’t include psycopg2 by default. So we need to create a layer containing psycopg2 and attach it to the Lambda.

4. create a layer and add it to lamda.

- while creating a lyer we need to create a zip file of the psycopg2 library and attach it to the layer. 
1. Set Up Your Environment 
First, create a new directory for your layer: [inside-WSL]
`mkdir -p psycopg2-layer/python`
`cd psycopg2-layer/python`

2. Install Psycopg2-Binary
- for x86_64:
`pip3 install --platform manylinux2014_x86_64 --target . --python-version 3.12 --only-binary=:all: psycopg2-binary`
- for arm64:
`pip3 install --platform manylinux2014_aarch64 --target . --python-version 3.12 --only-binary=:all: psycopg2-binary`
- change the python-version accordingly

4. Package the Layer
`cd ..`
`zip -r psycopg2-layer.zip python`

5. copy the zip file to desktop
`cp ~/psycopg2-layer/psycopg2-layer.zip /mnt/c/Users/Gaurav/Desktop/`

# CREATING A LAYER 
- Open the AWS Lambda console
- Navigate to “Layers” in the left sidebar
- Click “Create layer”
- Provide a name for your layer (e.g., “psycopg2-layer”)
- Upload the zip file you created
- Select the compatible runtimes (Python 3.12 in this case)
- Choose the appropriate architecture (x86_64 or arm64)
- Click “Create” to finalize the layer

# Use the Layer in Your Lambda Function
- Open your Lambda function in the AWS console
- Scroll down to the “Layers” section
- Click “Add a layer”
- Choose “Custom layers” or copy the arn of the layer and select through it.
- Select the psycopg2 layer you just created
- Click “Add”
