# Flask Tutoiral

SQLAlchemy

$ export FLASK_ENV=development
$ export FLASK_APP=hello
$ flask run
 * Running on http://127.0.0.1:5000/

FLASK_DEBUG = 0/1

As a shortcut, if the file is named app.py or wsgi.py, you don’t have to set the FLASK_APP environment variable.

 python -m flask fails or flask


## HTML Escaping

```python
from markupsafe import escape

@app.route("/<name>")
def hello(name):
    return f"Hello, {escape(name)}!"

```

# Flask Request

request.method
request.form
request.files
request.get_json()
request.args.get('key', '') - Query String
request.cookies.get('username')

# Flask Route


@app.route('/projects/') - Represent a Directory
@app.route('/projects') - Represent a File

@app.route('/login', methods=['GET', 'POST'])
@app.route('/path/<path:subpath>')

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # show the post with the given id, the id is an integer
    return f'Post {post_id}'


# Static Files

'''
url_for('static', filename='style.css')
'''



# Rendering Templates

Inside templates you also have access to the config, request, session and g 1 objects as well as the url_for() and get_flashed_messages() functions.

'''python
from flask import render_template

@app.route('/hello/')
@app.route('/hello/<name>')
def hello(name=None):
    return render_template('hello.html', name=name)
'''


# Flask Functions 

url_for - 

Generates a URL to the given endpoint with the method provided.
It accepts the name of the function as its first argument and any number of keyword arguments, each corresponding to a variable part of the URL rule. Unknown variable parts are appended to the URL as query parameters.


make_response()
redirect()
abort()
jsonify() - 
flash() - set flash message
get_flashed_messages() - get session flash message

# Other Function


secure_filename
from werkzeug.utils import secure_filename


