<!--
.. title: Flask Collage for Project Night Challengers
.. slug: flask-collage-for-project-night-challengers
.. date: 2019-03-17 00:20:18 UTC-05:00
.. tags: flask, web-dev
.. category: web-dev
.. link: 
.. description: 
.. type: text
-->

# Flask Collage for Project Night Challengers

Build a small web app using Flask which accepts the meetup.com event id for tonight
as a parameter and would fetch the profile pictures of all the attendees to create a
collage. [Here](https://twitter.com/Tathagata/status/746302962830540801) is an example
of such a collage.

You'll need:

 - `pip install flask`
 - `pip install Flask-WTF`
 - `pip install meetup-api`

How to create a basic Flask app:
Follow the instructions [here](http://flask.pocoo.org/docs/0.11/quickstart/)

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run(debug=True)
```
`python testflask.py`

To get you started, the following piece of code will help you fetch the thumbnail
images from meetup.com.

```python
import meetup.api
client = meetup.api.Client('your_key')

rsvps=client.GetRsvps(event_id='235484841', urlname='_ChiPy_')
member_id = ','.join([str(i['member']['member_id']) for i in rsvps.results])
members = client.GetMembers(member_id=member_id)

for member in members.results:
    try:
        print '{0},{1},{2}'.format(member['name'], member['id'], member['photo']['thumb_link'])
    except:
        pass # ignore those who do not have a complete profile
```

1. Can you include the name along with the images in your collage?

2. Add a search box to your collage, where you can search some one by name. 
On a successful search, it should display that person and their name. On failure, it should give a proper error message.

3. Add the following list of questions to your search result page that collects feedback on what an attendee would like to do 

Choices:
- Help others with Python 101 questions
- Help others with Python Data Science questions
- Help others with Python Web Dev questions
- Python 101 course (Beginner)
- Attend Coding Workshop (Intermediate)
- Attend RasberryPi Lab (Intermediate)
- Work on my own project, get help from others 

4. Deploy your app to a public hosting, share the link with the world!

5. Currently we are accepting RSVPs on both ChiPy's site and Chicago Pythonista's
meetup page. Can you fetch the thumbnails from both the pages, eliminate the
duplicates, and merge them to generate the collage?

