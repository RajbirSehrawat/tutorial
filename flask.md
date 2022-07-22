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

```
request.method
request.form
request.files
request.get_json()
request.args.get('key', '') - Query String
request.cookies.get('username')
```

# Flask Route

```
@app.route('/projects/') - Represent a Directory
@app.route('/projects') - Represent a File

@app.route('/login', methods=['GET', 'POST'])
@app.route('/path/<path:subpath>')

@app.route('/post/<int:post_id>')
def show_post(post_id):
    # show the post with the given id, the id is an integer
    return f'Post {post_id}'
```

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


#Python Default Logging

```python
#!/usr/bin/env python
import logging

logging.basicConfig(format='%(asctime)s,%(msecs)d %(levelname)-8s [%(filename)s:%(lineno)d] %(message)s',
    datefmt='%Y-%m-%d:%H:%M:%S',
    level=logging.DEBUG)

logger = logging.getLogger(__name__)
logger.debug("This is a debug log")
logger.info("This is an info log")
logger.critical("This is critical")
logger.error("An error occurred")
```

#How to generate good secret keys

```
python -c 'import secrets; print(secrets.token_hex())'
'192b9bdd22ab9ed4d12e236c78afcb9a393ec15f71bbf5dc987d54727823bcbf'
```

# Configuring from Python Files
The configuration files themselves are actual Python files. Only values in uppercase are actually stored in the config object later on.

```
app = Flask(__name__)
app.config.from_object('yourapplication.default_settings')
app.config.from_envvar('YOURAPPLICATION_SETTINGS')
```

### Configuring from Data Files

```
import toml
app.config.from_file("config.toml", load=toml.load)
```

```
import json
app.config.from_file("config.json", load=json.load)
```

# Blueprints and Views

```
auth.py
bp = Blueprint('auth', __name__, url_prefix='/auth')

in main file

from . import auth
app.register_blueprint(auth.bp)
```
# Session

```python
    # Store in session
    session['name'] = "name"

    # Get value from session
    name = session.get('user_id')

    #remove the username from the session if it's there
    session.pop('username', None)

    #clear session or delete all session varidables
    session.clear()
```

# Flask Call Back

```
before_request()
after_request()
after_this_request()
```