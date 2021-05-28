
We saw in the previous challenge how to plug a website to our **Prediction API** in order to allow regular users make prediction.

Now let's create our own website ! 🔥

We are going to use **Streamlit** which will allow us to create a website very easily and without any web development skills.

## First, let's create another website project

We will create a new project directory for the code of our website.

Again, this directory will be located inside of our local GitHub directory where we store all of our GitHub repositories: `~/code/<user.github_nickname>`.

Create a new project directory named `TaxiFareWebsite`.

```bash
cd ~/code/<user.github_nickname>
mkdir TaxiFareWebsite
cd TaxiFareWebsite
```

Initialise a new git repository:

```bash
git init
```

Create a corresponding repository on our **GitHub** account:

``` bash
gh repo create
```

Go to the GitHub repo in order to make sure that everything is ok:

``` bash
gh repo view --web
```

The repository is empty, which is normal since we have not pushed any code yet...

We are now all set!

## Create a streamlit website

First, we need an `app.py` file inside of our project. The file will contain the code for our page.

``` bash
touch app.py
```

Then, let's copy the `Makefile` that is provided inside of the project... It will allow us to run useful commands for:
- `install_requirements` : dependencies
- `streamlit` : run the **Streamlit** web server in order to see what our website looks like
- `heroku_login` : login to **Heroku**
- `heroku_create_app` : create an app on **Heroku** for our website
- `deploy_heroku` : deploy our app when we are satisfied with its content

You project should look like this:

```
.
├── Makefile
└── app.py
```

Not too overwhelming, right ? 😉

Well... This is half the work.

Lets add some content to our website in `app.py`:

``` python
import streamlit as st

'''
# TaxiFareModel front
'''

st.markdown('''
Remember that there are several ways to output content into your web page...

Either as with the title by just creating a string (or an f-string). Or as with this paragraph using the `st.` functions
''')

'''
## Here we would like to add some controllers in order to ask the user to select the parameters of the ride

1. Let's ask for:
- date and time
- pickup longitude
- pickup latitude
- dropoff longitude
- dropoff latitude
- passenger count
'''

'''
## Once we have these, let's call our API in order to retrieve a prediction

See ? No need to load a `model.joblib` file in this app, we do not even need to know anything about Data Science in order to retrieve a prediction...

🤔 How could we call our API ? Off course... The `requests` package 💡
'''

url = 'https://taxifare.lewagon.ai/predict_fare/'

if url == 'https://taxifare.lewagon.ai/predict_fare/':

    st.markdown('Maybe you want to use your own API for the prediction, not the one provided by Le Wagon...')

'''

2. Let's build a dictionary containing the parameters for our API...

3. Let's call our API using the `requests` package...

4. Let's retrieve the prediction from the **JSON** returned by the API...

## Finally, we can display the prediction to the user
'''
```

Let's run the **Streamlit** web server and see what our website looks like:

``` bash
make streamlit
```

We have a website of our own running on our machine 🎉

## Now we want to plug our API to the website

... So that users can actually make some predictions!

👉 Let's follow the instructions inside the web page and replace the content with some `requests` package magic and a call to our API!

👉 Again, alternatively, you may use this Le Wagon **Prediction API** if you you do not have one in production:

https://taxifare.lewagon.ai/

⚠️ Pay attention to the format of the parameters, this API uses a `/` before the querystring... You need to provide it 😉

https://taxifare.lewagon.ai/predict_fare/?key=2012-10-06%2012:10:20.0000001&pickup_datetime=2012-10-06%2012:10:20%20UTC&pickup_longitude=40.7614327&pickup_latitude=-73.9798156&dropoff_longitude=40.6513111&dropoff_latitude=-73.8803331&passenger_count=2

Let's inspect `app.py` and check what is being done inside...

Replace the URL to the prediction API with our own and update the code accordingly.

Now let's get crazy with the page content 🎉

Maybe add some map 🗺

Once we are satisfied, let's push the code to production! 🔥

## Deploy

Now that we checked our app works locally, we might want it to run free on a remote server.

We will see once again how **Heroku** is easy to use, here we simply need to:

Copy the provided `Procfile` and `setup.sh` inside of our project.

Are we not missing something ?

🤔 How are the packages that `app.py` is using going to be installed on **Heroku** ?

We need to add a `setup.py`, a `MANIFEST.in`, and a `requirements.txt` containing the name of the required packages to our project!

Let's fill their content...

The project should now look like this:

```
.
├── MANIFEST.in
├── Makefile
├── Procfile
├── app.py
├── requirements.txt
├── setup.py
└── setup.sh
```

Now, we can login to **Heroku**

``` bash
heroku login
```

Create an app for our website on **Heroku**... Remember the app name should be unique on the internet.

💡 You might want to [change the region](https://devcenter.heroku.com/articles/regions) if you are not located inside of Europe...

```bash
heroku create YOUR_APP_NAME --region eu
```

Finally, we can push our website to **Heroku** 🚀

```bash
git push heroku master
```

Then scale it:

```bash
heroku ps:scale web=1
```

Click on the link provided by the command line `https://YOUR_APP_NAME.herokuapp.com/` and you should access to your website 🎉
