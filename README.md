# Individual Project 1
# Continuous Delivery of Flask Application on GCP

Goals
- Create a Google App Engine app using GCP Cloud Shell environment
- Push source code to Github
- Configure Cloud Build to Deploy Changes on build

# 1.	Create Github repo

![Image](../master/images/1.gif?raw=true) 

# 2.	Create project in GCP
![Image](../master/images/2.gif?raw=true) 
 
# 3.	Activate cloud-shell and add ssh-keys.  	
```
ssh-keygen -t rsa 
```
Upload key to Github ssh settings.

![Image](../master/images/3.gif?raw=true) 
![Image](../master/images/4.gif?raw=true) 
 
# 4.	Create initial project scaffold using the launch editor.
```
•	Makefile: touch Makefile
•	requirements.txt: touch requirements.txt
•	app.py: touch app.yaml
•	main.py: touch main.py
```
![Image](../master/images/5.gif?raw=true) 
 
# 5.	Create and source the virtual environment
```
virtualenv --python $(which python) venv
source venv/bin/activate
```
# 6.	Install packages
```
make install
```

# 7.	Verify project is working
```
gcloud projects describe $GOOGLE_CLOUD_PROJECT
```
![Image](../master/images/6.gif?raw=true)  

# 8.	Create app engine
```
gcloud app create 
```
this will ask for the region. Go ahead and pick your region


# 9.	Run flask locally
```
python main.py
```
![Image](../master/images/7.gif?raw=true)  


# 10.	Web preview

![Image](../master/images/8.gif?raw=true) 

# 11.	Update main.py
```
from flask import Flask
from flask import jsonify


app = Flask(__name__)

@app.route('/')
def hello():
    """Return a friendly HTTP greeting."""
    return 'Hello I like to make AI Apps'

@app.route('/name/<value>')
def name(value):
    val = {"value": value}
    return jsonify(val)

if __name__ == '__main__':
    app.run(host='127.0.0.1', port=8080, debug=True)
```

![Image](../master/images/9.gif?raw=true)  

# 12.	Test out passing in parameters to exercise this function:
```
@app.route('/name/<value>')
def name(value):
    val = {"value": value}
    return jsonify(val)
```

![Image](../master/images/10.gif?raw=true) 

# 13.	Now we can deploy the app
```
gcloud app deploy
```
![Image](../master/images/11.gif?raw=true)  

# 14.	Now we can stream the log files
```
gcloud app logs tail -s default
```


# 15.	Now we can view the public url and make changes publically available.

![Image](../master/images/12.gif?raw=true) 
 
# 16.	Setup continuous deployment – make changes rapidly and deploy changes to production

- Enable APIs
- Grant App Engine access to Cloud service

![Image](../master/images/13.gif?raw=true) 
![Image](../master/images/14.gif?raw=true) 
  

# 17.	Create cloudbuild.yaml file
- Add some commands using a prior project

![Image](../master/images/15.gif?raw=true)  

# 18.	Add and commit to my Github repo
```
git status
git commit –m “adding project”
git config –-global user.email “epark21@uncc.edu”
git config –-global user.name “epark21”
git push
```

# 19.	Enable build trigger.  Select your source – Github and select our project.

![Image](../master/images/16.gif?raw=true) 
 
We can see that this is being auto-triggered 

![Image](../master/images/17.gif?raw=true) 
 
We can also take a look at the Output

![Image](../master/images/18.gif?raw=true) 
 
Now we can test out the target URL.

![Image](../master/images/19.gif?raw=true) 
 
# Yes it has been deployed successfully and we are able to deploy changes on the build.

